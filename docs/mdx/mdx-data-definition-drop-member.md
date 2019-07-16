---
title: Instrução DROP MEMBER (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4e8e38a3ff3f40f44c911a277f99ab9b629c7c87
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038187"
---
# <a name="mdx-data-definition---drop-member"></a>Definição de dados MDX – DROP MEMBER


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
  
  
