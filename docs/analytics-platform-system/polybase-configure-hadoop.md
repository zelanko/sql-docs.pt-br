---
title: Configurar o PolyBase para acessar dados externos no Hadoop | Microsoft Docs
description: Explica como configurar o PolyBase no Parallel Data Warehouse para se conectar ao Hadoop externo.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d87ba02342948d140afb68c2d9d13a2aef9464eb
ms.sourcegitcommit: 5afec8b4b73ce1727e4e5cf875d1e1ce9df50eab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47450334"
---
# <a name="configure-polybase-to-access-external-data-in-hadoop"></a>Configurar o PolyBase para acessar dados externos no Hadoop

O artigo explica como usar o PolyBase em um dispositivo de APS para consultar dados externos no Hadoop.

## <a name="prerequisites"></a>Prerequisites

O PolyBase é compatível com dois provedores de Hadoop, HDP (Hortonworks Data Platform) e CDH (Cloudera Distributed Hadoop). Hadoop segue o padrão de "Major" para suas novas versões, e todas as versões em uma versão Major e Minor com suporte são suportadas. Há suporte para os seguintes provedores de Hadoop:
 - Hortonworks HDP 1.3 em Linux/Windows Server  
 - Hortonworks HDP 2.1 – 2.6 no Linux
 - Hortonworks HDP 2.1 a 2.3 no Windows Server  
 - Cloudera CDH 4.3 em Linux  
 - Cloudera CDH 5.1 – 5.5, 5.9 – 5.13 em Linux

### <a name="configure-hadoop-connectivity"></a>Configurar a conectividade do Hadoop

Primeiro, configure os pontos de acesso para usar o provedor específico do Hadoop.

1. Execute [sp_configure](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) com "conectividade hadoop" e defina um valor apropriado para o seu provedor. Para localizar o valor para o seu provedor, consulte [configuração do PolyBase](../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md). 

   ```sql  
   -- Values map to various external data sources.  
   -- Example: value 7 stands for Hortonworks HDP 2.1 to 2.6 on Linux,
   -- 2.1 to 2.3 on Windows Server, and Azure blob storage  
   sp_configure @configname = 'hadoop connectivity', @configvalue = 7;
   GO

   RECONFIGURE
   GO
   ```  

2. Reiniciar a região de pontos de acesso usando a página Status do serviço no [Gerenciador de configuração de dispositivo](launch-the-configuration-manager.md).
  
## <a id="pushdown"></a> Habilitar a computação de aplicação  

Para melhorar o desempenho da consulta, habilite a computação de aplicação para seu cluster do Hadoop:  
  
1. Abra uma conexão de área de trabalho remota ao nó de controle do PDW.

2. Localize o arquivo **yarn-site. XML** no nó de controle. Normalmente, o caminho é:  

   ```xml  
   C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf\  
   ```  

3. No computador do Hadoop, localize o arquivo análogo no diretório da configuração do Hadoop. No arquivo, localize e copie o valor da chave de configuração yarn.application.classpath.  
  
4. No nó de controle, no **arquivo yarn** localizar o **classpath** propriedade. Cole o valor do computador do Hadoop no elemento de valor.  
  
5. Para todas as versões do CDH 5.X, você precisará adicionar os parâmetros de configuração mapreduce.application.classpath ao final do arquivo yarn.site.xml ou ao arquivo mapred-site.xml. O HortonWorks inclui essas configurações nas configurações yarn.application.classpath. Veja [Configuração do PolyBase](../relational-databases/polybase/polybase-configuration.md) para obter exemplos.

## <a name="configure-an-external-table"></a>Configurar uma tabela externa

Para consultar os dados em sua fonte de dados do Hadoop, você deve definir uma tabela externa para usar em consultas Transact-SQL. As etapas a seguir descrevem como configurar a tabela externa.

1. Crie uma chave mestra no banco de dados. Ela é necessária para criptografar o segredo da credencial.

   ```sql
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
   ```

2. Crie uma credencial no escopo do banco de dados para clusters de Hadoop protegido por Kerberos.

   ```sql
   -- IDENTITY: the Kerberos user name.  
   -- SECRET: the Kerberos password  
   CREATE DATABASE SCOPED CREDENTIAL HadoopUser1
   WITH IDENTITY = '<hadoop_user_name>', Secret = '<hadoop_password>';  
   ```

3. Criar uma fonte de dados externa com [CREATE EXTERNAL DATA SOURCE](../t-sql/statements/create-external-data-source-transact-sql.md).

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

