---
title: Sequência de escape de função escalar | Microsoft Docs
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
ms.openlocfilehash: 36e108fcc61b2390d5fd72ac4ad322778ccfb4b2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68057069"
---
# <a name="scalar-function-escape-sequence"></a>Sequência de escape de função escalar
O ODBC usa sequências de escape para funções escalares. A sintaxe dessa sequência de escape é a seguinte:  
  
```  
{fn scalar-function}  
```  
  
## <a name="remarks"></a>Comentários  
 Na notação BNF, a sintaxe é a seguinte:  
  
 *ODBC-escalar-function-escape* :: =  
  
 *ODBC-ESC-Initiator* FN *função escalar-do ODBC-ESC-terminador*  
  
 *escalar-função* :: = *nome-função* (*lista de argumentos*)  
  
 (As definições para o *nome de função* não terminais e nome de *função* (*lista de argumentos*) são derivadas da lista de funções escalares no [Apêndice E: funções escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).)  
  
 *ODBC-ESC-Initiator* :: = {  
  
 *ODBC-ESC-terminador* :: =}  
  
 Para determinar se a fonte de dados dá suporte a procedimentos e o driver dá suporte à sintaxe de invocação de procedimento ODBC, um aplicativo pode chamar **SQLGetInfo**. Para obter mais informações, consulte o [Apêndice E: funções escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).
