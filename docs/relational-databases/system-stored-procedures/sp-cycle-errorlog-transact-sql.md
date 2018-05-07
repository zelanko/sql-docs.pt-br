---
title: sp_cycle_errorlog (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cycle_errorlog_TSQL
- sp_cycle_errorlog
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cycle_errorlog
ms.assetid: 61a12cbf-78a3-4052-8604-3b29d07573fd
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 42484c0855123181611bf4881c057dec05b8d1e5
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="spcycleerrorlog-transact-sql"></a>sp_cycle_errorlog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fecha o arquivo de log de erros atual e alterna os números de extensão de log de erros, como um reinício do servidor. O novo log de erros contém informações de versão e direitos autorais, além de uma linha que indica que o novo log foi criado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_cycle_errorlog  
```  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="remarks"></a>Remarks  
 Sempre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciado, o log de erros atual é renomeado para **errorlog.1**; **errorlog.1** se torna **errorlog. 2**, **errorlog. 2** se torna **errorlog. 3**, e assim por diante. **sp_cycle_errorlog** permite alternar os arquivos de log de erros sem interromper e iniciar o servidor.  
  
## <a name="permissions"></a>Permissões  
 Permissões de execução para **sp_cycle_errorlog** são restritas a membros do **sysadmin** função de servidor fixa.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir alterna o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
EXEC sp_cycle_errorlog ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_cycle_agent_errorlog &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cycle-agent-errorlog-transact-sql.md)  
  
  
