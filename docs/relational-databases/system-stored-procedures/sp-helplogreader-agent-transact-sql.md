---
title: sp_helplogreader_agent (Transact-SQL) | Microsoft Docs
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
f1_keywords:
- sp_helplogreader_agent
- sp_helplogreader_agent_TSQL
helpviewer_keywords: sp_helplogreader_agent
ms.assetid: ff837209-e2b3-481a-a48f-8530bfe53d97
caps.latest.revision: "28"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ee9020dff1819069c3449bd85cbbf61d440acd91
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sphelplogreaderagent-transact-sql"></a>sp_helplogreader_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna propriedades de trabalho do Agente de Leitor de Log para o banco de dados de publicação. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helplogreader_agent [ [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher** =] **'***publicador***'**  
 É o nome do Publicador. *publicador* é **sysname**, com um padrão NULL.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ID do agente.|  
|**name**|**nvarchar (100)**|O nome do agente.|  
|**publisher_security_mode**|**smallint**|O modo de segurança usado pelo agente ao se conectar ao Publicador que pode ser um dos seguintes:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação<br /><br /> **1** = autenticação do Windows.|  
|**publisher_login**|**sysname**|Logon usado na conexão com o Publicador.|  
|**publisher_password**|**nvarchar (524)**|Por motivos de segurança, um valor de  **\* \* \* \* \* \* \* \* \* \***  é sempre retornado.|  
|**job_id**|**uniqueidentifier**|ID exclusiva do trabalho de agente.|  
|**job_login**|**nvarchar(512)**|É a conta do Windows sob a qual o Log Reader Agent é executado, que é retornada no formato *domínio*\\*nome de usuário*.|  
|**job_password**|**sysname**|Por motivos de segurança, um valor de  **\* \* \* \* \* \* \* \* \* \***  é sempre retornado.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helplogreader_agent** é usado em replicação transacional.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** a função de servidor fixa no publicador ou membros do **db_owner** função de banco de dados fixa no banco de dados de publicação pode executar **sp_helplogreader_agent**.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e modificar configurações de segurança de replicação](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [sp_addlogreader_agent &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)   
 [sp_changelogreader_agent &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md)  
  
  
