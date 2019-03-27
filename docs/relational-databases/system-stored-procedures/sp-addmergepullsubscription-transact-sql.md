---
title: sp_addmergepullsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepullsubscription_TSQL
- sp_addmergepullsubscription
helpviewer_keywords:
- sp_addmergepullsubscription
ms.assetid: d63909a0-8ea7-4734-9ce8-8204d936a3e4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 59e639c1dd319d7db074d692d3776105abe89f0f
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58493738"
---
# <a name="spaddmergepullsubscription-transact-sql"></a>sp_addmergepullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Adiciona uma assinatura pull a uma publicação de mesclagem. Esse procedimento armazenado é executado no assinante, no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addmergepullsubscription [ @publication= ] 'publication'   
    [ , [ @publisher= ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publisher_db' ]   
    [ , [ @subscriber_type= ] 'subscriber_type' ]   
    [ , [ @subscription_priority= ] subscription_priority ]   
    [ , [ @sync_type= ] 'sync_type' ]   
    [ , [ @description= ] 'description' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação. *publicação* está **sysname**, sem padrão.  
  
`[ @publisher = ] 'publisher'` É o nome do publicador. *Publisher* está **sysname**, com um padrão de nome do servidor local. O Publicador deve ser um servidor válido.  
  
`[ @publisher_db = ] 'publisher_db'` É o nome do banco de dados publicador. *publisher_db* está **sysname**, com um padrão NULL.  
  
`[ @subscriber_type = ] 'subscriber_type'` É o tipo de assinante. *subscriber_type* está **nvarchar(15)** e pode ser **global**, **local** ou **anônimo**. Em [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e em versões posteriores, assinaturas locais são chamadas de assinaturas de cliente e assinaturas globais são referidas como assinaturas de servidor.  
  
`[ @subscription_priority = ] subscription_priority` É a prioridade da assinatura. *subscription_priority*está **real**, com um padrão NULL. Para assinaturas locais e anônimas, a prioridade é **0,0**. A prioridade é usada pelo resolvedor padrão para escolher um vencedor quando são detectados conflitos. Para assinantes globais, a prioridade de assinatura deve ser abaixo de 100, que é a prioridade do publicador.  
  
`[ @sync_type = ] 'sync_type'` É o tipo de sincronização de assinatura. *sync_type*está **nvarchar(15)**, com um padrão de **automática**. Pode ser **automáticas** ou **none**. Se **automática**, o esquema e os dados iniciais para tabelas publicadas serão transferidos para o assinante primeiro. Se **none**, supõe-se o assinante já tem o esquema e os dados iniciais para tabelas publicadas. Tabelas de sistema e dados sempre são transferidos.  
  
> [!NOTE]  
>  Não é recomendável especificar um valor de **none**.  
  
`[ @description = ] 'description'` É uma descrição breve desta assinatura pull. *Descrição*está **nvarchar (255)**, com um padrão NULL. Esse valor é exibido pelo Replication Monitor na **nome amigável** coluna, que pode ser usada para classificar as assinaturas para uma publicação monitorada.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addmergepullsubscription** é usado para replicação de mesclagem.  
  
 Se usando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para sincronizar a assinatura, o [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) procedimento armazenado deve ser executado no assinante para criar um agente e trabalho para sincronizar com a publicação.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_0_1.sql)]  
  
 [!code-sql[HowTo#sp_addmergepullsub_websync_anon](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_0_2.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou **db_owner** banco de dados fixa podem executar **sp_addmergepullsubscription**.  
  
## <a name="see-also"></a>Consulte também  
 [Criar uma assinatura pull](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)   
 [sp_changemergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [sp_helpmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
