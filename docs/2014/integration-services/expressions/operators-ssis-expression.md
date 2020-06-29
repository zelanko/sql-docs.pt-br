---
title: Operadores (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS, operators
- SQL Server Integration Services, operators
- operators [Integration Services]
- expressions [Integration Services], operators
ms.assetid: 33df3a3d-1f5c-429b-a3b9-52b7d8689089
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2851d5b0f8681b46a8c5b4efc714620fa5cd64f0
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85428303"
---
# <a name="operators-ssis-expression"></a>Operadores (Expressão SSIS)
  Esta seção descreve os operadores que a linguagem de expressão fornece e a precedência e a associação de operadores usados pelo avaliador de expressão.  
  
 A tabela a seguir lista os tópicos sobre os operadores desta seção.  
  
|Operador|DESCRIÇÃO|  
|--------------|-----------------|  
|[Conversão &#40;Expressão SSIS&#41;](cast-ssis-expression.md)|Converte uma expressão de um tipo de dados para um tipo de dados diferente.|  
|[&#40;&#41; &#40;Parênteses&#41; &#40;Expressão SSIS&#41;](parentheses-ssis-expression.md)|Identifica a ordem de avaliação de expressões.|  
|[+ &#40;Adicionar&#41; &#40;SSIS&#41;](add-ssis.md)|Soma duas expressões numéricas.|  
|[+ &#40;Concatenar&#41; &#40;Expressão SSIS&#41;](concatenate-ssis-expression.md)|Concatena duas expressões.|  
|[+ &#40;Subtrair&#41; &#40;Expressão SSIS&#41;](subtract-ssis-expression.md)|Subtrai a segunda expressão numérica da primeira.|  
|[+ &#40;Negar&#41; &#40;Expressão SSIS&#41;](negate-ssis-expression.md)|Nega uma expressão numérica.|  
|[&#42; &#40;Multiplicar&#41; &#40;Expressão SSIS&#41;](multiply-ssis-expression.md)|Multiplica duas expressões numéricas.|  
|[Dividir &#40;Expressão SSIS&#41;](divide-ssis-expression.md)|Divide a primeira expressão numérica pela segunda.|  
|[&#40;Módulo&#41; &#40;Expressão SSIS&#41;](modulo-ssis-expression.md)|Fornece o resto inteiro após dividir a primeira expressão numérica pela segunda.|  
|[&#124;&#124; &#40;OR lógica&#41; &#40;Expressão SSIS&#41;](logical-or-ssis-expression.md)|Executa uma operação OR lógica.|  
|[&& &#40;AND lógico&#41; &#40;Expressão SSIS&#41;](logical-and-ssis-expression.md)|Executa uma operação AND lógica.|  
|[\! &#40;NOT lógico&#41; &#40;Expressão SSIS&#41;](logical-not-ssis-expression.md)|Nega um operando booliano.|  
|[&#124; &#40;OR inclusivo de bit a bit&#41; &#40;Expressão SSIS&#41;](bitwise-inclusive-or-ssis-expression.md)|Executa uma operação OR de bit a bit de dois valores de inteiro.|  
|[^ &#40;OR exclusivo de bit a bit&#41; &#40;Expressão SSIS&#41;](bitwise-exclusive-or-ssis-expression.md)|Executa uma operação OR de bit a bit exclusiva de dois valores inteiros.|  
|[& &#40;AND bit a bit&#41; &#40;Expressão SSIS&#41;](bitwise-and-ssis-expression.md)|Executa uma operação AND de bit a bit de dois valores de inteiro.|  
|[~ &#40;Not bit a bit&#41; &#40;Expressão SSIS&#41;](bitwise-not-ssis-expression.md)|Executa uma negação bit a bit de um inteiro.|  
|[== &#40;Igual&#41; &#40;Expressão do SSIS&#41;](equal-ssis-expression.md)|Executará uma comparação para determinar se duas expressões são iguais.|  
|[\!= &#40;Diferente&#41; &#40;Expressão SSIS&#41;](unequal-ssis-expression.md)|Executará uma comparação para determinar se duas expressões não forem iguais.|  
|[&#62; &#40;Maior que&#41; &#40;Expressão SSIS&#41;](greater-than-ssis-expression.md)|Executa uma comparação para determinar se a primeira expressão é maior que a segunda.|  
|[&#60; &#40;Menor que&#41; &#40;Expressão SSIS&#41;](less-than-ssis-expression.md)|Executa uma comparação para determinar se a primeira expressão é menor que a segunda.|  
|[&#62;= &#40;Maior que ou igual a&#41; &#40;Expressão SSIS&#41;](greater-than-or-equal-to-ssis-expression.md)|Executa uma comparação para determinar se a primeira expressão é maior que ou igual à segunda.|  
|[&#60;= &#40;Menor que ou igual a&#41; &#40;Expressão SSIS&#41;](less-than-or-equal-to-ssis-expression.md)|Executa uma comparação para determinar se a primeira expressão é menor que ou igual à segunda.|  
|[? : &#40;Condicional&#41; &#40;Expressão SSIS&#41;](conditional-ssis-expression.md)|Retorna uma de duas expressões baseadas na avaliação de uma expressão booliana.|  
  
 Para obter informações sobre a colocação de cada operador na hierarquia de precedência, consulte [Operator Precedence and Associativity](operator-precedence-and-associativity.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Funções &#40;Expressão do SSIS&#41;](functions-ssis-expression.md)   
 [Exemplos de expressões avançadas do Integration Services](examples-of-advanced-integration-services-expressions.md)   
 [Expressões do SSIS &#40;Integration Services&#41;](integration-services-ssis-expressions.md)  
  
  
