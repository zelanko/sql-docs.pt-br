---
title: Transformação Amostragem Percentual | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.percentagesamplingtrans.f1
helpviewer_keywords:
- testing mining models
- sampling seeds [Integration Services]
- data mining [Analysis Services], sample data sets
- Percentage Sampling transformation
- sample data sets [Integration Services]
- datasets [Integration Services], sample
- training mining models
ms.assetid: 59767e52-f732-4b3f-8602-be50d0a64ef2
caps.latest.revision: 46
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4fcd0b5154175ec74f86ecaea4ad96439b7ea8b8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37296906"
---
# <a name="percentage-sampling-transformation"></a>transformação Amostragem Percentual
  A transformação Amostragem Percentual cria um conjunto de dados de exemplo, selecionando um percentual das linhas de entrada da transformação. O conjunto de dados de exemplo é uma seleção aleatória das linhas da entrada da transformação, para que o exemplo resultante seja representativo da entrada.  
  
> [!NOTE]  
>  Além do percentual especificado, a transformação Amostragem Percentual utiliza um algoritmo para determinar se uma linha pode ser incluída na saída de exemplo. Isso significa que o número de linhas na saída de exemplo pode não refletir exatamente o percentual especificado. Por exemplo, ao especificar 10% para um conjunto de dados de entrada com 25.000 linhas, é possível que não seja possível gerar uma amostra com 2.500 linhas. A amostra pode ter algumas linhas a menos ou a mais.  
  
 A transformação Amostragem Percentual é particularmente útil para mineração de dados. Utilizando-se essa transformação, você pode dividir aleatoriamente um conjunto de dados em dois: um para treinar o modelo de mineração de dados e o outro para testá-lo.  
  
 A transformação Amostragem Percentual também é útil para criar conjuntos de dados de exemplo para desenvolvimento de pacote. Aplicando-se a transformação Amostragem Percentual a um fluxo de dados, você pode reduzir de modo uniforme o tamanho do conjunto de dados, preservando as características de seus dados. O pacote de teste pode ser então executado mais rapidamente, pois ele usa um conjunto de dados pequeno, porém representativo.  
  
## <a name="configuration-the-percentage-sampling-transformation"></a>Configuração da transformação Amostragem Percentual  
 Você pode especificar uma amostragem da semente para modificar o comportamento do gerador de números aleatórios que a transformação utiliza para selecionar linhas. Se a mesma amostragem da semente for utilizada, a transformação sempre criará a mesma saída de exemplo. Se nenhuma semente for especificada, a transformação usará a contagem de tiques do sistema operacional para criar o número aleatório. Portanto, você pode optar por utilizar uma semente padrão quando quiser verificar os resultados da transformação durante o desenvolvimento e teste de um pacote e, em seguida, fazer a alteração para utilizar uma semente aleatória quando o pacote for colocado em produção.  
  
 Essa transformação é semelhante à transformação Amostragem de Linhas, que cria um conjunto dados de exemplo, selecionando um número especificado de linhas de entrada. Para obter mais informações, consulte [Row Sampling Transformation](row-sampling-transformation.md).  
  
 A transformação Amostragem Percentual inclui a propriedade personalizada `SamplingValue`. Essa propriedade pode ser atualizada por uma expressão de propriedade quando o pacote é carregado. Para obter mais informações, consulte [Expressões do Integration Services &#40;SSIS&#41;](../../expressions/integration-services-ssis-expressions.md), [Usar expressões de propriedade em pacotes](../../expressions/use-property-expressions-in-packages.md) e [Propriedades personalizadas da transformação](transformation-custom-properties.md).  
  
 A transformação tem uma entrada e duas saídas. Não dá suporte a uma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Transformação Amostragem Percentual** , consulte [Percentage Sampling Transformation Editor](../../percentage-sampling-transformation-editor.md).  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../../common-properties.md)  
  
-   [Propriedades personalizadas de Transformação](transformation-custom-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](../set-the-properties-of-a-data-flow-component.md).  
  
  
