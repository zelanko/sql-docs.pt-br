---
title: Prever (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PREDICT
dev_langs:
- kbMDX
helpviewer_keywords:
- Predict function
ms.assetid: a82f3edd-249b-4559-98d3-6e10d81a095d
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 7bec1c96bd70b9b75c3a8c212cf1f6c04c27c73e
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="predict-mdx"></a>Predict (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
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
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

