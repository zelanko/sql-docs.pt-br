---
title: AddCalculatedMembers (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ADDCALCULATEDMEMBERS
dev_langs:
- kbMDX
helpviewer_keywords:
- AddCalculatedMembers function
ms.assetid: c676cf70-7c24-46ea-b88c-d4a389a71d48
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 277489f47a80cbaeda8b9ccd1f2d4ab386b44b22
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="addcalculatedmembers-mdx"></a>AddCalculatedMembers (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna um conjunto gerado, adicionando membros calculados a um conjunto especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
AddCalculatedMembers(Set_Expression)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
## <a name="remarks"></a>Remarks  
 Por padrão, a linguagem MDX exclui membros calculados quando resolve funções de conjunto. O **AddCalculatedMembers** função examina a expressão de conjunto especificada em *Set_Expression,* e inclui membros calculados são irmãos dos membros contidos no escopo dessa expressão de conjunto.  
  
> [!NOTE]  
>  Essa função só pode ser usada com expressões de conjunto de uma dimensão.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir demonstra o uso dessa função.  
  
```  
-- This query returns the calculated members for the cube  
-- by retrieving all members, and then excluding non-calculated members.  
SELECT   
   AddCalculatedMembers(  
      {[Measures].Members}  
      )-[Measures].Members ON COLUMNS  
FROM [Adventure Works]   
```  
  
 O exemplo a seguir retorna o `Measures.[Unit Price]` membro, além de todos os membros calculados no **medidas** dimensão, do **Adventure Works** cubo.  
  
```  
SELECT  
   AddCalculatedMembers({Measures.[Unit Price]}) ON COLUMNS  
FROM   
   [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
