---
title: Instrução CREATE CELL CALCULATION (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7e69aa9e3da29abe054aaf272c5fe3ed12172a4d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63309138"
---
# <a name="mdx-data-definition---create-cell-calculation"></a>Definição de dados MDX – CREATE CELL CALCULATION


  Cria um cálculo que avalia uma expressão MDX (Multidimensional Expressions) em um conjunto especificado de tuplas em um cubo.  
  
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
  
 *String*  
 Um valor de cadeia de caracteres válido.  
  
 *MDX_Expression*  
 Uma expressão MDX válida.  
  
 *Logical_Expression*  
 Uma expressão lógica MDX válida.  
  
 *Integer*  
 Um valor inteiro válido.  
  
 *Calculation_Name*  
 Uma cadeia de caracteres válida que fornece o nome de uma propriedade de cálculo de célula.  
  
 *Scalar_Expression*  
 Uma expressão escalar MDX válida.  
  
## <a name="remarks"></a>Comentários  
 Ao usar células calculadas, o aplicativo cliente pode especificar um valor de acúmulo para um conjunto de células específico, em vez de um conjunto inteiro de células como no caso de uma fórmula de acúmulo ou de um membro calculado. Por exemplo, é possível especificar que qualquer célula do conjunto definido por `{[Canada],[Time].[2000]}` pode conter um valor definido por uma fórmula. Qualquer outra célula que não está contida nesse conjunto é calculada normalmente.  
  
> [!NOTE]  
>  A forma de Backus-Naur (BNF) de `{*(<comment> | <whitespace> | <newline>)}` será analisada como `{*}` para fins de compatibilidade com versões anteriores.  
  
## <a name="see-also"></a>Consulte também  
 [Criando células calculadas no escopo da sessão](../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-session-scoped-calculated-cells.md)   
 [Criando cálculos de célula no escopo da consulta &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-query-scoped-cell-calculations.md)   
 [Criando cálculos de célula em MDX &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-build-cell-calculations.md)   
 [Usando propriedades da célula &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-cell-properties-using-cell-properties.md)   
 [Conteúdo de FORMAT_STRING &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-cell-properties-format-string-contents.md)   
 [Conteúdo de FORE_COLOR e Back_color &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-cell-properties-fore-color-and-back-color-contents.md)   
 [Instruções de definição de dados MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
