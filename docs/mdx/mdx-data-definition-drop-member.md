---
description: Definição de dados MDX – DROP MEMBER
title: Instrução DROP MEMBER (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f71232997c24a1bdca9a1294a804e8b30660d704
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483849"
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
  
## <a name="see-also"></a>Consulte Também  
 [Instrução CREATE MEMBER &#40;MDX&#41;](../mdx/mdx-data-definition-create-member.md)   
 [Instruções de definição de dados MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
