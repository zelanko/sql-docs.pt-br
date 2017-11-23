---
title: sp_MSchange_logreader_agent_properties (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_MSchange_logreader_agent_properties_TSQL
- sp_MSchange_logreader_agent_properties
helpviewer_keywords: sp_MSchange_logreader_agent_properties
ms.assetid: 925df9d3-a041-4046-8e17-c47f40edb86d
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ea342cad83b587382ca9e25141facd613263a20e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spmschangelogreaderagentproperties-transact-sql"></a>sp_MSchange_logreader_agent_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as propriedades de um trabalho de Log Reader Agent é executado em um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou versão posterior do distribuidor. Esse procedimento armazenado é usado para alterar propriedades quando o Publicador é executado em uma instância do [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. Esse procedimento armazenado é executado no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [  **@publisher**  =] **'***publicador***'**  
 É o nome do Publicador. *publicador* é **sysname**, sem padrão.  
  
 [  **@publisher_db=** ] **'***publisher_db***'**  
 É o nome do banco de dados de publicação. *publisher_db* é **sysname**, sem padrão.  
  
 [  **@publisher_security_mode** =] *publisher_security_mode*  
 É o modo de segurança usado pelo agente ao conectar-se ao Publicador. *publisher_security_mode* é **smallint**, sem padrão.  
  
 **0** especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação.  
  
 **1** Especifica autenticação do Windows.  
  
 [  **@publisher_login** =] **'***publisher_login***'**  
 É o logon usado na conexão com o Publicador. *publisher_login* é **sysname**, sem padrão. *publisher_login* deve ser especificado quando *publisher_security_mode* é **0**. Se *publisher_login* é NULL e *publisher_security_mode* é **1**, em seguida, a conta do Windows especificada na *job_login* será usado ao conectar-se ao publicador.  
  
 [  **@publisher_password** =] **'***publisher_password***'**  
 É a senha usada ao conectar-se ao Publicador. *publisher_password* é **sysname**, sem padrão.  
  
 [  **@job_login** =] **'***job_login***'**  
 É o logon da conta do Windows na qual o agente é executado. *job_login* é **nvarchar (257)**, sem padrão. *Isso não pode ser alterado para não* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *publicador.*  
  
 [  **@job_password** =] **'***job_password***'**  
 É a senha da conta do Windows na qual o agente é executado. *job_password* é **sysname**, sem padrão.  
  
 [  **@publisher_type** =] **'***publisher_type***'**  
 Especifica o tipo de Publicador quando o Publicador não está sendo executado em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *publisher_type* é **sysname**, e pode ser um dos valores a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|Especifica um Editor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|Especifica um Publicador Oracle padrão.|  
|**ORACLE GATEWAY**|Especifica um Editor Oracle Gateway.|  
  
 Para obter mais informações sobre as diferenças entre um publicador Oracle e um publicador Oracle Gateway, consulte [visão geral da publicação Oracle](../../relational-databases/replication/non-sql/oracle-publishing-overview.md).  
  
## <a name="remarks"></a>Comentários  
 **sp_MSchange_logreader_agent_properties** é usado em replicação transacional.  
  
 Você deve especificar todos os parâmetros ao executar **sp_MSchange_logreader_agent_properties**. Executar [sp_helplogreader_agent &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) para retornar as propriedades atuais do trabalho do Log Reader Agent.  
  
 Depois de alterar o logon ou a senha de um agente, você deve parar e reiniciar o agente antes que as alterações entrem em vigor.  
  
 Quando o publicador é executado em uma instância do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou versão posterior, você deve usar [sp_changelogreader_agent](../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md) para alterar as propriedades do Log Reader Agent.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** pode executar a função de servidor fixa no distribuidor **sp_MSchange_logreader_agent_properties**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)  
  
  
