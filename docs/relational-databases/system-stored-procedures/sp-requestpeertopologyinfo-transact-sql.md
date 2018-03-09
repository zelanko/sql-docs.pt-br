---
title: sp_requestpeertopologyinfo (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
- sp_requestpeertopologyinfo
- sp_requestpeertopologyinfo_TSQL
helpviewer_keywords:
- sp_requestpeertopologyinfo
ms.assetid: 15cd28bd-5a72-41fb-ae1b-726baaa6fad5
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 85f682f36295211edd67862bcc11d0d1922318e6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sprequestpeertopologyinfo-transact-sql"></a>sp_requestpeertopologyinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Preenche o [MSpeer_topologyresponse](../../relational-databases/system-tables/mspeer-topologyresponse-transact-sql.md) tabela do sistema com informações sobre uma topologia de replicação transacional ponto a ponto. Executar [sp_gettopologyinfo](../../relational-databases/system-stored-procedures/sp-gettopologyinfo-transact-sql.md) para obter informações da tabela no formato XML.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_requestpeertopologyinfo [ @publication = ] 'publication'  
        [ ,[ @requestid=] request_id OUTPUT  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @publication=] '*publicação*'  
 É o nome da publicação para a qual executar uma solicitação de status de todas as topologias. *publicação* é **sysname**, sem padrão.  
  
 [ @request_id=] *request_id*  
 É o número da ID atribuído a uma solicitação de status da topologia. *request_id* é **int**, com um padrão NULL. Essa ID pode ser usada por [sp_gettopologyinfo](../../relational-databases/system-stored-procedures/sp-gettopologyinfo-transact-sql.md).  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 sp_requestpeertopologyinfo é usado em replicação transacional ponto a ponto. Execute sp_requestpeertopologyinfo antes de executar [sp_gettopologyinfo](../../relational-databases/system-stored-procedures/sp-gettopologyinfo-transact-sql.md). Esses procedimentos são usados pelo Assistente para Configurar Topologia Ponto a Ponto, mas eles também podem ser usados diretamente se você precisar de informações sobre topologia em um formato XML. Se você preferir resultados tabulares, consulte o [MSpeer_topologyresponse](../../relational-databases/system-tables/mspeer-topologyresponse-transact-sql.md) tabela do sistema.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de servidor fixa sysadmin ou na função de banco de dados fixa db_owner.  
  
## <a name="see-also"></a>Consulte também  
 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
