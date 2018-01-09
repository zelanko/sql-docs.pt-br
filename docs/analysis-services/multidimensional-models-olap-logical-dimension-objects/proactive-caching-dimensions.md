---
title: "Cache pró-ativo (dimensões) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- dimensions [Analysis Services], proactive caching
- proactive caching [Analysis Services]
ms.assetid: 7d57fe93-6e5f-4a50-844f-dd2bbdbb94a5
caps.latest.revision: "8"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5df335ed29cb7e899347b189d3c48183f1d5b020
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="proactive-caching-dimensions"></a>Cache pró-ativo (dimensões)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]O cache pró-ativo fornece criação automática de cache MOLAP e gerenciamento para objetos OLAP. Os cubos incorporam imediatamente as alterações feitas nos dados no banco de dados, com base em modificações recebidas do banco de dados. O objetivo do cache pró-ativo é oferecer o desempenho do MOLAP tradicional, além de manter a instantaneidade e facilidade de gerenciamento oferecida pelo ROLAP.  
  
 Um objeto simples <xref:Microsoft.AnalysisServices.ProactiveCaching> é composto de: especificação de tempo e notificação de tabela. A especificação de tempo define o período de tempo para atualizar o cache depois que uma notificação de alteração for recebida. A notificação de tabela define o esquema de notificação entre a tabela de dados e o objeto <xref:Microsoft.AnalysisServices.ProactiveCaching>.  
  
  
