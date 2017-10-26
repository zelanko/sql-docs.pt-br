---
title: "Sequência de Escape de função escalar | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- escape sequences [ODBC], scalar function
- scalar functions [ODBC], escape sequences
- ODBC escape sequences [ODBC], scalar function
ms.assetid: aaf5d516-e090-445f-8839-9e39581c69c7
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3c161938df59fe09526d1030f57352fbc1325701
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="scalar-function-escape-sequence"></a>Sequência de Escape de função escalar
ODBC usa sequências de escape para funções escalares. A sintaxe dessa sequência de escape é da seguinte maneira:  
  
```  
{fn scalar-function}  
```  
  
## <a name="remarks"></a>Comentários  
 Na notação BNF, a sintaxe é:  
  
 *ODBC escalar-função escape* :: =  
  
 *Iniciador de esc ODBC* fn *função escalar ODBC esc terminador*  
  
 *função escalar* :: = *nome de função* (*lista de argumentos*)  
  
 (As definições para os sem terminais *nome de função* e *nome de função* (*lista de argumentos*) são derivados da lista de funções escalares em [ Apêndice e: funções escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).)  
  
 *Iniciador de esc ODBC* :: = {  
  
 *Terminador de esc ODBC* :: =}  
  
 Para determinar se a fonte de dados oferece suporte a procedimentos e o driver oferece suporte à sintaxe de invocação de procedimento ODBC, um aplicativo pode chamar **SQLGetInfo**. Para obter mais informações, consulte [apêndice e: escalar funções](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).

