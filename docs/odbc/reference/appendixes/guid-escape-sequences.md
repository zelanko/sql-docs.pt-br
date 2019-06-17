---
title: Sequências de Escape GUID | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC escape sequences [ODBC], GUID
- escape sequences [ODBC], guid
- guid escape sequence [ODBC]
ms.assetid: 71d43ef9-4a31-493e-b9e0-f864e9ef3ce6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bf41671abc6393a18fad06e1debd297fed1f04c5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188961"
---
# <a name="guid-escape-sequences"></a>Sequências de escape GUID
ODBC usa sequências de escape para literais GUID. A sintaxe dessa sequência de escape é da seguinte maneira:  
  
```  
{guid 'nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn'}  
```  
  
## <a name="remarks"></a>Comentários  
 Na notação BNF, a sintaxe é:  
  
 *Escape de ODBC-guid* :: =  
     *Guid de iniciador do ODBC-esc* '*valor de guid*' *terminador de esc ODBC*  
  
 *Iniciador do ODBC-esc* :: = {  
  
 *Terminador de esc ODBC* :: =}  
  
 *guid-value* ::= *clock-low-value guid-separator clock-middle-value guid-separator clock-high-value guid-separator clock-seq-value guid-separator node-value*  
  
 *guid-separator* ::= -  
  
 *clock-low-value* ::= *hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit*  
  
 *clock-middle-value* ::= *hex_digit hex_digit hex_digit hex_digit*  
  
 *clock-high-value* ::= *hex_digit hex_digit hex_digit hex_digit*  
  
 *clock-seq-value* ::= *hex_digit hex_digit hex_digit hex_digit*  
  
 *clock-node-value* ::= *hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit*  
  
 *hex_digit* :: = 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; A &#124; B &#124; C &#124; 1!d &#124; E &#124; F  
  
 A sequência de escape literal GUID tem suporte se o tipo de dados GUID é suportado pela fonte de dados. Um aplicativo deve chamar **SQLGetTypeInfo** para determinar se esse tipo de dados tem suporte.