4. Criar um formato de arquivo externo com [CREATE EXTERNAL FILE FORMAT](../t-sql/statements/create-external-file-format-transact-sql.md).

   ```sql
   -- FORMAT TYPE: Type of format in Hadoop (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).
   CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
         FORMAT_TYPE = DELIMITEDTEXT,
         FORMAT_OPTIONS (FIELD_TERMINATOR ='|',
               USE_TYPE_DEFAULT = TRUE)  
   ```

5. Criar uma tabela externa que aponta para dados armazenados no Hadoop com [CREATE EXTERNAL TABLE](../t-sql/statements/create-external-table-transact-sql.md). Neste exemplo, os dados externos contém os dados de sensor do carro.

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

6. Crie estatísticas em uma tabela externa.

   ```sql
   CREATE STATISTICS StatsForSensors on CarSensor_Data(CustomerKey, Speed)  
   ```

## <a name="polybase-queries"></a>Consultas do PolyBase

O PolyBase é adequado para três funções:  
  
- Consultas ad hoc em tabelas externas.  
- Importação de dados.  
- Exportação de dados.  

As consultas a seguir fornecem exemplo com os dados de sensor de carro fictícia.

### <a name="ad-hoc-queries"></a>Consulta ad hoc  

A seguinte consulta ad hoc junções relacionais com dados do Hadoop. Ele seleciona clientes que conduzem a mais rápido do que 35 km/h ingressando dados estruturados de cliente armazenados no APS com dados de sensor do carro armazenados no Hadoop.  

```sql  
SELECT DISTINCT Insured_Customers.FirstName,Insured_Customers.LastName,
       Insured_Customers. YearlyIncome, CarSensor_Data.Speed  
FROM Insured_Customers, CarSensor_Data  
WHERE Insured_Customers.CustomerKey = CarSensor_Data.CustomerKey and CarSensor_Data.Speed > 35
ORDER BY CarSensor_Data.Speed DESC  
OPTION (FORCE EXTERNALPUSHDOWN);   -- or OPTION (DISABLE EXTERNALPUSHDOWN)  
```  

### <a name="importing-data"></a>Importando dados  

A consulta a seguir importa dados externos no APS. Este exemplo importa dados para drivers rápidas para APS para fazer uma análise mais detalhada. Para melhorar o desempenho, ela aproveita a tecnologia de Columnstore no APS.  

```sql
CREATE TABLE Fast_Customers
WITH
(CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = HASH (CustomerKey))
AS
SELECT DISTINCT
      Insured_Customers.CustomerKey, Insured_Customers.FirstName, Insured_Customers.LastName,   
      Insured_Customers.YearlyIncome, Insured_Customers.MaritalStatus  
from Insured_Customers INNER JOIN   
(  
      SELECT * FROM CarSensor_Data where Speed > 35   
) AS SensorD  
ON Insured_Customers.CustomerKey = SensorD.CustomerKey  
```  

### <a name="exporting-data"></a>Exportando dados  

A consulta a seguir exporta dados dos pontos de acesso para o Hadoop. Ele pode ser usado para arquivar dados relacionais para o Hadoop enquanto ainda poderá consultá-lo.

```sql
-- Export data: Move old data to Hadoop while keeping it query-able via an external table.  
CREATE EXTERNAL TABLE [dbo].[FastCustomers2009] 
WITH (  
      LOCATION='/archive/customer/2009',  
      DATA_SOURCE = HadoopHDP2,  
      FILE_FORMAT = TextFileFormat
)  
AS
SELECT T.* FROM Insured_Customers T1 JOIN CarSensor_Data T2  
ON (T1.CustomerKey = T2.CustomerKey)  
WHERE T2.YearMeasured = 2009 and T2.Speed > 40;  
```  

## <a name="view-polybase-objects-in-ssdt"></a>Exibir objetos PolyBase no SSDT  

No SQL Server Data Tools, as tabelas externas são exibidas em uma pasta separada **tabelas externas**. As fontes de dados externas e os formatos de arquivo externos estão em subpastas em **Recursos Externos**.  
  
![Objetos PolyBase no SSDT](media/polybase/external-tables-datasource.png)  

## <a name="next-steps"></a>Próximas etapas

Explore mais maneiras de configurar o PolyBase nos seguintes artigos:

[PolyBase configuração e segurança para o Hadoop ](../relational-databases/polybase/polybase-configuration.md).  
 
