---
title: "Inicializar uma assinatura | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "replicação de instantâneo [SQL Server], inicializando assinaturas"
  - "replicação transacional, inicializando assinaturas"
  - "inicializando assinaturas [replicação do SQL Server]"
  - "assinaturas [replicação do SQL Server], inicializando"
  - "inicializando assinaturas [replicação do SQL Server], sobre a inicialização de assinaturas"
  - "replicação de mesclagem [replicação do SQL Server], inicializando assinaturas"
ms.assetid: d6013845-cb7a-4203-8e21-edce32f1d330
caps.latest.revision: 32
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 32
---
# Inicializar uma assinatura
  Os assinantes em uma topologia de replicação devem ser inicializados, de modo a terem uma cópia do esquema de cada artigo na publicação que assinaram e quaisquer objetos de replicação que sejam necessários, como procedimentos armazenados, gatilhos e tabelas de metadados. Além disso, o Assinante recebe, geralmente, um conjunto de dados inicial. O método de inicialização padrão usa um instantâneo completo que inclui esquema, objetos de replicação e dados, mas as publicações também podem ser inicializadas sem um instantâneo completo.  
  
 Para obter mais informações, consulte [inicializar uma assinatura com um instantâneo](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md) e [inicializar um transacional assinatura sem um instantâneo](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
  