---
title: sp_droppullsubscription (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
applies_to:
- SQL Server
f1_keywords:
- sp_droppullsubscription
- sp_droppullsubscription_TSQL
helpviewer_keywords:
- sp_droppullsubscription
ms.assetid: 7352d94a-f8f2-42ea-aaf1-d08c3b5a0e76
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 13245c763bea2a34b6c7a95b13c046e43c3d4a31
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spdroppullsubscription-transact-sql"></a>sp_droppullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Descarta uma assinatura no banco de dados atual do Assinante. Esse procedimento armazenado é executado no Assinante, no banco de dados de assinatura pull.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_droppullsubscription [ @publisher= ] 'publisher'  
        , [ @publisher_db= ] 'publisher_db'  
        , [ @publication= ] 'publication'  
    [ , [ @reserved= ] reserved ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher=** ] **'***publicador***'**  
 É o nome do servidor remoto. *publicador* é **sysname**, sem padrão. Se **todos os**, a assinatura será descartada em todos os publicadores.  
  
 [  **@publisher_db=** ] **'***publisher_db***'**  
 É o nome do banco de dados Publicador. *publisher_db* é **sysname**, sem padrão. **todos os** significa que todos os bancos de dados do publicador.  
  
 [  **@publication=** ] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, sem padrão. Se **todos os**, a assinatura será descartada em todas as publicações.  
  
 [  **@reserved=** ] *reservado*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_droppullsubscription** é usado em replicação de instantâneo e replicação transacional.  
  
 **sp_droppullsubscription** exclui a linha correspondente a [MSreplication_subscriptions &#40; Transact-SQL &#41; ](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md) tabela e o Distributor Agent correspondente no assinante. Se nenhuma linha for deixada em [MSreplication_subscriptions &#40; Transact-SQL &#41; ](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md), descarta a tabela.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_droptranpullsubscription](../../relational-databases/replication/codesnippet/tsql/sp-droppullsubscription-_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** pode executar a função de servidor fixa ou o usuário que criou a assinatura pull **sp_droppullsubscription**. O **db_owner** função fixa de banco de dados só é possível executar **sp_droppullsubscription** se o usuário que criou a assinatura pull pertence a essa função.  
  
## <a name="see-also"></a>Consulte também  
 [Excluir uma assinatura Pull](../../relational-databases/replication/delete-a-pull-subscription.md)   
 [sp_addpullsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_change_subscription_properties &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)   
 [sp_helppullsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_dropsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)  
  
  
