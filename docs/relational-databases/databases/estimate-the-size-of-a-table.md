---
title: "Estimar o tamanho de uma tabela | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "páginas [SQL Server], espaço"
  - "espaço [SQL Server], tabelas"
  - "tamanho de linha [SQL Server]"
  - "tamanho [SQL Server], tabelas"
  - "tamanho de coluna [SQL Server]"
  - "prevendo o tamanho da tabela [SQL Server]"
  - "tamanho da tabela [SQL Server]"
  - "estimando o tamanho da tabela"
  - "índices clusterizados, tamanho da tabela"
  - "espaço em disco [SQL Server], tabelas"
  - "alocação de espaço [SQL Server], tamanho da tabela"
  - "criando bancos de dados [SQL Server], estimando o tamanho"
  - "linhas livres reservadas por página [SQL Server]"
  - "calculando o tamanho da tabela"
ms.assetid: 15c17c92-616f-402e-894b-907a296efe5f
caps.latest.revision: 30
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 30
---
# Estimar o tamanho de uma tabela
  Você pode usar as seguintes etapas para estimar a quantidade de espaço necessária para armazenar dados em uma tabela:  
  
1.  Calcular o espaço necessário para o heap ou índice clusterizado seguindo as instruções em [Estimar o tamanho de um heap](../../relational-databases/databases/estimate-the-size-of-a-heap.md) ou [Estimar o tamanho de um índice clusterizado](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md).  
  
2.  Calcule o espaço necessário para cada índice não clusterizado, seguindo as instruções em [Estimar o tamanho de um índice não clusterizado](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md).  
  
3.  Some os valores calculados nas etapas 1 e 2.  
  
## Consulte também  
 [Estimar o tamanho de um banco de dados](../../relational-databases/databases/estimate-the-size-of-a-database.md)   
 [Estimando o tamanho de um heap](../../relational-databases/databases/estimate-the-size-of-a-heap.md)   
 [Estimar o tamanho de um índice clusterizado](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)   
 [Estimar o tamanho de um índice não clusterizado](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)  
  
  