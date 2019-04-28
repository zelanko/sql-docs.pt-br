---
title: Fórmulas de validação cruzada | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: fd1ea582-29a1-4154-8de2-47bab3539b4d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c0f3d10776e661eaa15ed39a141fe06608d8dbde
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62722628"
---
# <a name="cross-validation-formulas"></a>Fórmulas de validação cruzada
  Quando você gera um relatório de validação cruzada, ele contém medidas de exatidão para cada modelo, dependendo do tipo de modelo de mineração (ou seja, o algoritmo que foi usado para criar o modelo), o tipo de dados do atributo previsível, e o valor do atributo previsível, se qualquer.  
  
 Esta seção lista as medidas usadas no relatório de validação cruzada e descrevem o método de cálculo.  
  
 Para obter uma análise das medidas de precisão por tipo de modelo, consulte [Medidas no relatório de validação cruzada](measures-in-the-cross-validation-report.md).  
  
## <a name="formulas-used-for-cross-validation-measures"></a>Fórmulas usadas para medidas de validação cruzada  
  
> [!NOTE]  
>  **Importante:** Estas medidas de precisão são computadas para cada atributo de destino. Para cada atributo, você pode especificar ou omitir um valor de destino. Se um caso no conjunto de dados não tiver nenhum valor para o atributo de destino, o caso será tratado como tendo um valor especial chamado de *valor ausente*. Não são consideradas as linhas com valores ausentes durante a computação da medida de exatidão para um atributo de destino específico. Observe que, como as pontuações são computadas individualmente para cada atributo, se valores estiverem presentes para o atributo de destino, mas ausentes para outros atributos, isso não afetará a pontuação do atributo de destino.  
  
|Measure|Aplica-se a|Implementação|  
|-------------|----------------|--------------------|  
|**Verdadeiro positivo**|Atributo diferenciado, valor especificado|Contagem de casos que atendem estas condições:<br /><br /> Casos que contém o valor de destino.<br /><br /> O modelo previu que o caso contém o valor de destino.|  
|**True Negativo**|Atributo diferenciado, valor especificado|Contagem de casos que atendem estas condições:<br /><br /> Caso não contém o valor de destino.<br /><br /> O modelo previu que o caso não contém o valor de destino.|  
|**Falso positivo**|Atributo diferenciado, valor especificado|Contagem de casos que atendem estas condições:<br /><br /> O valor atual é igual ao valor de destino.<br /><br /> O modelo previu que o caso contém o valor de destino.|  
|**False Negativo**|Atributo diferenciado, valor especificado|Contagem de casos que atendem estas condições:<br /><br /> O valor atual não é igual ao valor de destino.<br /><br /> O modelo previu que o caso não contém o valor de destino.|  
|**Aprovado/reprovado**|Atributo diferenciado, nenhum destino especificado|Contagem de casos que atendem estas condições:<br /><br /> Passa se o estado previsível com a mais alta probabilidade é o mesmo que o estado de entrada e a probabilidade é maior que o valor de **Limite de Estado**.<br /><br /> Caso contrário, falha.|  
|**Comparação de Precisão**|Atributos diferenciados. Valor designado pode ser especificado mas não é necessário.|A probabilidade média de log para todas as linhas com valores para o atributo de destino, em que a probabilidade de log para cada caso é calculada como Log(ActualProbability/MarginalProbability). Para Raiz quadrada do erro médio para todos os casos de partição, dividida pelo número de casos na partição, excluindo as linhas com valores ausentes para o atributo de destino.<br /><br /> A comparação de precisão pode ser um valor positivo ou negativo. Um valor positivo significa um modelo efetivo que supera a previsão aleatória.|  
|**Pontuação de log**|Atributos diferenciados. Valor designado pode ser especificado mas não é necessário.|Log da probabilidade real para cada caso, somado, e depois dividido pelo número de linhas no conjunto de dados de entrada, exceto as linhas com valores ausentes para o atributo de destino.<br /><br /> Como a probabilidade é representada como uma fração decimal, as pontuações de log são sempre números negativos. Uma pontuação próxima de 0 é melhor.|  
|**Probabilidade de Casos**|Cluster|Soma das pontuações de probabilidade de cluster para todos os casos, dividida pelo número de casos na partição, excluindo as linhas com valores ausentes para o atributo de destino.|  
|**Erro de média absoluta**|Atributos contínuos|Soma do erro absoluto para todos os casos na partição, dividida pelo número de casos na partição.|  
|**Erro de raiz quadrada média**|Atributos contínuos|Raiz quadrada do erro de quadrado da média para a partição.|  
|**Erro de quadrado da média de raiz**|Atributos diferenciados. Valor designado pode ser especificado mas não é necessário.|Raiz quadrada da média dos quadrados de complemento da pontuação de probabilidade, dividida pelo número de casos na partição, excluindo as linhas com valores ausentes para o atributo de destino.|  
|**Erro de quadrado da média de raiz**|Atributo diferenciado, nenhum destino especificado.|Raiz quadrada da média dos quadrados de complemento da pontuação de probabilidade, dividida pelo número de casos na partição, excluindo os casos com valores ausentes para o atributo de destino.|  
  
## <a name="see-also"></a>Consulte também  
 [Teste e validação &#40;Mineração de dados&#41;](testing-and-validation-data-mining.md)   
 [Validação cruzada &#40;Analysis Services – Data Mining&#41;](cross-validation-analysis-services-data-mining.md)  
  
  
