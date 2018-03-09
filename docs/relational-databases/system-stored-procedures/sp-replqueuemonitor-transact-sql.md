---
title: sp_replqueuemonitor (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- sp_replqueuemonitor
- sp_replqueuemonitor_TSQL
helpviewer_keywords: sp_replqueuemonitor
ms.assetid: 6909a3f1-43a2-4df5-a6a5-9e6f347ac841
caps.latest.revision: "25"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bd29cdd9e22873dd7d10db99078f25ce7e15d55f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spreplqueuemonitor-transact-sql"></a>sp_replqueuemonitor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Lista as mensagens da fila de um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fila ou [!INCLUDE[msCoName](../../includes/msconame-md.md)] enfileiramento de mensagens para assinaturas de atualização enfileiradas para uma publicação especificada. Se as filas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] forem usadas, esse procedimento armazenado será executado no banco de dados de assinatura. Se o Enfileiramento de Mensagens for usado, esse procedimento armazenado será executado no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_replqueuemonitor [ @publisher = ] 'publisher'  
    [ , [ @publisherdb = ] 'publisher_db' ]  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @tranid = ] 'tranid' ]  
    [ , [ @queuetype = ] 'queuetype' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher**  =] **'***publicador***'**  
 É o nome do Publicador. *publicador* é **sysname**, com um padrão NULL. O servidor deve ser configurado para publicação. NULL para todos os Publicadores.  
  
 [  **@publisherdb**  =] **'***publisher_db***'** ]  
 É o nome do banco de dados de publicação. *publisher_db* é **sysname**, com um padrão NULL. NULL para todos os bancos de dados de publicação.  
  
 [  **@publication**  =] **'***publicação***'** ]  
 É o nome da publicação. *publicação*é **sysname**, com um padrão NULL. NULL para todas as publicações.  
  
 [  **@tranid**  =] **'***tranid***'** ]  
 É a ID da transação. *tranid*é **sysname**, com um padrão NULL. NULL para todas as transações.  
  
 [**@queuetype=** ] **'***queuetype***'** ]  
 É o tipo de fila que armazena transações. *queuetype* é **tinyint** com um padrão de **0**, e pode ser um destes valores.  
  
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
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_replqueuemonitor**.  
  
## <a name="see-also"></a>Consulte também  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
