---
title: "Instrução DROP ACTION (MDX) | Microsoft Docs"
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
f1_keywords:
- DROP
- DROP ACTION
- Action
- DROP_ACTION
dev_langs: kbMDX
helpviewer_keywords:
- DROP ACTION statement
- deleting actions
- removing actions
- actions [MDX]
- dropping actions
ms.assetid: 74b3cfee-dea8-4968-a54c-1754d52ee1bd
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: da43adf7916807db6548f2f5acf86e4be5f5fb05
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="mdx-data-definition---drop-action"></a>Definição de dados MDX - ação de SOLTAR
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Exclui uma ação especificada de um cubo especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP ACTION CURRENTCUBE | Cube_Name  
   .Action_Name   
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Name*  
 Uma expressão de cadeia de caracteres válida que fornece o nome do cubo.  
  
 *Action_Name*  
 Uma expressão de cadeia de caracteres válida que fornece o nome da ação que está sendo descartada.  
  
## <a name="see-also"></a>Consulte também  
 [Criar ação instrução &#40; MDX &#41;](../mdx/mdx-data-definition-create-action.md)   
 [Instruções de definição de dados MDX &#40; MDX &#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
