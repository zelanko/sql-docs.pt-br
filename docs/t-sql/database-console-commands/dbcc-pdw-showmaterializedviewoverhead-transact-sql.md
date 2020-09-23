---
description: DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD (Transact-SQL)
title: DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD  (Transact-SQL)
ms.custom: seo-dt-2019
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 77c9309afc762a1aa68cfcc22ee6fba4cf119246
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91114931"
---
# <a name="dbcc-pdw_showmaterializedviewoverhead-transact-sql"></a>DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD (Transact-SQL)  

[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

Exibe o número de alterações incrementais nas tabelas de base mantidas para exibições materializadas em [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. A taxa de sobrecarga é calculada como TOTAL_ROWS / MAX (1, BASE_VIEW_ROWS).

![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe

```syntaxsql
DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD ( " [ schema_name .] materialized_view_name  " )
[;]
```

## <a name="arguments"></a>Argumentos

 *schema_name*     
 É o nome do esquema ao qual a exibição pertence.

*materialized_view_name*   
É o nome da exibição materializada.

## <a name="remarks"></a>Comentários

Para manter as exibições materializadas atualizadas com as alterações de dados nas tabelas base, o mecanismo do data warehouse adiciona linhas de acompanhamento a cada exibição afetada para refletir as alterações. A seleção de uma exibição materializada inclui a verificação do índice columnstore clusterizado da exibição e a aplicação de alterações incrementais.As linhas de acompanhamento (TOTAL_ROWS – BASE_VIEW_ROWS) não são eliminadas enquanto os usuários não RECOMPILAREM a exibição materializada.  

A overhead_ratio é calculada como TOTAL_ROWS/MAX(1, BASE_VIEW_ROWS).  Se ela for alta, o desempenho de SELECT será prejudicado.Os usuários podem recompilar a exibição materializada para reduzir a taxa de sobrecarga.

## <a name="permissions"></a>Permissões  
  
Requer a permissão VIEW DATABASE STATE.  

## <a name="examples"></a>Exemplos  

### <a name="a-this-example-returns-the-overhead-ratio-of-a-materialized-view"></a>a. Este exemplo retorna a taxa de sobrecarga de uma exibição materializada.

```sql
DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD ( "dbo.MyIndexedView" )
```

Saída:

|OBJECT_ID|BASE_VIEW_ROWS|TOTAL_ROWS|OVERHEAD_RATIO|
|--------|--------|--------|--------|  
|1234|1|3 |3.0 |

</br>

### <a name="b-this-example-shows-how-the-materialized-view-overhead-increases-as-data-changes-in-base-tables"></a>B. Este exemplo mostra como a sobrecarga da exibição materializada aumenta conforme os dados são alterados nas tabelas base

Criar uma tabela
```sql
CREATE TABLE t1 (c1 INT NOT NULL, c2 INT NOT NULL, c3 INT NOT NULL)
```
Inserir cinco linhas em t1
```sql
INSERT INTO t1 VALUES (1, 1, 1)
INSERT INTO t1 VALUES (2, 2, 2) 
INSERT INTO t1 VALUES (3, 3, 3) 
INSERT INTO t1 VALUES (4, 4, 4) 
INSERT INTO t1 VALUES (5, 5, 5) 
```
Criar exibições materializadas MV1
```sql
CREATE MATERIALIZED VIEW MV1 
WITH (DISTRIBUTION = HASH(c1))  
AS
SELECT c1, COUNT(*) total_number 
FROM dbo.t1 WHERE c1 < 3
GROUP BY c1  
```
A seleção na exibição materializada retorna duas linhas.

|c1|total_number|
|--------|--------| 
|1|1| 
|2|1|

Verifique a sobrecarga da exibição materializada antes de qualquer alteração de dados na tabela base.
```sql
DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD ("dbo.mv1")
```
Saída:

|OBJECT_ID|BASE_VIEW_ROWS|TOTAL_ROWS|OVERHEAD_RATIO|
|--------|--------|--------|--------|  
|587149137|2|2 |1,00000000000000000 |

Atualize a tabela base.  Essa consulta atualiza a mesma coluna na mesma linha 100 vezes para o mesmo valor.  O conteúdo da exibição materializada não é alterado.
```sql
DECLARE @p INT
SELECT @p = 1
WHILE (@p < 101)
BEGIN
UPDATE t1 SET c1 = 1 WHERE c1 = 1
SELECT @p = @p+1
END  
```

A seleção na exibição materializada retorna o mesmo resultado de antes.  

|c1|total_number|
|--------|--------| 
|1|1| 
|2|1|

Veja abaixo a saída de DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD ("dbo.mv1").  100 linhas são adicionadas à exibição materializada (total_row – base_view_rows) e a overhead_ratio é aumentada. 

|OBJECT_ID|BASE_VIEW_ROWS|TOTAL_ROWS|OVERHEAD_RATIO|
|--------|--------|--------|--------|  
|587149137|2|102 |51,00000000000000000 |

Depois de recriar a exibição materializada, todas as linhas de acompanhamento para alterações de dados incrementais são eliminadas e a taxa de sobrecarga de exibição é reduzida.  

```sql
ALTER MATERIALIZED VIEW dbo.MV1 REBUILD
GO
DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD ("dbo.mv1")
```
Saída

|OBJECT_ID|BASE_VIEW_ROWS|TOTAL_ROWS|OVERHEAD_RATIO|
|--------|--------|--------|--------|  
|587149137|2|2 |1,00000000000000000 |

## <a name="see-also"></a>Confira também

[Ajuste de desempenho com a Exibição Materializada](/azure/sql-data-warehouse/performance-tuning-materialized-views)   
[CREATE MATERIALIZED VIEW AS SELECT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-materialized-view-as-select-transact-sql?view=azure-sqldw-latest)   
[ALTER MATERIALIZED VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-materialized-view-transact-sql?view=azure-sqldw-latest)   
[EXPLAIN &#40;Transact-SQL&#41;](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_column_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-column-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_mappings &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-mappings-transact-sql?view=azure-sqldw-latest)   
[Exibições de Catálogo do Azure Synapse Analytics e do Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[Exibições do sistema com suporte no Azure Synapse Analytics](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[Instruções T-SQL com suporte no Azure Synapse Analytics](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements)
