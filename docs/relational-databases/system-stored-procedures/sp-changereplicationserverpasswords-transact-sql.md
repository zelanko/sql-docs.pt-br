---
title: sp_changereplicationserverpasswords (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changereplicationserverpasswords_TSQL
- sp_changereplicationserverpasswords
helpviewer_keywords:
- sp_changereplicationserverpasswords
ms.assetid: 9333da96-3a1c-4adb-9a74-5dac9ce596df
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 9feddab12ea972ea4d7764fccfdd91a7f9b89cec
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68762249"
---
# <a name="sp_changereplicationserverpasswords-transact-sql"></a>sp_changereplicationserverpasswords (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Altera as senhas armazenadas para [!INCLUDE[msCoName](../../includes/msconame-md.md)] a conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows ou logon usado pelos agentes de replicação ao se conectar a servidores em uma topologia de replicação. Geralmente, é necessário alterar uma senha para cada agente individual executando em um servidor, mesmo que todos usem o mesmo logon ou conta. Esse procedimento armazenado permite que você altere a senha de todas as ocorrências de um determinado logon ou conta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows usada por todos os agentes de  replicação executados em um servidor. Esse procedimento armazenado é executado em qualquer servidor na topologia de replicação, no banco de dados mestre.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_changereplicationserverpasswords [ @login_type = ] login_type  
        , [ @login = ] 'login'   
        , [ @password = ] 'password'  
    [ , [ @server = ] 'server' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @login_type = ] login_type`É o tipo de autenticação para as credenciais fornecidas. *LOGIN_TYPE* é **tinyint**, sem padrão.  
  
 **1** = autenticação integrada do Windows  
  
 **0** =  0[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação  
  
`[ @login = ] 'login'`É o nome da conta do Windows ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do logon que está sendo alterado. o *logon* é **nvarchar (257)**, sem padrão  
  
`[ @password = ] 'password'`É a nova senha a ser armazenada para o *logon*especificado. a *senha* é **sysname**, sem padrão.  
  
> [!NOTE]  
>  Depois de alterar a senha de replicação de um agente, você deve parar e reiniciar cada agente que a usa para que a alteração entre em vigor para aquele agente.  
  
`[ @server = ] 'server'`É a conexão do servidor para a qual a senha armazenada está sendo alterada. o *servidor* é **sysname**e pode ser um destes valores:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**distribuidor**|Todas as conexões do agente com o Distribuidor.|  
|**programa**|Todas as conexões do agente com o Publicador.|  
|**farão**|Todas as conexões do agente com o Assinante.|  
|**%** os|Todas as conexões do agente com todos os servidores em uma topologia de replicação.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_changereplicationserverpasswords** é usado com todos os tipos de replicação.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_changereplicationserverpasswords**.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir e modificar as configurações de segurança de replicação](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
  
