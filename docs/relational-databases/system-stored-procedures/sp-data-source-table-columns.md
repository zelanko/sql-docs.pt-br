---
description: sp_data_source_table_columns (Transact-SQL)
title: sp_data_source_table_columns | Microsoft Docs
ms.custom: ''
ms.date: 11/10/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sp_data_source_table_columns
helpviewer_keywords:
- PolyBase
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4153b7546dfce226cb056b7a548efb69f5175e06
ms.sourcegitcommit: 4c3949f620d09529658a2172d00bfe37aeb1a387
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2020
ms.locfileid: "96128770"
---
# <a name="sp_data_source_table_columns-transact-sql"></a>sp_data_source_table_columns (Transact-SQL)

[!INCLUDE [sqlserver2019](../../includes/applies-to-version/sqlserver2019.md)]

Retorna a lista de colunas na tabela de fonte de dados externa.
  
> [!NOTE]
> Esse procedimento é introduzido no [SQL 2019 CU5](../../big-data-cluster/release-notes-big-data-cluster.md#cu5).

![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sqlsyntax
sp_data_source_table_columns
         [ @data_source = ] 'data_source'
       , [ @table_location = ] 'table_location'
[ ; ]
```  

## <a name="arguments"></a>Argumentos

`[ @data_source = ] 'data_source'`   
O nome da fonte de dados externa da qual obter os metadados. O tipo é `sysname` .

`[ @table_location = ] 'table_location'`   
A cadeia de caracteres de local de tabela que identifica a tabela. `table_location` o tipo é `nvarchar(max)` .

## <a name="returns"></a>Retornos

O procedimento armazenado retorna as seguintes informações:

|Nome da coluna |Tipo de Dados |Descrição|
|---|---|---|
|NAME|nvarchar(max)|O nome da coluna.
|TYPE|nvarchar(200)|Nome do tipo de SQL Server
|LENGTH|INT|Comprimento da coluna
|PRECISION|INT|Precisão da coluna
|SCALE|INT|Escala da coluna
|COLLATION|nvarchar(200)|SQL Server Agrupamento de coluna
|IS_NULLABLE|bit|Esta coluna é anulável.
|SOURCE_TYPE_NAME|nvarchar(max)|Nome de tipo específico de back-end. Usado principalmente para depuração. Para fontes ODBC, isso corresponderá à coluna TYPE_NAME resultado para SQLColumns ().
|COMENTÁRIOS|nvarchar(max)|Comentários gerais ou a descrição da coluna. Atualmente, sempre nulo.|

## <a name="permissions"></a>Permissões  

Requer a permissão ALTER ANY EXTERNAL DATA SOURCE.
  
## <a name="remarks"></a>Comentários  

A instância de SQL Server deve ter o recurso  [polybase](../../relational-databases/polybase/polybase-guide.md) instalado.

Este procedimento armazenado dá suporte a conectores para:

- SQL Server
- Oracle
- Teradata
- MongoDB
- CosmosDB

O procedimento armazenado não oferece suporte a conectores de origem ODBC DTA genéricos.

A noção de vazio versus não vazio se relaciona com o comportamento do driver ODBC e da [ `SQLTables` função](../native-client-odbc-api/sqltables.md). Não vazio indica que um objeto contém tabelas, não linhas. Por exemplo, um esquema vazio não contém tabelas no SQL Server. Um banco de dados vazio contém sem tabelas no Teradata. os resultados são uma representação SQL Server do esquema de back-end, conforme interpretado pelo conector do polybase para o back-end. A diferença aqui é que, em vez de apenas passar os resultados da chamada ODBC para o back-end, os resultados são baseados no resultado do código de mapeamento do tipo polybase.

Use [`sp_data_source_objects`](sp-data-source-objects.md) e `sp_data_source_table_columns` para descobrir objetos externos. Esses procedimentos armazenados do sistema retornam o esquema de tabelas que estão disponíveis para serem virtualizadas. O Azure Data Studio usa esses dois procedimentos armazenados para dar suporte à [virtualização de dados](../../azure-data-studio/extensions/data-virtualization-extension.md). Use `sp_data_source_table_columns` para descobrir esquemas de tabela externos representados em SQL Server tipos de dados.

Devido a diferenças entre agrupamentos em dados de origem do Hadoop e agrupamentos com suporte no SQL Server 2019, os comprimentos de tipo de dados recomendados para colunas de tipo de dados varchar em tabelas externas podem ser muito maiores do que o esperado. Isso ocorre por design.

## <a name="example"></a>Exemplo  

O exemplo a seguir retorna as colunas da tabela para uma tabela externa em um SQL Server nomeado `server` , pertencente a um esquema chamado `schema` .
  
```sql
DECLARE @data_source SYSNAME = N'ExternalDataSourceName';
DECLARE @table_location NVARCHAR(400) = N'[database].[schema].[table]';
EXEC sp_data_source_table_columns @data_source, @table_location
```  
  
## <a name="see-also"></a>Consulte também

- [Introdução ao PolyBase](../polybase/polybase-guide.md)
- [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)
- [CREATE EXTERNAL TABLE AS SELECT (Transact-SQL)](../../t-sql/statements/create-external-table-as-select-transact-sql.md)
- [CREATE EXTERNAL TABLE (Transact-SQL)](../../t-sql/statements/create-external-table-transact-sql.md)