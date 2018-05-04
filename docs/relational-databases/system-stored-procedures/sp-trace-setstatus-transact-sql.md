---
title: sp_trace_setstatus (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_trace_setstatus_TSQL
- sp_trace_setstatus
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_setstatus
ms.assetid: 29e7a7d7-b9c1-414a-968a-fc247769750d
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 966a568e3195f194bb442eae5cf8f4b3bff550c5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sptracesetstatus-transact-sql"></a>sp_trace_setstatus (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica a situação atual do rastreamento especificado.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Em vez disso, use Eventos Estendidos.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_trace_setstatus [ @traceid = ] trace_id , [ @status = ] status  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@traceid=** ] *trace_id*  
 É a ID do rastreamento a ser modificado. *trace_id* é **int**, sem padrão. O usuário emprega este *trace_id* valor para identificar, modificar e controlar o rastreamento. Para obter informações sobre como recuperar o *trace_id*, consulte [fn_trace_getinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md).  
  
 [ **@status=** ] *status*  
 Especifica a ação a ser implementada no rastreamento. *status* é **int**, sem padrão.  
  
 A tabela a seguir descreve o status que pode ser especificado.  
  
|Status|Description|  
|------------|-----------------|  
|**0**|Interrompe o rastreamento especificado.|  
|**1**|Inicia o rastreamento especificado.|  
|**2**|Fecha o rastreamento especificado e exclui sua definição do servidor.|  
  
> [!NOTE]  
>  Um rastreamento deve ser interrompido primeiro antes de ser encerrado. Um rastreamento deve ser interrompido e encerrado primeiro antes de ser exibido.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 A tabela a seguir descreve os valores de código que os usuários podem obter após a conclusão do procedimento armazenado.  
  
|Código de retorno|Description|  
|-----------------|-----------------|  
|**0**|Nenhum erro.|  
|**1**|Erro desconhecido.|  
|**8**|O status especificado não é válido.|  
|**9**|O Identificador de Rastreamento especificado não é válido.|  
|**13**|Memória insuficiente. Retornado quando não há memória suficiente para executar a ação especificada.|  
  
 Se o rastreamento já estiver no estado especificado, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará **0**.  
  
## <a name="remarks"></a>Remarks  
 Os parâmetros de rastreamento de SQL todos os procedimentos armazenados (**sp_trace_xx**) são rigorosamente tipados. Se esses parâmetros não forem chamados com os tipos de dados com parâmetro de entrada corretos, como especificado na descrição do argumento, o procedimento armazenado retornará um erro.  
  
 Para obter um exemplo de como usar procedimentos armazenados de rastreamento, veja [Criar um rastreamento &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 O usuário deve ter a permissão ALTER TRACE.  
  
## <a name="see-also"></a>Consulte também  
 [sys.fn_trace_geteventinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sys.fn_trace_getfilterinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)   
 [sp_trace_generateevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [Rastreamento do SQL](../../relational-databases/sql-trace/sql-trace.md)  
  
  
