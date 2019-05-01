---
title: Ascendentes (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3122b3aa2f53da69f88e6ffad508f12c8e10da1c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63249815"
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
 O **ascendentes** função retorna todos os ancestrais de um membro do membro até a parte superior da hierarquia do membro; mais especificamente, ele executa uma passagem pós-pedido da hierarquia para o membro especificado e, em seguida, Retorna que todos os membros ascendentes relacionados ao membro, incluindo ele mesmo, em um conjunto. Isso está em contraste com o [ancestral](../mdx/ancestor-mdx.md) função, que retorna um membro ascendente específico, ou ancestral, em um nível específico.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna a contagem de pedidos do revendedor para o `[Sales Territory].[Northwest]` membro e todos os descendentes daquele membro a partir de **Adventure Works** cubo. O **ascendentes** função constrói o conjunto que inclui o `[Sales Territory].[Northwest]` membro e seus ascendentes para o eixo de linhas.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
