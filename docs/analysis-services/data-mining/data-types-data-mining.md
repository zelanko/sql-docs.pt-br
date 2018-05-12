---
title: Tipos de dados (mineração de dados) | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4b62c9a4ebc9caf9875a1e5b6aef987bf0b4fa8a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="data-types-data-mining"></a>Tipos de dados (Mineração de Dados)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Quando você cria um modelo ou uma estrutura de mineração no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], deve definir os tipos de dados para cada uma das colunas na estrutura de mineração. O tipo de dados informa ao mecanismo de análise se os dados na fonte de dados são numéricos ou de texto, e como devem ser processados. Por exemplo, se a fonte de dados contiver dados numéricos, você poderá especificar se os números serão tratados como inteiros ou com o uso de casas decimais.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dá suporte aos seguintes tipos de dados para colunas de estrutura de mineração:  
  
|Tipo de Dados|Tipos de conteúdo com suporte|  
|---------------|-----------------------------|  
|**Texto**|Cyclical, Discrete, Discretized, Key Sequence, Ordered, Sequence|  
|**Longo**|Continuous, Cyclical, Discrete, Discretized, Key, Key Sequence, Key Time, Ordered, Sequence, Time<br /><br /> Classificados|  
|**Booliano**|Cyclical, Discrete, Ordered|  
|**Double**|Continuous, Cyclical, Discrete, Discretized, Key, Key Sequence, Key Time, Ordered, Sequence, Time<br /><br /> Classificados|  
|**Data**|Continuous, Cyclical, Discrete, Discretized, Key, Key Sequence, Key Time, Ordered|  
  
> [!NOTE]  
>  Os tipos de conteúdo Tempo e Sequência têm suporte apenas por algoritmos de terceiros. Os tipos de conteúdo Cyclical e Ordered têm suporte, mas a maioria dos algoritmos os tratam como valores discretos e não executam processamento especial.  
  
 A tabela também mostra os *tipos de conteúdo* com suporte para cada tipo de dados.  
  
 O tipo de conteúdo é especificado para mineração de dados e permite personalizar o modo como os dados são processados ou calculados no modelo de mineração. Por exemplo, mesmo que a coluna contenha números, convém modelá-las como valores discretos. Se a coluna contiver números, você também poderá especificar que eles sejam compartimentalizados ou discretizados, ou especificar que o modelo trate deles como valores contínuos. Assim, o tipo de conteúdo pode ter um grande efeito no modelo. Para obter uma lista de todos os tipos de conteúdo, consulte [Tipos de conteúdo &#40;Data Mining&#41;](../../analysis-services/data-mining/content-types-data-mining.md).  
  
> [!NOTE]  
>  Em outros sistemas de aprendizado de máquina, você pode encontrar os termos *dados nominais*, *fatores* ou *categorias*, *dados ordinais*ou *dados de sequência*. Em geral, elas correspondem a tipos de conteúdo. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o tipo de dados especifica somente o tipo de valor para o armazenamento, não seu uso no modelo.  
  
## <a name="specifying-a-data-type"></a>Especificando um tipo de dados  
 Se você criar o modelo de mineração diretamente usando DMX, poderá definir o tipo de dados para cada coluna à medida que definir o modelo, e o Analysis Services criará a estrutura de mineração correspondente com os tipos de dados especificados ao mesmo tempo. Se você criar o modelo ou a estrutura de mineração usando um assistente, o Analysis Services vai sugerir um tipo de dados ou será possível escolher um tipo de dados em uma lista.  
  
## <a name="changing-a-data-type"></a>Alterando um tipo de dados  
 Se você alterar o tipo de dados de uma coluna, sempre terá que reprocessar a estrutura de mineração e qualquer modelo de mineração baseado nessa estrutura. Às vezes, se você alterar o tipo de dados, essa coluna não poderá mais ser usada em um modelo específico. Nesse caso, o Analysis Services gerará um erro quando você reprocessar o modelo ou processará o modelo, mas omitirá essa coluna em particular.  
  
## <a name="see-also"></a>Consulte também  
 [Conteúdo tipos & #40; mineração de dados & #41;](../../analysis-services/data-mining/content-types-data-mining.md)   
 [Conteúdo tipos & #40; DMX & #41;](../../dmx/content-types-dmx.md)   
 [Algoritmos de mineração de dados e &#40; Analysis Services – Data Mining e &#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Estruturas de mineração & #40; Analysis Services – mineração de dados & #41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Tipos de dados & #40; DMX & #41;](../../dmx/data-types-dmx.md)   
 [Colunas do modelo de mineração](../../analysis-services/data-mining/mining-model-columns.md)   
 [Colunas de estrutura de mineração](../../analysis-services/data-mining/mining-structure-columns.md)  
  
  
