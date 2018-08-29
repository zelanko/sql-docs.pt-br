---
title: sp_helplogreader_agent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helplogreader_agent
- sp_helplogreader_agent_TSQL
helpviewer_keywords:
- sp_helplogreader_agent
ms.assetid: ff837209-e2b3-481a-a48f-8530bfe53d97
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ef9fd50728a4bc9ebf661b2dbb22ad8ca4e9f4ad
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43031817"
---
# <a name="sphelplogreaderagent-transact-sql"></a>sp_helplogreader_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna propriedades de trabalho do Agente de Leitor de Log para o banco de dados de publicação. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helplogreader_agent [ [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@publisher**=] **'***publisher***'**  
 É o nome do Publicador. *Publisher* está **sysname**, com um padrão NULL.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ID do agente.|  
|**name**|**nvarchar(100)**|O nome do agente.|  
|**publisher_security_mode**|**smallint**|O modo de segurança usado pelo agente ao se conectar ao Publicador que pode ser um dos seguintes:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação<br /><br /> **1** = autenticação do Windows.|  
|**publisher_login**|**sysname**|Logon usado na conexão com o Publicador.|  
|**publisher_password**|**nvarchar(524)**|Por motivos de segurança, um valor de **\* \* \* \* \* \* \* \* \* \*** é sempre retornado.|  
|**job_id**|**uniqueidentifier**|ID exclusiva do trabalho de agente.|  
|**job_login**|**nvarchar(512)**|É a conta Windows na qual o Log Reader Agent é executado, o que é retornada no formato *domínio*\\*username*.|  
|**job_password**|**sysname**|Por motivos de segurança, um valor de **\* \* \* \* \* \* \* \* \* \*** é sempre retornado.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_helplogreader_agent** é usado em replicação transacional.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa no publicador ou membros da **db_owner** banco de dados fixa do banco de dados de publicação podem executar **sp_helplogreader_agent**.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e modificar configurações de segurança de replicação](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)   
 [sp_changelogreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md)  
  
  
