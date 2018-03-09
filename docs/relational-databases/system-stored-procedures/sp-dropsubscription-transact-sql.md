---
title: sp_dropsubscription (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
- sp_dropsubscription
- sp_dropsubscription_TSQL
helpviewer_keywords: sp_dropsubscription
ms.assetid: 7551f345-5510-4684-ab53-f9057249d13a
caps.latest.revision: "23"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 43185571b06705011346dc08ded48e587a624311
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spdropsubscription-transact-sql"></a>sp_dropsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Descarta assinaturas para um artigo específico, publicação ou conjunto de assinaturas no Publicador. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dropsubscription [ [ @publication= ] 'publication' ]  
    [ , [ @article= ] 'article' ]  
        , [ @subscriber= ] 'subscriber'  
    [ , [ @destination_db= ] 'destination_db' ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
    [ , [ @reserved= ] 'reserved' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=** ] **'***publicação***'**  
 É o nome da publicação associada. *publicação* é **sysname**, com um padrão NULL. Se **todos os**, todas as assinaturas para todas as publicações do assinante especificado serão canceladas. *publicação* é um parâmetro obrigatório.  
  
 [  **@article=** ] **'***artigo***'**  
 É o nome do artigo. *artigo* é **sysname**, com um valor padrão de NULL. Se **todos os**, especificado de assinaturas para todos os artigos para cada publicação e o assinante serão descartadas. Use **todos os** para publicações que permitem imediatas de atualização.  
  
 [  **@subscriber=** ] **'***assinar*r**'**  
 É o nome do Assinante que terá suas assinaturas removidas. *assinante* é **sysname**, sem padrão. Se **todos os**, todas as assinaturas para todos os assinantes serão descartadas.  
  
 [  **@destination_db=** ] **'***destination_db***'**  
 É o nome do banco de dados de destino. *destination_db* é **sysname**, com um padrão NULL. Se for NULL, todas as assinaturas daquele Assinante serão descartadas.  
  
 [  **@ignore_distributor =** ] *ignore_distributor*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@reserved=** ] **'***reservado***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_dropsubscription** é usado em replicação de instantâneo e transacional.  
  
 Se você descartar a assinatura de um artigo em uma publicação de sincronização imediata, não poderá adicioná-la novamente, exceto se descartar as assinaturas em todos os artigos de publicação e os adicionar novamente, todos de uma vez.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_droptransubscription](../../relational-databases/replication/codesnippet/tsql/sp-dropsubscription-tran_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa, o **db_owner** pode executar a função de banco de dados fixa ou o usuário que criou a assinatura **sp_dropsubscription**.  
  
## <a name="see-also"></a>Consulte também  
 [Excluir uma assinatura Push](../../relational-databases/replication/delete-a-push-subscription.md)   
 [sp_addsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_changesubstatus &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changesubstatus-transact-sql.md)   
 [sp_helpsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
