---
title: Tipos de dados (mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data types [data mining]
- columns [data mining], data types
- data mining [Analysis Services], data types
ms.assetid: 4af5b7db-790b-459c-b2b4-00f0cf6b5ce4
caps.latest.revision: 46
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 2aab17ed95f87fd64b1bb55ee9ec26ffdfb002ff
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008790"
---
# <a name="data-types-data-mining"></a>Tipos de dados (Mineração de Dados)
  Quando você cria um modelo ou uma estrutura de mineração no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], deve definir os tipos de dados para cada uma das colunas na estrutura de mineração. O tipo de dados informa ao mecanismo de mineração de dados se os dados na fonte de dados são numéricos ou de texto, e como devem ser processados. Por exemplo, se a fonte de dados contiver dados numéricos, você poderá especificar se os números serão tratados como inteiros ou com o uso de casas decimais.  
  
 Cada tipo de dados suporta um ou mais tipos de conteúdo. Ao configurar o tipo de conteúdo, você pode personalizar o modo como os dados na coluna são processados ou calculados no modelo de mineração.  
  
 Por exemplo, se houver dados numéricos em uma coluna, você poderá optar por tratá-los como um tipo de dados numérico ou de texto. Se você escolher o tipo de dados numérico, poderá definir vários tipos de conteúdo diferentes: é possível discretizar os números ou tratá-los como valores contínuos. Para obter uma lista de todos os tipos de conteúdo, consulte [Content Types &#40;Data Mining&#41;](content-types-data-mining.md).  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dá suporte aos seguintes tipos de dados para colunas de estrutura de mineração:  
  
|Tipo de Dados|Tipos de conteúdo com suporte|  
|---------------|-----------------------------|  
|`Text`|Cyclical, Discrete, Discretized, Key Sequence, Ordered, Sequence|  
|`Long`|Continuous, Cyclical, Discrete, Discretized, Key, Key Sequence, Key Time, Ordered, Sequence, Time<br /><br /> Classificados|  
|`Boolean`|Cyclical, Discrete, Ordered|  
|`Double`|Continuous, Cyclical, Discrete, Discretized, Key, Key Sequence, Key Time, Ordered, Sequence, Time<br /><br /> Classificados|  
|`Date`|Continuous, Cyclical, Discrete, Discretized, Key, Key Sequence, Key Time, Ordered|  
  
> [!NOTE]  
>  Os tipos de conteúdo Tempo e Sequência têm suporte apenas por algoritmos de terceiros. Os tipos de conteúdo Cyclical e Ordered têm suporte, mas a maioria dos algoritmos os tratam como valores discretos e não executam processamento especial.  
  
## <a name="specifying-a-data-type"></a>Especificando um tipo de dados  
 Se você criar o modelo de mineração diretamente usando DMX, poderá definir o tipo de dados para cada coluna à medida que definir o modelo, e o Analysis Services criará a estrutura de mineração correspondente com os tipos de dados especificados ao mesmo tempo. Se você criar o modelo ou a estrutura de mineração usando um assistente, o Analysis Services vai sugerir um tipo de dados ou será possível escolher um tipo de dados em uma lista.  
  
## <a name="changing-a-data-type"></a>Alterando um tipo de dados  
 Se você alterar o tipo de dados de uma coluna, sempre terá que reprocessar a estrutura de mineração e qualquer modelo de mineração baseado nessa estrutura. Às vezes, se você alterar o tipo de dados, essa coluna não poderá mais ser usada em um modelo específico. Nesse caso, o Analysis Services gerará um erro quando você reprocessar o modelo ou processará o modelo, mas omitirá essa coluna em particular.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de conteúdo &#40;mineração de dados&#41;](content-types-data-mining.md)   
 [Tipos de conteúdo &#40;DMX&#41;](/sql/dmx/content-types-dmx)   
 [Algoritmos de mineração de dados &#40;Analysis Services – mineração de dados&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [Estruturas de mineração &#40;Analysis Services – mineração de dados&#41;](mining-structures-analysis-services-data-mining.md)   
 [Tipos de dados &#40;DMX&#41;](/sql/dmx/data-types-dmx)   
 [Colunas do modelo de mineração](mining-model-columns.md)   
 [Colunas da estrutura de mineração](mining-structure-columns.md)  
  
  
