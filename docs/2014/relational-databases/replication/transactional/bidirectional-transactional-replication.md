---
title: Replicação transacional bidirecional | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- bidirectional replication
- transactional replication, bidirectional replication
- bidirectional transactional replication
ms.assetid: 98772e95-67ed-4010-8108-5113dbe709ff
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a2cf5fbf215338b273be0924e6930906c8698aff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188599"
---
# <a name="bidirectional-transactional-replication"></a>replicação transacional bidirecional
  Replicação transacional bidirecional é uma topologia de replicação transacional específica que permite a dois servidores trocarem alterações entre si: cada servidor publica dados e, então, assina uma publicação com os mesmos dados do outro servidor. O parâmetro **@loopback_detection** de [sp_addsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql) é definido para TRUE a fim de garantir que as alterações sejam enviadas somente ao Assinante e não resultem na alteração sendo enviada de volta ao Publicador.  
  
 Em [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e versões posteriores, essa topologia também tem suporte para replicação transacional ponto a ponto, mas replicação bidirecional pode fornecer desempenho aprimorado.  
  
## <a name="see-also"></a>Consulte também  
 [Peer-to-Peer Transactional Replication](peer-to-peer-transactional-replication.md)  
  
  
