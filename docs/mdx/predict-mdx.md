---
description: Predict (MDX)
title: Predict (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 97d65cec90020b14bba242b4183ada8f02c2c368
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471668"
---
# <a name="predict-mdx"></a>Predict (MDX)


    
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
  
## <a name="remarks"></a>Comentários  
 A função **Predict** avalia a expressão de cadeia de caracteres especificada no contexto do modelo de mineração especificado.  
  
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
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
