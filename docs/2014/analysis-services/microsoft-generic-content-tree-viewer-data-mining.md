---
title: Visualizador de árvore de conteúdo genérica da Microsoft (mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.contentviewer.f1
ms.assetid: 751b4393-f6fd-48c1-bcef-bdca589ce34c
caps.latest.revision: 36
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 85c2cccfe0d5b578c0faa359ca3c276b654aaa21
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37286172"
---
# <a name="microsoft-generic-content-tree-viewer-data-mining"></a>Visualizador de árvore de conteúdo genérica da Microsoft (Mineração de Dados)
  O **Visualizador de Árvore de Conteúdo Genérica da Microsoft** exibe informações detalhadas sobre o conteúdo de um modo de mineração de dados em um formato de tabela HTML padronizado. Esta exibição é útil porque expõe a estrutura subjacente do modelo, assim como detalhes sobre coeficientes, a distribuição de valores e muito mais.  
  
 O conteúdo atual exibido na tabela varia dependendo do algoritmo usado e podem incluir colunas, regras, propriedades, atributos, nós e fórmulas. Para obter mais informações sobre o conteúdo do modelo e sobre como interpretar as informações de cada tipo de modelo, consulte [Conteúdo do modelo de mineração &#40;Analysis Services – Mineração de Dados&#41;](data-mining/mining-model-content-analysis-services-data-mining.md).  
  
 As informações exibidas no visualizador usam uma estrutura comum que é baseada no conjunto de linhas do esquema de conteúdo dos modelos de mineração. O conjunto de linhas do esquema de conteúdo é uma estrutura genérica para armazenar padrões, estatísticas e outros conteúdos de um modelo de mineração de dados. Para obter uma lista das colunas do conjunto de linhas do esquema de mineração de dados para modelos de mineração, consulte [Conjunto de linhas DMSCHEMA_MINING_MODEL_CONTENT](schema-rowsets/data-mining/dmschema-mining-model-content-rowset.md).  
  
## <a name="options"></a>Opções  
 **Legenda de nó (ID exclusiva)**  
 Este painel exibe uma lista de todos os nós no modelo de mineração selecionado. A maneira como os nós são organizados na árvore é diferente dependendo do tipo de modelo que você está exibindo.  
  
 Você pode clicar em cada nó para exibir detalhes sobre ele no painel **Detalhes do nó** .  
  
 **Detalhes do nó**  
 Exibe informações detalhadas sobre o conteúdo do nó selecionado. Cada nó armazena suas informações em um formato padronizado, mas o conteúdo e o significado de cada linha da tabela dependem do tipo de modelo ou tipo de nó que você está exibindo. Por exemplo, as informações armazenadas para um nó que representa uma regra em um modelo de associação contêm informações diferentes de um nó que representa uma árvore em um modelo de árvores de decisão.  
  
 Para obter informações sobre como interpretar as informações de um tipo específico de modelo, consulte [Conteúdo do modelo de mineração &#40;Analysis Services – Mineração de Dados&#41;](data-mining/mining-model-content-analysis-services-data-mining.md).  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmos de mineração de dados &#40;Analysis Services - mineração de dados&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visualizadores do modelo de mineração &#40; Designer do modelo de mineração de dados &#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Consultas de mineração de dados](data-mining/data-mining-queries.md)  
  
  
