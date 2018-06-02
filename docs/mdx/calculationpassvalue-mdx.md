---
title: CalculationPassValue (MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 88d7d8c52105feb14c982586f9a819977fc81ed0
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34577228"
---
# <a name="calculationpassvalue-mdx"></a>CalculationPassValue (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
 Um valor de sinalizador de acesso que especifica que o *Pass_Value* parâmetro contém o índice com base em zero da fase de cálculo. ABSOLUTE é o valor padrão se nenhum valor de sinalizador de acesso for especificado.  
  
 RELATIVE  
 Um valor de sinalizador de acesso que especifica que o *Pass_Value* parâmetro contém um desvio relativo da fase de cálculo de disparo. Se o desvio for resolvido em um índice de fase de cálculo inferior a 0, a fase de cálculo 0 será usada e nenhum erro ocorrerá.  
  
 ALL  
 Quando esse sinalizador é definido, todos os valores são nulos, com exceção dos carregados pelo mecanismo de armazenamento. Quando não é definido, os valores são agregados sem nenhum cálculo aplicado.  
  
## <a name="remarks"></a>Remarks  
 Se uma expressão numérica for fornecida, a função retornará um valor numérico avaliando a expressão numérica MDX especificada na fase de cálculo e modificada (opcional) por um sinalizador de acesso e um modificador de sinalizador de acesso.  
  
 Se uma expressão de cadeia de caracteres for fornecida, a função retornará um valor de cadeia de caracteres avaliando a expressão de cadeia de caracteres MDX especificada na fase de cálculo especificada e, opcionalmente modificado por um sinalizador de acesso e um modificador de sinalizador de acesso *.*  
  
 Com a resolução de recursão automática em [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], essa função tem pouco uso prático.  
  
> [!NOTE]  
>  Somente os administradores podem usar o **CalculationPassValue** função dentro de um script MDX. Um erro ocorre se um script MDX que contém essa função é executado no contexto de uma função que não tem privilégios de administrador.  
  
## <a name="see-also"></a>Consulte também  
 [CalculationCurrentPass &#40;MDX&#41;](../mdx/calculationcurrentpass-mdx.md)   
 [IIf &#40;MDX&#41;](../mdx/iif-mdx.md)   
 [Referência de função MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
