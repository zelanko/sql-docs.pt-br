---
title: sp_mergesubscription_cleanup (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
- sp_mergesubscription_cleanup
- sp_mergesubscription_cleanup_TSQL
helpviewer_keywords:
- sp_mergesubscription_cleanup
ms.assetid: bfad414f-2bda-4bf5-9507-56a1e743dfc4
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7c30f8192f454fe465a2aa3b3af5b43fb3acc17a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spmergesubscriptioncleanup-transact-sql"></a>sp_mergesubscription_cleanup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove metadados, como gatilhos e entradas, **sysmergesubscriptions** e **sysmergearticles** depois que a assinatura push de mesclagem especificada for removida no publicador. Esse procedimento armazenado é executado no assinante no banco de dados de assinatura.  
  
> [!NOTE]  
>  Para uma assinatura pull, os metadados são removidos quando [sp_dropmergepullsubscription &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md) é executado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_mergesubscription_cleanup [ @publisher =] 'publisher'  
        , [ @publisher_db =] 'publisher_db'  
        , [ @publication =] 'publication'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher =**] **'***publicador***'**  
 É o nome do Publicador. *publicador* é **sysname**, sem padrão.  
  
 [  **@publisher_db =**] **'***publisher_db***'**  
 É o nome do banco de dados Publicador. *publisher_db* é **sysname**, sem padrão.  
  
 [  **@publication =**] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_mergesubscription_cleanup** é usado em replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_mergesubscription_cleanup**.  
  
## <a name="see-also"></a>Consulte também  
 [Excluir uma assinatura Push](../../relational-databases/replication/delete-a-push-subscription.md)   
 [sp_expired_subscription_cleanup &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-expired-subscription-cleanup-transact-sql.md)   
 [sp_subscription_cleanup &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
