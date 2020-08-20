---
description: sp_requestpeertopologyinfo (Transact-SQL)
title: sp_requestpeertopologyinfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_requestpeertopologyinfo
- sp_requestpeertopologyinfo_TSQL
helpviewer_keywords:
- sp_requestpeertopologyinfo
ms.assetid: 15cd28bd-5a72-41fb-ae1b-726baaa6fad5
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9bbd80d75ce96748613cfefe9048dc68b777aae1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489154"
---
# <a name="sp_requestpeertopologyinfo-transact-sql"></a>sp_requestpeertopologyinfo (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Popula a tabela do sistema [MSpeer_topologyresponse](../../relational-databases/system-tables/mspeer-topologyresponse-transact-sql.md) com informações sobre uma topologia de replicação transacional ponto a ponto. Execute [sp_gettopologyinfo](../../relational-databases/system-stored-procedures/sp-gettopologyinfo-transact-sql.md) para obter informações da tabela em formato XML.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_requestpeertopologyinfo [ @publication = ] 'publication'  
        [ ,[ @requestid=] request_id OUTPUT  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @publication =] '*publicação*'  
 É o nome da publicação para a qual executar uma solicitação de status de todas as topologias. a *publicação* é **sysname**, sem padrão.  
  
 [ @request_id =] *request_id*  
 É o número da ID atribuído a uma solicitação de status da topologia. *request_id* é **int**, com um padrão de NULL. Essa ID pode ser usada pelo [sp_gettopologyinfo](../../relational-databases/system-stored-procedures/sp-gettopologyinfo-transact-sql.md).  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 sp_requestpeertopologyinfo é usado em replicação transacional ponto a ponto. Execute sp_requestpeertopologyinfo antes de executar [sp_gettopologyinfo](../../relational-databases/system-stored-procedures/sp-gettopologyinfo-transact-sql.md). Esses procedimentos são usados pelo Assistente para Configurar Topologia Ponto a Ponto, mas eles também podem ser usados diretamente se você precisar de informações sobre topologia em um formato XML. Se você preferir resultados tabulares, consulte a tabela do sistema [MSpeer_topologyresponse](../../relational-databases/system-tables/mspeer-topologyresponse-transact-sql.md) .  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de servidor fixa sysadmin ou na função de banco de dados fixa db_owner.  
  
## <a name="see-also"></a>Consulte Também  
 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
