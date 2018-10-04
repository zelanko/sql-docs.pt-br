---
title: Replicação transacional bidirecional | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- bidirectional replication
- transactional replication, bidirectional replication
- bidirectional transactional replication
ms.assetid: 98772e95-67ed-4010-8108-5113dbe709ff
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 86cdfaa9e7bf61b76acb953e3f2c6a1feb7d1dad
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48126764"
---
# <a name="bidirectional-transactional-replication"></a>replicação transacional bidirecional
  Replicação transacional bidirecional é uma topologia de replicação transacional específica que permite a dois servidores trocarem alterações entre si: cada servidor publica dados e, então, assina uma publicação com os mesmos dados do outro servidor. O parâmetro **@loopback_detection** de [sp_addsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql) é definido para TRUE a fim de garantir que as alterações sejam enviadas somente ao Assinante e não resultem na alteração sendo enviada de volta ao Publicador.  
  
 Em [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e versões posteriores, essa topologia também tem suporte para replicação transacional ponto a ponto, mas replicação bidirecional pode fornecer desempenho aprimorado.  
  
## <a name="see-also"></a>Consulte também  
 [Peer-to-Peer Transactional Replication](peer-to-peer-transactional-replication.md)  
  
  
