---
title: Consultas do PolyBase | Microsoft Docs
ms.custom: ''
ms.date: 12/08/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: polybase
ms.tgt_pltfrm: ''
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3dfda421d6fe8bc221c49863eacba740d44bd690
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37312116"
---
# <a name="polybase-queries"></a>Consultas do PolyBase
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este artigo fornece exemplos de consultas que usam o recurso [PolyBase](../../relational-databases/polybase/polybase-guide.md) do SQL Server (a partir de 2016). Antes de usar esses exemplos, você também deve entender as instruções T-SQL necessárias para configurar o PolyBase (confira [PolyBase T-SQL objects](../../relational-databases/polybase/polybase-t-sql-objects.md)(Objetos T-SQL do PolyBase).)
  
## <a name="queries"></a>Consultas  
 Execute instruções Transact-SQL em tabelas externas ou use as ferramentas de BI para consultar tabelas externas.
  
## <a name="select-from-external-table"></a>SELECT da tabela externa  
 Uma consulta simples que retorna dados de uma tabela externa definida.  
  
```sql  
SELECT TOP 10 * FROM [dbo].[SensorData];   
```
  
 Uma consulta simples que inclui um predicado.

```
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65;
```

## <a name="join-external-tables-with-local-tables"></a>JOIN de tabelas externas com tabelas locais

```
SELECT InsuranceCustomers.FirstName,   
                           InsuranceCustomers.LastName,   
                           SensorData.Speed  
FROM InsuranceCustomers INNER JOIN SensorData    
ON InsuranceCustomers.CustomerKey = SensorData.CustomerKey   
WHERE SensorData.Speed > 65   
ORDER BY SensorData.Speed DESC  
  
```  
  
## <a name="pushdown-computation-to-hadoop"></a>Computação de aplicação para Hadoop

Variações de aplicação são mostradas aqui.

### <a name="pushdown-for-selecting-a-subset-of-rows"></a>Aplicação para selecionar um subconjunto de linhas

Use aplicação de predicado para melhorar o desempenho de uma consulta que seleciona um subconjunto de linhas de uma tabela externa.

Neste exemplo, o SQL Server 2016 inicia um trabalho de map-reduce para recuperar as linhas que correspondem ao predicado `customer.account_balance < 200000` no Hadoop. Como a consulta pode ser concluída com êxito sem examinar todas as linhas na tabela, somente as linhas que atendem aos critérios de predicado são copiadas para o SQL Server. Isso economiza bastante tempo e exige menos espaço de armazenamento temporário quando o número de saldos do cliente < 200000 é pequeno em comparação com o número de clientes com saldos o cliente >= 200000.

```
SELECT * FROM customer WHERE customer.account_balance < 200000
SELECT * FROM SensorData WHERE Speed > 65;  
```

### <a name="pushdown-for-selecting-a-subset-of-columns"></a>Aplicação para selecionar um subconjunto de colunas

Use aplicação de predicado para melhorar o desempenho de uma consulta que seleciona um subconjunto de colunas de uma tabela externa.

Nesta consulta, o SQL Server inicia um trabalho map-reduce para pré-processar o arquivo de texto delimitado por Hadoop para que somente os dados de duas colunas, customer.name e customer.zip_code, serão copiados para o SQL Server PDW.

```
SELECT customer.name, customer.zip_code FROM customer WHERE customer.account_balance < 200000
```

### <a name="pushdown-for-basic-expressions-and-operators"></a>Aplicação de operadores e expressões básicas

O SQL Server permite os seguintes operadores e expressões básicas para a aplicação de predicado.

+ Operadores de comparação binária ( \<, >, =, !=, <>, >=, <= ) para valores de hora, data e numéricos.

+ Operadores aritméticos ( +, -, *, /, % ).

+ Operadores lógicos (AND, OR).

+ Operadores unários (NOT, IS NULL, IS NOT NULL).

Os operadores BETWEEN, NOT, IN e LIKE podem ser propagados. O comportamento real depende de como o otimizador de consulta reescreve as expressões do operador como uma série de instruções que usam operadores relacionais básicos.

A consulta neste exemplo tem vários predicados que podem ser propagados para o Hadoop. O SQL Server pode enviar por push trabalhos map-reduce para o Hadoop para executar o predicado `customer.account_balance <= 200000`. A expressão `BETWEEN 92656 and 92677` também é composta por operações binárias e lógicas que podem ser enviadas por push para Hadoop. A lógica **E** no `customer.account_balance and customer.zipcode` é uma expressão final.

Dada essa combinação de predicados, os trabalhos map-reduce podem executar tudo da cláusula WHERE. Apenas os dados que atendem aos critérios de SELECT serão copiados para o SQL Server PDW.

```
SELECT * FROM customer WHERE customer.account_balance <= 200000 AND customer.zipcode BETWEEN 92656 AND 92677
```

### <a name="force-pushdown"></a>Forçar aplicação

```
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65
OPTION (FORCE EXTERNALPUSHDOWN);
```

### <a name="disable-pushdown"></a>Desabilitar aplicação

```
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65
OPTION (DISABLE EXTERNALPUSHDOWN);
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
INSERT INTO dbo.FastCustomer2009  
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
