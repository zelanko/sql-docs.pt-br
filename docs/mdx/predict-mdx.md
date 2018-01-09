---
title: Prever (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: PREDICT
dev_langs: kbMDX
helpviewer_keywords: Predict function
ms.assetid: a82f3edd-249b-4559-98d3-6e10d81a095d
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: d7266e462167dcae27a30b033c368f910b6dfc0f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="predict-mdx"></a>Predict (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

    
> [!CAUTION]  
>  Esta função está no processo de ser removida devido a inconsistências internas.  
>   
>  Analise a seção de exemplo para obter uma solução alternativa usando uma expressão DMX.  
  
 Retorna um valor de uma expressão numérica avaliada em função sobre um modelo de mineração de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Predict(Mining_Model_Name,String_Expression)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Mining_Model_Name*  
 Uma expressão de cadeia de caracteres válida que representa o nome de um modelo de mineração.  
  
 *String_Expression*  
 Uma expressão de cadeia de caracteres válida que avalia uma expressão DMX válida para o modelo de mineração especificado.  
  
## <a name="remarks"></a>Remarks  
 O **prever** função avalia a expressão de cadeia de caracteres especificada dentro do contexto do modelo de mineração especificado.  
  
 A sintaxe e as funções de mineração de dados são documentadas na refereência do DMS (Data Mining Expressions).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir prevê o nome do cluster e a distância dele em relação a um cliente específico usando o modelo de mineração Clusters de Clientes:  
  
```  
WITH MEMBER MEASURES.CLNAME AS   
PREDICT("Customer Clusters", "Cluster()")  
MEMBER MEASURES.CLDISTANCE AS   
PREDICT("Customer Clusters", "ClusterDistance(Cluster())")  
SELECT {MEASURES.CLNAME, MEASURES.CLDISTANCE} ON 0   
FROM [Adventure Works]  
WHERE([Customer].[Customer Geography].[Customer].&[12012])  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
