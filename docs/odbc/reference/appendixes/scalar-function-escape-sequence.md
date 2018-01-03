---
title: "Sequência de Escape de função escalar | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- escape sequences [ODBC], scalar function
- scalar functions [ODBC], escape sequences
- ODBC escape sequences [ODBC], scalar function
ms.assetid: aaf5d516-e090-445f-8839-9e39581c69c7
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6792312d9b82b54460a35dd6f614c206c7bdfe3d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
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
