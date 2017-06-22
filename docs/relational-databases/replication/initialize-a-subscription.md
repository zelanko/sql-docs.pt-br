---
title: Inicializar uma assinatura | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshot replication [SQL Server], initializing subscriptions
- transactional replication, initializing subscriptions
- initializing subscriptions [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], about initializing subscriptions
- merge replication [SQL Server replication], initializing subscriptions
ms.assetid: d6013845-cb7a-4203-8e21-edce32f1d330
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cb6afeb29ea5a834ae67e9521f690fba748c7c68
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="initialize-a-subscription"></a>Inicializar uma assinatura
  Os assinantes em uma topologia de replicação devem ser inicializados, de modo a terem uma cópia do esquema de cada artigo na publicação que assinaram e quaisquer objetos de replicação que sejam necessários, como procedimentos armazenados, gatilhos e tabelas de metadados. Além disso, o Assinante recebe, geralmente, um conjunto de dados inicial. O método de inicialização padrão usa um instantâneo completo que inclui esquema, objetos de replicação e dados, mas as publicações também podem ser inicializadas sem um instantâneo completo.  
  
 Para obter mais informações, consulte [Initialize a Subscription with a Snapshot](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md) e [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
  
