---
description: sp_changeqreader_agent (Transact-SQL)
title: sp_changeqreader_agent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changeqreader_agent_TSQL
- sp_changeqreader_agent
helpviewer_keywords:
- sp_changeqreader_agent
ms.assetid: d3fe79c5-31ef-4565-bf38-b476b5fb16f7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 08e7e0571cab57d50da670495af95709482899a3
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543652"
---
# <a name="sp_changeqreader_agent-transact-sql"></a>sp_changeqreader_agent (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Altera as propriedades de segurança de um Agente de Leitor de Fila. Esse procedimento armazenado é executado no Distribuidor, no banco de dados de distribuição, ou no Publicador, no banco de dados de publicação.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_changeqreader_agent [ [ @job_login = ] 'job_login' ]  
    [ , [ @job_password = ] 'job_password' ]  
    [ , [ @frompublisher = ] frompublisher   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @job_login = ] 'job_login'` É o logon da [!INCLUDE[msCoName](../../includes/msconame-md.md)] conta do Windows na qual o agente é executado. *job_login* é **nvarchar (257)**, com um padrão de NULL.  
  
`[ @job_password = ] 'job_password'` É a senha para a conta do Windows na qual o agente é executado. *job_password* é **sysname**, com um padrão de NULL.  
  
`[ @frompublisher = ] frompublisher` É se o procedimento estiver sendo executado no Publicador. *frompublisher* é bit, com um valor padrão de **0**. Um valor de **1** significa que o procedimento está sendo executado do Publicador no banco de dados de publicação.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_changeqreader_agent** é usado na replicação transacional.  
  
 **sp_changeqreader_agent** é usado para alterar a conta do Windows na qual um agente de leitor de fila é executado. Você pode alterar a senha de um logon de Windows existente ou pode fornecer um logon e uma senha de Windows novos.  
  
 Depois de alterar o logon ou a senha de um agente, você deve parar e reiniciar o agente antes que as alterações entrem em vigor.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_changeqreader_agent**.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir e modificar configurações de segurança de replicação](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [sp_addqreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md)  
  
  
