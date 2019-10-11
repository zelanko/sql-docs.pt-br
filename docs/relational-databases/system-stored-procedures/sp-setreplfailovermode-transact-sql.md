---
title: sp_setreplfailovermode (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_setreplfailovermode
- sp_setreplfailovermode_TSQL
helpviewer_keywords:
- sp_setreplfailovermode
ms.assetid: ca98a4c3-bea4-4130-88d7-79e0fd1e85f6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5b39a5fa53560abb825b303d37d111bcbd7d0886
ms.sourcegitcommit: 79e6d49ae4632f282483b0be935fdee038f69cc2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2019
ms.locfileid: "72173567"
---
# <a name="sp_setreplfailovermode-transact-sql"></a>sp_setreplfailovermode (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Permite definir o modo de operação de failover para assinaturas habilitadas para atualização imediata com atualização enfileirada como failover. Esse procedimento armazenado é executado no Assinante no banco de dados de assinatura. Para obter mais informações sobre modos de failover, consulte [assinaturas atualizáveis para replicação transacional](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_setreplfailovermode [ @publisher= ] 'publisher'  
    [ , [ @publisher_db = ] 'publisher_db' ]  
    [ , [ @publication= ] 'publication' ]  
    [ , [ @failover_mode= ] 'failover_mode' ]  
    [ , [ @override = ] override ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'` é o nome da publicação. a *publicação* é **sysname**, sem padrão. A publicação já deve existir.  
  
`[ @publisher_db = ] 'publisher_db'` é o nome do banco de dados de publicação. *publisher_db* é **sysname**, sem padrão.  
  
`[ @publication = ] 'publication'` é o nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
`[ @failover_mode = ] 'failover_mode'` é o modo de failover para a assinatura. *failover_mode* é **nvarchar (10)** e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**imediato** ou de **sincronização**|Modificações de dados feitas no Assinante são copiadas em massa para o Publicador à medida que ocorrem.|  
|**queued**|As modificações de dados são armazenadas em uma fila [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
> [!NOTE]  
>  O Serviço de Enfileiramento de Mensagens da [!INCLUDE[msCoName](../../includes/msconame-md.md)] foi preterido e não tem mais suporte.  
  
`[ @override = ] override` somente uso interno.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 o **sp_setreplfailovermode** é usado na replicação de instantâneo ou na replicação transacional para a qual as assinaturas estão habilitadas, para atualização em fila com failover para atualização imediata ou para atualização imediata com failover para atualização em fila.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou da função de banco de dados fixa **db_owner** podem executar **sp_setreplfailovermode**.  
  
## <a name="see-also"></a>Consulte também  
 [Alternar entre modos de atualização para uma assinatura transacional atualizável](../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
