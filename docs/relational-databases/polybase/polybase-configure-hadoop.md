---
title: 'Acessar dados externos: Hadoop – PolyBase'
ms.date: 12/13/2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>= sql-server-2016 || =sqlallproducts-allversions'
ms.custom: seo-dt-2019
ms.openlocfilehash: 979d0f5d57c7d761e5c9c3f1b302046312396554
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79286900"
---
# <a name="configure-polybase-to-access-external-data-in-hadoop"></a>Configurar o PolyBase para acessar dados externos no Hadoop

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

O artigo explica como usar o PolyBase em uma instância do SQL Server para consultar dados externos no Hadoop.

## <a name="prerequisites"></a>Pré-requisitos

- Se você ainda não instalou o PolyBase, veja [Instalação do PolyBase](polybase-installation.md). O artigo sobre a instalação explica os pré-requisitos.

<!--SQL Server 2019-->
::: moniker range=">= sql-server-ver15 || =sqlallproducts-allversions"

- Começando com o SQL Server 2019, você também precisa [habilitar o recurso do PolyBase](polybase-installation.md#enable).

::: moniker-end

- O PolyBase é compatível com dois provedores de Hadoop, HDP (Hortonworks Data Platform) e CDH (Cloudera Distributed Hadoop). O Hadoop segue o padrão "Principal.Secundária.Versão" para suas novas versões, e há suporte para todas as versões em uma versão Principal e Secundária com suporte. Há suporte para os seguintes provedores do Hadoop:

  - Hortonworks HDP 1.3, 2.1-2.6, 3.0 no Linux
  - Hortonworks HDP 1.3, 2.1-2.3 no Windows Server
  - Cloudera CDH 4.3, 5.1 – 5.5, 5.9 – 5.13 no Linux

> [!NOTE]
> O PolyBase é compatível com as zonas de criptografia do Hadoop, começando com o SQL Server 2016 SP1 CU7 e o SQL Server 2017 CU3. Caso esteja usando os [grupos de escala horizontal do PolyBase](polybase-scale-out-groups.md), todos os nós de computação também deverão estar em um build que tenha suporte para zonas de criptografia do Hadoop.

### <a name="configure-hadoop-connectivity"></a>Configurar a conectividade do Hadoop

Primeiro, configure o PolyBase do SQL Server para usar o provedor específico do Hadoop.

1. Execute [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) com “conectividade do hadoop” e defina um valor adequado para seu provedor. Para encontrar o valor de seu provedor, consulte [Configuração de conectividade do PolyBase](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md). Por padrão, a conectividade de Hadoop é definida como 7.

   ```sql  
   -- Values map to various external data sources.  
   -- Example: value 7 stands for Hortonworks HDP 2.1 to 2.6 on Linux,
   -- 2.1 to 2.3 on Windows Server, and Azure blob storage  
   sp_configure @configname = 'hadoop connectivity', @configvalue = 7;
   GO

   RECONFIGURE
   GO
   ```  

2. É necessário reiniciar o SQL Server usando **services.msc**. A reinicialização do o SQL Server reiniciará estes serviços:  

   - Serviço de movimentação de dados de PolyBase do SQL Server  
   - Mecanismo PolyBase do SQL Server  
  
   ![parar e iniciar os serviços do PolyBase em services.msc](../../relational-databases/polybase/media/polybase-stop-start.png "parar e iniciar os serviços do PolyBase em Services. msc")  
  
## <a id="pushdown"></a> Habilitar cálculo de aplicação  

Para melhorar o desempenho de consulta, habilite a computação de aplicação para seu cluster do Hadoop:  
  
1. Localize o arquivo **yarn-site.xml** no caminho de instalação do SQL Server. Normalmente, o caminho é:  

   ```xml  
   C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Polybase\Hadoop\conf\  
   ```  

1. No computador do Hadoop, localize o arquivo análogo no diretório da configuração do Hadoop. No arquivo, localize e copie o valor da chave de configuração yarn.application.classpath.  
  
1. No computador do SQL Server, no **yarn-site.xml file**, localize a propriedade **yarn.application.classpath**. Cole o valor do computador do Hadoop no elemento de valor.  
  
1. Para todas as versões do CDH 5.X, você precisará adicionar os parâmetros de configuração mapreduce.application.classpath ao final do arquivo yarn-site.xml ou ao arquivo mapred-site.xml. O HortonWorks inclui essas configurações nas configurações yarn.application.classpath. Veja [Configuração do PolyBase](../../relational-databases/polybase/polybase-configuration.md) para obter exemplos.

## <a name="configure-an-external-table"></a>Configurar uma tabela externa

Para consultar os dados em sua fonte de dados do Hadoop, você precisa definir uma tabela externa para usar em consultas Transact-SQL. As etapas a seguir descrevem como configurar a tabela externa.

1. Crie uma chave mestra no banco de dados, caso ainda não exista. Isso é necessário para criptografar o segredo da credencial.

     ```sql
      CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';  
     ```
    ## <a name="arguments"></a>Argumentos
    PASSWORD ='password'

    É a senha usada para criptografar a chave mestra no banco de dados. password precisa atender aos requisitos da política de senha do Windows do computador que está hospedando a instância do SQL Server.
1. Crie uma credencial com escopo do banco de dados para clusters do Hadoop protegidos por Kerberos.

   ```sql
   -- IDENTITY: the Kerberos user name.  
   -- SECRET: the Kerberos password  
   CREATE DATABASE SCOPED CREDENTIAL HadoopUser1
   WITH IDENTITY = '<hadoop_user_name>', Secret = '<hadoop_password>';  
   ```

2. Crie uma fonte de dados externa, usando [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).

   ```sql
   -- LOCATION (Required) : Hadoop Name Node IP address and port.  
   -- RESOURCE MANAGER LOCATION (Optional): Hadoop Resource Manager location to enable pushdown computation.  
   -- CREDENTIAL (Optional):  the database scoped credential, created above.  
   CREATE EXTERNAL DATA SOURCE MyHadoopCluster WITH (  
         TYPE = HADOOP,
         LOCATION ='hdfs://10.xxx.xx.xxx:xxxx',
         RESOURCE_MANAGER_LOCATION = '10.xxx.xx.xxx:xxxx',
         CREDENTIAL = HadoopUser1
   );  
   ```

3. Crie um formato de arquivo externo com [CREATE EXTERNAL FILE FORMAT](../../t-sql/statements/create-external-file-format-transact-sql.md).

   ```sql
   -- FORMAT TYPE: Type of format in Hadoop (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).
   CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
         FORMAT_TYPE = DELIMITEDTEXT,
         FORMAT_OPTIONS (FIELD_TERMINATOR ='|',
               USE_TYPE_DEFAULT = TRUE))
   ```

4. Crie uma tabela externa que aponta para dados armazenados no Hadoop com [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md). Neste exemplo, os dados externos contêm os dados de sensor do carro.

   ```sql
   -- LOCATION: path to file or directory that contains the data (relative to HDFS root).  
   CREATE EXTERNAL TABLE [dbo].[CarSensor_Data] (  
         [SensorKey] int NOT NULL,
         [CustomerKey] int NOT NULL,
         [GeographyKey] int NULL,
         [Speed] float NOT NULL,
         [YearMeasured] int NOT NULL  
   )  
   WITH (LOCATION='/Demo/',
         DATA_SOURCE = MyHadoopCluster,  
         FILE_FORMAT = TextFileFormat  
   );  
   ```

5. Crie estatísticas em uma tabela externa.

   ```sql
   CREATE STATISTICS StatsForSensors on CarSensor_Data(CustomerKey, Speed)  
   ```

## <a name="polybase-queries"></a>Consultas do PolyBase

O PolyBase é adequado para três funções:  
  
- Consultas ad hoc em tabelas externas.  
- importar dados.  
- exportar dados.  

As consultas a seguir fornecem exemplo com os dados de sensor de carro fictícios.

### <a name="ad-hoc-queries"></a>Consulta ad hoc  

A consulta ad hoc a seguir associa dados relacionais aos dados do Hadoop. Ela seleciona clientes que dirigem mais rápido do que 35 km/h, unindo dados estruturados do cliente armazenados no SQL Server com os dados de sensor de carro armazenados no Hadoop.  

```sql  
SELECT DISTINCT Insured_Customers.FirstName,Insured_Customers.LastName,
       Insured_Customers. YearlyIncome, CarSensor_Data.Speed  
FROM Insured_Customers, CarSensor_Data  
WHERE Insured_Customers.CustomerKey = CarSensor_Data.CustomerKey and CarSensor_Data.Speed > 35
ORDER BY CarSensor_Data.Speed DESC  
OPTION (FORCE EXTERNALPUSHDOWN);   -- or OPTION (DISABLE EXTERNALPUSHDOWN)  
```  

### <a name="importing-data"></a>Importando dados  

A consulta a seguir importa dados externos para o SQL Server. Este exemplo importa dados de motoristas velozes para o SQL Server para fazer uma análise mais detalhada. Para melhorar o desempenho, ela aproveita a tecnologia de Columnstore.  

```sql
SELECT DISTINCT
      Insured_Customers.FirstName, Insured_Customers.LastName,   
      Insured_Customers.YearlyIncome, Insured_Customers.MaritalStatus  
INTO Fast_Customers from Insured_Customers INNER JOIN   
(  
      SELECT * FROM CarSensor_Data where Speed > 35   
) AS SensorD  
ON Insured_Customers.CustomerKey = SensorD.CustomerKey  
ORDER BY YearlyIncome  
  
CREATE CLUSTERED COLUMNSTORE INDEX CCI_FastCustomers ON Fast_Customers;  
```  

### <a name="exporting-data"></a>Exportando dados  

A consulta a seguir exporta dados do SQL Server para o Hadoop. Para fazer isso, primeiro você precisa habilitar a exportação do PolyBase. Em seguida, crie uma tabela externa para o destino antes de exportar dados para ele.

```sql
-- Enable INSERT into external table  
sp_configure 'allow polybase export', 1;  
reconfigure  
  
-- Create an external table.
CREATE EXTERNAL TABLE [dbo].[FastCustomers2009] (  
      [FirstName] char(25) NOT NULL,
      [LastName] char(25) NOT NULL,
      [YearlyIncome] float NULL,
      [MaritalStatus] char(1) NOT NULL  
)  
WITH (  
      LOCATION='/old_data/2009/customerdata',  
      DATA_SOURCE = HadoopHDP2,  
      FILE_FORMAT = TextFileFormat,  
      REJECT_TYPE = VALUE,  
      REJECT_VALUE = 0  
);  

-- Export data: Move old data to Hadoop while keeping it query-able via an external table.  
INSERT INTO dbo.FastCustomer2009  
SELECT T.* FROM Insured_Customers T1 JOIN CarSensor_Data T2  
ON (T1.CustomerKey = T2.CustomerKey)  
WHERE T2.YearMeasured = 2009 and T2.Speed > 40;  
```  

## <a name="view-polybase-objects-in-ssms"></a>Exibir objetos do PolyBase no SSMS  

No SSMS, as tabelas externas são exibidas em uma pasta separada **Tabelas Externas**. As fontes de dados externas e os formatos de arquivo externos estão em subpastas em **Recursos Externos**.  
  
![Objetos do PolyBase no SSMS](media/polybase-management.png)  

## <a name="next-steps"></a>Próximas etapas

Explore mais maneiras de usar e monitorar o PolyBase nos seguintes artigos:

[Grupos de expansão do PolyBase](../../relational-databases/polybase/polybase-scale-out-groups.md).  
[Solução de problemas do PolyBase](polybase-troubleshooting.md).  
