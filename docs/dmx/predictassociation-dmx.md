---
title: PredictAssociation (DMX) | Microsoft Docs
ms.custom: ''
ms.date: 09/14/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- PredictAssociation
dev_langs:
- DMX
helpviewer_keywords:
- PredictAssociation function
ms.assetid: 33eb66b5-84c6-449f-aaae-316345bc4ad5
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: e1d65c529dd268560b34d25a1cb767aefe4575db
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="predictassociation-dmx"></a>PredictAssociation (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Prevê associação de membro.  
  
Por exemplo, você pode usar a função PredictAssociation para obter o conjunto de recomendações devido ao estado atual do carrinho de compras de um cliente. 
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
PredictAssociation(<table column reference>, option1, option2, n ...)  
```  
  
## <a name="applies-to"></a>Aplica-se a  
 Algoritmos que contêm tabelas aninhadas previsíveis, incluindo alguns algoritmos de classificação e associação. Algoritmos de classificação que oferecem suporte a tabelas aninhadas incluem o [!INCLUDE[msCoName](../includes/msconame-md.md)] árvores de decisão, [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes, e [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmos de rede Neural.  
  
## <a name="return-type"></a>Tipo de retorno  
 \<expressão de tabela >  
  
## <a name="remarks"></a>Remarks  
 As opções para o **PredictAssociation** função incluem EXCLUDE_NULL, INCLUDE_NULL, INCLUSIVE, EXCLUSIVE (padrão), INPUT_ONLY, INCLUDE_STATISTICS e INCLUDE_NODE_ID.  
  
> [!NOTE]  
>  INCLUSIVE, EXCLUSIVE, INPUT_ONLY e INCLUDE_STATISTICS aplicam-se somente à referência da coluna da tabela, e EXCLUDE_NULL e INCLUDE_NULL aplicam-se apenas à referência da coluna escalar.  
  
 INCLUDE_STATISTICS só retorna **$Probability** e **$AdjustedProbability**.  
  
 Se o parâmetro numérico *n* for especificado, o **PredictAssociation** função retorna os valores de provavelmente n principais com base na probabilidade:  
  
```  
PredictAssociation(colref, [$AdjustedProbability], n)  
```  
  
 Se você incluir **$AdjustedProbability**, a instrução retorna a parte superior *n* valores com base no **$AdjustedProbability**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa o **PredictAssociation** função para retornar os quatro produtos da Adventure Works de bancos de dados que são mais prováveis de serem vendidos juntos.  
  
```  
SELECT  
  PredictAssociation([Association].[v Assoc Seq Line Items],4)  
From  
  [Association]  
```  
O exemplo a seguir demonstra como você pode usar uma tabela aninhada como entrada para a função de previsão, usando a cláusula de forma. A consulta de forma cria um conjunto de linhas com customerId como uma coluna e uma tabela aninhada como uma segunda coluna, que contém a lista de produtos que um cliente já foi colocado. 

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

  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40;DMX&#41; referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funções &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funções de previsão geral &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
