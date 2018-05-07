---
title: sp_dropmergepublication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
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
- sp_dropmergepublication
- sp_dropmergepublication_TSQL
helpviewer_keywords:
- sp_dropmergepublication
ms.assetid: 9e1cb96e-5889-4f97-88cd-f60cf313ce68
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 9a360ce767a80dd9f77f35a22d92b65d3a52777c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spdropmergepublication-transact-sql"></a>sp_dropmergepublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Descarta uma publicação de mesclagem e seu Agente de Instantâneo associado. Todas as assinaturas devem ser descartadas antes de descartar uma publicação de mesclagem. Os artigos na publicação são descartados automaticamente. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dropmergepublication [ @publication= ] 'publication'   
    [ , [ @ignore_distributor = ] ignore_distributor ]   
    [ , [ @reserved = ] reserved ]  
    [ , [ @ignore_merge_metadata = ] ignore_merge_metadata ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=**] **'***publicação***'**  
 É o nome da publicação a ser removida. *publicação* é **sysname**, sem padrão. Se **todos os**, todas as publicações de mesclagem existentes são removidas, bem como o trabalho do agente de instantâneo associado a eles. Se você especificar um valor específico para *publicação*, somente aquela publicação e seu trabalho do agente de instantâneo associado serão descartados.  
  
 [  **@ignore_distributor =**] *ignore_distributor*  
 Usado para remover uma publicação sem tarefas de limpeza no Distribuidor. *ignore_distributor* é **bit**, com um padrão de **0**. Esse parâmetro também é usado ao reinstalar o Distribuidor.  
  
 [  **@reserved=**] *reservado*  
 É reservado para uso futuro. *reservado* é **bit**, com um padrão de **0**.  
  
 [  **@ignore_merge_metadata=** ] *ignore_merge_metadata*  
 Somente para uso interno.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_dropmergepublication** é usado em replicação de mesclagem.  
  
 **sp_dropmergepublication** recursivamente descarta todos os artigos que estão associados uma publicação e, em seguida, descarta a própria publicação. Uma publicação não poderá ser removida se tiver uma ou mais assinaturas associadas. Para obter informações sobre como remover assinaturas, consulte [excluir uma assinatura Push](../../relational-databases/replication/delete-a-push-subscription.md) e [excluir uma assinatura Pull](../../relational-databases/replication/delete-a-pull-subscription.md).  
  
 Executar **sp_dropmergepublication** descartar uma publicação não remove objetos publicados no banco de dados de publicação ou objetos correspondente do banco de dados de assinatura. Use DROP \<objeto > para remover esses objetos manualmente, se necessário.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_dropmergepublication](../../relational-databases/replication/codesnippet/tsql/sp-dropmergepublication-_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_dropmergepublication**.  
  
## <a name="see-also"></a>Consulte também  
 [Excluir uma publicação](../../relational-databases/replication/publish/delete-a-publication.md)   
 [sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [sp_changemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_helpmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
