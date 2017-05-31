---
title: MSSQL_ENG014005 | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG014005 error
ms.assetid: f168f0d6-cb11-45d4-9781-c374d7f388ee
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 185ea6a67ab4ce799aa3c2ff11c3651127b08292
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="mssqleng014005"></a>MSSQL_ENG014005
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|14005|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Não foi possível descartar a publicação. Existe uma assinatura para ela.|  
  
## <a name="explanation"></a>Explicação  
 Você tentou descartar uma publicação que tem uma ou mais assinatura associadas. Uma publicação pode ser descartada somente se não houver nenhuma assinatura associada.  
  
## <a name="user-action"></a>Ação do usuário  
 Descarte as assinaturas antes de descartar a publicação. Se você usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para descartar a publicação, haverá a opção de descartar automaticamente todas as assinaturas associadas antes de descartar a publicação. Se você usar procedimentos armazenados, primeiro será necessário descartar explicitamente as assinaturas. Para obter mais informações, consulte [Delete a Push Subscription](../../relational-databases/replication/delete-a-push-subscription.md) e [Delete a Pull Subscription](../../relational-databases/replication/delete-a-pull-subscription.md).  
  
 Se não existirem assinaturas para a publicação ou se o erro for exibido ao criar uma publicação, talvez exista uma assinatura anterior que não foi limpa completamente quando você tentou removê-la. Execute [sp_removedbreplication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) no banco de dados para remover todas as configurações e todos os objetos relacionados à replicação.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de erros e eventos &#40;Replicação&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
