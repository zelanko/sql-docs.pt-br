---
title: MSSQL_ENG014005 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG014005 error
ms.assetid: f168f0d6-cb11-45d4-9781-c374d7f388ee
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: fc1d7d9cdbdf9dd5c4f573c4893e35cad7f3ae98
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36005646"
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
 Descarte as assinaturas antes de descartar a publicação. Se você usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para descartar a publicação, haverá a opção de descartar automaticamente todas as assinaturas associadas antes de descartar a publicação. Se você usar procedimentos armazenados, primeiro será necessário descartar explicitamente as assinaturas. Para obter mais informações, consulte [Delete a Push Subscription](delete-a-push-subscription.md) e [Delete a Pull Subscription](delete-a-pull-subscription.md).  
  
 Se não existirem assinaturas para a publicação ou se o erro for exibido ao criar uma publicação, talvez exista uma assinatura anterior que não foi limpa completamente quando você tentou removê-la. Execute [sp_removedbreplication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) no banco de dados para remover todas as configurações e todos os objetos relacionados à replicação.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de erros e eventos &#40;Replicação&#41;](errors-and-events-reference-replication.md)  
  
  
