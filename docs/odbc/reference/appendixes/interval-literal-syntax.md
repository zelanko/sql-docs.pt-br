---
title: Sintaxe Literal intervalado | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- literals [ODBC], interval
- interval literals [ODBC]
- ODBC literals [ODBC], interval
ms.assetid: 2f2d22c1-51d6-4055-9f5a-53bc31e9fea0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3387b07a8e769206a6a495addff4287000691fec
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290566"
---
# <a name="interval-literal-syntax"></a>Sintaxe literal de intervalo
A seguinte sintaxe é usada para literais de intervalo em ODBC.  
  
 *intervalo-literal ::= INTERVALO* [+*&#124;*-] *interval-string interval-qualifier*  
  
 *intervalo-string* ::= *citação* { *ano-mês-literal* &#124; *dia-literal* } *citação*  
  
 *ano-mês-literal* ::= *anos-valor* &#124; [*anos-valor* -] *meses-valor*  
  
 *dia-tempo-literal* ::= *intervalo de tempo diário* &#124; intervalo de *tempo*  
  
 *intervalo de tempo de dia* ::= valor de *dias* *[valor de horas* [: valor de*minutos*[:*valor de segundos*]]]  
  
 *intervalo de tempo* ::= *valor de horas* [: valor de*minutos* [:*valor de segundos* ] ]  
  
 &#124; *valor de minutos* [:*valor de segundos]*  
  
 valor *de &#124; segundos*  
  
 *valor de anos* ::= *valor de data-hora*  
  
 *valor de meses* ::= *valor de data-hora*  
  
 *dias-valor* ::= *data-hora-valor*  
  
 *horas-valor* ::= *valor de data-hora*  
  
 *minutos de valor* ::= *valor de data-hora*  
  
 *valor de segundos* ::= *segundos-inteiro-valor* [.[ *fração de segundos*] ]  
  
 *valor de segundos inteiros* ::= *inteiro não assinado*  
  
 *fração de segundos* ::= *inteiro não assinado*  
  
 *valor de data-hora* ::= *inteiro não assinado*  
  
 *classificatória de* intervalo:=campo *inicial* PARA *campo final* &#124; campo de tempo de data *única*  
  
 *campo de início* ::= *campo de tempo não-segunda data* [(interval-leading-field-precision )]*interval-leading-field-precision*  
  
 *campo final* ::= *campo de tempo de data não-segunda* &#124; SEGUNDO[(intervalo-fracional-segundos-precisão)]*interval-fractional-seconds-precision*  
  
 *campo de tempo de data única* ::= campo de tempo de data de *segunda* data *[(interval-leading-field-precision)]*&#124; SECOND[(interval-leading-field-precision [,*(interval-fractional-seconds-precision)]**interval-leading-field-precision*  
  
 *datetime-field* ::= *non-second-datetime-field* &#124; SECOND  
  
 *não-segunda data-data-time-field* ::= ANO &#124; MÊS &#124; DIA &#124; HORA &#124; MINUTO  
  
 *intervalo-fracional-segundos-precisão::=* *inteiro não assinado*  
  
 *interval-leading-field-precision* ::= *unsigned-in-inteiro*  
  
 *citar* ::= '  
  
 *indeferido-inteiro* ::= *dígito...*
