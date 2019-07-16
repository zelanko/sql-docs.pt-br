---
title: Sintaxe Literal de intervalo | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6352a5ae894adb09f714a78386bfecfa3ce1df77
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041623"
---
# <a name="interval-literal-syntax"></a>Sintaxe literal de intervalo
A sintaxe a seguir é usada para literais de intervalo em ODBC.  
  
 *literal de intervalo:: = intervalo* [+ *&#124;* -] *qualificador de intervalo de cadeia de caracteres do intervalo*  
  
 *interval-string* ::= *quote* { *year-month-literal* &#124; *day-time-literal* } *quote*  
  
 *ano-mês-literal* :: = *valor de ano* &#124; [*valor de ano* -] *valor de meses*  
  
 *day-time-literal* ::= *day-time-interval* &#124; *time-interval*  
  
 *day-time-interval* ::= *days-value* [*hours-value* [:*minutes-value*[:*seconds-value*]]]  
  
 *intervalo de tempo* :: = *valor de horas* [:*valor de minutos* [:*valor de segundos* ]]  
  
 &#124; *minutes-value* [:*seconds-value* ]  
  
 &#124; *seconds-value*  
  
 *valor de ano* :: = *valor datetime*  
  
 *valor de meses* :: = *valor datetime*  
  
 *valor de dias* :: = *valor datetime*  
  
 *valor de horas* :: = *valor datetime*  
  
 *valor de minutos* :: = *valor datetime*  
  
 *seconds-value* ::= *seconds-integer-value* [.[*seconds-fraction*] ]  
  
 *seconds-integer-value* ::= *unsigned-integer*  
  
 *seconds-fraction* ::= *unsigned-integer*  
  
 *datetime-value* ::= *unsigned-integer*  
  
 *interval-qualifier* ::= *start-field* TO *end-field* &#124; *single-datetime-field*  
  
 *start-field* ::= *non-second-datetime-field* [(*interval-leading-field-precision* )]  
  
 *end-field* ::= *non-second-datetime-field* &#124; SECOND[(*interval-fractional-seconds-precision*)]  
  
 *único campo de data e hora* :: = *campo Data e hora que não é segundo* [(*intervalo líderes-campo precisão*)] &#124; segundo [(*intervalo-líderes de campo de precisão*  [, (*intervalo de--segundos-precisão fracionária*)]  
  
 *datetime-field* ::= *non-second-datetime-field* &#124; SECOND  
  
 *non-second-datetime-field* ::= YEAR &#124; MONTH &#124; DAY &#124; HOUR &#124; MINUTE  
  
 *interval-fractional-seconds-precision* ::= *unsigned-integer*  
  
 *interval-leading-field-precision* ::= *unsigned-integer*  
  
 *cotação* :: = '  
  
 *unsigned-integer* ::= *digit...*
