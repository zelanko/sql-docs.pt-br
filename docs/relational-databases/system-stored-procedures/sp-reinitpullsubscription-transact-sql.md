---
title: sp_reinitpullsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_reinitpullsubscription_TSQL
- sp_reinitpullsubscription
helpviewer_keywords:
- sp_reinitpullsubscription
ms.assetid: 7d9abe49-ce92-47f3-82c9-aea749518c91
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ab14d01f4d77d249b0d2ff74afd2e6c08668c18e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spreinitpullsubscription-transact-sql"></a>sp_reinitpullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Marca uma assinatura pull transacional ou anônima para reinicialização da próxima vez que o Agente de Distribuição for executado. Esse procedimento armazenado é executado no Assinante, no banco de dados de assinatura pull.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_reinitpullsubscription [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher=**] **'***publicador***'**  
 É o nome do Publicador. *publicador* é **sysname**, sem padrão.  
  
 [  **@publisher_db=**] **'***publisher_db***'**  
 É o nome do banco de dados Publicador. *publisher_db* é **sysname**, sem padrão.  
  
 [  **@publication=**] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, com um padrão de all, que marca todas as assinaturas para reinicialização.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_reinitpullsubscription** é usado em replicação transacional.  
  
 **sp_reinitpullsubscription** não há suporte para replicação transacional ponto a ponto.  
  
 **sp_reinitpullsubscription** pode ser chamado do assinante para reinicializar a assinatura, durante a próxima execução do Distribution Agent.  
  
 Assinaturas para publicações criadas com um valor de **false** para **@immediate_sync** não podem ser reiniciadas no assinante.  
  
 Você pode reinicializar uma assinatura pull executando **sp_reinitpullsubscription** no assinante ou **sp_reinitsubscription** no publicador.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_reinitpullsub](../../relational-databases/replication/codesnippet/tsql/sp-reinitpullsubscriptio_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_reinitpullsubscription**.  
  
## <a name="see-also"></a>Consulte também  
 [Reinicializar uma assinatura](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [Reinicializar as assinaturas](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
