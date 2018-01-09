---
title: Usando eixos de consulta e Slicer em um exemplo Simple (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- slicer axis
- query axis [MDX]
ms.assetid: 85bcb26f-5971-4153-b334-61f8d8b475b5
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5e3dd069c68623f9f0cc5f4fa90a06ca9a3568e1
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-query-and-slicer-axes---using-axes-in-a-simple-example"></a>Eixo da segmentação de dados - usando eixos em um exemplo Simple e consulta MDX
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]O exemplo simples apresentado neste tópico ilustra os fundamentos de como especificar e usar eixos de consulta e segmentação de dados.  
  
## <a name="the-cube"></a>O cubo  
 Um cubo, chamado CuboTeste, possui duas dimensões simples nomeadas Rota e Tempo. Cada dimensão tem apenas uma hierarquia de usuário, chamadas respectivamente Rota e Tempo. Como as medidas do cubo fazem parte da dimensão Medidas, esse cubo possui três dimensões no total.  
  
## <a name="the-query"></a>A consulta  
 A consulta serve para fornecer uma matriz com a qual a medida Pacotes pode ser comparada por rotas e horas.  
  
 No exemplo de consulta MDX a seguir, as hierarquias Rota e Tempo são os eixos de consulta e a dimensão Medidas é o eixo de slicer. A função [Members](../../../mdx/members-set-mdx.md) indica que a linguagem MDX usará os membros da hierarquia ou do nível para construir um conjunto. O uso da função **Members** significa que você não terá que declarar explicitamente cada membro de uma hierarquia específica ou um nível em uma consulta MDX.  
  
```  
SELECT  
   { Route.nonground.Members } ON COLUMNS,  
   { Time.[1st half].Members } ON ROWS  
FROM TestCube  
WHERE ( [Measures].[Packages] )  
```  
  
## <a name="the-results"></a>O resultado  
 O resultado é uma grade que identifica o valor da medida Pacotes em cada intersecção das dimensões de eixo COLUMNS e ROWS. A tabela a seguir mostra como seria essa grade.  
  
||aérea|marítima|  
|-|---------|---------|  
|1º trimestre|60|50|  
|2º trimestre|45|45|  
  
## <a name="see-also"></a>Consulte Também  
 [Especificando o conteúdo de um eixo de consulta &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md)   
 [Especificando o conteúdo de um eixo da segmentação &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md)  
  
  
