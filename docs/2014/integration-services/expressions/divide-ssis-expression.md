---
title: Dividir (Expressão SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- / (divide)
- divide operator (/)
ms.assetid: 5bde9223-872d-443e-8a27-57735e1d8f3d
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a3dc1c33e2d3239311c14a6e0657a85775dc4e6a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37182673"
---
# <a name="divide-ssis-expression"></a>Divide (SSIS Expression)
  Divide a primeira expressão numérica pela segunda.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
dividend / divisor  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *dividend*  
 É a expressão numérica a ser dividida. *dividend* pode ser qualquer expressão numérica válida. Para obter mais informações, consulte [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
 *divisor*  
 É a expressão numérica pela qual dividir o dividendo. *divisor* pode ser qualquer expressão numérica com exceção de zero.  
  
## <a name="result-types"></a>Tipos de resultado  
 Determinado por tipos de dados dos dois argumentos. Para obter mais informações, consulte [Integration Services Data Types in Expressions](integration-services-data-types-in-expressions.md).  
  
## <a name="remarks"></a>Remarks  
 Se qualquer operando for nulo, o resultado será nulo.  
  
 Dividir por zero não é legal. Dependendo de como a subexpressão *divisor* é avaliada, um do seguintes erros acontece:  
  
-   Se a subexpressão *divisor* que é avaliada como zero for uma constante, o erro é exibido no tempo de design, fazendo com que a expressão falhe na validação.  
  
-   Se a subexpressão *divisor* avaliada como zero contiver variáveis, mas nenhuma coluna de entrada, o componente ao qual a expressão pertence falhará na validação de pré-execução que ocorre antes de o pacote ser executado.  
  
-   Se a subexpressão *divisor* avaliada como zero contiver as colunas de entrada, o erro será exibido no tempo de execução e será tratado de acordo com as regras do fluxo de erros do componente de fluxo de regras.  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo divide dois literais numéricos.  
  
```  
25 / 5  
```  
  
 Este exemplo divide valores na coluna **ListPrice** pelos valores na coluna **StandardCost** .  
  
```  
ListPrice / StandardCost  
```  
  
## <a name="see-also"></a>Consulte também  
 [Associatividade e precedência de operador](operator-precedence-and-associativity.md)   
 [Operadores &#40;expressão do SSIS&#41;](operators-ssis-expression.md)  
  
  
