---
title: sp_dropmergesubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergesubscription_TSQL
- sp_dropmergesubscription
helpviewer_keywords:
- sp_dropmergesubscription
ms.assetid: 34244ae6-bd98-4a6a-bbd3-85f50edfcdc0
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: be9ad08f1591ef6f7e8893b09031a2e695be031d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750555"
---
# <a name="sp_dropmergesubscription-transact-sql"></a>sp_dropmergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Descarta uma assinatura de uma publicação de mesclagem e seu Agente de Mesclagem associado. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dropmergesubscription [ [ @publication= ] 'publication' ]   
    [ , [ @subscriber= ] 'subscriber'    
    [ , [ @subscriber_db= ] 'subscriber_db' ]   
    [ , [ @subscription_type= ] 'subscription_type' ]   
    [ , [ @ignore_distributor = ] ignore_distributor ]   
    [ , [ @reserved = ] reserved ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação. a *publicação* é **sysname**, com um padrão de NULL. A publicação já deve existir e estar em conformidade com as regras para identificadores.  
  
`[ @subscriber = ] 'subscriber'`É o nome do Assinante. o *assinante* é **sysname**, com um padrão de NULL.  
  
`[ @subscriber_db = ] 'subscriber_db'`É o nome do banco de dados de assinatura. *subscription_database*é **sysname**, com um padrão de NULL.  
  
`[ @subscription_type = ] 'subscription_type'`É o tipo de assinatura. *subscription_type*é **nvarchar (15)** e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**os**|Assinaturas push, pull e anônimas|  
|**modo**|Assinatura anônima.|  
|**push**|Assinatura push.|  
|**recebimento**|Assinatura pull.|  
|**ambos** (padrão)|Assinaturas push e pull.|  
  
`[ @ignore_distributor = ] ignore_distributor`Indica se este procedimento armazenado é executado sem se conectar ao distribuidor. *ignore_distributor* é **bit**, com um padrão de **0**. Esse parâmetro pode ser usado para descartar uma assinatura sem tarefas de limpeza no Distribuidor. Também é útil, se for necessário reinstalar o Distribuidor.  
  
`[ @reserved = ] reserved`É reservado para uso futuro. *reservado* é **bit**, com um padrão de **0**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_dropmergesubscription** é usado na replicação de mesclagem.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_dropmergesubscription](../../relational-databases/replication/codesnippet/tsql/sp-dropmergesubscription_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou a função de banco de dados fixa **db_owner** podem ser executados **sp_dropmergesubscription**.  
  
## <a name="see-also"></a>Consulte Também  
 [Excluir uma assinatura push](../../relational-databases/replication/delete-a-push-subscription.md)   
 [Excluir uma assinatura pull](../../relational-databases/replication/delete-a-pull-subscription.md)   
 [&#41;&#40;Transact-SQL de sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changemergesubscription](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpmergesubscription](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)  
  
  
