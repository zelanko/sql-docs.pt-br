---
title: Operadores aritméticos (DMX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- arithmetic operators
ms.assetid: befe4f0c-e5dd-4ae1-b88e-6ac7aab2181a
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: c256882453ca3536a21babb2d87b774e9aab3d6d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="operators---arithmetic"></a>Operadores - aritmética
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Você pode usar operadores aritméticos em extensões DMX (Data Mining) para computações aritméticas no [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], incluindo adição, subtração, multiplicação e divisão.  
  
 A tabela a seguir identifica os operadores aritméticos aos quais a DMX oferece suporte.  
  
|Operador|Description|  
|--------------|-----------------|  
|[+ &#40; Adicionar &#41; &#40; DMX &#41;](../dmx/add-dmx.md)|Soma dois números.|  
|[-&#40; Subtrair &#41; &#40; DMX &#41;](../dmx/subtract-dmx.md)|Subtrai um número de outro.|  
|[&#42; &#40; Multiplique &#41; &#40; DMX &#41;](../dmx/multiply-dmx.md)|Multiplica um número por outro.|  
|[&#40; divisão &#41; &#40; DMX &#41;](../dmx/divide-dmx.md)|Divide um número pelo outro.|  
  
 As regras a seguir determinam a ordem de prioridade para operadores aritméticos em uma expressão DMX:  
  
-   Quando houver mais de um operador aritmético em uma expressão, a multiplicação e a divisão serão calculadas primeiramente, seguidas da subtração e da adição.  
  
-   Quando todos os operadores aritméticos em uma expressão tiverem o mesmo nível de prioridade, a ordem de execução será da esquerda para a direita.  
  
-   Expressões entre parênteses têm prioridade sobre todas as outras operações.  
  
## <a name="see-also"></a>Consulte Também  
 [Extensões de mineração de dados &#40; DMX &#41; Referência](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Convenções de sintaxe](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Elementos de sintaxe](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Expressões &#40; DMX &#41;](../dmx/expressions-dmx.md)   
 [Funções de previsão geral &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [Operadores &#40; DMX &#41;](../dmx/operators-dmx.md)   
 [Estrutura e o uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
