---
title: Definir uma relação de fato e propriedades de relação de fato | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2341335d1d9c4904e1832e0a8087c0fa8198fd58
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="define-a-fact-relationship-and-fact-relationship-properties"></a>Definir uma relação de fato e propriedades de relação de fato
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Quando você definir uma nova dimensão de cubo ou um novo grupo de medidas, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tentará detectar se existe uma relação de fatos e definirá o uso da dimensão como **Fact**. É possível exibir ou editar uma relação de dimensão de fatos na guia **Uso da Dimensão** do Designer de Cubo. A relação de dimensão de fatos entre uma dimensão e um grupo de medidas apresenta as seguintes restrições:  
  
-   Uma dimensão de cubo pode ter apenas uma relação de fatos com um determinado grupo de medidas.  
  
-   Uma dimensão de cubo pode ter relações de fatos separadas com vários grupos de medidas.  
  
-   O atributo de granularidade da relação deve ser o atributo de chave (como Número da Transação) da dimensão. Isso cria uma relação de um para um entre a dimensão e os fatos da tabela de fatos.  
  
  
