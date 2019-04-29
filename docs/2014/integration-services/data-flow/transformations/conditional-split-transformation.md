---
title: Transformação Divisão Condicional | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.conditionalsplittrans.f1
helpviewer_keywords:
- Conditional Split transformation
- route rows to different outputs [Integration Services]
ms.assetid: 3f8b5825-226f-413c-ba8f-0bb931ca3770
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: dcfbbac9eacc96384a723088cf8f20cc939bdc48
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62900820"
---
# <a name="conditional-split-transformation"></a>Transformação Divisão Condicional
  A transformação Divisão Condicional pode rotear linhas de dados para saídas diferentes, dependendo do conteúdo dos dados. A implementação da transformação Divisão Condicional é semelhante a uma estrutura de decisão CASE em uma linguagem de programação. A transformação avalia expressões e, com base nos resultados, direciona a linha de dados para a saída especificada. Essa transformação também fornece uma saída padrão, de forma que, se uma linha não corresponder a nenhuma expressão, ela será direcionada para a saída padrão.  
  
## <a name="configuration-of-the-conditional-split-transformation"></a>Configuração da transformação Divisão Condicional  
 É possível configurar a transformação Divisão Condicional do seguinte modo:  
  
-   Para cada condição a ser testada pela transformação, forneça uma expressão a ser avaliada pelo Booleano.  
  
-   Especifique a ordem na qual as condições são avaliadas. A ordem é importante, pois uma linha é enviada à saída correspondente para a primeira condição avaliada como true.  
  
-   Especifique a saída padrão para transformação. É necessário especificar uma saída padrão para a transformação.  
  
 Cada linha de entrada pode ser enviada a apenas uma saída, sendo esta saída a primeira condição avaliada como true. Por exemplo, as condições a seguir direcionam todas as linhas da coluna **FirstName** que começam com a letra *A* para uma saída, as linhas que começam com a letra *B* para uma saída diferente e todas as outras linhas para uma saída padrão.  
  
 Saída 1  
  
 `SUBSTRING(FirstName,1,1) == "A"`  
  
 Saída 2  
  
 `SUBSTRING(FirstName,1,1) == "B"`  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] inclui funções e operadores que podem ser usados para criar as expressões que avaliam dados de entrada e direcionar dados de saída. Para obter mais informações, consulte [Expressões do Integration Services &#40;SSIS&#41;](../../expressions/integration-services-ssis-expressions.md).  
  
 A transformação Divisão Condicional inclui a propriedade personalizada `FriendlyExpression`. Essa propriedade pode ser atualizada por uma expressão de propriedade quando o pacote é carregado. Para obter mais informações, consulte [Usar expressões de propriedade em pacotes](../../expressions/use-property-expressions-in-packages.md) e [Propriedades personalizadas da transformação](transformation-custom-properties.md).  
  
 Esta transformação tem uma entrada, uma ou mais saídas e uma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que você quer definir na caixa de diálogo **Editor de Transformação Divisão Condicional** , consulte [Editor de Transformação Divisão Condicional](../../conditional-split-transformation-editor.md).  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../../common-properties.md)  
  
-   [Propriedades personalizadas de Transformação](transformation-custom-properties.md)  
  
 Para obter mais informações sobre como definir propriedades, clique em um dos seguintes tópicos:  
  
-   [Dividir um conjunto de dados por meio da transformação Divisão Condicional](conditional-split-transformation.md)  
  
-   [Definir as propriedades de um componente de fluxo de dados](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [Dividir um conjunto de dados por meio da transformação Divisão Condicional](conditional-split-transformation.md)  
  
## <a name="see-also"></a>Consulte também  
 [Fluxo de Dados](../data-flow.md)   
 [Transformações do Integration Services](integration-services-transformations.md)  
  
  
