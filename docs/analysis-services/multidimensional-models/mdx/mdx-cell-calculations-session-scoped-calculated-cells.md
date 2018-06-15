---
title: Criando no escopo da sessão calculados células | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4ca621d103f294a88fec93dbf6f24d7402279efa
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34023153"
---
# <a name="mdx-cell-calculations---session-scoped-calculated-cells"></a>Cálculos de célula MDX - células calculadas no escopo da sessão
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
    
> [!IMPORTANT]  
>  Esta sintaxe não está mais em uso. Em vez dela, use atribuições MDX. Para obter mais informações sobre atribuições, consulte [O script básico de MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md).  
  
 Para criar células calculadas disponíveis para todas as consultas da mesma sessão, você pode usar a instrução [CREATE CELL CALCULATION](../../../mdx/mdx-data-definition-create-cell-calculation.md) ou a instrução [ALTER CUBE](../../../mdx/mdx-data-definition-alter-cube.md) . Ambas produzem o mesmo resultado.  
  
## <a name="create-cell-calculation-syntax"></a>Sintaxe de CREATE CELL CALCULATION  
  
> [!IMPORTANT]  
>  Esta sintaxe não está mais em uso. Em vez dela, use atribuições MDX. Para obter mais informações sobre atribuições, consulte [O script básico de MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md).  
  
 Use a sintaxe a seguir para usar a instrução CREATE CELL CALCULATION para definir uma célula calculada no escopo da sessão:  
  
```  
CREATE CELL CALCULATION Cube_Expression.<CREATE CELL CALCULATION body clause>  
  
<CREATE CELL CALCULATION body clause> ::=CellCalc_Identifier FOR String_Expression AS 'MDX_Expression'   
   [ <CREATE CELL CALCULATION property clause> [ , <CREATE CELL CALCULATION property clause> ... ] ]  
  
<CREATE CELL CALCULATION property clause> ::=  
   ( CONDITION = 'Logical_Expression' ) |   
   ( DISABLED = { TRUE | FALSE } ) |   
   ( DESCRIPTION =String_Expression ) |   
   ( CALCULATION_PASS_NUMBER = Integer_Expression ) |   
   ( CALCULATION_PASS_DEPTH = Integer_Expression ) |   
   ( SOLVE_ORDER = Integer_Expression ) |   
   ( FORMAT_STRING = String_Expression ) |   
   ( CellProperty_Identifier = Scalar_Expression )  
```  
  
## <a name="alter-cube-syntax"></a>Sintaxe de ALTER CUBE  
  
> [!IMPORTANT]  
>  Esta sintaxe não está mais em uso. Em vez dela, use atribuições MDX. Para obter mais informações sobre atribuições, consulte [O script básico de MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md).  
  
 Use a sintaxe a seguir para usar a instrução ALTER CUBE para definir uma célula calculada no escopo da sessão:  
  
```  
ALTER CUBE Cube_Identifier CREATE CELL CALCULATION  
FOR String_Expression AS 'MDX_Expression'   
   [ <CREATE CELL CALCULATION property clause> [ , <CREATE CELL CALCULATION property clause> ... ] ]  
  
<CREATE CELL CALCULATION property clause> ::=  
   ( CONDITION = 'Logical_Expression' ) |   
   ( DISABLED = { TRUE | FALSE } ) |   
   ( DESCRIPTION =String_Expression ) |   
   ( CALCULATION_PASS_NUMBER = Integer_Expression ) |   
   ( CALCULATION_PASS_DEPTH = Integer_Expression ) |   
   ( SOLVE_ORDER = Integer_Expression ) |   
   ( FORMAT_STRING = String_Expression ) |   
   ( CellProperty_Identifier = Scalar_Expression )  
```  
  
 O valor `String_Expression` contém uma lista de expressões de conjunto MDX ortogonais e unidimensionais, sendo que cada uma deve resolver uma das categorias de conjuntos listadas na tabela a seguir.  
  
|Categoria|Description|  
|--------------|-----------------|  
|Conjunto vazio|Uma expressão de conjunto MDX resolvida em um conjunto vazio. Nesse caso, o escopo da célula calculada é o cubo inteiro.|  
|Conjunto de membro único|Uma expressão de conjunto MDX resolvida em um único membro.|  
|Conjunto de membros do nível|Uma expressão de conjunto MDX resolvida nos membros de um mesmo nível. Um exemplo disso é a função MDX *Level_Expression*.**Members** . Para incluir membros calculados, use a função MDX *Level_Expression*.**AllMembers** .<br /><br /> Para obter mais informações, consulte [AllMembers &#40;MDX&#41;](../../../mdx/allmembers-mdx.md).|  
|Conjunto de descendentes|Uma expressão de conjunto MDX resolvida nos descendentes de um membro especificado. Um exemplo disso é a função MDX **Descendants**(*Member_Expression*, *Level_Expresion*, *Desc_Flag*).<br /><br /> Para obter mais informações, consulte [Descendants &#40;MDX&#41;](../../../mdx/descendants-mdx.md).|  
  
## <a name="see-also"></a>Consulte também  
 [Criando cálculos de célula em MDX & #40; MDX & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-build-cell-calculations.md)  
  
  
