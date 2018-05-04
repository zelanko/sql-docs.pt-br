---
title: Sequência de Escape de função escalar | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], scalar function
- scalar functions [ODBC], escape sequences
- ODBC escape sequences [ODBC], scalar function
ms.assetid: aaf5d516-e090-445f-8839-9e39581c69c7
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 513df8ccd679ec2236822f780400c3cc39e37609
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="scalar-function-escape-sequence"></a>Sequência de Escape de função escalar
ODBC usa sequências de escape para funções escalares. A sintaxe dessa sequência de escape é da seguinte maneira:  
  
```  
{fn scalar-function}  
```  
  
## <a name="remarks"></a>Remarks  
 Na notação BNF, a sintaxe é:  
  
 *ODBC escalar-função escape* :: =  
  
 *Iniciador de esc ODBC* fn *função escalar ODBC esc terminador*  
  
 *função escalar* :: = *nome de função* (*lista de argumentos*)  
  
 (As definições para os sem terminais *nome de função* e *nome de função* (*lista de argumentos*) são derivados da lista de funções escalares em [ Apêndice e: funções escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).)  
  
 *Iniciador de esc ODBC* :: = {  
  
 *Terminador de esc ODBC* :: =}  
  
 Para determinar se a fonte de dados oferece suporte a procedimentos e o driver oferece suporte à sintaxe de invocação de procedimento ODBC, um aplicativo pode chamar **SQLGetInfo**. Para obter mais informações, consulte [apêndice e: escalar funções](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).
