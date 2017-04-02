---
title: "Replica&#231;&#227;o transacional bidirecional | Microsoft Docs"
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
  - "replicação bidirecional"
  - "replicação transacional, replicação bidirecional"
  - "replicação transacional bidirecional"
ms.assetid: 98772e95-67ed-4010-8108-5113dbe709ff
caps.latest.revision: 27
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 27
---
# Replica&#231;&#227;o transacional bidirecional
  Replicação transacional bidirecional é uma topologia de replicação transacional específica que permite a dois servidores trocarem alterações entre si: cada servidor publica dados e, então, assina uma publicação com os mesmos dados do outro servidor. O **@loopback_detection** parâmetro [sp_addsubscription & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) é definido como TRUE para garantir que as alterações só serão enviadas ao assinante e não resultem na alteração sendo enviada de volta para o publicador.  
  
 Em [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e versões posteriores, essa topologia também é compatível com replicação transacional ponto a ponto, mas replicação bidirecional pode proporcionar melhor desempenho.  
  
## Consulte também  
 [Replicação transacional ponto a ponto](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  