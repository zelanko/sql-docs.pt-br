---
title: SELECT FROM &lt;modelo&gt; (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5611ce3da4f12bca5cb271cabe8af3e149dcbf35
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67928320"
---
# <a name="select-from-ltmodelgt-dmx"></a>SELECT FROM &lt;modelo&gt; (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Executa uma junção de previsão vazia, enquanto retornando o valor ou valores mais prováveis para as colunas especificadas. Só o conteúdo do modelo de mineração é usado para criar a previsão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SELECT <expression list> [TOP <n>] FROM <model>   
[WHERE <condition list>]   
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *lista de expressões*  
 Lista separada por vírgulas, de expressões ou de colunas de previsão ou somente previsão.  
  
 *n*  
 Opcional. Um inteiro que especifica quantas linhas serão retornadas.  
  
 *modelo*  
 Identificador de modelo.  
  
 *lista de condições*  
 Opcional. Condições para restringir os valores retornados da lista de colunas.  
  
 *Expressão*  
 Opcional. Uma expressão que retorna um valor escalar.  
  
## <a name="remarks"></a>Comentários  
 As colunas na *lista de expressões* deve ser definido como previsão ou somente previsão ou relacionados a uma coluna previsível.  
  
## <a name="naive-bayes-example"></a>Exemplo de Naive Bayes  
 O exemplo a seguir executa uma junção de previsão vazia na coluna Comprador de bicicleta, retornando o estado mais provável do modelo de mineração Naive Bayes de TM.  
  
```  
SELECT ([Bike Buyer]) FROM [TM_Naive_Bayes]  
```  
  
## <a name="time-series-example"></a>Exemplo de série temporal  
 O exemplo a seguir realiza uma previsão na coluna Valor do modelo Previsão, retornando as quatro etapas de tempo seguintes. A coluna Região modelo combina modelos de bicicleta e regiões em um único identificador. A consulta usa o [PredictTimeSeries &#40;DMX&#41; ](../dmx/predicttimeseries-dmx.md) função para realizar uma previsão.  
  
```  
SELECT [Model Region], PredictTimeSeries(Amount, 4)   
FROM Forecasting  
```  
  
## <a name="see-also"></a>Consulte também  
 [SELECT &#40;DMX&#41;](../dmx/select-dmx.md)   
 [Extensões de mineração de dados &#40;DMX&#41; instruções de definição de dados](../dmx/dmx-statements-data-definition.md)   
 [Extensões de mineração de dados &#40;DMX&#41; instruções de manipulação de dados](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instruções de DMX &#40extensões de Mineração de Dados&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
