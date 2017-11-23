---
title: sp_addqueued_artinfo (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
- sp_addqueued_artinfo
- sp_addqueued_artinfo_TSQL
helpviewer_keywords: sp_addqueued_artinfo
ms.assetid: decdb6eb-3dcd-4053-a21d-fd367c3fbafb
caps.latest.revision: "20"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d9d843930ab1626ac4caadc169567163043e8b1b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spaddqueuedartinfo-transact-sql"></a>sp_addqueued_artinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  
  
> [!IMPORTANT]  
>  O [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) procedimento deve ser usado em vez de **sp_addqueued_artinfo**. [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) gera um script que contém o **sp_addqueued_artinfo** e **sp_addsynctrigger** chamadas.  
  
 Cria o [MSsubscription_articles](../../relational-databases/system-tables/mssubscription-articles-transact-sql.md) tabela no assinante que é usado para rastrear as informações de assinatura de artigo (atualização enfileirada e atualização imediata com atualização enfileirada como Failover). Esse procedimento armazenado é executado no assinante no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addqueued_artinfo [ @artid= ] 'artid'  
        , [ @article= ] 'article'  
        , [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
        , [ @dest_table= ] 'dest_table'  
        , [ @owner = ] 'owner'  
        , [ @cft_table= ] 'cft_table'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@artid=** ] **'***artid***'**  
 É o nome da ID do artigo. *artid* é **int**, sem padrão  
  
 [  **@article=**] **'***artigo***'**  
 É o nome do artigo para o qual gerar um script. *artigo* é **sysname**, sem padrão  
  
 [  **@publisher=**] **'***publicador***'**  
 É o nome do servidor do Publicador. *publicador* é **sysname**, sem padrão.  
  
 [  **@publisher_db=**] **'***publisher_db***'**  
 É o nome do banco de dados Publicador. *publisher_db* é **sysname**, sem padrão.  
  
 [  **@publication=**] **'***publicação***'**  
 É o nome da publicação para a qual gerar um script. *publicação* é **sysname**, sem padrão.  
  
 [  **@dest_table=** ] *' dest_table***'**  
 É o nome da tabela de destino. *dest_table* é **sysname**, sem padrão.  
  
 [ **@owner =** ] **'***proprietário***'**  
 É o proprietário da assinatura. *proprietário* é **sysname**, sem padrão.  
  
 [  **@cft_table=** ] **'***cft_table***'**  
 Nome da tabela de conflito de atualização enfileirada para esse artigo. *cft_table*é **sysname**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addqueued_artinfo** é usado pelo agente de distribuição como parte da inicialização de assinatura. Esse procedimento armazenado não é executado com frequência pelos usuários, mas pode ser útil se o usuário precisar configurar manualmente uma assinatura.  
  
 [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) em vez de **sp_addqueued_artinfo**.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_addqueued_artinfo**.  
  
## <a name="see-also"></a>Consulte também  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [sp_script_synctran_commands &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)   
 [MSsubscription_articles &#40; Transact-SQL &#41;](../../relational-databases/system-tables/mssubscription-articles-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
