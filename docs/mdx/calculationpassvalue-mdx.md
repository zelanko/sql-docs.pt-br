---
description: CalculationPassValue (MDX)
title: CalculationPassValue (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 98d30326b709f7bd651b7941e48d412a7b875ffd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88425038"
---
# <a name="calculationpassvalue-mdx"></a>CalculationPassValue (MDX)


  Retorna o valor numérico ou de cadeia de caracteres de uma linguagem MDX avaliada na fase de cálculo especificada de um cubo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
      Numeric syntax  
CalculationPassValue(Numeric_Expression,Pass_Value [, ABSOLUTE | RELATIVE [,ALL]])  
String syntax  
CalculationPassValue(String_Expression ,Pass_Value [, ABSOLUTE | RELATIVE [,ALL]])  
```  
  
## <a name="arguments"></a>Argumentos  
 *Numeric_Expression*  
 Uma expressão numérica válida, geralmente uma linguagem MDX de coordenadas de célula, que retorna um número.  
  
 *String_Expression*  
 Uma expressão de cadeia de caracteres válida, geralmente uma expressão MDX válida de coordenadas de célula, que retorna um número expresso como uma cadeia de caracteres.  
  
 *Pass_Value*  
 Uma expressão numérica válida que especifica o número de fase de cálculo.  
  
 ABSOLUTE  
 Um valor de sinalizador de acesso que especifica que o parâmetro de *Pass_Value* contém o índice de base zero da passagem de cálculo. ABSOLUTE é o valor padrão se nenhum valor de sinalizador de acesso for especificado.  
  
 RELATIVE  
 Um valor de sinalizador de acesso que especifica que o parâmetro *Pass_Value* contém um deslocamento relativo da fase de cálculo do cálculo de gatilho. Se o desvio for resolvido em um índice de fase de cálculo inferior a 0, a fase de cálculo 0 será usada e nenhum erro ocorrerá.  
  
 ALL  
 Quando esse sinalizador é definido, todos os valores são nulos, com exceção dos carregados pelo mecanismo de armazenamento. Quando não é definido, os valores são agregados sem nenhum cálculo aplicado.  
  
## <a name="remarks"></a>Comentários  
 Se uma expressão numérica for fornecida, a função retornará um valor numérico avaliando a expressão numérica MDX especificada na fase de cálculo e modificada (opcional) por um sinalizador de acesso e um modificador de sinalizador de acesso.  
  
 Se uma expressão de cadeia de caracteres for fornecida, a função retornará um valor de cadeia de caracteres avaliando a expressão de cadeia de caracteres MDX especificada na passagem de cálculo especificada e, opcionalmente, modificada por um sinalizador de acesso e um modificador de sinalizador de acesso *.*  
  
 Com a resolução de recursão automática no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , essa função tem pouco uso prático.  
  
> [!NOTE]  
>  Somente os administradores podem usar a função **CalculationPassValue** dentro de um script MDX. Um erro ocorre se um script MDX que contém essa função é executado no contexto de uma função que não tem privilégios de administrador.  
  
## <a name="see-also"></a>Consulte Também  
 [CalculationCurrentPass&#41;MDX &#40;](../mdx/calculationcurrentpass-mdx.md)   
 [&#40;de&#41;MDX IIf ](../mdx/iif-mdx.md)   
 [Referência da Função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
