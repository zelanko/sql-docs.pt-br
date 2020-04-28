---
title: PredictAssociation (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ea0a9915e062d7b6f15b63e18976e88cc339202d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "76939503"
---
# <a name="predictassociation-dmx"></a>PredictAssociation (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Prevê associação de membro.  
  
Por exemplo, você pode usar a função PredictAssociation para obter o conjunto de recomendações dadas o estado atual da cesta de compras de um cliente. 
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
PredictAssociation(<table column reference>, option1, option2, n ...)  
```  
  
## <a name="applies-to"></a>Aplica-se A  
 Algoritmos que contêm tabelas aninhadas previsíveis, incluindo associação e alguns algoritmos de classificação. Os algoritmos de classificação que dão suporte [!INCLUDE[msCoName](../includes/msconame-md.md)] a tabelas aninhadas incluem as árvores de decisão, [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes e [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmos de rede neural.  
  
## <a name="return-type"></a>Tipo de retorno  
 \<> de expressão de tabela  
  
## <a name="remarks"></a>Comentários  
 As opções para a função **PredictAssociation** incluem EXCLUDE_NULL, INCLUDE_NULL, inclusivo, exclusivo (padrão), INPUT_ONLY, INCLUDE_STATISTICS e INCLUDE_NODE_ID.  
  
> [!NOTE]  
>  INCLUSIVE, EXCLUSIVE, INPUT_ONLY e INCLUDE_STATISTICS aplicam-se somente à referência da coluna da tabela, e EXCLUDE_NULL e INCLUDE_NULL aplicam-se apenas à referência da coluna escalar.  
  
 INCLUDE_STATISTICS retorna somente **$Probability** e **$AdjustedProbability**.  
  
 Se o parâmetro numérico *n* for especificado, a função **PredictAssociation** retornará os n maiores valores mais prováveis com base na probabilidade:  
  
```  
PredictAssociation(colref, [$AdjustedProbability], n)  
```  
  
 Se você incluir **$AdjustedProbability**, a instrução retornará os *n* valores principais com base na **$AdjustedProbability**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa a função **PredictAssociation** para retornar os quatro produtos no banco de dados Adventure Works que têm mais probabilidade de serem vendidos juntos.  
  
```  
SELECT  
  PredictAssociation([Association].[v Assoc Seq Line Items],4)  
From  
  [Association]  
```  
O exemplo a seguir demonstra como você pode usar uma tabela aninhada como entrada para a função de previsão, usando a cláusula SHAPE. A consulta de forma cria um conjunto de linhas com customerId como uma coluna e uma tabela aninhada como uma segunda coluna, que contém a lista de produtos que um cliente já colocou. 

~~~~
SELECT T.[CustomerId], PredictAssociation(MyNestedTable, 5) // returns top 5 associated items
FROM My Model
PREDICTION JOIN
SHAPE {
    OPENQUERY([Adventure Works DW],'SELECT CustomerID, OrderNumber
    FROM vAssocSeqOrders ORDER BY OrderNumber')
} APPEND (
    {OPENQUERY([Adventure Works DW],'SELECT OrderNumber, model FROM 
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}
  RELATE OrderNumber to OrderNumber) AS T
~~~~  

  
## <a name="see-also"></a>Consulte Também  
 [Referência de função&#41; DMX &#40;extensões de mineração de dados](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funções &#40;&#41;DMX](../dmx/functions-dmx.md)   
 [Funções de previsão gerais &#40;&#41;DMX](../dmx/general-prediction-functions-dmx.md)  
  
  
