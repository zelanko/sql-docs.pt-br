---
title: sp_gettopologyinfo (Transact-SQL) | Microsoft Docs
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
- sp_gettopologyinfo_TSQL
- sp_gettopologyinfo
helpviewer_keywords:
- sp_gettopologyinfo
ms.assetid: 8bbe8a06-a4aa-4219-8402-12db6a4682c6
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d0e03caea5a8620be8678dcac6cca307e33445c1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spgettopologyinfo-transact-sql"></a>sp_gettopologyinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre uma topologia de replicação transacional ponto a ponto. Executar [sp_requestpeertopologyinfo](../../relational-databases/system-stored-procedures/sp-requestpeertopologyinfo-transact-sql.md) para coletar informações antes de executar esse procedimento.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_gettopologyinfo [ @request_id = ] request_id  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @request_id=] *request_id*  
 É a ID de uma solicitação de status de topologia. *request_id* é **int**, com um padrão NULL. Para obter uma ID, use o @request_id parâmetro a partir de saída [sp_requestpeertopologyinfo](../../relational-databases/system-stored-procedures/sp-requestpeertopologyinfo-transact-sql.md) ou consultar o [MSpeer_topologyrequest](../../relational-databases/system-tables/mspeer-topologyrequest-transact-sql.md) tabela do sistema.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 sp_gettopologyinfo retorna um conjunto de resultados que tem uma única coluna XML. Os dados na coluna XML são o mesmo que os dados de [MSpeer_topologyresponse](../../relational-databases/system-tables/mspeer-topologyresponse-transact-sql.md) tabela do sistema.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 sp_gettopologyinfo é usado em replicação transacional ponto a ponto. Executar [sp_requestpeertopologyinfo](../../relational-databases/system-stored-procedures/sp-requestpeertopologyinfo-transact-sql.md) antes de executar sp_gettopologyinfo. Esses procedimentos são usados pelo Assistente para Configurar Topologia Ponto a Ponto, mas eles também podem ser usados diretamente se você precisar de informações sobre topologia em um formato XML. Se você preferir resultados tabulares, consulte o [MSpeer_topologyresponse](../../relational-databases/system-tables/mspeer-topologyresponse-transact-sql.md) tabela do sistema.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de servidor fixa sysadmin ou na função de banco de dados fixa db_owner.  
  
## <a name="see-also"></a>Consulte também  
 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
