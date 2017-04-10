---
title: "Definir uma rela&#231;&#227;o de fato e propriedades de rela&#231;&#227;o de fato | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "dimensões de fato [Analysis Services]"
ms.assetid: d8e41724-da77-4ac1-bc42-956b5d91ea5d
caps.latest.revision: 10
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 10
---
# Definir uma rela&#231;&#227;o de fato e propriedades de rela&#231;&#227;o de fato
  Quando você definir uma nova dimensão de cubo ou um novo grupo de medidas, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tentará detectar se existe uma relação de fatos e definirá o uso da dimensão como **Fact**. É possível exibir ou editar uma relação de dimensão de fatos na guia **Uso da Dimensão** do Designer de Cubo. A relação de dimensão de fatos entre uma dimensão e um grupo de medidas apresenta as seguintes restrições:  
  
-   Uma dimensão de cubo pode ter apenas uma relação de fatos com um determinado grupo de medidas.  
  
-   Uma dimensão de cubo pode ter relações de fatos separadas com vários grupos de medidas.  
  
-   O atributo de granularidade da relação deve ser o atributo de chave (como Número da Transação) da dimensão. Isso cria uma relação de um para um entre a dimensão e os fatos da tabela de fatos.  
  
  