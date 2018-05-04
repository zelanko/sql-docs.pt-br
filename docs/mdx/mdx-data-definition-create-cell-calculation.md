---
title: Instrução CREATE CELL CALCULATION (MDX) | Microsoft Docs
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
- CELL CALCULATION
- CREATE
- CALCULATION
- CELL
- CREATE_CELL_CALCULATION
- CREATE CELL
- CREATE CELL CALCULATION
dev_langs:
- kbMDX
helpviewer_keywords:
- calculations [Analysis Services], creating
- CREATE CELL CALCULATION statement
- cubes [Analysis Services], calculations
ms.assetid: 01ced1b3-ada1-4b55-b350-e4255c3cc679
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: cb0f441fbb42602dad9bed7b06b4299680f5456c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-data-definition---create-cell-calculation"></a>Definição de dados MDX - criar o CÁLCULO de CÉLULA
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
 *Cadeia de caracteres*  
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
  
## <a name="remarks"></a>Remarks  
 Ao usar células calculadas, o aplicativo cliente pode especificar um valor de acúmulo para um conjunto de células específico, em vez de um conjunto inteiro de células como no caso de uma fórmula de acúmulo ou de um membro calculado. Por exemplo, é possível especificar que qualquer célula do conjunto definido por `{[Canada],[Time].[2000]}` pode conter um valor definido por uma fórmula. Qualquer outra célula que não está contida nesse conjunto é calculada normalmente.  
  
> [!NOTE]  
>  A forma de Backus-Naur (BNF) de `{*(<comment> | <whitespace> | <newline>)}` será analisada como `{*}` para fins de compatibilidade com versões anteriores.  
  
## <a name="see-also"></a>Consulte também  
 [Criando células calculadas no escopo da sessão](../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-session-scoped-calculated-cells.md)   
 [Criando cálculos de célula no escopo da consulta & #40; MDX & #41;](../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-query-scoped-cell-calculations.md)   
 [Criando cálculos de célula em MDX &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-build-cell-calculations.md)   
 [Usando propriedades de célula & #40; MDX & #41;](../analysis-services/multidimensional-models/mdx/mdx-cell-properties-using-cell-properties.md)   
 [Conteúdo de FORMAT_STRING & #40; MDX & #41;](../analysis-services/multidimensional-models/mdx/mdx-cell-properties-format-string-contents.md)   
 [Conteúdo de FORE_COLOR e Back_color &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-cell-properties-fore-color-and-back-color-contents.md)   
 [Instruções de definição de dados MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
