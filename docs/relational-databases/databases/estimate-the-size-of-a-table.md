---
title: Estimar o tamanho de uma tabela | Microsoft Docs
description: Use este procedimento para estimar a quantidade de espaço exigida para armazenar dados em uma tabela no SQL Server.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
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
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d2cec3c9f67a07cb36c6ba7f4a11225b5544b252
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86002193"
---
# <a name="estimate-the-size-of-a-table"></a>Estimar o tamanho de uma tabela
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  Você pode usar as seguintes etapas para estimar a quantidade de espaço necessária para armazenar dados em uma tabela:  
  
1.  Calcular o espaço necessário para o heap ou índice clusterizado seguindo as instruções em [Estimar o tamanho de um heap](../../relational-databases/databases/estimate-the-size-of-a-heap.md) ou [Estimar o tamanho de um índice clusterizado](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md).  
  
2.  Calcule o espaço necessário para cada índice não clusterizado, seguindo as instruções em [Estimar o tamanho de um índice não clusterizado](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md).  
  
3.  Some os valores calculados nas etapas 1 e 2.  

## <a name="see-also"></a>Consulte Também  
 [Estimar o tamanho de um banco de dados](../../relational-databases/databases/estimate-the-size-of-a-database.md)   
 [Estimar o tamanho de um heap](../../relational-databases/databases/estimate-the-size-of-a-heap.md)   
 [Estimar o tamanho de um índice clusterizado](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)   
 [Estimar o tamanho de um índice não clusterizado](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)  
  
  
