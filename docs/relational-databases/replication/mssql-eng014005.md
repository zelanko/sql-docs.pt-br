---
title: "MSSQL_ENG014005 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "erro MSSQL_ENG014005"
ms.assetid: f168f0d6-cb11-45d4-9781-c374d7f388ee
caps.latest.revision: 13
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# MSSQL_ENG014005
    
## Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|14005|  
|Origem do evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Não foi possível descartar a publicação. Existe uma assinatura para ela.|  
  
## Explicação  
 Você tentou descartar uma publicação que tem uma ou mais assinatura associadas. Uma publicação pode ser descartada somente se não houver nenhuma assinatura associada.  
  
## Ação do usuário  
 Descarte as assinaturas antes de descartar a publicação. Se você usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para descartar a publicação, haverá a opção de descartar automaticamente todas as assinaturas associadas antes de descartar a publicação. Se você usar procedimentos armazenados, primeiro será necessário descartar explicitamente as assinaturas. Para obter mais informações, consulte [Excluir uma assinatura Push](../../relational-databases/replication/delete-a-push-subscription.md) e [Excluir uma assinatura Pull](../../relational-databases/replication/delete-a-pull-subscription.md).  
  
 Se não existirem assinaturas para a publicação ou se o erro for exibido ao criar uma publicação, talvez exista uma assinatura anterior que não foi limpa completamente quando você tentou removê-la. Executar [sp_removedbreplication & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) no banco de dados para remover todos os objetos e configurações relacionadas à replicação.  
  
## Consulte também  
 [Erros e eventos referência & #40. Replicação e 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  