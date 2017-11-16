---
title: "Procurar um modelo usando o Visualizador de árvore de conteúdo genérica da Microsoft | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining model content, viewing
ms.assetid: 4a5f7c51-c704-4214-b05d-21cf735e6d96
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: dcb5c01581dd9d42e7504dc00f514544479b27fc
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

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
  
 Para obter mais informações sobre o significado geral dos termos usados no conteúdo do modelo de mineração, consulte [Conteúdo do modelo de mineração  40Analysis Services – Mineração de dados&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md). O tópico também contém links para informações sobre o conteúdo do modelo de mineração para tipos específicos de modelos. Cada tipo de modelo de mineração contém informações altamente específicas do algoritmo e os padrões encontrados nos dados; portanto, é recomendável consultar o tópico de referência técnica para cada tipo de modelo para compreender bem cada tipo de modelo.  
  
## <a name="querying-mining-model-content"></a>Consultando o conteúdo do modelo de mineração  
 As mesmas informações fornecidas pelo Visualizador de Árvore de Conteúdo Genéricas da [!INCLUDE[msCoName](../../includes/msconame-md.md)] também estão disponíveis através da consulta ao modelo de mineração. Você pode criar consultas no conteúdo do modelo de mineração usando instruções DMX (Data Mining Extensions). Por exemplo, no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], você pode realizar uma consulta de conteúdo executando a seguinte instrução DMX:  
  
```  
SELECT * FROM [<mining model name>].CONTENT  
```  
  
 Para obter mais informações, consulte [Consultas de mineração de dados](../../analysis-services/data-mining/data-mining-queries.md).  
  
## <a name="see-also"></a>Consulte também  
 [Visualizador de árvore de conteúdo genérica da Microsoft &#40;Mineração de dados&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c)   
 [Algoritmos de mineração de dados &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)  
  
  

