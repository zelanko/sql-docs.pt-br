---
title: Estimar o tamanho de uma tabela | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- pages [SQL Server], space
- space [SQL Server], tables
- row size [SQL Server]
- size [SQL Server], tables
- column size [SQL Server]
- predicting table size [SQL Server]
- table size [SQL Server]
- estimating table size
- clustered indexes, table size
- disk space [SQL Server], tables
- space allocation [SQL Server], table size
- designing databases [SQL Server], estimating size
- reserved free rows per page [SQL Server]
- calculating table size
ms.assetid: 15c17c92-616f-402e-894b-907a296efe5f
caps.latest.revision: 29
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 8410df06898ed7c536c8a6bc8c368c1ec68d6457
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36020020"
---
# <a name="estimate-the-size-of-a-table"></a>Estimar o tamanho de uma tabela
  Você pode usar as seguintes etapas para estimar a quantidade de espaço necessária para armazenar dados em uma tabela:  
  
1.  Calcular o espaço necessário para o heap ou índice clusterizado seguindo as instruções em [Estimar o tamanho de um heap](estimate-the-size-of-a-heap.md) ou [Estimar o tamanho de um índice clusterizado](estimate-the-size-of-a-clustered-index.md).  
  
2.  Calcule o espaço necessário para cada índice não clusterizado, seguindo as instruções em [Estimar o tamanho de um índice não clusterizado](estimate-the-size-of-a-nonclustered-index.md).  
  
3.  Some os valores calculados nas etapas 1 e 2.  
  
## <a name="see-also"></a>Consulte também  
 [Estimar o tamanho de um banco de dados](estimate-the-size-of-a-database.md)   
 [Estimar o tamanho de um heap](estimate-the-size-of-a-heap.md)   
 [Estimar o tamanho de um índice clusterizado](estimate-the-size-of-a-clustered-index.md)   
 [Estimar o tamanho de um índice não clusterizado](estimate-the-size-of-a-nonclustered-index.md)  
  
  