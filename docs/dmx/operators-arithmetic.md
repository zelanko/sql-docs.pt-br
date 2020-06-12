---
title: Operadores aritméticos (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 149cd67594cac64fc8ad315b2fca9bb1cda373d5
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669309"
---
# <a name="operators---arithmetic"></a>Operadores – aritméticos
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Você pode usar operadores aritméticos em DMX (extensões de mineração de dados) para cálculos aritméticos no [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , incluindo adição, subtração, multiplicação e divisão.  
  
 A tabela a seguir identifica os operadores aritméticos aos quais a DMX oferece suporte.  
  
|Operador|Descrição|  
|--------------|-----------------|  
|[+ &#40;adicionar&#41; &#40;DMX&#41;](../dmx/add-dmx.md)|Soma dois números.|  
|[-&#40;subtrair&#41; &#40;DMX&#41;](../dmx/subtract-dmx.md)|Subtrai um número de outro.|  
|[&#42; &#40;multiplicar&#41; &#40;DMX&#41;](../dmx/multiply-dmx.md)|Multiplica um número por outro.|  
|[&#40;dividir&#41; &#40;DMX&#41;](../dmx/divide-dmx.md)|Divide um número pelo outro.|  
  
 As regras a seguir determinam a ordem de prioridade para operadores aritméticos em uma expressão DMX:  
  
-   Quando houver mais de um operador aritmético em uma expressão, a multiplicação e a divisão serão calculadas primeiramente, seguidas da subtração e da adição.  
  
-   Quando todos os operadores aritméticos em uma expressão tiverem o mesmo nível de prioridade, a ordem de execução será da esquerda para a direita.  
  
-   Expressões entre parênteses têm prioridade sobre todas as outras operações.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-reference.md)   
 [Referência de função&#41; DMX &#40;extensões de mineração de dados](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Referência de operador de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Referência de instrução&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-statements.md)   
 [&#40;as convenções de sintaxe de&#41; DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [As extensões de mineração de dados &#40;elementos de sintaxe DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Expressões &#40;DMX&#41;](../dmx/expressions-dmx.md)   
 [Funções de previsão gerais &#40;&#41;DMX](../dmx/general-prediction-functions-dmx.md)   
 [Operadores &#40;&#41;DMX](../dmx/operators-dmx.md)   
 [Estrutura e uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
