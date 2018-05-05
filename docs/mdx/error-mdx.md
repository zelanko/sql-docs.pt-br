---
title: Erro (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ERROR
dev_langs:
- kbMDX
helpviewer_keywords:
- Error function
ms.assetid: 2caac19b-b297-443e-9299-648ef88a5039
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 11759b5793cad582ec0639aef1d05389e3117ad7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
 [Referência de função MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
