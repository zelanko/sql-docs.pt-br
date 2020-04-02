---
title: Cenários de consulta do PolyBase | Microsoft Docs
description: Veja exemplos de consultas usando o recurso PolyBase do SQL Server, incluindo SELECT, JOIN de tabelas externas com tabelas locais, importar/exportar dados e novas exibições de catálogo.
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
keywords:
- PolyBase
helpviewer_keywords:
- PolyBase, import and export
- Hadoop, import with PolyBase
- Hadoop, export with PolyBase
- Azure blob storage, import with PolyBase
- Azure blob storage, export with PolyBase
ms.assetid: 2c5aa2bd-af7d-4f57-9a28-9673c2a4c07e
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>= sql-server-2016 || =sqlallproducts-allversions'
ms.openlocfilehash: aeac57c5ae6facfeb092592c2f3dca851bb9b87b
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "80217087"
---
# <a name="polybase-query-scenarios"></a>Cenários de consulta do PolyBase

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo fornece exemplos de consultas que usam o recurso [PolyBase](../../relational-databases/polybase/polybase-guide.md) do SQL Server (a partir de 2016). Antes de usar esses exemplos, primeiro é necessário instalar e configurar o PolyBase. Para obter mais informações, consulte a [Visão geral do PolyBase](polybase-guide.md).
  
Execute instruções Transact-SQL em tabelas externas ou use as ferramentas de BI para consultar tabelas externas.
  
## <a name="select-from-external-table"></a>SELECT da tabela externa  

Uma consulta simples que retorna dados de uma tabela externa definida.  

```sql  
SELECT TOP 10 * FROM [dbo].[SensorData];   
```

Uma consulta simples que inclui um predicado.

```sql
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65;
```

## <a name="join-external-tables-with-local-tables"></a>JOIN de tabelas externas com tabelas locais

```sql
SELECT InsuranceCustomers.FirstName,   
   InsuranceCustomers.LastName,   
   SensorData.Speed  
FROM InsuranceCustomers INNER JOIN SensorData    
ON InsuranceCustomers.CustomerKey = SensorData.CustomerKey   
WHERE SensorData.Speed > 65   
ORDER BY SensorData.Speed DESC  
  
```  

## <a name="import-data"></a>Importar dados

Importe dados do Hadoop ou armazenamento do Azure para SQL Server, para armazenamento persistente. Use SELECT INTO para importar dados referenciados por uma tabela externa para armazenamento persistente no SQL Server. Crie uma tabela relacional rapidamente e crie um índice de repositório de coluna sobre a tabela em uma segunda etapa.

```sql
-- PolyBase scenario - import external data into SQL Server
-- Import data for fast drivers into SQL Server to do more in-depth analysis
-- Leverage columnstore technology
  
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

## <a name="export-data"></a>Exportar dados

Exporte dados do SQL Server para o Hadoop ou armazenamento do Azure. 

Primeiro, habilite a funcionalidade de exportação definindo o valor `sp_configure` de "permitir exportação de polybase" como 1. Em seguida, crie uma tabela externa que aponta para o diretório de destino. A instrução CREATE EXTERNAL TABLE cria o diretório de destino, caso ele ainda não exista. Em seguida, use INSERT INTO para exportar dados de uma tabela local do SQL Server para a fonte de dados externa. 

Os resultados da instrução SELECT são exportados para o local especificado no formato de arquivo especificado. Os arquivos externos são nomeados *QueryID_date_time_ID.format*, em que *ID* é um identificador incremental e *formato* é o formato de dados exportados. Por exemplo, um nome de arquivo pode ser QID776_20160130_182739_0.orc.

> [!NOTE]
> Ao exportar dados para o Hadoop ou Armazenamento de Blobs do Azure por meio do PolyBase, somente os dados serão exportados, não os nomes das colunas (metadados) conforme definido no comando CRIAR TABELA EXTERNA.

```sql  
-- PolyBase scenario  - export data from SQL Server to Hadoop
-- Create an external table
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
INSERT INTO dbo.FastCustomers2009  
SELECT T.* FROM Insured_Customers T1 JOIN CarSensor_Data T2  
ON (T1.CustomerKey = T2.CustomerKey)  
WHERE T2.YearMeasured = 2009 and T2.Speed > 40;  
```

## <a name="new-catalog-views"></a>Novas exibições do catálogo

As novas exibições do catálogo a seguir mostram os recursos externos.

```sql
SELECT * FROM sys.external_data_sources;   
SELECT * FROM sys.external_file_formats;  
SELECT * FROM sys.external_tables;  
```

 Determine se uma tabela é uma tabela externa usando `is_external`  

```sql  
SELECT name, type, is_external FROM sys.tables WHERE name='myTableName'   
```  

## <a name="next-steps"></a>Próximas etapas  

Para saber mais sobre como solucionar problemas, consulte [PolyBase troubleshooting](../../relational-databases/polybase/polybase-troubleshooting.md)(Solução de problemas do PolyBase).
