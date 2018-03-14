---
title: Inicializar uma assinatura | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 703a1aedae5a16236fe64c087dee9ed81667e9c3
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2018
---
# <a name="initialize-a-subscription"></a>Inicializar uma assinatura
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Os assinantes em uma topologia de replicação devem ser inicializados, de modo a terem uma cópia do esquema de cada artigo na publicação que assinaram e quaisquer objetos de replicação que sejam necessários, como procedimentos armazenados, gatilhos e tabelas de metadados. Além disso, o Assinante recebe, geralmente, um conjunto de dados inicial. O método de inicialização padrão usa um instantâneo completo que inclui esquema, objetos de replicação e dados, mas as publicações também podem ser inicializadas sem um instantâneo completo.  
  
 Para obter mais informações, consulte [Initialize a Subscription with a Snapshot](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md) e [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
  
