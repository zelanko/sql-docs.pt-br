---
title: sp_droppublication (Transact-SQL) | Microsoft Docs
description: Descarta uma publicação e seu Snapshot Agent associado. Esse procedimento armazenado é executado no Publicador do banco de dados de publicação.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_droppublication_TSQL
- sp_droppublication
helpviewer_keywords:
- sp_droppublication
ms.assetid: b52b37e6-4fec-40cf-abba-7dce4ff395fd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 980b40421b51594ef0d687521ba9e436c2a16c4c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85783828"
---
# <a name="sp_droppublication-transact-sql"></a>sp_droppublication (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Descarta uma publicação e seu Snapshot Agent associado. Todas as assinaturas devem ser descartadas antes de descartar uma publicação. Os artigos na publicação são descartados automaticamente. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_droppublication [ @publication= ] 'publication'   
    [ , [ @ignore_distributor = ] ignore_distributor ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação a ser descartada. a *publicação* é **sysname**, sem padrão. Se **All** for especificado, todas as publicações serão removidas do banco de dados de publicação, exceto aquelas com assinaturas.  
  
`[ @ignore_distributor = ] ignore_distributor` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_droppublication** é usado na replicação de instantâneo e na replicação transacional.  
  
 **sp_droppublication** remove recursivamente todos os artigos associados a uma publicação e, em seguida, descarta a publicação em si. Uma publicação não poderá ser removida se tiver uma ou mais assinaturas associadas. Para obter informações sobre como remover assinaturas, consulte [excluir uma assinatura push](../../relational-databases/replication/delete-a-push-subscription.md) e [excluir uma assinatura pull](../../relational-databases/replication/delete-a-pull-subscription.md).  
  
 A execução de **sp_droppublication** para descartar uma publicação não remove objetos publicados do banco de dados de publicação ou dos objetos correspondentes do banco de dados de assinatura. Use DROP \<object> para remover esses objetos manualmente, se necessário.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_droppublication**.  
  
## <a name="examples"></a>Exemplos  
 [!code-sql[HowTo#sp_droppublication](../../relational-databases/replication/codesnippet/tsql/sp-droppublication-trans_1.sql)]  
  
## <a name="see-also"></a>Consulte Também  
 [Excluir uma publicação](../../relational-databases/replication/publish/delete-a-publication.md)   
 [&#41;&#40;Transact-SQL de sp_addpublication](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helppublication](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
