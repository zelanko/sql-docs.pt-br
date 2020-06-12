---
title: Visualizador de árvore de conteúdo genérica da Microsoft (mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.contentviewer.f1
ms.assetid: 751b4393-f6fd-48c1-bcef-bdca589ce34c
author: minewiskan
ms.author: owend
ms.openlocfilehash: 96a259ed9436bb7c8b79a8eb9da1c3c899e6d994
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545478"
---
# <a name="microsoft-generic-content-tree-viewer-data-mining"></a>Visualizador de árvore de conteúdo genérica da Microsoft (Mineração de Dados)
  O **Visualizador de Árvore de Conteúdo Genérica da Microsoft** exibe informações detalhadas sobre o conteúdo de um modo de mineração de dados em um formato de tabela HTML padronizado. Esta exibição é útil porque expõe a estrutura subjacente do modelo, assim como detalhes sobre coeficientes, a distribuição de valores e muito mais.  
  
 O conteúdo atual exibido na tabela varia dependendo do algoritmo usado e podem incluir colunas, regras, propriedades, atributos, nós e fórmulas. Para obter mais informações sobre o conteúdo do modelo e sobre como interpretar as informações de cada tipo de modelo, consulte [Conteúdo do modelo de mineração &#40;Analysis Services – Mineração de Dados&#41;](data-mining/mining-model-content-analysis-services-data-mining.md).  
  
 As informações exibidas no visualizador usam uma estrutura comum que é baseada no conjunto de linhas do esquema de conteúdo dos modelos de mineração. O conjunto de linhas do esquema de conteúdo é uma estrutura genérica para armazenar padrões, estatísticas e outros conteúdos de um modelo de mineração de dados. Para obter uma lista das colunas do conjunto de linhas do esquema de mineração de dados para modelos de mineração, consulte [Conjunto de linhas DMSCHEMA_MINING_MODEL_CONTENT](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset).  
  
## <a name="options"></a>Opções  
 **Legenda do nó (ID exclusivo)**  
 Este painel exibe uma lista de todos os nós no modelo de mineração selecionado. A maneira como os nós são organizados na árvore é diferente dependendo do tipo de modelo que você está exibindo.  
  
 Você pode clicar em cada nó para exibir detalhes sobre ele no painel **Detalhes do nó** .  
  
 **Detalhes do nó**  
 Exibe informações detalhadas sobre o conteúdo do nó selecionado. Cada nó armazena suas informações em um formato padronizado, mas o conteúdo e o significado de cada linha da tabela dependem do tipo de modelo ou tipo de nó que você está exibindo. Por exemplo, as informações armazenadas para um nó que representa uma regra em um modelo de associação contêm informações diferentes de um nó que representa uma árvore em um modelo de árvores de decisão.  
  
 Para obter informações sobre como interpretar as informações de um tipo específico de modelo, consulte [Conteúdo do modelo de mineração &#40;Analysis Services – Mineração de Dados&#41;](data-mining/mining-model-content-analysis-services-data-mining.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Algoritmos de mineração de dados &#40;mineração de dados Analysis Services&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visualizadores de modelo de mineração &#40;designer de modelo de mineração de dados&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Consultas de mineração de dados](data-mining/data-mining-queries.md)  
  
  
