---
title: sp_cycle_agent_errorlog (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_cycle_agent_errorlog
- sp_cycle_agent_errorlog_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_cycle_agent_errorlog
ms.assetid: 8aa96182-60b7-4d7b-b2a7-ccce70378c6e
caps.latest.revision: "16"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 59c6136224bc639c4609dd149ade598b3ef80940
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="spcycleagenterrorlog-transact-sql"></a>sp_cycle_agent_errorlog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Fecha o arquivo de log de erros atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e alterna os números de extensão do log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent exatamente como um reinício do servidor. O novo log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent contém uma linha que indica que o novo log foi criado.  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_cycle_agent_errorlog  
```  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="remarks"></a>Comentários  
 Sempre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é iniciado, atual [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] log de erros do agente foi renomeada para **SQLAgent. 1**; **SQLAgent. 1** se torna **SQLAgent. 2**, **SQLAgent. 2** se torna **SQLAgent. 3**, e assim por diante. **sp_cycle_agent_errorlog** permite alternar os arquivos de log de erros sem interromper e iniciar o servidor.  
  
 Esse procedimento armazenado deve ser executado a partir de **msdb** banco de dados.  
  
## <a name="permissions"></a>Permissões  
 Permissões de execução para **sp_cycle_agent_errorlog** são restritas a membros do **sysadmin** função de servidor fixa.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir alterna o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_cycle_agent_errorlog ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_cycle_errorlog &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-cycle-errorlog-transact-sql.md)  
  
  
