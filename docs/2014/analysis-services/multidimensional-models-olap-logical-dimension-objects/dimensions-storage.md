---
title: Armazenamento de dimensão | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- dimensions [Analysis Services], storage
- storing data [Analysis Services]
- storage [Analysis Services], dimensions
- relational OLAP
- multidimensional OLAP
- MOLAP
- storing data [Analysis Services], dimensions
- ROLAP
ms.assetid: 8d74b932-2174-4e1f-8414-636455880b6a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ce5bf2a376712d603be3099f7ccefa0e6b799219
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62728482"
---
# <a name="dimension-storage"></a>Armazenamento de dimensões
  As dimensões [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no dão suporte a dois modos de armazenamento:  
  
-   OLAP relacional (ROLAP)  
  
-   OLAP multidimensional (MOLAP)  
  
 O modo de armazenamento determina o local e a forma dos dados de uma dimensão. O MOLAP é o modo de armazenamento padrão para dimensões. **Tópicos relacionados:**[modos de armazenamento de partição e processamento](../multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md)  
  
## <a name="molap"></a>MOLAP  
 Dados de uma dimensão que usam MOLAP são armazenados em uma estrutura multidimensional na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Essa estrutura multidimensional é criada e populada quando a dimensão é processada. As dimensões MOLAP fornecem melhores desempenho de consulta do que de dimensões ROLAP.  
  
## <a name="rolap"></a>ROLAP  
 Dados de uma dimensão que usa ROLAP são armazenados nas tabelas usadas para definir a dimensão. O modo de armazenamento ROLAP pode ser usado para oferecer suporte para grandes dimensões sem duplicar grandes quantidades de dados, mas diminuindo o desempenho da consulta. Como a dimensão depende diretamente das tabelas na exibição de fonte de dados, usados para definir a dimensão, o modo de armazenamento ROLAP também oferece suporte ao OLAP em tempo real.  
  
> [!IMPORTANT]  
>  Se a dimensão usa o modo de armazenamento ROLAP e a dimensão está incluída em um cubo que usa o armazenamento MOLAP, qualquer alteração de esquema na tabela de origem deve ser seguida por processamento imediato do cubo. Se não fizer isso, poderá gerar resultados inconsistentes quando consultar o cubo. **Tópico relacionado:**[automatizar Analysis Services tarefas administrativas com o SSIS](../instances/automate-analysis-services-administrative-tasks-with-ssis.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Modos e processamento de armazenamento de partição](../multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md)  
  
  
