---
title: Seqüência de fuga da função escalar | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8347b8e6f0fab6dffc5295fb3b8260a6a56ed123
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305069"
---
# <a name="scalar-function-escape-sequence"></a>Sequência de escape de função escalar
ODBC usa seqüências de fuga para funções escalares. A sintaxe desta seqüência de fuga é a seguinte:  
  
```  
{fn scalar-function}  
```  
  
## <a name="remarks"></a>Comentários  
 Na notação da BNF, a sintaxe é a seguinte:  
  
 *ODBC-escalador-função-escape* ::=  
  
 *ODBC-esc-iniciador* fn *escalador-função ODBC-esc-terminator*  
  
 *função escalar* ::= *nome de função* *(lista de argumentos)*  
  
 (As definições para o *nome da função* e nome de *função* não terminais *(lista de argumentos)* são derivadas da lista de funções escalares no [apêndice E: Funções escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).)  
  
 *ODBC-esc-iniciador* ::= {  
  
 *ODBC-esc-terminator* ::= }  
  
 Para determinar se a fonte de dados suporta procedimentos e o driver suporta a sintaxe de invocação do procedimento ODBC, um aplicativo pode chamar **sQLGetInfo**. Para obter mais informações, consulte [Apêndice E: Funções escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).
