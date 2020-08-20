---
description: sp_trace_setstatus (Transact-SQL)
title: sp_trace_setstatus (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_trace_setstatus_TSQL
- sp_trace_setstatus
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_setstatus
ms.assetid: 29e7a7d7-b9c1-414a-968a-fc247769750d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 464bf489f8e0d62ea0096b917b29d1bcc099c811
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480916"
---
# <a name="sp_trace_setstatus-transact-sql"></a>sp_trace_setstatus (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Modifica a situação atual do rastreamento especificado.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Em vez disso, use Eventos Estendidos.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_trace_setstatus [ @traceid = ] trace_id , [ @status = ] status  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @traceid = ] trace_id` É a ID do rastreamento a ser modificado. *trace_id* é **int**, sem padrão. O usuário emprega esse *trace_id* valor para identificar, modificar e controlar o rastreamento. Para obter informações sobre como recuperar o *trace_id*, consulte [sys. fn_trace_getinfo &#40;&#41;do Transact-SQL ](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md).  
  
`[ @status = ] status` Especifica a ação a ser implementada no rastreamento. o *status* é **int**, sem padrão.  
  
 A tabela a seguir descreve o status que pode ser especificado.  
  
|Status|Descrição|  
|------------|-----------------|  
|**0**|Interrompe o rastreamento especificado.|  
|**1**|Inicia o rastreamento especificado.|  
|**2**|Fecha o rastreamento especificado e exclui sua definição do servidor.|  
  
> [!NOTE]  
>  Um rastreamento deve ser interrompido primeiro antes de ser encerrado. Um rastreamento deve ser interrompido e encerrado primeiro antes de ser exibido.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 A tabela a seguir descreve os valores de código que os usuários podem obter após a conclusão do procedimento armazenado.  
  
|Código de retorno|Descrição|  
|-----------------|-----------------|  
|**0**|Sem erros.|  
|**1**|Erro desconhecido.|  
|**8**|O status especificado não é válido.|  
|**9**|O Identificador de Rastreamento especificado não é válido.|  
|**13**|Memória insuficiente. Retornado quando não há memória suficiente para executar a ação especificada.|  
  
 Se o rastreamento já estiver no estado especificado, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará **0**.  
  
## <a name="remarks"></a>Comentários  
 Parâmetros de todos os procedimentos armazenados de rastreamento do SQL (**sp_trace_xx**) são estritamente tipados. Se esses parâmetros não forem chamados com os tipos de dados com parâmetro de entrada corretos, como especificado na descrição do argumento, o procedimento armazenado retornará um erro.  
  
 Para obter um exemplo de como usar procedimentos armazenados de rastreamento, veja [Criar um rastreamento &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 O usuário deve ter a permissão ALTER TRACE.  
  
## <a name="see-also"></a>Consulte Também  
 [sys. fn_trace_geteventinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sys. fn_trace_getfilterinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_trace_generateevent ](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_trace_setfilter ](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [Rastreamento do SQL](../../relational-databases/sql-trace/sql-trace.md)  
  
  
