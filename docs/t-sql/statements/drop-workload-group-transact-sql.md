---
title: DROP WORKLOAD GROUP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/10/2020
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_WORKLOAD_GROUP_TSQL
- DROP WORKLOAD GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- DROP WORKLOAD GROUP statement
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azure-sqldw-latest||=azuresqldb-mi-current'
ms.openlocfilehash: 74725f71656141c4e441f80b4ba059012b4b65bb
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552751"
---
# <a name="drop-workload-group-transact-sql"></a>DROP WORKLOAD GROUP (Transact-SQL)

[!INCLUDE[select-product](../../includes/select-product.md)]

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

||||
|---|---|---|
|**_\* SQL Server \*_** &nbsp;|[Instância gerenciada<br />do Banco de Dados SQL](drop-workload-group-transact-sql.md?view=azuresqldb-mi-current)|[Azure Synapse<br />Analytics](drop-workload-group-transact-sql.md?view=azure-sqldw-latest)|
||||

&nbsp;

## <a name="sql-server-and-sql-database-managed-instance"></a>Instância gerenciada do SQL Server e do Banco de Dados SQL

[!INCLUDE [DROP WORKLOAD GROUP](../../includes/drop-workload-group.md)]
  
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

||||
|---|---|---|
|[SQL Server](drop-workload-group-transact-sql.md?view=sql-server-2017)|**_Instância gerenciada do \*Banco de Dados SQL<br /> \*_** &nbsp;|[Azure Synapse<br />Analytics](drop-workload-group-transact-sql.md?view=azure-sqldw-latest)|
||||

&nbsp;

##  <a name="sql-server-and-sql-database-managed-instance"></a>Instância gerenciada do SQL Server e do Banco de Dados SQL

[!INCLUDE [DROP WORKLOAD GROUP](../../includes/drop-workload-group.md)]

::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

||||
|---|---|---|
|[SQL Server](drop-workload-group-transact-sql.md?view=sql-server-2017)|[Instância gerenciada<br />do Banco de Dados SQL](drop-workload-group-transact-sql.md?view=azuresqldb-mi-current)| **_\* Azure Synapse<br />Analytics \*_** &nbsp;|
||||

&nbsp;

## <a name="azure-synapse-analytics"></a>Azure Synapse Analytics 

Remove um grupo de carga de trabalho.  Quando a instrução for concluída, as configurações estarão em vigor.

![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

## <a name="syntax"></a>Sintaxe

```syntaxsql
DROP WORKLOAD GROUP group_name  
```

## <a name="arguments"></a>Argumentos

*group_name*  
É o nome de um grupo de carga de trabalho definido pelo usuário existente.

## <a name="remarks"></a>Comentários

Um grupo de carga de trabalho não poderá ser removido se houver classificadores para ele.  Remova os classificadores para que o grupo de carga de trabalho seja descartado.  Se houver solicitações ativas usando recursos do grupo de carga de trabalho que está sendo removido, a instrução de remoção da carga de trabalho será bloqueada por trás delas.

## <a name="examples"></a>Exemplos

Use o exemplo de código a seguir para determinar quais classificadores precisam ser descartados para que o grupo de carga de trabalho possa ser removido.

```sql
SELECT c.name as classifier_name
      ,'DROP WORKLOAD CLASSIFIER '+c.name as drop_command
  FROM sys.workload_management_workload_classifiers c
  JOIN sys.workload_management_workload_groups g
    ON c.group_name = g.name
  WHERE g.name = 'wgXYZ' --change the filter to the workload being dropped
```

## <a name="permissions"></a>Permissões

Requer a permissão CONTROL DATABASE

## <a name="see-also"></a>Confira também

- [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)
- [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)
- [sys.workload_management_workload_groups](../../relational-databases/system-catalog-views/sys-workload-management-workload-groups-transact-sql.md)
- [sys.dm_workload_management_workload_groups_stats](../../relational-databases/system-dynamic-management-views/sys-dm-workload-management-workload-group-stats-transact-sql.md)
- [Início Rápido: Configurar isolamento da carga de trabalho com o T-SQL](/azure/sql-data-warehouse/quickstart-configure-workload-isolation-tsql)

::: moniker-end
