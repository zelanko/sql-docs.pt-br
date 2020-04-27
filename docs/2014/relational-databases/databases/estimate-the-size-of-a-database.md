---
title: Estimar o tamanho de um banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6370b6b08639f57419b08a1c380b440d0d98a591
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62871452"
---
# <a name="estimate-the-size-of-a-database"></a>Estimar o tamanho de um banco de dados
  Ao projetar um banco de dados, você terá de estimar o quão grande ele ficará quando estiver completo com dados. A estimativa do tamanho do banco de dados pode ajudá-lo a determinar a configuração de hardware que será necessária para fazer o seguinte:  
  
-   Alcançar o desempenho solicitado pelos aplicativos.  
  
-   Garantir a quantia física apropriada de espaço em disco exigida para armazenar os dados e índices.  
  
 O cálculo do tamanho de um banco de dados também pode ajudar a determinar se o design de banco de dados precisa ser refinado. Por exemplo, você pode determinar que o tamanho do banco de dados seja grande demais para implementar em sua empresa e que mais normalização seja necessária. Ao contrário, o tamanho calculado pode ser menor que o esperado. Isto permitiria desnormalizar o banco de dados para melhorar desempenho da consulta.  
  
 Para estimar o tamanho do banco de dados, estime o tamanho de cada tabela individualmente e adicione os valores obtidos. O tamanho da tabela depende se a tabela possui índices e, se possuir, de que tipo de índices.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|DESCRIÇÃO|  
|-----------|-----------------|  
|[Estimar o tamanho de uma tabela](estimate-the-size-of-a-table.md)|Define as etapas e cálculos necessários para estimar a quantidade de espaço exigida para armazenar os dados em uma tabela e índices associados.|  
|[Estimar o tamanho de um heap](estimate-the-size-of-a-heap.md)|Define as etapas e cálculos necessários para estimar a quantidade de espaço exigida para armazenar os dados em um heap. Um heap é uma tabela que não tem um índice clusterizados.|  
|[Estimar o tamanho de um índice clusterizado](estimate-the-size-of-a-clustered-index.md)|Define as etapas e cálculos necessários para estimar a quantidade de espaço exigida para armazenar os dados em um índice clusterizado.|  
|[Estimar o tamanho de um índice não clusterizado](estimate-the-size-of-a-nonclustered-index.md)|Define as etapas e cálculos necessários para estimar a quantidade de espaço exigida para armazenar os dados em um índice não clusterizado.|  
  
  
