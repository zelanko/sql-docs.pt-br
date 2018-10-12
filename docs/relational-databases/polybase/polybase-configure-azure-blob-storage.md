---
title: Configurar o PolyBase para acessar dados externos no Armazenamento de Blobs do Azure | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6b1bd34a017cc067a93e8b307adc5c8069ac8e0d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47831334"
---
# <a name="configure-polybase-to-access-external-data-in-azure-blob-storage"></a>Configurar o PolyBase para acessar dados externos no Armazenamento de Blobs do Azure

[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

O artigo explica como usar o PolyBase em uma instância do SQL Server para consultar dados externos no Hadoop.

## <a name="prerequisites"></a>Prerequisites

Se você ainda não instalou o PolyBase, veja [Instalação do PolyBase](polybase-installation.md). O artigo sobre a instalação explica os pré-requisitos.

### <a name="configure-azure-blob-storage-connectivity"></a>Configurar a conectividade do Armazenamento de Blobs do Azure

Primeiro, configure o PolyBase do SQL Server para usar o Armazenamento de Blobs do Azure.

1. Execute [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) com "conectividade do hadoop" definido como um provedor do Armazenamento de Blobs do Azure. Para encontrar o valor dos provedores, consulte [Configuração de conectividade do PolyBase](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md). Por padrão, a conectividade de Hadoop é definida como 7.

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
  
   ![Parar e iniciar serviços de PolyBase em services.msc](../../relational-databases/polybase/media/polybase-stop-start.png "Parar e iniciar serviços de PolyBase em services.msc")  
  
## <a name="configure-an-external-table"></a>Configurar uma tabela externa

Para consultar os dados em sua fonte de dados do Hadoop, você precisa definir uma tabela externa para usar em consultas Transact-SQL. As etapas a seguir descrevem como configurar a tabela externa.

1. Crie uma chave mestra no banco de dados. Isso é necessário para criptografar o segredo da credencial.

   ```sql
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
   ```

1. Crie uma credencial com escopo de banco de dados para o Armazenamento de Blobs do Azure.

   ```sql
   -- IDENTITY: any string (this is not used for authentication to Azure storage).  
   -- SECRET: your Azure storage account key.  
   CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
   WITH IDENTITY = 'user', Secret = '<azure_storage_account_key>';
   ```

1. Crie uma fonte de dados externa, usando [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).

   ```sql
   -- LOCATION:  Azure account storage account name and blob container name.  
   -- CREDENTIAL: The database scoped credential created above.  
   CREATE EXTERNAL DATA SOURCE AzureStorage with (  
         TYPE = HADOOP,
         LOCATION ='wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',  
         CREDENTIAL = AzureStorageCredential  
   );  
   ```

1. Crie um formato de arquivo externo com [CREATE EXTERNAL FILE FORMAT](../../t-sql/statements/create-external-file-format-transact-sql.md).

   ```sql
   -- FORMAT TYPE: Type of format in Hadoop (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).
   CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
         FORMAT_TYPE = DELIMITEDTEXT,
         FORMAT_OPTIONS (FIELD_TERMINATOR ='|',
               USE_TYPE_DEFAULT = TRUE)  
   ```

1. Crie uma tabela externa que aponta para dados armazenados no armazenamento do Azure com [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md). Neste exemplo, os dados externos contêm os dados de sensor do carro.

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

1. Crie estatísticas em uma tabela externa.

   ```sql
   CREATE STATISTICS StatsForSensors on CarSensor_Data(CustomerKey, Speed)  
   ```

## <a name="polybase-queries"></a>Consultas do PolyBase

O PolyBase é adequado para três funções:  
  
- consultas ad hoc em tabelas externas.  
- importar dados.  
- exportar dados.  

As consultas a seguir fornecem exemplo com os dados de sensor de carro fictícios.

### <a name="ad-hoc-queries"></a>Consultas ad hoc  

A seguinte consulta ad hoc une dados relacionais com os dados do Hadoop. Ela seleciona clientes que dirigem mais rápido do que 35 km/h, unindo dados estruturados do cliente armazenados no SQL Server com os dados de sensor de carro armazenados no Hadoop.  

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

A consulta a seguir exporta dados do SQL Server para Armazenamento de Blobs do Azure. Para fazer isso, primeiro você precisa habilitar a exportação do PolyBase. Em seguida, crie uma tabela externa para o destino antes de exportar dados para ele.

```sql
-- Enable INSERT into external table  
sp_configure ‘allow polybase export’, 1;  
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
