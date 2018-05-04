---
title: Cache pró-ativo (dimensões) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cf1dee51b8ff659257eb290907dafa8536c386f1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="proactive-caching-dimensions"></a>Cache pró-ativo (dimensões)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  O cache pró-ativo fornece criação automática de cache MOLAP e gerenciamento de objetos OLAP. Os cubos incorporam imediatamente as alterações feitas nos dados no banco de dados, com base em modificações recebidas do banco de dados. O objetivo do cache pró-ativo é oferecer o desempenho do MOLAP tradicional, além de manter a instantaneidade e facilidade de gerenciamento oferecida pelo ROLAP.  
  
 Um objeto simples <xref:Microsoft.AnalysisServices.ProactiveCaching> é composto de: especificação de tempo e notificação de tabela. A especificação de tempo define o período de tempo para atualizar o cache depois que uma notificação de alteração for recebida. A notificação de tabela define o esquema de notificação entre a tabela de dados e o objeto <xref:Microsoft.AnalysisServices.ProactiveCaching>.  
  
  
