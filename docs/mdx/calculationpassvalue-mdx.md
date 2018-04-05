---
title: CalculationPassValue (MDX) | Microsoft Docs
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
- CALCULATIONPASSVALUE
dev_langs:
- kbMDX
helpviewer_keywords:
- CalculationPassValue function
ms.assetid: 1b4012cb-c8c7-441a-bb9c-59430703b189
caps.latest.revision: 45
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: dd5ed7f5ef6eb60b37c5066f7535d34913572871
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
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
  
 Se uma expressão de cadeia de caracteres for fornecida, a função retornará um valor de cadeia de caracteres avaliando a expressão de cadeia de caracteres MDX especificada na fase de cálculo especificada e, opcionalmente modificado por um sinalizador de acesso e um modificador de sinalizador de acesso*.*  
  
 Com a resolução de recursão automática em [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], essa função tem pouco uso prático.  
  
> [!NOTE]  
>  Somente os administradores podem usar o **CalculationPassValue** função dentro de um script MDX. Um erro ocorre se um script MDX que contém essa função é executado no contexto de uma função que não tem privilégios de administrador.  
  
## <a name="see-also"></a>Consulte Também  
 [CalculationCurrentPass &#40; MDX &#41;](../mdx/calculationcurrentpass-mdx.md)   
 [IIf &#40; MDX &#41;](../mdx/iif-mdx.md)   
 [Referência de função MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
