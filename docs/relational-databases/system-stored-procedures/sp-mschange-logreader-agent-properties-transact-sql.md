---
title: sp_MSchange_logreader_agent_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_MSchange_logreader_agent_properties_TSQL
- sp_MSchange_logreader_agent_properties
helpviewer_keywords:
- sp_MSchange_logreader_agent_properties
ms.assetid: 925df9d3-a041-4046-8e17-c47f40edb86d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 30f7ee9e8488fad2311adae55f973bab8a22ec22
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52770288"
---
# <a name="spmschangelogreaderagentproperties-transact-sql"></a>sp_MSchange_logreader_agent_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as propriedades de um trabalho do Log Reader Agent que é executado em um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou versão posterior do distribuidor. Esse procedimento armazenado é usado para alterar propriedades quando o Publicador é executado em uma instância do [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. Esse procedimento armazenado é executado no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_MSchange_logreader_agent_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publisher_security_mode = ] publisher_security_mode  
        , [ @publisher_login = ] 'publisher_login'  
        , [ @publisher_password = ] 'publisher_password'   
        , [ @job_login = ] 'job_login'  
        , [ @job_password = ] 'job_password'  
        , [ @publisher_type = ] 'publisher_type'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@publisher** =] **'***publisher***'**  
 É o nome do Publicador. *Publisher* está **sysname**, sem padrão.  
  
 [  **@publisher_db=** ] **'***publisher_db***'**  
 É o nome do banco de dados de publicação. *publisher_db* está **sysname**, sem padrão.  
  
 [ **@publisher_security_mode**=] *publisher_security_mode*  
 É o modo de segurança usado pelo agente ao conectar-se ao Publicador. *publisher_security_mode* está **smallint**, sem padrão.  
  
 **0** especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação.  
  
 **1** Especifica a autenticação do Windows.  
  
 [ **@publisher_login**=] **'***publisher_login***'**  
 É o logon usado na conexão com o Publicador. *publisher_login* está **sysname**, sem padrão. *publisher_login* deve ser especificado quando *publisher_security_mode* é **0**. Se *publisher_login* for NULL e *publisher_security_mode* está **1**, em seguida, a conta do Windows especificada na *job_login* será usado ao conectar-se ao publicador.  
  
 [ **@publisher_password**=] **'***publisher_password***'**  
 É a senha usada ao conectar-se ao Publicador. *publisher_password* está **sysname**, sem padrão.  
  
 [ **@job_login**=] **'***job_login***'**  
 É o logon da conta do Windows na qual o agente é executado. *job_login* está **nvarchar(257)**, sem padrão. *Isso não pode ser alterado para um não -* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *publicador.*  
  
 [ **@job_password**=] **'***job_password***'**  
 É a senha da conta do Windows na qual o agente é executado. *job_password* está **sysname**, sem padrão.  
  
 [ **@publisher_type**=] **'***publisher_type***'**  
 Especifica o tipo de Publicador quando o Publicador não está sendo executado em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *publisher_type* está **sysname**, e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**MSSQLSERVER**|Especifica um Editor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|Especifica um Publicador Oracle padrão.|  
|**ORACLE GATEWAY**|Especifica um Editor Oracle Gateway.|  
  
 Para obter mais informações sobre as diferenças entre um publicador Oracle e um publicador Oracle Gateway, consulte [visão geral da publicação Oracle](../../relational-databases/replication/non-sql/oracle-publishing-overview.md).  
  
## <a name="remarks"></a>Comentários  
 **sp_MSchange_logreader_agent_properties** é usado em replicação transacional.  
  
 Você deve especificar todos os parâmetros ao executar **sp_MSchange_logreader_agent_properties**. Execute [sp_helplogreader_agent &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) para retornar as propriedades atuais do trabalho do Log Reader Agent.  
  
 Depois de alterar o logon ou a senha de um agente, você deve parar e reiniciar o agente antes que as alterações entrem em vigor.  
  
 Quando o publicador é executado em uma instância do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou versão posterior, você deve usar [sp_changelogreader_agent](../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md) para alterar as propriedades do Log Reader Agent.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa no distribuidor pode executar **sp_MSchange_logreader_agent_properties**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)  
  
  
