---
title: sp_expired_subscription_cleanup (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_expired_subscription_cleanup
- SP_EXPIRED_SUBSCRIPTION_CLEANUP_TSQL
helpviewer_keywords:
- sp_expired_subscription_cleanup
ms.assetid: 6abc29fe-d77a-4673-9d99-ae31c688012c
author: stevestein
ms.author: sstein
ms.openlocfilehash: fb556a464077092cacd7107a8c2b4b124c6db707
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68124426"
---
# <a name="sp_expired_subscription_cleanup-transact-sql"></a>sp_expired_subscription_cleanup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Verifica o estado de todas as assinaturas de cada publicação e descarta as que expiraram. Esse procedimento armazenado é executado no Publicador em qualquer banco de dados ou no distribuidor no banco de dados de distribuição para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] um não publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_expired_subscription_cleanup [ [ @publisher = ] 'publisher' ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'`É o nome de um não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador. a *publicação* é **sysname**, com um valor padrão de NULL. Esse parâmetro não deve ser especificado para um Editor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_expired_subscription_cleanup** é usado em todos os tipos de replicação.  
  
 **sp_expired_subscription_cleanup** é executado pelo trabalho de limpeza de assinatura expirada para detectar e remover assinaturas expiradas dos bancos de dados de publicação a cada 24 horas. Se alguma assinatura estiver desatualizada, ou seja, não estiver sincronizada com o Publicador no período de retenção, a publicação será declarada expirada e os rastreamentos da assinatura serão excluídos do Publicador. Para obter mais informações, consulte [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_expired_subscription_cleanup**.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_mergesubscription_cleanup](../../relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_subscription_cleanup](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
