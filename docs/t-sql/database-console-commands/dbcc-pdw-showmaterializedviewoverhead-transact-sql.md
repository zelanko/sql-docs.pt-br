---
title: DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD (Transact-SQL) | Microsoft Docs
ms.custom: ''
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
ms.openlocfilehash: ddbb104690c4ded69b1c15628e2f509644c11cb3
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2019
ms.locfileid: "68809875"
---
# <a name="dbcc-pdw_showmaterializedviewoverhead-transact-sql-preview"></a>DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD (Transact-SQL) (versão prévia)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Exibe o número de alterações incrementais nas tabelas de base mantidas para exibições materializadas em [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. A taxa de sobrecarga é calculada como TOTAL_ROWS / MAX (1, BASE_VIEW_ROWS).

![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe

```
DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD ( " [ schema_name .] materialized_view_name  " )
[;]
```
  
## <a name="arguments"></a>Argumentos

 *schema_name*     
 É o nome do esquema ao qual a exibição pertence.

*materialized_view_name*   
É o nome da exibição materializada.

## <a name="remarks"></a>Remarks

Conforme as tabelas subjacentes na definição de uma exibição materializada são modificadas, todas as alterações incrementais nas tabelas base são mantidas para a exibição materializada.  A seleção de uma exibição materializada inclui a verificação da estrutura columnstore clusterizada para a exibição materializada e a aplicação dessas alterações incrementais.   Se o número de alterações incrementais mantidas for alto, o desempenho selecionado poderá se degradar.  Os usuários podem recompilar a exibição materializada para recriar a estrutura de columnstore clusterizada e consolidar todas as alterações incrementais nas tabelas de base.
  
## <a name="permissions"></a>Permissões  
  
Requer a permissão VIEW DATABASE STATE.  

## <a name="example"></a>Exemplo  

Este exemplo retorna o espaço de delta usado em uma exibição materializada.

```sql
DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD ( "dbo.MyIndexedView" )
```

Saída:

|OBJECT_ID|BASE_VIEW_ROWS|TOTAL_ROWS|OVERHEAD_RATIO|
|--------|--------|--------|--------|  
|1234|1|3 |3.0 |

</br>

|OBJECT_ID |BASE_VIEW_ROWS|TOTAL_ROWS|OVERHEAD_RATIO|
|--------|--------|--------|--------|
|4567|0|0|0,0|

</br>

|OBJECT_ID|BASE_VIEW_ROWS|TOTAL_ROWS|OVERHEAD_RATIO|
|--------|--------|--------|--------|
|789|0|2|2.0|

## <a name="see-also"></a>Confira também

[CREATE MATERIALIZED VIEW AS SELECT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-materialized-view-as-select-transact-sql?view=azure-sqldw-latest)   
[ALTER MATERIALIZED VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-materialized-view-transact-sql?view=azure-sqldw-latest)   
[EXPLAIN &#40;Transact-SQL&#41;](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_column_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-column-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_mappings &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-mappings-transact-sql?view=azure-sqldw-latest)   
[Exibições de Catálogo do SQL Data Warehouse e Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[Exibições do sistema com suporte no SQL Data Warehouse do Azure](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[Instruções T-SQL com suporte no SQL Data Warehouse do Azure](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements)