---
description: Ascendants (MDX)
title: Ascendentes (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: eb485e2785facba4a47647f8a51548e0140b3efb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491462"
---
# <a name="ascendants-mdx"></a>Ascendants (MDX)


  Retorna o conjunto dos ascendentes de um membro especificado, inclusive o próprio membro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Ascendants(Member_Expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Comentários  
 A função **ascendentes** retorna todos os ancestrais de um membro do próprio membro até a parte superior da hierarquia do membro; mais especificamente, ele executa uma passagem de ordem posterior da hierarquia para o membro especificado e, em seguida, retorna todos os membros de ascendentes relacionados ao membro, inclusive em um conjunto. Isso é diferente da função [ancestral](../mdx/ancestor-mdx.md) , que retorna um membro ascendentes específico, ou ancestral, em um nível específico.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna a contagem de pedidos de revendedor para o `[Sales Territory].[Northwest]` membro e todos os ascendentes do membro do cubo **Adventure Works** . A função **ascendentes** constrói o conjunto que inclui o `[Sales Territory].[Northwest]` membro e seu ascendentes para o eixo de linhas.  
  
```  
SELECT  
   Measures.[Reseller Order Count] ON COLUMNS,  
   Order(  
      Ascendants(  
         [Sales Territory].[Northwest]  
      ),  
      DESC  
   ) ON ROWS  
FROM  
   [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
