---
title: Estimar o tamanho de um banco de dados | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- space allocation [SQL Server], database size
- calculating database size
- increasing database size
- database size [SQL Server], estimating
- predicting database size
- size [SQL Server], databases
- estimating database size
- designing databases [SQL Server], estimating size
ms.assetid: 5b240161-eba4-44b0-946c-61a8fc00fc8c
caps.latest.revision: "20"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1fd8ebd7223c44cdfb5b830ae0f9fc5ea08f3266
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="estimate-the-size-of-a-database"></a>Estimar o tamanho de um banco de dados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Ao projetar um banco de dados, você terá de estimar o quão grande ele ficará quando estiver preenchido com os dados. A estimativa do tamanho do banco de dados pode ajudá-lo a determinar a configuração de hardware que será necessária para fazer o seguinte:  
  
-   Alcançar o desempenho solicitado pelos aplicativos.  
  
-   Garantir a quantia física apropriada de espaço em disco exigida para armazenar os dados e índices.  
  
 O cálculo do tamanho de um banco de dados também pode ajudar a determinar se o design de banco de dados precisa ser refinado. Por exemplo, você pode determinar que o tamanho do banco de dados seja grande demais para implementar em sua empresa e que mais normalização seja necessária. Ao contrário, o tamanho calculado pode ser menor que o esperado. Isto permitiria desnormalizar o banco de dados para melhorar desempenho da consulta.  
  
 Para estimar o tamanho do banco de dados, estime o tamanho de cada tabela individualmente e adicione os valores obtidos. O tamanho da tabela depende se a tabela possui índices e, se possuir, de que tipo de índices.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Estimar o tamanho de uma tabela](../../relational-databases/databases/estimate-the-size-of-a-table.md)|Define as etapas e cálculos necessários para estimar a quantidade de espaço exigida para armazenar os dados em uma tabela e índices associados.|  
|[Estimando o tamanho de um heap](../../relational-databases/databases/estimate-the-size-of-a-heap.md)|Define as etapas e cálculos necessários para estimar a quantidade de espaço exigida para armazenar os dados em um heap. Um heap é uma tabela que não tem um índice clusterizados.|  
|[Estimar o tamanho de um índice clusterizado](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)|Define as etapas e cálculos necessários para estimar a quantidade de espaço exigida para armazenar os dados em um índice clusterizado.|  
|[Estimar o tamanho de um índice não clusterizado](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)|Define as etapas e cálculos necessários para estimar a quantidade de espaço exigida para armazenar os dados em um índice não clusterizado.|  
  
  
