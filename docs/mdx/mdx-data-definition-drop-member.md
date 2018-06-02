---
title: Instrução DROP MEMBER (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5de7a54dd7b6b6ac35a44639c04cc1072117de7b
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579578"
---
# <a name="mdx-data-definition---drop-member"></a>Definição de dados MDX - membro de SOLTAR
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Remove um membro calculado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP MEMBER   
   CURRENTCUBE | Cube_Name  
      .Member_Name   
               [,CURRENTCUBE | Cube_Name.Member_Name ...n]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Name*  
 Uma expressão de cadeia de caracteres válida que fornece um nome de cubo.  
  
 *Member_Identifier*  
 Uma expressão de cadeia de caracteres válida que fornece um nome de membro ou uma chave de membro.  
  
## <a name="see-also"></a>Consulte também  
 [Instrução CREATE MEMBER &#40;MDX&#41;](../mdx/mdx-data-definition-create-member.md)   
 [Instruções de definição de dados MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
