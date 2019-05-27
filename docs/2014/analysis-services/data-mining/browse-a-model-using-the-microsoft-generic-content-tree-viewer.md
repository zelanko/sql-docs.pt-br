---
title: Procurar um modelo usando o Visualizador de árvore de conteúdo genérica da Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining model content, viewing
ms.assetid: 4a5f7c51-c704-4214-b05d-21cf735e6d96
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bb080721ccb3e5b5aef190eda3d1088df09762c0
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66086064"
---
# <a name="browse-a-model-using-the-microsoft-generic-content-tree-viewer"></a>Procurar um modelo usando o Visualizador de Árvore de Conteúdo Genérica da Microsoft
  O Visualizador de Conteúdo do Modelo de Mineração Genérico da [!INCLUDE[msCoName](../../includes/msconame-md.md)] fornece informações detalhadas sobre os padrões encontrados pelo algoritmos de mineração e também fornece acesso a várias estatísticas geradas durante o processo de análise. A quantidade e o tipo de informação dependem do algoritmo usado, mas podem incluir as seguintes categorias:  
  
-   Segmentos de dados e suas características.  
  
-   Estatísticas descritivas sobre cada grupo ou sobre o conjunto de dados inteiro.  
  
-   O número de ramificações ou nós filho de uma árvore.  
  
-   Cálculos, como variância e média, para um cluster ou um conjunto de dados inteiro.  
  
 Exibir essas informações pode ajudar a entender melhor os resultados da análise. Você também pode identificar maneiras de ajustar e, em seguida, treinar novamente seu modelo. Ou pode decidir fazer um novo treinamento usando um outro algoritmo.  
  
## <a name="viewing-mining-model-content"></a>Exibindo conteúdo do modelo de mineração  
 O Visualizador de Conteúdo Genérico da [!INCLUDE[msCoName](../../includes/msconame-md.md)] exibe as colunas, as regras, as propriedades, os atributos, os nós e outros conteúdos no *conjunto de linhas de esquema de conteúdo* do modelo de mineração. O conjunto de linhas de esquema de conteúdo é uma estrutura genérica de apresentação de informações detalhadas sobre o conteúdo de um modelo de mineração de dados.  
  
 Estas informações detalhadas estão contidas em uma tabela HTML que representa os patterns, clusters ou árvores no modelo como nós. Você pode clicar em cada nó e expandi-lo para ver mais detalhes, como as fórmulas ou a contagem de valores distintos para um atributo numérico. Também pode explorar as relações filho-pai entre os nós.  
  
 Para obter mais informações sobre o significado geral dos termos usados no conteúdo do modelo de mineração, consulte [Conteúdo do modelo de mineração  40Analysis Services – Mineração de dados&#41;](mining-model-content-analysis-services-data-mining.md). O tópico também contém links para informações sobre o conteúdo do modelo de mineração para tipos específicos de modelos. Cada tipo de modelo de mineração contém informações altamente específicas do algoritmo e os padrões encontrados nos dados; portanto, é recomendável consultar o tópico de referência técnica para cada tipo de modelo para compreender bem cada tipo de modelo.  
  
## <a name="querying-mining-model-content"></a>Consultando o conteúdo do modelo de mineração  
 As mesmas informações fornecidas pelo Visualizador de Árvore de Conteúdo Genéricas da [!INCLUDE[msCoName](../../includes/msconame-md.md)] também estão disponíveis através da consulta ao modelo de mineração. Você pode criar consultas no conteúdo do modelo de mineração usando instruções DMX (Data Mining Extensions). Por exemplo, no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], você pode realizar uma consulta de conteúdo executando a seguinte instrução DMX:  
  
```  
SELECT * FROM [<mining model name>].CONTENT  
```  
  
 Para obter mais informações, consulte [Consultas de mineração de dados](data-mining-queries.md).  
  
## <a name="see-also"></a>Consulte também  
 [Visualizador de árvore de conteúdo genérica da Microsoft &#40;Mineração de dados&#41;](../microsoft-generic-content-tree-viewer-data-mining.md)   
 [Algoritmos de mineração de dados &#40;Analysis Services – Data Mining&#41;](data-mining-algorithms-analysis-services-data-mining.md)  
  
  
