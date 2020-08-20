---
description: Definição de dados MDX – CREATE CELL CALCULATION
title: Instrução CREATE CELL CALCULAtion (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5080e6bfa0f7a0ac942c3c5aa65bd1883b3050ee
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494869"
---
# <a name="mdx-data-definition---create-cell-calculation"></a>Definição de dados MDX – CREATE CELL CALCULATION


  Cria um cálculo que avalia uma expressão MDX em um conjunto especificado de tuplas dentro de um cubo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
[WITH <CELL CALCULATION clause> Calculation_Name  
   [,WITH <CELL CALCULATION clause> Calculation_Name...n]  
CREATE CELL CALCULATION CURRENTCUBE | Cube_Name.Calculation_Name   
  
<CELL CALCULATION clause> ::=  
   FOR Set_Expression AS 'MDX_Expression'   
      [ [ CONDITION = 'Logical_Expression' ]   
    | [ DISABLED = { TRUE | FALSE } ]   
    | [ DESCRIPTION =String ]   
    | [ CALCULATION_PASS_NUMBER = Integer]   
    | [ CALCULATION_PASS_DEPTH = Integer]   
    | [ SOLVE_ORDER = Integer]   
    | [ Calculation_Name= Scalar_Expression ], ...n]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Name*  
 Uma cadeia de caracteres válida que fornece um nome de cubo.  
  
 *Calculation_Name*  
 Uma cadeia de caracteres válida que fornece um nome de cálculo de célula.  
  
 *Set_Expression*  
 Uma linguagem MDX válida que retorna um conjunto.  
  
 *Cadeia de caracteres*  
 Um valor de cadeia de caracteres válido.  
  
 *MDX_Expression*  
 Uma expressão MDX válida.  
  
 *Logical_Expression*  
 Uma expressão lógica MDX válida.  
  
 *Inteiro*  
 Um valor inteiro válido.  
  
 *Calculation_Name*  
 Uma cadeia de caracteres válida que fornece o nome de uma propriedade de cálculo de célula.  
  
 *Scalar_Expression*  
 Uma expressão escalar MDX válida.  
  
## <a name="remarks"></a>Comentários  
 Ao usar células calculadas, o aplicativo cliente pode especificar um valor de acúmulo para um conjunto de células específico, em vez de um conjunto inteiro de células como no caso de uma fórmula de acúmulo ou de um membro calculado. Por exemplo, é possível especificar que qualquer célula do conjunto definido por `{[Canada],[Time].[2000]}` pode conter um valor definido por uma fórmula. Qualquer outra célula que não está contida nesse conjunto é calculada normalmente.  
  
> [!NOTE]  
>  A forma de Backus-Naur (BNF) de `{*(<comment> | <whitespace> | <newline>)}` será analisada como `{*}` para fins de compatibilidade com versões anteriores.  
  
## <a name="see-also"></a>Consulte Também  
 [Criando células calculadas no escopo da sessão](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-cell-calculations-session-scoped-calculated-cells)   
 [Criando cálculos de célula com escopo de consulta &#40;&#41;MDX ](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-cell-calculations-query-scoped-cell-calculations)   
 [Criando cálculos de célula em MDX &#40;MDX&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-cell-calculations-build-cell-calculations)   
 [Usando propriedades de célula &#40;MDX&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-cell-properties-using-cell-properties)   
 [FORMAT_STRING conteúdo &#40;MDX&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-cell-properties-format-string-contents)   
 [Conteúdo de FORE_COLOR e BACK_COLOR &#40;MDX&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-cell-properties-fore-color-and-back-color-contents)   
 [Instruções de definição de dados MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
