---
title: sys.sp_cleanup_temporal_history | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: 
ms.prod_service: sql-database
ms.service: sql-database
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6eff30b4-b261-4f1f-b93c-1f69d754298d
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1539ae456b1159cf4fdd458948a905171e3d33aa
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="temporal-table---sysspcleanuptemporalhistory"></a>Tabela temporal - sys.sp_cleanup_temporal_history
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

Remove todas as linhas da tabela de histórico temporal que corresponde a período HISTORY_RETENTION configurado em uma única transação.
  
## <a name="syntax"></a>Sintaxe  
```  
sp_cleanup_temporal_history [@schema_name = ] schema_name, [@table_name = ] table_name [, [@row_count=] @row_count_var [OUTPUT]]
```  
  
## <a name="arguments"></a>Argumentos  

*@table_name*

O nome da tabela temporal para qual a retenção de limpeza é chamada.

*schema_name*

O nome do esquema ao qual tabela temporal atual pertence a

*row_count_var* [OUTPUT]

O parâmetro de saída que retorna o número de linhas excluídas. Esse parâmetro se a tabela de histórico tem columnstore índice clusterizado, irá retornar sempre 0.
  
## <a name="remarks"></a>Remarks
Esse procedimento armazenado pode ser usado somente com tabelas temporais que o período de retenção finito especificado.
Use este procedimento armazenado apenas se você precisa limpar imediatamente todas as linhas antigas da tabela de histórico. Você deve saber o que ele pode ter um impacto significativo sobre o log de banco de dados e o subsistema de e/s, ele exclui todas as linhas qualificadas dentro da mesma transação. 

É recomendável sempre confiar em uma tarefa em segundo plano interno para limpeza que remove antigos linhas com o mínimo de impacto em cargas de trabalho regulares e banco de dados em geral.

## <a name="permissions"></a>Permissões  
 Requer permissões db_owner.  

## <a name="example"></a>Exemplo

```
declare @rowcnt int
EXEC sys.sp_cleanup_temporal_history 'dbo', 'Department', @rowcnt output
select @rowcnt
```

## <a name="see-also"></a>Consulte também

[Política de retenção de tabelas temporais](https://docs.microsoft.com/azure/sql-database/sql-database-temporal-tables-retention-policy)
