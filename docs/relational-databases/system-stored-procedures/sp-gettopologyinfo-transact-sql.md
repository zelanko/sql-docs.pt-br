---
description: sp_gettopologyinfo (Transact-SQL)
title: sp_gettopologyinfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_gettopologyinfo_TSQL
- sp_gettopologyinfo
helpviewer_keywords:
- sp_gettopologyinfo
ms.assetid: 8bbe8a06-a4aa-4219-8402-12db6a4682c6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 423739aa8ae2407b2b536fa9e2313c9073e0b6c6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88469406"
---
# <a name="sp_gettopologyinfo-transact-sql"></a>sp_gettopologyinfo (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna informações sobre uma topologia de replicação transacional ponto a ponto. Execute [sp_requestpeertopologyinfo](../../relational-databases/system-stored-procedures/sp-requestpeertopologyinfo-transact-sql.md) para coletar informações antes de executar este procedimento.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_gettopologyinfo [ @request_id = ] request_id  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @request_id =] *request_id*  
 É a ID de uma solicitação de status de topologia. *request_id* é **int**, com um padrão de NULL. Para obter uma ID, use o @request_id parâmetro de saída de [sp_requestpeertopologyinfo](../../relational-databases/system-stored-procedures/sp-requestpeertopologyinfo-transact-sql.md) ou consulte a tabela do sistema [MSpeer_topologyrequest](../../relational-databases/system-tables/mspeer-topologyrequest-transact-sql.md) .  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 sp_gettopologyinfo retorna um conjunto de resultados que tem uma única coluna XML. Os dados na coluna XML são os mesmos que os dados na tabela do sistema [MSpeer_topologyresponse](../../relational-databases/system-tables/mspeer-topologyresponse-transact-sql.md) .  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 sp_gettopologyinfo é usado em replicação transacional ponto a ponto. Execute [sp_requestpeertopologyinfo](../../relational-databases/system-stored-procedures/sp-requestpeertopologyinfo-transact-sql.md) antes de executar sp_gettopologyinfo. Esses procedimentos são usados pelo Assistente para Configurar Topologia Ponto a Ponto, mas eles também podem ser usados diretamente se você precisar de informações sobre topologia em um formato XML. Se você preferir resultados tabulares, consulte a tabela do sistema [MSpeer_topologyresponse](../../relational-databases/system-tables/mspeer-topologyresponse-transact-sql.md) .  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de servidor fixa sysadmin ou na função de banco de dados fixa db_owner.  
  
## <a name="see-also"></a>Consulte Também  
 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
