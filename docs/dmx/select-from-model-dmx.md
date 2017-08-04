---
title: SELECT FROM &lt;modelo&gt; (DMX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SELECT
- FROM
dev_langs:
- DMX
helpviewer_keywords:
- empty prediction joins [DMX]
- SELECT FROM <model> statement
ms.assetid: dc5b9a01-e308-4ee8-84fc-ba4b991c60aa
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c51d5d3f3a5a1c8e9b94f72367739d592f1918c8
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="select-from-ltmodelgt-dmx"></a>SELECT FROM &lt;modelo&gt; (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 As colunas de *lista de expressões* deve ser definida como previsão ou somente previsão ou relacionados a uma coluna previsível.  
  
## <a name="naive-bayes-example"></a>Exemplo de Naive Bayes  
 O exemplo a seguir executa uma junção de previsão vazia na coluna Comprador de bicicleta, retornando o estado mais provável do modelo de mineração Naive Bayes de TM.  
  
```  
SELECT ([Bike Buyer]) FROM [TM_Naive_Bayes]  
```  
  
## <a name="time-series-example"></a>Exemplo de série temporal  
 O exemplo a seguir realiza uma previsão na coluna Valor do modelo Previsão, retornando as quatro etapas de tempo seguintes. A coluna Região modelo combina modelos de bicicleta e regiões em um único identificador. A consulta usa o [PredictTimeSeries &#40; DMX &#41;](../dmx/predicttimeseries-dmx.md) função para executar a previsão.  
  
```  
SELECT [Model Region], PredictTimeSeries(Amount, 4)   
FROM Forecasting  
```  
  
## <a name="see-also"></a>Consulte também  
 [SELECIONAR &#40; DMX &#41;](../dmx/select-dmx.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Instruções de definição de dados](../dmx/dmx-statements-data-definition.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Instruções de manipulação de dados](../dmx/dmx-statements-data-manipulation.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

