---
title: sp_replqueuemonitor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replqueuemonitor
- sp_replqueuemonitor_TSQL
helpviewer_keywords:
- sp_replqueuemonitor
ms.assetid: 6909a3f1-43a2-4df5-a6a5-9e6f347ac841
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e8eb21085625c7f2f0071c18da80501774088fdc
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52789368"
---
# <a name="spreplqueuemonitor-transact-sql"></a>sp_replqueuemonitor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Lista as mensagens de fila de uma [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fila ou [!INCLUDE[msCoName](../../includes/msconame-md.md)] enfileiramento de mensagens para assinaturas de atualização em fila para uma publicação especificada. Se as filas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] forem usadas, esse procedimento armazenado será executado no banco de dados de assinatura. Se o Enfileiramento de Mensagens for usado, esse procedimento armazenado será executado no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_replqueuemonitor [ @publisher = ] 'publisher'  
    [ , [ @publisherdb = ] 'publisher_db' ]  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @tranid = ] 'tranid' ]  
    [ , [ @queuetype = ] 'queuetype' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@publisher** =] **'***publisher***'**  
 É o nome do Publicador. *Publisher* está **sysname**, com um padrão NULL. O servidor deve ser configurado para publicação. NULL para todos os Publicadores.  
  
 [ **@publisherdb** =] **'***publisher_db***'** ]  
 É o nome do banco de dados de publicação. *publisher_db* está **sysname**, com um padrão NULL. NULL para todos os bancos de dados de publicação.  
  
 [ **@publication** =] **'***publicação***'** ]  
 É o nome da publicação. *publicação*está **sysname**, com um padrão NULL. NULL para todas as publicações.  
  
 [ **@tranid** =] **'***tranid***'** ]  
 É a ID da transação. *tranid*está **sysname**, com um padrão NULL. NULL para todas as transações.  
  
 [**@queuetype=** ] **'***queuetype***'** ]  
 É o tipo de fila que armazena transações. *queuetype* está **tinyint** com um padrão de **0**, e pode ser um destes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|Todos os tipos de filas|  
|**1**|Enfileiramento de Mensagens|  
|**2**|Fila do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] |  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_replqueuemonitor** é usado em replicação de instantâneo ou replicação transacional com assinaturas de atualização enfileirada. As mensagens em fila que não contêm comandos SQL ou são parte de um comando SQL abrangente não são exibidas.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou **db_owner** banco de dados fixa podem executar **sp_replqueuemonitor**.  
  
## <a name="see-also"></a>Consulte também  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
