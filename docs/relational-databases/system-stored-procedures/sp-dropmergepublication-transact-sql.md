---
title: sp_dropmergepublication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergepublication
- sp_dropmergepublication_TSQL
helpviewer_keywords:
- sp_dropmergepublication
ms.assetid: 9e1cb96e-5889-4f97-88cd-f60cf313ce68
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ff7b235f27b11749673019de222d555d57f364c1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85783816"
---
# <a name="sp_dropmergepublication-transact-sql"></a>sp_dropmergepublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Descarta uma publicação de mesclagem e seu Agente de Instantâneo associado. Todas as assinaturas devem ser descartadas antes de descartar uma publicação de mesclagem. Os artigos na publicação são descartados automaticamente. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dropmergepublication [ @publication= ] 'publication'   
    [ , [ @ignore_distributor = ] ignore_distributor ]   
    [ , [ @reserved = ] reserved ]  
    [ , [ @ignore_merge_metadata = ] ignore_merge_metadata ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação a ser descartada. a *publicação* é **sysname**, sem padrão. Se **tudo**, todas as publicações de mesclagem existentes serão removidas, bem como o trabalho de agente de instantâneo associado a elas. Se você especificar um valor específico para *publicação*, somente essa publicação e seu trabalho agente de instantâneo associado serão removidos.  
  
`[ @ignore_distributor = ] ignore_distributor`Usado para descartar uma publicação sem realizar tarefas de limpeza no distribuidor. *ignore_distributor* é **bit**, com um padrão de **0**. Esse parâmetro também é usado ao reinstalar o Distribuidor.  
  
`[ @reserved = ] reserved`É reservado para uso futuro. *reservado* é **bit**, com um padrão de **0**.  
  
`[ @ignore_merge_metadata = ] ignore_merge_metadata`Somente para uso interno.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_dropmergepublication** é usado na replicação de mesclagem.  
  
 **sp_dropmergepublication** descarta recursivamente todos os artigos associados a uma publicação e, em seguida, descarta a publicação em si. Uma publicação não poderá ser removida se tiver uma ou mais assinaturas associadas. Para obter informações sobre como remover assinaturas, consulte [excluir uma assinatura push](../../relational-databases/replication/delete-a-push-subscription.md) e [excluir uma assinatura pull](../../relational-databases/replication/delete-a-pull-subscription.md).  
  
 A execução de **sp_dropmergepublication** para descartar uma publicação não remove objetos publicados do banco de dados de publicação ou dos objetos correspondentes do banco de dados de assinatura. Use DROP \<object> para remover esses objetos manualmente, se necessário.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_dropmergepublication](../../relational-databases/replication/codesnippet/tsql/sp-dropmergepublication-_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou a função de banco de dados fixa **db_owner** podem ser executados **sp_dropmergepublication**.  
  
## <a name="see-also"></a>Consulte Também  
 [Excluir uma publicação](../../relational-databases/replication/publish/delete-a-publication.md)   
 [&#41;&#40;Transact-SQL de sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changemergepublication](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
