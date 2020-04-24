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
ms.openlocfilehash: f0f50ecd1b6cb74367512822b0257094aa3e3d5b
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81636398"
---
# <a name="drop-workload-group-transact-sql"></a>DROP WORKLOAD GROUP (Transact-SQL)

## <a name="click-a-product"></a>Clique em um produto!

Na linha a seguir, clique em qualquer nome de produto de seu interesse. O clique exibe conteúdo diferente aqui nesta página da Web, apropriado para qualquer produto no qual você clicar.

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||=sqlallproducts-allversions"

> |||||
> |---|---|---|---|
> |**_\* SQL Server \*_** &nbsp;|[Instância gerenciada<br />do Banco de Dados SQL](drop-workload-group-transact-sql.md?view=azuresqldb-mi-current)|[Azure Synapse<br />Analytics](drop-workload-group-transact-sql.md?view=azure-sqldw-latest)|

&nbsp;

## <a name="sql-server-and-sql-database-managed-instance"></a>Instância gerenciada do SQL Server e do Banco de Dados SQL

Descarta um grupo de carga de trabalho do Administrador de Recursos definido pelo usuário existente.

![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

## <a name="syntax"></a>Sintaxe

```syntaxsql
DROP WORKLOAD GROUP group_name
[;]
```

## <a name="arguments"></a>Argumentos

*group_name* é o nome de um grupo de carga de trabalho definido pelo usuário existente.

## <a name="remarks"></a>Comentários

A instrução DROP WORKLOAD GROUP não é permitida nos grupos padrão ou internos do Administrador de Recursos.

Ao executar instruções DDL, é recomendável estar familiarizado com os estados do Administrador de Recursos. Para obter mais informações, consulte [Resource Governor](../../relational-databases/resource-governor/resource-governor.md).

Se um grupo de carga de trabalho contiver sessões ativas, o descarte ou a movimentação do grupo para um pool de recursos diferente não terá êxito quando a instrução ALTER RESOURCE GOVERNOR RECONFIGURE for chamada para aplicar a alteração. Para evitar esse problema, é possível executar uma das seguintes ações:

- Aguardar até que todas as sessões do grupo afetado sejam desconectadas e depois executar novamente a instrução ALTER RESOURCE GOVERNOR RECONFIGURE.

- Interromper explicitamente as sessões do grupo afetado usando o comando KILL e depois executar novamente a instrução ALTER RESOURCE GOVERNOR RECONFIGURE.

- Reinicie o servidor. Depois que o processo de reinicialização estiver concluído, o grupo excluído não será criado e um grupo movido usará a atribuição do novo pool de recursos.

- Em um cenário no qual você emitiu a instrução DROP WORKLOAD GROUP mas decide que não deseja parar sessões explicitamente para aplicar a mudança, é possível recriar o grupo usando o mesmo nome que ele tinha antes de você emitir a instrução DROP e depois mover o grupo para o pool de recursos original. Para aplicar as alterações, execute a instrução ALTER RESOURCE GOVERNOR RECONFIGURE.

## <a name="permissions"></a>Permissões

Requer a permissão CONTROL SERVER.

## <a name="examples"></a>Exemplos

O seguinte exemplo descarta o grupo de carga de trabalho denominado `adhoc`.

```
DROP WORKLOAD GROUP adhoc;
GO
ALTER RESOURCE GOVERNOR RECONFIGURE;
GO
```

## <a name="see-also"></a>Consulte Também

- [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)
- [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)  
- [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)
- [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)
- [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)
- [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)
- [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

> ||||
> |---|---|---|
> |[SQL Server](drop-workload-group-transact-sql.md?view=sql-server-2017)||[Instância gerenciada<br />do Banco de Dados SQL](drop-workload-group-transact-sql.md?view=azuresqldb-mi-current)||**_\* Azure Synapse<br />Analytics \*_** &nbsp;||||

&nbsp;

## <a name="azure-synapse-analytics-preview"></a>Azure Synapse Analytics (versão prévia)

Remove um grupo de carga de trabalho.  Quando a instrução for concluída, as configurações estarão em vigor.

![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

## <a name="syntax"></a>Sintaxe

```
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

[CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)

::: moniker-end
