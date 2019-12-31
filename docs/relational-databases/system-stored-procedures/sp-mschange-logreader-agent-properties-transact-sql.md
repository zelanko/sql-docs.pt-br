---
title: sp_MSchange_logreader_agent_properties (T-SQL)
description: Descreve o sp_MSchange_logreader_agent_properties procedimento armazenado usado para alterar as propriedades do Agente de Leitor de Log para uma topologia de Replicação do SQL Server.
ms.custom: seo-lt-2019
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
ms.openlocfilehash: 37a36218b4e9e93a761c776e76a6596f40a6c0eb
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2019
ms.locfileid: "75322260"
---
# <a name="sp_mschange_logreader_agent_properties-transact-sql"></a>sp_MSchange_logreader_agent_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera as propriedades de um trabalho agente de leitor de log executado em um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] distribuidor de versão ou posterior. Esse procedimento armazenado é usado para alterar propriedades quando o Publicador é executado em uma instância do [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. Esse procedimento armazenado é executado no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @publisher = ] 'publisher'`É o nome do Publicador. o *Publicador* é **sysname**, sem padrão.  
  
`[ @publisher_db = ] 'publisher_db'`É o nome do banco de dados de publicação. *publisher_db* é **sysname**, sem padrão.  
  
`[ @publisher_security_mode = ] publisher_security_mode`É o modo de segurança usado pelo agente ao se conectar ao Publicador. *publisher_security_mode* é **smallint**, sem padrão.  
  
 **0** especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a autenticação.  
  
 **1** especifica a autenticação do Windows.  
  
`[ @publisher_login = ] 'publisher_login'`É o logon usado ao conectar-se ao Publicador. *publisher_login* é **sysname**, sem padrão. *publisher_login* deve ser especificado quando *publisher_security_mode* é **0**. Se *publisher_login* for nulo e *publisher_security_mode* for **1**, a conta do Windows especificada em *job_login* será usada durante a conexão com o Publicador.  
  
`[ @publisher_password = ] 'publisher_password'`É a senha usada ao conectar-se ao Publicador. *publisher_password* é **sysname**, sem padrão.  
  
`[ @job_login = ] 'job_login'`É o logon da conta do Windows na qual o agente é executado. *job_login* é **nvarchar (257)**, sem padrão. *Isso não pode ser alterado para um não* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *Publicador.*  
  
`[ @job_password = ] 'job_password'`É a senha para a conta do Windows na qual o agente é executado. *job_password* é **sysname**, sem padrão.  
  
`[ @publisher_type = ] 'publisher_type'`Especifica o tipo de Publicador quando o Publicador não estiver em execução [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]em uma instância do. *publisher_type* é **sysname**e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**MSSQLSERVER**|Especifica um Editor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|Especifica um Publicador Oracle padrão.|  
|**ORACLE GATEWAY**|Especifica um Editor Oracle Gateway.|  
  
 Para obter mais informações sobre as diferenças entre um Publicador Oracle e um Publicador de gateway da Oracle, consulte [visão geral da publicação Oracle](../../relational-databases/replication/non-sql/oracle-publishing-overview.md).  
  
## <a name="remarks"></a>Comentários  
 **sp_MSchange_logreader_agent_properties** é usado na replicação transacional.  
  
 Você deve especificar todos os parâmetros ao executar **sp_MSchange_logreader_agent_properties**. Execute [sp_helplogreader_agent &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) para retornar as propriedades atuais do trabalho agente de leitor de log.  
  
 Depois de alterar o logon ou a senha de um agente, você deve parar e reiniciar o agente antes que as alterações entrem em vigor.  
  
 Quando o Publicador é executado em uma [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] instância do ou versão posterior, você deve usar [sp_changelogreader_agent](../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md) para alterar as propriedades do agente de leitor de log.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** no distribuidor podem executar **sp_MSchange_logreader_agent_properties**.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_addlogreader_agent](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)  
  
  
