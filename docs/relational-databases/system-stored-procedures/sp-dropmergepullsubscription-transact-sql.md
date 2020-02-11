---
title: sp_dropmergepullsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergepullsubscription
- sp_dropmergepullsubscription_TSQL
helpviewer_keywords:
- sp_dropmergepullsubscription
ms.assetid: 9301dd80-72f7-4adb-9b13-87e7f9114248
author: stevestein
ms.author: sstein
ms.openlocfilehash: ab2cda06971e56a8c15e2fb7382977a36fe7a34a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67933882"
---
# <a name="sp_dropmergepullsubscription-transact-sql"></a>sp_dropmergepullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Descarta uma assinatura pull de mesclagem. Esse procedimento armazenado é executado no Assinante no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dropmergepullsubscription [ @publication= ] 'publication'   
        , [ @publisher= ] 'publisher'   
        , [ @publisher_db= ] 'publisher_db'   
    [ , [ @reserved= ] 'reserved' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação. a *publicação* é **sysname**, com um padrão de NULL. Este parâmetro é necessário. Especifique um valor de **todos** para remover assinaturas para todas as publicações  
  
`[ @publisher = ] 'publisher'`É o nome do Publicador. o *Publicador*é **sysname**, com um padrão de NULL. Este parâmetro é necessário.  
  
`[ @publisher_db = ] 'publisher_db'`É o nome do banco de dados do Publicador. *publisher_db*é **sysname**, com um padrão de NULL. Este parâmetro é necessário.  
  
`[ @reserved = ] 'reserved'`É reservado para uso futuro. *reservado* é **bit**, com um padrão de **0**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_dropmergepullsubscription** é usado na replicação de mesclagem.  
  
 **sp_dropmergepullsubscription** descarta a agente de mesclagem desta assinatura pull de mesclagem, embora a agente de mesclagem não seja criada em **sp_addmergepullsubscription**.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_dropmergepullsubscription](../../relational-databases/replication/codesnippet/tsql/sp-dropmergepullsubscrip_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou o usuário que criou a assinatura pull de mesclagem podem executar **sp_dropmergepullsubscription**. A função de banco de dados fixa **db_owner** só poderá ser executada **sp_dropmergepullsubscription** se o usuário que criou a assinatura pull de mesclagem pertencer a essa função.  
  
## <a name="see-also"></a>Consulte Também  
 [Excluir uma assinatura pull](../../relational-databases/replication/delete-a-pull-subscription.md)   
 [&#41;&#40;Transact-SQL de sp_addmergepullsubscription](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changemergepullsubscription](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropmergesubscription](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpmergepullsubscription](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)  
  
  
