---
title: Deixa (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: LEAVES
dev_langs: kbMDX
helpviewer_keywords: Leaves function
ms.assetid: 09f908aa-1b2d-4af9-8c8d-c023915241b2
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 1920799f04128a692a333e80ac5024cbdbae564a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="leaves-mdx"></a>Leaves (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna um conjunto composto de todos os atributos (limitado, opcionalmente, aos que pertencem a uma dimensão específica). Para cada atributo x no conjunto retornado, se x for o atributo de granularidade, ou estiver relacionado direta ou indiretamente a esse atributo, a granularidade será definida no atributo x sem afetar a fatia. O **deixa** função é projetada para uso dentro de uma instrução SCOPE ou no lado esquerdo de uma atribuição.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Leaves( [ Dimension_expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Dimension_Expression*  
 Uma linguagem MDX válida que retorna uma dimensão.  
  
## <a name="remarks"></a>Comentários  
 Membros folha são tuplas formadas pela junção cruzada do mais baixo nível de todas as hierarquias de atributo. Os membros calculados são excluídos.  
  
-   Se um nome de dimensão for especificado, o **deixa** função retorna um conjunto que contém os membros folha do atributo de chave para a dimensão especificada.  
  
-   Se a dimensão for associada a vários grupos de medidas, a dimensão da medida no escopo atual será usada.  
  
-   Se um nome de dimensão não for especificado, a função retornará um conjunto que contém os membros folha do cubo inteiro.  
  
    > [!NOTE]  
    >  Se a expressão de dimensão for resolvida em uma hierarquia e o nome exclusivo da hierarquia for igual ao nome exclusivo da dimensão (propriedade de dimensão de cubo HierarchyUniqueNameStyle=ExcludeDimensionName e nome da hierarquia = nome da dimensão), a dimensão será usada.  
  
    > [!IMPORTANT]  
    >  Um erro será gerado se nem todos os atributos tiverem a mesma granularidade nos grupos de medidas do escopo atual.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
