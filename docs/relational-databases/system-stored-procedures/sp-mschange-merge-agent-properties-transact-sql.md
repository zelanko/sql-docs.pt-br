---
title: sp_MSchange_merge_agent_properties (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_MSchange_merge_agent_properties_TSQL
- sp_MSchange_merge_agent_properties
helpviewer_keywords:
- sp_MSchange_merge_agent_properties
ms.assetid: f775fa0f-28c7-4863-89ce-7bcfa1ab8b5e
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f3563086e662ceb1dbe5cb8e8ea5b96b0c9430cc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spmschangemergeagentproperties-transact-sql"></a>sp_MSchange_merge_agent_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as propriedades de um trabalho do Merge Agent que é executado em um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou versão posterior do distribuidor. Esse procedimento armazenado é usado para alterar propriedades quando o Publicador é executado em uma instância do [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. Esse procedimento armazenado é executado no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_MSchange_merge_agent_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
        , [ @subscriber = ] 'subscriber'   
        , [ @subscriber_db = ] 'subscriber_db'   
        , [ @property = ] 'property'   
        , [ @value = ] 'value' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher**  =] **'***publicador***'**  
 É o nome do Publicador. *publicador* é **sysname**, sem padrão.  
  
 [  **@publisher_db=** ] **'***publisher_db***'**  
 É o nome do banco de dados de publicação. *publisher_db* é **sysname**, sem padrão.  
  
 [  **@publication =** ] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, sem padrão.  
  
 [  **@subscriber=** ] **'***assinante***'**  
 É o nome do Assinante. *assinante* é **sysname**, sem padrão.  
  
 [  **@subscriber_db=** ] **'***subscriber_db***'**  
 É o nome do banco de dados de assinatura. *subscriber_db* é **sysname**, sem padrão.  
  
 [  **@property =** ] **'***propriedade***'**  
 É a propriedade da publicação a ser alterada. *propriedade* é **sysname**, sem padrão.  
  
 [  **@value =** ] **'***valor***'**  
 É o novo valor da propriedade. *valor* é **nvarchar (524)**, com um padrão NULL.  
  
 Essa tabela descreve as propriedades do trabalho de Agente de Mesclagem que podem ser alteradas e restrições nos valores dessas propriedades.  
  
|Propriedade|Valor|Description|  
|--------------|-----------|-----------------|  
|**Descrição**||Uma descrição breve da assinatura.|  
|**merge_job_login**||Logon para a conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows na qual o agente é executado.|  
|**merge_job_password**||Senha para a conta do Windows na qual o trabalho do agente é executado.|  
|**publisher_login**||Logon a ser usado na conexão com um Publicador para sincronizar a assinatura.|  
|**publisher_password**||Senha do Publicador.<br /><br /> [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]|  
|**publisher_security_mode**|**1**|Autenticação do Windows.<br /><br /> [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]|  
||**0**|Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**subscriber_login**||Logon a ser usado na conexão com um Assinante para sincronizar a assinatura.|  
|**subscriber_password**||Senha do assinante.<br /><br /> [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]|  
|**subscriber_security_mode**|**1**|Autenticação do Windows.<br /><br /> [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]|  
||**0**|Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
> [!NOTE]  
>  Depois de alterar o logon ou a senha de um agente, você deve parar e reiniciar o agente antes que as alterações entrem em vigor.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_MSchange_merge_agent_properties** é usado em replicação de mesclagem.  
  
 Quando o publicador é executado em uma instância do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou versão posterior, você deve usar [sp_changemergesubscription](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md) para alterar as propriedades de um trabalho do agente de mesclagem que sincroniza uma assinatura push executa no distribuidor.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** pode executar a função de servidor fixa no distribuidor **sp_MSchange_merge_agent_properties**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_addmergepushsubscription_agent &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)   
 [sp_addmergesubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)  
  
  
