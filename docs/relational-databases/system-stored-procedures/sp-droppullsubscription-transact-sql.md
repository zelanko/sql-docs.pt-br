---
title: sp_droppullsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_droppullsubscription
- sp_droppullsubscription_TSQL
helpviewer_keywords:
- sp_droppullsubscription
ms.assetid: 7352d94a-f8f2-42ea-aaf1-d08c3b5a0e76
author: stevestein
ms.author: sstein
ms.openlocfilehash: f4ad522c13987f7617def29d5ff112a5a26db8b9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68771449"
---
# <a name="sp_droppullsubscription-transact-sql"></a>sp_droppullsubscription (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Descarta uma assinatura no banco de dados atual do Assinante. Esse procedimento armazenado é executado no Assinante, no banco de dados de assinatura pull.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_droppullsubscription [ @publisher= ] 'publisher'  
        , [ @publisher_db= ] 'publisher_db'  
        , [ @publication= ] 'publication'  
    [ , [ @reserved= ] reserved ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'`É o nome do servidor remoto. o *Publicador* é **sysname**, sem padrão. Se **tudo**, a assinatura será descartada em todos os Publicadores.  
  
`[ @publisher_db = ] 'publisher_db'`É o nome do banco de dados do Publicador. *publisher_db* é **sysname**, sem padrão. **tudo** significa todos os bancos de dados do Publicador.  
  
`[ @publication = ] 'publication'`É o nome da publicação. a *publicação* é **sysname**, sem padrão. Se **tudo**, a assinatura será descartada para todas as publicações.  
  
`[ @reserved = ] reserved` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_droppullsubscription** é usado na replicação de instantâneo e na replicação transacional.  
  
 **sp_droppullsubscription** exclui a linha correspondente no [MSreplication_subscriptions &#40;tabela de&#41;do Transact-SQL](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md) e o agente de distribuidor correspondente no Assinante. Se nenhuma linha for deixada em [MSreplication_subscriptions &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md), ela descartará a tabela.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_droptranpullsubscription](../../relational-databases/replication/codesnippet/tsql/sp-droppullsubscription-_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou o usuário que criou a assinatura pull podem executar **sp_droppullsubscription**. A função de banco de dados fixa **db_owner** só poderá executar **sp_droppullsubscription** se o usuário que criou a assinatura pull pertencer a essa função.  
  
## <a name="see-also"></a>Consulte Também  
 [Excluir uma assinatura pull](../../relational-databases/replication/delete-a-pull-subscription.md)   
 [&#41;&#40;Transact-SQL de sp_addpullsubscription](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_change_subscription_properties](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helppullsubscription](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropsubscription](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)  
  
  
