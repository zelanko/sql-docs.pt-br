---
title: Ascendentes (MDX) | Microsoft Docs
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
- ASCENDANTS
dev_langs:
- kbMDX
helpviewer_keywords:
- Ascendants function
ms.assetid: a2baf4a2-7d66-4766-b708-739a3c21b09e
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: a8f2d48317bb6cb0fb5a066348ae1beed8a0f35f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="ascendants-mdx"></a>Ascendants (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Retorna o conjunto dos ascendentes de um membro especificado, inclusive o próprio membro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Ascendants(Member_Expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Uma linguagem MDX válida que retorna um membro.  
  
## <a name="remarks"></a>Remarks  
 O **ascendentes** função retorna todos os ancestrais de um membro do membro até a parte superior da hierarquia de membros; mais especificamente, ele executa um passagem pós-pedido da hierarquia para o membro especificado e, em seguida, retorna todos os membros ascendentes relacionados ao membro, incluindo ele mesmo, em um conjunto. Isso é, em comparação com o [ancestral](../mdx/ancestor-mdx.md) função, que retorna um membro ascendente específico, ou ancestral, em um nível específico.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
