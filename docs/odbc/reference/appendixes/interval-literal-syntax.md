---
title: Sintaxe de literal de intervalo | Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81290566"
---
# <a name="interval-literal-syntax"></a>Sintaxe literal de intervalo
A sintaxe a seguir é usada para literais de intervalo no ODBC.  
  
 *Interval-literal:: = intervalo* [+*&#124;*-] *intervalo-cadeia de caracteres de intervalo-qualificador*  
  
 *intervalo-cadeia de caracteres* :: = *cotação* { *year-month-literal* &#124; *Day-Time-literal* *}*  
  
 *ano-mês-literal* :: = *anos-valor* &#124; [*anos-valor* -] *meses-valor*  
  
 *Day-Time-literal* :: = *Day-time-interval* &#124; *intervalo de tempo*  
  
 *Day-time-interval* :: = *dias-valor* [*horas-valor* [:*minutos-valor*[:*segundos-valor*]]]  
  
 *time-interval* :: = *hours-Value* [:*minutos-valor* [:*segundos-valor* ]]  
  
 &#124; *minutos-valor* [:*segundos-valor* ]  
  
 &#124; *segundos-valor*  
  
 *anos-valor* :: = *DateTime – valor*  
  
 *months-valor* :: = *DateTime – valor*  
  
 *dias-valor* :: = *DateTime-valor*  
  
 *horas-valor* :: = *DateTime-valor*  
  
 *minutos-valor* :: = *DateTime – valor*  
  
 *segundos-valor* :: = *segundos-inteiro-valor* [. [ *segundos-fração*] ]  
  
 *segundos-valor inteiro* :: = *não assinado-inteiro*  
  
 *segundos-fração* :: = *sem sinal-inteiro*  
  
 *DateTime-valor* :: = *sem sinal-inteiro*  
  
 *Interval-qualificador* :: = *Start-Field* para *end-Field* &#124; *single-DateTime-Field*  
  
 *Start-Field* :: = *não-segundo-DateTime-Field* [(*Interval-entrelinha-Field-Precision* )]  
  
 *campo de término* :: = *não-segundo-data-hora-campo* &#124; segundo [(*intervalo – fração-segundo-precisão*)]  
  
 *single-DateTime-Field* :: = *não-segundo-DateTime-Field* [(*Interval-entrelinha-field-Precision*)] &#124; segundo [(*intervalo-entrelinha-campo-precisão* [, (*intervalo-fração-segundos-precisão*)]  
  
 *DateTime-campo* :: = *não-segundo-datetime-campo* &#124; segundo  
  
 *não-segundo-data-hora-campo* :: = ano &#124; mês &#124; dia &#124; hora &#124; minuto  
  
 *intervalo-fração-segundos-precisão* :: = *não assinado-inteiro*  
  
 *intervalo-entrelinha-campo-precisão* :: = *não assinado-inteiro*  
  
 *cotação* :: = '  
  
 *sem sinal-inteiro* :: = *dígito..* .
