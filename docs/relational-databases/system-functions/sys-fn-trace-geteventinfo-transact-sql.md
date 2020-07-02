---
title: sys.fn_trace_geteventinfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_trace_geteventinfo
- fn_trace_geteventinfo_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- events [SQL Server], status information
- fn_trace_geteventinfo function
- sys.fn_trace_geteventinfo function
- status information [SQL Server], events
ms.assetid: 5b1c858a-ca43-4e2b-9d67-8654daaf0cc5
author: rothja
ms.author: jroth
ms.openlocfilehash: e079f473cbf08dc1a67f031d973149be0e987a2a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85762810"
---
# <a name="sysfn_trace_geteventinfo-transact-sql"></a>sys.fn_trace_geteventinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Retorna informações sobre um evento sendo rastreado.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Em vez disso, use Eventos Estendidos.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn_trace_geteventinfo ( trace_id )  
```  
  
## <a name="arguments"></a>Argumentos  
 *trace_id*  
 É a identificação do rastreamento. *trace_id* é **int**, sem padrão.  
  
## <a name="tables-returned"></a>Tabelas retornadas  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**1008**|**int**|ID do evento rastreado|  
|**columnid**|**int**|Números de ID de todas as colunas coletadas para cada evento|  
  
## <a name="remarks"></a>Comentários  
 Quando passado a ID de um rastreamento específico, **fn_trace_geteventinfo** retorna informações sobre esse rastreamento. Quando é passada uma ID inválida, a função retorna um conjunto de linhas vazio.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER TRACE no servidor.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna informações sobre o rastreamento número 2.  
  
```  
SELECT * FROM fn_trace_geteventinfo(2) ;  
GO  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_trace_setevent](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_trace_setfilter](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [Criar um rastreamento &#40;&#41;de Transact-SQL](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_trace_create](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_trace_generateevent](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_trace_setstatus](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [sys. fn_trace_getinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)   
 [sys. fn_trace_gettable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-gettable-transact-sql.md)   
 [sys.fn_trace_getfilterinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)  
  
  
