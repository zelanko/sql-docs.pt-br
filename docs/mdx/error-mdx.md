---
title: Erro (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: ERROR
dev_langs: kbMDX
helpviewer_keywords: Error function
ms.assetid: 2caac19b-b297-443e-9299-648ef88a5039
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: f7137691a6532a2c19ce6229846e20b2ed3dce36
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="error-mdx"></a>Função Error (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Identifica um erro, fornecendo uma mensagem de erro específica (opcional).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Error( [ Error_Text ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Error_Text*  
 Uma expressão de cadeia de caracteres válida que contém a mensagem de erro a ser retornada.  
  
## <a name="examples"></a>Exemplos  
 A consulta a seguir mostra como usar o **erro** função dentro de uma medida calculada:  
  
 `WITH MEMBER MEASURES.ERRORDEMO AS ERROR("THIS IS AN ERROR")`  
  
 `SELECT`  
  
 `MEASURES.ERRORDEMO ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
