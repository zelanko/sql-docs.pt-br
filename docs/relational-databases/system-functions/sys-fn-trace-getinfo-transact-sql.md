---
title: sys.fn_trace_getinfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- fn_trace_getinfo
- fn_trace_getinfo_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- traces [SQL Server], status information
- status information [SQL Server], traces
- sys.fn_trace_getinfo function
- fn_trace_getinfo function
ms.assetid: 04b140fe-110a-47b8-98b5-e4c161beb6c9
caps.latest.revision: 33
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3ecb0f6c0d1563ccc68a2ede30b75ba887a479b5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysfntracegetinfo-transact-sql"></a>sys.fn_trace_getinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre um rastreamento especificado ou todos os rastreamentos existentes.  
  
> **IMPORTANTE:** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Em vez disso, use Eventos Estendidos.    
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.fn_trace_getinfo ( { trace_id | NULL | 0 | DEFAULT } )  
```  
  
## <a name="arguments"></a>Argumentos  
 *trace_id*  
 É a identificação do rastreamento. *trace_id* é **int**.  Entradas válidas são o número da ID de um rastreamento, NULL, 0 ou DEFAULT. NULL, 0 e DEFAULT são valores equivalentes neste contexto. Especifique NULL, 0 ou DEFAULT para retornar informações para todos os rastreamentos da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="tables-returned"></a>Tabelas retornadas  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|traceid|**Int**|Identificação do rastreamento.|  
|propriedade|**Int**|Propriedade do rastreamento.<br /><br /> 1 = Opções de rastreamento. Para obter mais informações, consulte @options na [sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md).<br /><br /> 2 = Nome do arquivo<br /><br /> 3 = Tamanho máximo<br /><br /> 4 = Hora da parada<br /><br /> 5 = Status do rastreamento atual. 0 = parado; 1 - em execução.|  
|value|**sql_variant**|Informações sobre a propriedade do rastreamento especificado.|  
  
## <a name="remarks"></a>Remarks  
 Quando é passada a identificação de um rastreamento específico, fn_trace_getinfo retorna informações sobre esse rastreamento. Quando é passada uma ID inválida, a função retorna um conjunto de linhas vazio.  
  
 fn_trace_getinfo acrescenta uma extensão  .trc ao nome de qualquer arquivo de rastreamento incluído no conjunto de resultados. Para obter informações sobre como definir um rastreamento, consulte [sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md). Para obter informações similares sobre filtros de rastreamento, consulte [fn_trace_getfilterinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md).  
  
 Para obter um exemplo completo de como usar procedimentos armazenados de rastreamento, consulte [criar um rastreamento &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER TRACE no servidor.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna informações sobre todos os rastreamentos ativos.  
  
```  
SELECT * FROM sys.fn_trace_getinfo(0) ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Criar um rastreamento &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)   
 [sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)   
 [sp_trace_generateevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [sys.fn_trace_getfilterinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)   
 [sys.fn_trace_geteventinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sys.fn_trace_gettable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-gettable-transact-sql.md)  
  
  
