---
title: sp_reinitmergepullsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
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
- sp_reinitmergepullsubscription
- sp_reinitmergepullsubscription_TSQL
helpviewer_keywords:
- sp_reinitmergepullsubscription
ms.assetid: 48464bc9-60aa-4886-b526-163f010102b8
caps.latest.revision: 32
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 54245be4b829b4dc6bffe59d79c93d63576338f6
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43031188"
---
# <a name="spreinitmergepullsubscription-transact-sql"></a>sp_reinitmergepullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Marca uma assinatura pull de mesclagem para reinicialização, na próxima execução do Agente de Mesclagem. Esse procedimento armazenado é executado no Assinante, no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_reinitmergepullsubscription [ [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @upload_first = ] 'upload_first'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@publisher** =] **'***publisher***'**  
 É o nome do Publicador. *Publisher* está **sysname**, com um padrão de ALL.  
  
 [ **@publisher_db** =] **'***publisher_db***'**  
 É o nome do banco de dados Publicador. *publisher_db* está **sysname**, com um padrão de ALL.  
  
 [ **@publication** =] **'***publicação***'**  
 É o nome da publicação. *publicação* está **sysname**, com um padrão de ALL.  
  
 [ **@upload_first** =] **'***upload_first***'**  
 Especifica se as alterações no Assinante são carregadas antes da assinatura ser reinicializada. *upload_first* está **nvarchar (5)**, com um padrão de FALSE. Se **verdadeira**, as alterações são carregadas antes que a assinatura seja reiniciada. Se **falsos**, as alterações não são carregadas.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_reinitmergepullsubscription** é usado em replicação de mesclagem.  
  
 Se você adicionar, descartar ou alterar um filtro com parâmetros, as alterações pendentes no Assinante não poderão ser carregadas no Publicador durante a reinicialização. Para carregar alterações pendentes, sincronize todas as assinaturas antes de alterar o filtro.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_reinitmergepullsub](../../relational-databases/replication/codesnippet/tsql/sp-reinitmergepullsubscr_1.sql)]  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_reinitmergepullsubwithupload](../../relational-databases/replication/codesnippet/tsql/sp-reinitmergepullsubscr_2.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou o **db_owner** banco de dados fixa podem executar **sp_reinitmergepullsubscription**.  
  
## <a name="see-also"></a>Consulte também  
 [Reinicializar uma assinatura](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [Reinicializar as assinaturas](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
