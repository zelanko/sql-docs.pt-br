---
title: Definir uma relação de fatos e as propriedades da relação de fatos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- fact dimensions [Analysis Services]
ms.assetid: d8e41724-da77-4ac1-bc42-956b5d91ea5d
author: minewiskan
ms.author: owend
ms.openlocfilehash: 15f67a4bdf699bbc6443fc76ce54bcfb35831827
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547088"
---
# <a name="define-a-fact-relationship-and-fact-relationship-properties"></a>Definir uma relação de fato e propriedades de relação de fato
  Quando você definir uma nova dimensão de cubo ou um novo grupo de medidas, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tentará detectar se existe uma relação de fatos e, em seguida, definirá o uso da dimensão como `Fact`. É possível exibir ou editar uma relação de dimensão de fatos na guia **Uso da Dimensão** do Designer de Cubo. A relação de dimensão de fatos entre uma dimensão e um grupo de medidas apresenta as seguintes restrições:  
  
-   Uma dimensão de cubo pode ter apenas uma relação de fatos com um determinado grupo de medidas.  
  
-   Uma dimensão de cubo pode ter relações de fatos separadas com vários grupos de medidas.  
  
-   O atributo de granularidade da relação deve ser o atributo de chave (como Número da Transação) da dimensão. Isso cria uma relação de um para um entre a dimensão e os fatos da tabela de fatos.  
  
  
