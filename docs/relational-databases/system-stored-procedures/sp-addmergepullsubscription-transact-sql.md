---
description: sp_addmergepullsubscription (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 13e89d2dfe90789071821f7ad6714361f1954a8d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89529486"
---
# <a name="sp_addmergepullsubscription-transact-sql"></a>sp_addmergepullsubscription (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Adiciona uma assinatura pull a uma publicação de mesclagem. Esse procedimento armazenado é executado no Assinante no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @publication = ] 'publication'` É o nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
`[ @publisher = ] 'publisher'` É o nome do Publicador. O *Publicador* é **sysname**, com um padrão do nome do servidor local. O Publicador deve ser um servidor válido.  
  
`[ @publisher_db = ] 'publisher_db'` É o nome do banco de dados do Publicador. *publisher_db* é **sysname**, com um padrão de NULL.  
  
`[ @subscriber_type = ] 'subscriber_type'` É o tipo de assinante. *subscriber_type* é **nvarchar (15)** e pode ser **global**, **local** ou **anônimo**. No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e em versões posteriores, as assinaturas locais são conhecidas como assinaturas de cliente e as assinaturas globais são chamadas de assinaturas de servidor.  
  
`[ @subscription_priority = ] subscription_priority` É a prioridade da assinatura. *subscription_priority*é **real**, com um padrão de NULL. Para assinaturas locais e anônimas, a prioridade é **0,0**. A prioridade é usada pelo resolvedor padrão para escolher um vencedor quando são detectados conflitos. Para assinantes globais, a prioridade de assinatura deve ser abaixo de 100, que é a prioridade do publicador.  
  
`[ @sync_type = ] 'sync_type'` É o tipo de sincronização de assinatura. *sync_type*é **nvarchar (15)**, com um padrão de **automático**. Pode ser **automático** ou **nenhum**. Se **automático**, o esquema e os dados iniciais para tabelas publicadas serão transferidos para o assinante primeiro. Se não **houver nenhum**, supõe-se que o Assinante já tem o esquema e os dados iniciais para tabelas publicadas. Tabelas de sistema e dados sempre são transferidos.  
  
> [!NOTE]  
>  Não recomendamos especificar um valor de **nenhum**.  
  
`[ @description = ] 'description'` É uma breve descrição dessa assinatura pull. a *Descrição*é **nvarchar (255)**, com um padrão de NULL. Esse valor é exibido pelo Replication Monitor na coluna **nome amigável** , que pode ser usado para classificar as assinaturas de uma publicação monitorada.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addmergepullsubscription** é usado para replicação de mesclagem.  
  
 Se estiver usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para sincronizar a assinatura, o procedimento armazenado [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) deve ser executado no Assinante para criar um agente e um trabalho para sincronizar com a publicação.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_0_1.sql)]  
  
 [!code-sql[HowTo#sp_addmergepullsub_websync_anon](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_0_2.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_addmergepullsubscription**.  
  
## <a name="see-also"></a>Consulte Também  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [&#41;&#40;Transact-SQL de sp_addmergepullsubscription_agent ](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changemergepullsubscription ](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropmergepullsubscription ](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpmergepullsubscription ](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
