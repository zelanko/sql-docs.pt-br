---
title: sp_reinitmergesubscription (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
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
- sp_reinitmergesubscription_TSQL
- sp_reinitmergesubscription
helpviewer_keywords:
- sp_reinitmergesubscription
ms.assetid: 249a4048-e885-48e0-a92a-6577f59de751
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5b801376850844a0e1cba0e5b53b72114c0199f7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spreinitmergesubscription-transact-sql"></a>sp_reinitmergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Marca uma assinatura de mesclagem para reinicialização na próxima execução do Agente de Mesclagem. Esse procedimento armazenado é executado no publicador do banco de dados de publicação.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_reinitmergesubscription [ [ @publication = ] 'publication'  
    [ , [ @subscriber = ] 'subscriber'  
    [ , [ @subscriber_db = ] 'subscriber_db'  
    [ , [ @upload_first = ] 'upload_first'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication =** ] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, com um padrão de **todos os**.  
  
 [  **@subscriber =** ] **'***assinante***'**  
 É o nome do Assinante. *assinante* é **sysname**, com um padrão de **todos os**.  
  
 [  **@subscriber_db =** ] **'***subscriber_db***'**  
 É o nome do banco de dados do Assinante. *subscriber_db* é **sysname**, com um padrão de **todos os**.  
  
 [  **@upload_first =** ] **'***upload_first***'**  
 Especifica se as alterações no Assinante são carregadas antes da assinatura ser reinicializada. *upload_first* é **nvarchar (5)**, com um padrão de FALSE. Se **true**, as alterações são carregadas antes que a assinatura seja reiniciada. Se **false**, as alterações não são carregadas.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_reinitmergesubscription** é usado em replicação de mesclagem.  
  
 **sp_reinitmergesubscription** pode ser chamado do publicador para reinicializar assinaturas de mesclagem. Recomendamos reexecutar o Agente de Instantâneo também.  
  
 Se você adicionar, descartar ou alterar um filtro com parâmetros, as alterações pendentes no Assinante não poderão ser carregadas no Publicador durante a reinicialização. Para carregar alterações pendentes, sincronize todas as assinaturas antes de alterar o filtro.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_reinitmergepushsub](../../relational-databases/replication/codesnippet/tsql/sp-reinitmergesubscripti_1.sql)]  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_reinitmergepushsubwithupload](../../relational-databases/replication/codesnippet/tsql/sp-reinitmergesubscripti_2.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_reinitmergesubscription**.  
  
## <a name="see-also"></a>Consulte também  
 [Reinicializar as assinaturas](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
