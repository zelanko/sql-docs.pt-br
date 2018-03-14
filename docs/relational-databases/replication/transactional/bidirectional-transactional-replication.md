---
title: "Replicação transacional bidirecional | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bidirectional replication
- transactional replication, bidirectional replication
- bidirectional transactional replication
ms.assetid: 98772e95-67ed-4010-8108-5113dbe709ff
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ccca24e2509bdb0f3de8c8c98e1ab5b652856423
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2018
---
# <a name="bidirectional-transactional-replication"></a>replicação transacional bidirecional
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Replicação transacional bidirecional é uma topologia de replicação transacional específica que permite a dois servidores trocarem alterações entre si: cada servidor publica dados e, então, assina uma publicação com os mesmos dados do outro servidor. O parâmetro **@loopback_detection** de [sp_addsubscription &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) é definido para TRUE a fim de garantir que as alterações sejam enviadas somente ao Assinante e não resultem na alteração sendo enviada de volta ao Publicador.  
  
 Em [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e versões posteriores, essa topologia também tem suporte para replicação transacional ponto a ponto, mas replicação bidirecional pode fornecer desempenho aprimorado.  
  
## <a name="see-also"></a>Consulte Também  
 [Peer-to-Peer Transactional Replication](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
