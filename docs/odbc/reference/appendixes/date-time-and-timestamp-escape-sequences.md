---
title: Sequências de escape Date, time e timestamp | Microsoft Docs
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
ms.openlocfilehash: a2b9b62fae23932d1072ea319e1305a0853ca2d6
ms.sourcegitcommit: 19ff45e8a2f4193fe8827f39258d8040a88befc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2020
ms.locfileid: "83807533"
---
# <a name="date-time-and-timestamp-escape-sequences"></a>Sequências de escape de data, hora e carimbo de data/hora
O ODBC define as sequências de escape para os literais de data, hora e timestamp. A sintaxe dessas sequências de escape é a seguinte:  
  
```  
  
{d 'value'}  
{t 'value'}  
{ts 'value'}  
```  
  
 Na notação BNF, a sintaxe é a seguinte:  
  
```bnf 
ODBC-date-time-escape ::=  
     ODBC-date-escape  
     | ODBC-time-escape  
     | ODBC-timestamp-escape

ODBC-date-escape ::=  
     ODBC-esc-initiator d 'date-value' ODBC-esc-terminator

ODBC-time-escape ::=  
     ODBC-esc-initiator t 'time-value' ODBC-esc-terminator

ODBC-timestamp-escape ::=  
     ODBC-esc-initiator ts 'timestamp-value' ODBC-esc-terminator

ODBC-esc-initiator ::= {  

ODBC-esc-terminator ::= }  

date-value ::=   
     years-value date-separator months-value date-separator days-value

time-value ::=   
     hours-value time-separator minutes-value time-separator seconds-value

timestamp-value ::= date-value timestamp-separator time-value

date-separator ::= -  

time-separator ::= :  

timestamp-separator ::=  
     (The blank character)

years-value ::= digit digit digit digit

months-value ::= digit digit

days-value ::= digit digit

hours-value ::= digit digit

minutes-value ::= digit digit

seconds-value ::= digit digit[.digit...]  
```  
  
## <a name="remarks"></a>Comentários  
 As sequências de escape de data, hora e carimbo de hora literal têm suporte se a fonte de dados tiver suporte para os tipos de dados Date, time e timestamp. Um aplicativo deve chamar **SQLGetTypeInfo** para determinar se esses tipos de dados têm suporte.
