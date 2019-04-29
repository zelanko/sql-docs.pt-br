---
title: Sequência de Escape de função escalar | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], scalar function
- scalar functions [ODBC], escape sequences
- ODBC escape sequences [ODBC], scalar function
ms.assetid: aaf5d516-e090-445f-8839-9e39581c69c7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0913458d683d7641145b262552e147033dbfc054
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63032846"
---
# <a name="scalar-function-escape-sequence"></a>Sequência de escape de função escalar
ODBC usa sequências de escape para funções escalares. A sintaxe dessa sequência de escape é da seguinte maneira:  
  
```  
{fn scalar-function}  
```  
  
## <a name="remarks"></a>Comentários  
 Na notação BNF, a sintaxe é:  
  
 *ODBC escalar-função escape* :: =  
  
 *Iniciador do ODBC-esc* fn *função escalar ODBC esc terminador*  
  
 *scalar-function* ::= *function-name* (*argument-list*)  
  
 (As definições para os não terminais *nome da função* e *nome da função* (*lista de argumentos*) são derivados da lista de funções escalares em [ Apêndice e: Funções escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).)  
  
 *Iniciador do ODBC-esc* :: = {  
  
 *Terminador de esc ODBC* :: =}  
  
 Para determinar se a fonte de dados oferece suporte aos procedimentos e o driver dá suporte a sintaxe de invocação de procedimento ODBC, um aplicativo pode chamar **SQLGetInfo**. Para obter mais informações, consulte [apêndice e: Funções escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).
