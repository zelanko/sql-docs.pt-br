---
title: Inicializar uma assinatura | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshot replication [SQL Server], initializing subscriptions
- transactional replication, initializing subscriptions
- initializing subscriptions [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], about initializing subscriptions
- merge replication [SQL Server replication], initializing subscriptions
ms.assetid: d6013845-cb7a-4203-8e21-edce32f1d330
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 66ba96a96f95f91974f0a948db34c34ca0391f1b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/25/2020
ms.locfileid: "62721125"
---
# <a name="initialize-a-subscription"></a>Inicializar uma assinatura
  Os assinantes em uma topologia de replicação devem ser inicializados, de modo a terem uma cópia do esquema de cada artigo na publicação que assinaram e quaisquer objetos de replicação que sejam necessários, como procedimentos armazenados, gatilhos e tabelas de metadados. Além disso, o Assinante recebe, geralmente, um conjunto de dados inicial. O método de inicialização padrão usa um instantâneo completo que inclui esquema, objetos de replicação e dados, mas as publicações também podem ser inicializadas sem um instantâneo completo.  
  
 Para obter mais informações, consulte [Initialize a Subscription with a Snapshot](initialize-a-subscription-with-a-snapshot.md) e [Initialize a Transactional Subscription Without a Snapshot](initialize-a-transactional-subscription-without-a-snapshot.md).  
  
  
