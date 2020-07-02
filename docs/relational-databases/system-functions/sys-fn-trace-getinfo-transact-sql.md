---
title: sys.fn_trace_getinfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: rothja
ms.author: jroth
ms.openlocfilehash: fce5e207ef1ca7f28c0d2088e9f23e701d860b7d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85754012"
---
# <a name="sysfn_trace_getinfo-transact-sql"></a>sys.fn_trace_getinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Retorna informações sobre um rastreamento especificado ou todos os rastreamentos existentes.  
  
> **IMPORTANTE:** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Em vez disso, use Eventos Estendidos.    
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.fn_trace_getinfo ( { trace_id | NULL | 0 | DEFAULT } )  
```  
  
## <a name="arguments"></a>Argumentos  
 *trace_id*  
 É a identificação do rastreamento. *trace_id* é **int**.  As entradas válidas são o número de identificação de um rastreamento, NULL, 0 ou DEFAULT. NULL, 0 e DEFAULT são valores equivalentes neste contexto. Especifique NULL, 0 ou DEFAULT para retornar informações para todos os rastreamentos da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="tables-returned"></a>Tabelas retornadas  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|traceid|**int**|Identificação do rastreamento.|  
|propriedade|**int**|Propriedade do rastreamento.<br /><br /> 1 = Opções de rastreamento. Para obter mais informações, consulte @options em [sp_trace_create &#40;&#41;TRANSACT-SQL ](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md).<br /><br /> 2 = Nome do arquivo<br /><br /> 3 = Tamanho máximo<br /><br /> 4 = Hora da parada<br /><br /> 5 = Status do rastreamento atual. 0 = parado; 1 - em execução.|  
|value|**sql_variant**|Informações sobre a propriedade do rastreamento especificado.|  
  
## <a name="remarks"></a>Comentários  
 Quando é passada a identificação de um rastreamento específico, fn_trace_getinfo retorna informações sobre esse rastreamento. Quando é passada uma ID inválida, a função retorna um conjunto de linhas vazio.  
  
 fn_trace_getinfo acrescenta uma extensão  .trc ao nome de qualquer arquivo de rastreamento incluído no conjunto de resultados. Para obter informações sobre como definir um rastreamento, consulte [sp_trace_create &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md). Para obter informações semelhantes sobre filtros de rastreamento, consulte [Sys. fn_trace_getfilterinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md).  
  
 Para obter um exemplo completo de como usar os procedimentos armazenados de rastreamento, consulte [criar um rastreamento &#40;&#41;Transact-SQL ](../../relational-databases/sql-trace/create-a-trace-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER TRACE no servidor.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna informações sobre todos os rastreamentos ativos.  
  
```  
SELECT * FROM sys.fn_trace_getinfo(0) ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Criar um rastreamento &#40;&#41;de Transact-SQL](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_trace_create](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_trace_generateevent](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_trace_setevent](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_trace_setfilter](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_trace_setstatus](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [sys. fn_trace_getfilterinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)   
 [sys. fn_trace_geteventinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sys.fn_trace_gettable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-gettable-transact-sql.md)  
  
  
