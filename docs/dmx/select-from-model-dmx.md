---
title: SELECIONAR do &lt; modelo &gt; (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 43a7157c5ec7889b2f8cb7018423d909f3db3cb7
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970511"
---
# <a name="select-from-ltmodelgt-dmx"></a>SELECIONAR do &lt; modelo &gt; (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

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
  
 *expressão*  
 Opcional. Uma expressão que retorna um valor escalar.  
  
## <a name="remarks"></a>Comentários  
 As colunas na *lista de expressões* devem ser definidas como Predict ou Predict somente, ou relacionadas a uma coluna previsível.  
  
## <a name="naive-bayes-example"></a>Exemplo de Naive Bayes  
 O exemplo a seguir executa uma junção de previsão vazia na coluna Comprador de bicicleta, retornando o estado mais provável do modelo de mineração Naive Bayes de TM.  
  
```  
SELECT ([Bike Buyer]) FROM [TM_Naive_Bayes]  
```  
  
## <a name="time-series-example"></a>Exemplo de série temporal  
 O exemplo a seguir realiza uma previsão na coluna Valor do modelo Previsão, retornando as quatro etapas de tempo seguintes. A coluna Região modelo combina modelos de bicicleta e regiões em um único identificador. A consulta usa a função [PredictTimeSeries &#40;DMX&#41;](../dmx/predicttimeseries-dmx.md) para executar a previsão.  
  
```  
SELECT [Model Region], PredictTimeSeries(Amount, 4)   
FROM Forecasting  
```  
  
## <a name="see-also"></a>Consulte Também  
 [SELECIONAR&#41;&#40;DMX](../dmx/select-dmx.md)   
 [&#40;&#41; instruções de definição de dados DMX de extensões de mineração de dados](../dmx/dmx-statements-data-definition.md)   
 [&#40;instruções de manipulação de dados do DMX&#41; extensões do Data Mining](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instruções de DMX &#40extensões de Mineração de Dados&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
