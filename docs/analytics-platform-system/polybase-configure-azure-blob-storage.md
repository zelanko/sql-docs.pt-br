---
title: Usar o polybase para acessar dados externos no armazenamento de BLOBs do Azure
description: Explica como configurar o polybase em paralelo data warehouse para se conectar ao Hadoop externo.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 4ea61ea7e6983f9601783957eee6776f36eccfb4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74400721"
---
# <a name="configure-polybase-to-access-external-data-in-azure-blob-storage"></a>Configurar o polybase para acessar dados externos no armazenamento de BLOBs do Azure

O artigo explica como usar o polybase em uma instância de SQL Server para consultar dados externos no armazenamento de BLOBs do Azure.

> [!NOTE]
> Atualmente, os APS dão suporte apenas ao armazenamento de BLOBs do Azure com redundância local (LRS) padrão de uso geral v1.

## <a name="prerequisites"></a>Prerequisites

 - Armazenamento de BLOBs do Azure em sua assinatura.
 - Um contêiner criado no armazenamento de BLOBs do Azure.

### <a name="configure-azure-blob-storage-connectivity"></a>Configurar a conectividade do armazenamento de BLOBs do Azure

Primeiro, configure o APS para usar o armazenamento de BLOBs do Azure.

1. Execute [sp_configure](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) com ' conectividade do Hadoop ' definida como um provedor de armazenamento de BLOBs do Azure. Para encontrar o valor dos provedores, consulte [Configuração de conectividade do PolyBase](../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).

   ```sql  
   -- Values map to various external data sources.  
   -- Example: value 7 stands for Hortonworks HDP 2.1 to 2.6 on Linux,
   -- 2.1 to 2.3 on Windows Server, and Azure Blob storage  
   sp_configure @configname = 'hadoop connectivity', @configvalue = 7;
   GO

   RECONFIGURE
   GO
   ```  

2. Reinicie a região APS usando a página status do serviço no [Configuration Manager do dispositivo](launch-the-configuration-manager.md).
  
## <a name="configure-an-external-table"></a>Configurar uma tabela externa

Para consultar os dados em seu armazenamento de BLOBs do Azure, você deve definir uma tabela externa para usar em consultas Transact-SQL. As etapas a seguir descrevem como configurar a tabela externa.

1. Crie uma chave mestra no banco de dados. É necessário criptografar o segredo da credencial.

   ```sql
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
   ```

1. Crie uma credencial no escopo do banco de dados para o armazenamento de BLOBs do Azure.

   ```sql
   -- IDENTITY: any string (this is not used for authentication to Azure storage).  
   -- SECRET: your Azure storage account key.  
   CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
   WITH IDENTITY = 'user', Secret = '<azure_storage_account_key>';
   ```

1. Crie uma fonte de dados externa, usando [CREATE EXTERNAL DATA SOURCE](../t-sql/statements/create-external-data-source-transact-sql.md).

   ```sql
   -- LOCATION:  Azure account storage account name and blob container name.  
   -- CREDENTIAL: The database scoped credential created above.  
   CREATE EXTERNAL DATA SOURCE AzureStorage with (  
         TYPE = HADOOP,
         LOCATION ='wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',  
         CREDENTIAL = AzureStorageCredential  
   );  
   ```

1. Crie um formato de arquivo externo com [CREATE EXTERNAL FILE FORMAT](../t-sql/statements/create-external-file-format-transact-sql.md).

   ```sql
   -- FORMAT TYPE: Type of format in Azure Blob storage (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).
   -- In this example, the files are pipe (|) delimited
   CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
         FORMAT_TYPE = DELIMITEDTEXT,
         FORMAT_OPTIONS (FIELD_TERMINATOR ='|',
               USE_TYPE_DEFAULT = TRUE)  
   ```

1. Crie uma tabela externa que aponta para dados armazenados no armazenamento do Azure com [CREATE EXTERNAL TABLE](../t-sql/statements/create-external-table-transact-sql.md). Neste exemplo, os dados externos contêm os dados de sensor do carro.

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
         DATA_SOURCE = AzureStorage,  
         FILE_FORMAT = TextFileFormat  
   );  
   ```

1. Crie estatísticas em uma tabela externa.

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

A consulta ad hoc a seguir une relacional com dados no armazenamento de BLOBs do Azure. Ele seleciona os clientes que impulsionam mais de 35 mph, unindo dados estruturados do cliente armazenados em SQL Server com dados de sensor de carros armazenados no armazenamento de BLOBs do Azure.  

```sql  
SELECT DISTINCT Insured_Customers.FirstName,Insured_Customers.LastName,
       Insured_Customers. YearlyIncome, CarSensor_Data.Speed  
FROM Insured_Customers, CarSensor_Data  
WHERE Insured_Customers.CustomerKey = CarSensor_Data.CustomerKey and CarSensor_Data.Speed > 35
ORDER BY CarSensor_Data.Speed DESC  
```  

### <a name="importing-data"></a>Importando dados  

A consulta a seguir importa dados externos para o APS. Este exemplo importa dados para drivers rápidos em APS para fazer uma análise mais detalhada. Para melhorar o desempenho, ele aproveita a tecnologia Columnstore no APS.  

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

A consulta a seguir exporta dados de APS para o armazenamento de BLOBs do Azure. Ele pode ser usado para arquivar dados relacionais no armazenamento de BLOBs do Azure e ainda conseguir consultá-los.

```sql
-- Export data: Move old data to Azure Blob storage while keeping it query-able via an external table.  
CREATE EXTERNAL TABLE [dbo].[FastCustomers2009] 
WITH (  
      LOCATION='/archive/customer/2009',  
      DATA_SOURCE = AzureStorage,  
      FILE_FORMAT = TextFileFormat
)  
AS
SELECT T.* FROM Insured_Customers T1 JOIN CarSensor_Data T2  
ON (T1.CustomerKey = T2.CustomerKey)  
WHERE T2.YearMeasured = 2009 and T2.Speed > 40;  
```  

## <a name="view-polybase-objects-in-ssdt"></a>Exibir objetos polybase no SSDT  

Em SQL Server Data Tools, as tabelas externas são exibidas em uma pasta separada **tabelas externas**. As fontes de dados externas e os formatos de arquivo externos estão em subpastas em **Recursos Externos**.  
  
![Objetos do polybase no SSDT](media/polybase/external-tables-datasource.png)  

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o PolyBase, confira [O que é o PolyBase?](../relational-databases/polybase/polybase-guide.md). 

