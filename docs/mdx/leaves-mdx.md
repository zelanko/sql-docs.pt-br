---
description: Leaves (MDX)
title: Folhas (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7beab859a2953b3eba52e74d97bed5718c59ea90
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387302"
---
# <a name="leaves-mdx"></a>Leaves (MDX)


  Retorna um conjunto composto de todos os atributos (limitado, opcionalmente, aos que pertencem a uma dimensão específica). Para cada atributo x no conjunto retornado, se x for o atributo de granularidade, ou estiver relacionado direta ou indiretamente a esse atributo, a granularidade será definida no atributo x sem afetar a fatia. A **função** Leaves foi projetada para uso dentro de uma instrução Scope ou no lado esquerdo de uma atribuição.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Leaves( [ Dimension_expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Dimension_Expression*  
 Uma linguagem MDX válida que retorna uma dimensão.  
  
## <a name="remarks"></a>Comentários  
 Membros folha são tuplas formadas pela junção cruzada do mais baixo nível de todas as hierarquias de atributo. Os membros calculados são excluídos.  
  
-   Se um nome de dimensão for especificado, **a função** Leave retornará um conjunto que contém os membros folha do atributo de chave para a dimensão especificada.  
  
-   Se a dimensão for associada a vários grupos de medidas, a dimensão da medida no escopo atual será usada.  
  
-   Se um nome de dimensão não for especificado, a função retornará um conjunto que contém os membros folha do cubo inteiro.  
  
    > [!NOTE]  
    >  Se a expressão de dimensão for resolvida em uma hierarquia e o nome exclusivo da hierarquia for igual ao nome exclusivo da dimensão (propriedade de dimensão de cubo HierarchyUniqueNameStyle=ExcludeDimensionName e nome da hierarquia = nome da dimensão), a dimensão será usada.  
  
    > [!IMPORTANT]  
    >  Um erro será gerado se nem todos os atributos tiverem a mesma granularidade nos grupos de medidas do escopo atual.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
