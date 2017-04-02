---
title: "Tipos de publica&#231;&#227;o para Replica&#231;&#227;o Transacional | Microsoft Docs"
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
  - "replicação transacional, publicações"
ms.assetid: ad66aa34-3e37-401e-a6a1-fc1514eb6d50
caps.latest.revision: 32
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 32
---
# Tipos de publica&#231;&#227;o para Replica&#231;&#227;o Transacional
  A Replicação Transacional oferece três tipos de publicação:  
  
|Tipo de Publicação|Descrição|  
|----------------------|-----------------|  
|Publicação Transacional padrão|Apropriada para topologias em que todos os dados do Assinante são do modo somente leitura (a replicação transacional não impõe isto no Assinante).<br /><br /> As publicações transacionais padrão são criadas por padrão ao usar Transact-SQL ou RMO (Replication Management Objects). Ao usar o Assistente para nova publicação, elas são criadas selecionando **publicação transacional** sobre o **tipo de publicação** página.<br /><br /> Para obter mais informações sobre a criação de publicações, consulte [publica dados e objetos de banco de dados](../../../relational-databases/replication/publish/publish-data-and-database-objects.md).|  
|Publicação Transacional em uma topologia ponto a ponto|As características deste tipo de publicação são:<br /><br /> -Cada local tem dados idênticos e atua como um Publicador e Assinante.<br /><br /> -A mesma linha pode ser alterada apenas em um local de cada vez.<br /><br /> -Esta topologia é melhor adequada para ambientes de servidor que requerem alta disponibilidade e escalabilidade de leitura.<br /><br /> <br /><br /> Para obter mais informações, consulte [replicação transacional ponto a ponto](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).|  
  
## Consulte também  
 [Replicação transacional](../../../relational-databases/replication/transactional/transactional-replication.md)  
  
  