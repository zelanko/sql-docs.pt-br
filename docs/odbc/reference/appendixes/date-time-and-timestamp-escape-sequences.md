---
title: Sequências de fuga de data, hora e carimbo de tempo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC]
- escape sequences [ODBC], about escape sequences
- ODBC escape sequences [ODBC], about escape sequences
- ODBC escape sequences [ODBC]
ms.assetid: 67b7dee0-e5b1-4469-a626-0c7767852b80
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e6cbcdac00b4cd7497f53c9f3a13f4f7303b5154
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284338"
---
# <a name="date-time-and-timestamp-escape-sequences"></a>Sequências de escape de data, hora e carimbo de data/hora
O ODBC define seqüências de fuga para literais de data, hora e carimbo de data. A sintaxe dessas seqüências de fuga é a seguinte:  
  
```  
  
{d 'value'}  
{t 'value'}  
{ts 'value'}  
```  
  
 Na notação da BNF, a sintaxe é a seguinte:  
  
```  
  
      ODBC-date-time-escape ::=  
     ODBC-date-escape  
     | ODBC-time-escape  
     | ODBC-timestamp-escapeODBC-date-escape ::=  
     ODBC-esc-initiator d 'date-value' ODBC-esc-terminatorODBC-time-escape ::=  
     ODBC-esc-initiator t 'time-value' ODBC-esc-terminatorODBC-timestamp-escape ::=  
     ODBC-esc-initiator ts 'timestamp-value' ODBC-esc-terminatorODBC-esc-initiator ::= {  
ODBC-esc-terminator ::= }  
date-value ::=   
     years-value date-separator months-value date-separator days-valuetime-value ::=   
     hours-value time-separator minutes-value time-separatorseconds-valuetimestamp-value ::= date-value timestamp-separator time-valuedate-separator ::= -  
time-separator ::= :  
timestamp-separator ::=  
     (The blank character)years-value ::= digit digit digit digitmonths-value ::= digit digitdays-value ::= digit digithours-value ::= digit digitminutes-value ::= digit digitseconds-value ::= digit digit[.digit...]  
```  
  
## <a name="remarks"></a>Comentários  
 As seqüências de escape literal data, hora e carimbo de data são suportadas se os tipos de dados de data, hora e carimbo de data forem suportados pela fonte de dados. Um aplicativo deve ligar para **o SQLGetTypeInfo** para determinar se esses tipos de dados são suportados.
