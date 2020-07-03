---
title: sp_cycle_agent_errorlog (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cycle_agent_errorlog
- sp_cycle_agent_errorlog_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cycle_agent_errorlog
ms.assetid: 8aa96182-60b7-4d7b-b2a7-ccce70378c6e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ceda2ac8c7d5280515d28e489b0c568804a41242
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85868404"
---
# <a name="sp_cycle_agent_errorlog-transact-sql"></a>sp_cycle_agent_errorlog (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Fecha o arquivo de log de erros atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e alterna os números de extensão do log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent exatamente como um reinício do servidor. O novo log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent contém uma linha que indica que o novo log foi criado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_cycle_agent_errorlog  
```  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 Toda vez que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o agente é iniciado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] log de erros do agente atual é renomeado para **SQLAgent. 1**; O **SQLAgent. 1** se torna o **SQLAgent. 2**, o **SQLAgent. 2** se torna **SQLAgent. 3**e assim por diante. **sp_cycle_agent_errorlog** permite que você alterne os arquivos de log de erros sem parar e iniciar o servidor.  
  
 Esse procedimento armazenado deve ser executado do banco de dados **msdb** .  
  
## <a name="permissions"></a>Permissões  
 As permissões de execução para **sp_cycle_agent_errorlog** são restritas a membros da função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir alterna o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_cycle_agent_errorlog ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_cycle_errorlog](../../relational-databases/system-stored-procedures/sp-cycle-errorlog-transact-sql.md)  
  
  
