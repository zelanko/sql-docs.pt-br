---
title: SEQÜÊNCIAS DE Fuga GUID | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 44907bfbd884bf361ce5f2ab8b3f6d8a247aba44
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306967"
---
# <a name="guid-escape-sequences"></a>Sequências de escape GUID
ODBC usa seqüências de fuga para literais GUID. A sintaxe desta seqüência de fuga é a seguinte:  
  
```  
{guid 'nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn'}  
```  
  
## <a name="remarks"></a>Comentários  
 Na notação da BNF, a sintaxe é a seguinte:  
  
 *ODBC-guid-escape* ::=  
     *Guia oDBC-esc-iniciador* '*guid-value*' *ODBC-esc-terminator*  
  
 *ODBC-esc-iniciador* ::= {  
  
 *ODBC-esc-terminator* ::= }  
  
 *valor guia* ::= *relógio-baixo valor guid-separador relógio-separador de valor médio-separador-separador-relógio-separador de alto valor guia-separador relógio-seq-valor guid-separador-valor-valor*  
  
 *guia-separador* ::= -  
  
 *relógio de baixo valor* ::= *hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit*  
  
 *relógio-valor médio* ::= *hex_digit hex_digit hex_digit hex_digit*  
  
 *relógio de alto valor* ::= *hex_digit hex_digit hex_digit hex_digit*  
  
 *relógio-seq-valor* ::= *hex_digit hex_digit hex_digit hex_digit*  
  
 *valor da hex_digit* do hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit *hex_digit hex_digit hex_digit*  
  
 *hex_digit::=* 0 &#124; 1 &#124; 2 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; A &#124; B &#124; &#124; D &#124; e &#124; F  
  
 A seqüência de fuga literal GUID é suportada se o tipo de dados GUID for suportado pela fonte de dados. Um aplicativo deve ligar para **o SQLGetTypeInfo** para determinar se esse tipo de dados é suportado.
