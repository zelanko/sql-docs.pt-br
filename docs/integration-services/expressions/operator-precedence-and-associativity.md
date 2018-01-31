---
title: "Precedência de operador e capacidade de associação | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- associativity [Integration Services]
- precedence [Integration Services]
ms.assetid: 5094164f-dabc-45b5-b611-384feb2b3fe3
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2ac5173ee2e802b9c6c3331ef2f22ff963c890fe
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="operator-precedence-and-associativity"></a>Precedência de operador e capacidade de associação
  Cada operador no conjunto de operadores que o avaliador de expressão aceita tem uma precedência designada na hierarquia de precedência e inclui uma direção na qual ele será avaliado. A direção de avaliação para um operador é a capacidade de associação do operador. Os operadores com maior precedência são avaliados antes dos operadores com menor precedência. Se uma expressão complexa tiver vários operadores, a precedência de operador determina a ordem na qual as operações são executadas. A ordem de execução pode afetar o valor resultante significativamente. Alguns operadores têm precedência igual. Se uma expressão contiver vários operadores de precedência igual, os operadores serão avaliados de forma direcional, da esquerda para a direita ou da direita para a esquerda.  
  
 A tabela a seguir lista a precedência de operadores na ordem de cima para baixo. Os operadores ao mesmo nível têm precedência igual.  
  
|Símbolo do operador|Tipo de operação|Capacidade de associação|  
|---------------------|-----------------------|-------------------|  
|( )|Expression|Da esquerda para a direita|  
|–, !, ~|Unário|Da direita para a esquerda|  
|conversões|Unário|Da direita para a esquerda|  
|*, / ,%|Multiplicativo|Da esquerda para a direita|  
|+, –|Aditiva|Da esquerda para a direita|  
|\<, >, \<=, >=|Relacional|Da esquerda para a direita|  
|==, !=|Igualitário|Da esquerda para a direita|  
|&|AND bit a bit|Da esquerda para a direita|  
|^|OR exclusivo bit a bit|Da esquerda para a direita|  
|&#124;|OR inclusivo bit a bit|Da esquerda para a direita|  
|&&|AND lógico|Da esquerda para a direita|  
|&#124;&#124;|OR lógico|Da esquerda para a direita|  
|? :|Expressões condicionais|Da direita para a esquerda|  
  
## <a name="see-also"></a>Consulte Também  
 [Operadores &#40;Expressão do SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
