---
title: sp_changereplicationserverpasswords (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_changereplicationserverpasswords_TSQL
- sp_changereplicationserverpasswords
helpviewer_keywords:
- sp_changereplicationserverpasswords
ms.assetid: 9333da96-3a1c-4adb-9a74-5dac9ce596df
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: f95ea9768d9aaf6e599cb353f32fe6cfd19b4ee8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spchangereplicationserverpasswords-transact-sql"></a>sp_changereplicationserverpasswords (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as senhas armazenadas para o [!INCLUDE[msCoName](../../includes/msconame-md.md)] conta do Windows ou [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon usado por agentes de replicação ao se conectar a servidores em uma topologia de replicação. Geralmente, é necessário alterar uma senha para cada agente individual executando em um servidor, mesmo que todos usem o mesmo logon ou conta. Esse procedimento armazenado permite que você altere a senha de todas as ocorrências de um determinado logon ou conta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows usada por todos os agentes de  replicação executados em um servidor. Esse procedimento armazenado é executado em qualquer servidor na topologia de replicação, no banco de dados mestre.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_changereplicationserverpasswords [ @login_type = ] login_type  
        , [ @login = ] 'login'   
        , [ @password = ] 'password'  
    [ , [ @server = ] 'server' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@login_type** =] *login_type*  
 É o tipo de autenticação para as credenciais fornecidas. *login_type* é **tinyint**, sem padrão.  
  
 **1** = autenticação integrada do Windows  
  
 **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação  
  
 [ **@login** =] **'***login***'**  
 É o nome da conta do Windows ou do logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo alterado. *logon* é **nvarchar (257)**, sem padrão  
  
 [ **@password** =] **'***senha***'**  
 É a nova senha a ser armazenado especificado *logon*. *senha* é **sysname**, sem padrão.  
  
> [!NOTE]  
>  Depois de alterar a senha de replicação de um agente, você deve parar e reiniciar cada agente que a usa para que a alteração entre em vigor para aquele agente.  
  
 [ **@server** =] **'***server***'**  
 É a conexão de servidor para a qual a senha armazenada está sendo alterada. *servidor* é **sysname**, e pode ser um destes valores:  
  
|Value|Description|  
|-----------|-----------------|  
|**Distribuidor**|Todas as conexões do agente com o Distribuidor.|  
|**publisher**|Todas as conexões do agente com o Publicador.|  
|**Assinante**|Todas as conexões do agente com o Assinante.|  
|**%** (padrão)|Todas as conexões do agente com todos os servidores em uma topologia de replicação.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_changereplicationserverpasswords** é usado com todos os tipos de replicação.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** pode executar a função de servidor fixa **sp_changereplicationserverpasswords**.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e modificar configurações de segurança de replicação](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
  
