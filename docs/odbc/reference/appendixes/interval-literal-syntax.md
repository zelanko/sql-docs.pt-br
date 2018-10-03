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
manager: craigg
ms.openlocfilehash: d477dbc6b54d7ebd82b7e2ef8611f5f6dd807e83
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47694041"
---
# <a name="interval-literal-syntax"></a>Sintaxe literal de intervalo
A sintaxe a seguir é usada para literais de intervalo em ODBC.  
  
 *literal de intervalo:: = intervalo* [+*&#124;*-] *qualificador de intervalo de cadeia de caracteres do intervalo*  
  
 *intervalo de cadeia de caracteres* :: = *cotação* { *ano-mês-literal* &#124; *literal de hora do dia* } *aspas*  
  
 *ano-mês-literal* :: = *valor de ano* &#124; [*valor de ano* -] *valor de meses*  
  
 *literal de hora do dia* :: = *intervalo de tempo do dia* &#124; *intervalo de tempo*  
  
 *intervalo de tempo do dia* :: = *valor de dias* [*valor de horas* [:*valor de minutos*[:*valor de segundos*]]]  
  
 *intervalo de tempo* :: = *valor de horas* [:*valor de minutos* [:*valor de segundos* ]]  
  
 &#124;*valor de minutos* [:*valor de segundos* ]  
  
 &#124;*valor de segundos*  
  
 *valor de ano* :: = *valor datetime*  
  
 *valor de meses* :: = *valor datetime*  
  
 *valor de dias* :: = *valor datetime*  
  
 *valor de horas* :: = *valor datetime*  
  
 *valor de minutos* :: = *valor datetime*  
  
 *valor de segundos* :: = *valor de inteiro de segundos* [. [ *fração de segundos*]]  
  
 *valor de inteiro de segundos* :: = *inteiro não assinado*  
  
 *fração de segundos* :: = *inteiro não assinado*  
  
 *valor de data e hora* :: = *inteiro não assinado*  
  
 *intervalo-qualifier* :: = *campo inicial* TO *campo final* &#124; *único campo de data e hora*  
  
 *campo de início* :: = *campo Data e hora que não é segundo* [(*intervalo líderes-campo precisão* )]  
  
 *campo final* :: = *campo Data e hora que não é segundo* &#124; segundo [(*intervalo de--segundos-precisão fracionária*)]  
  
 *único campo de data e hora* :: = *campo Data e hora que não é segundo* [(*intervalo líderes-campo precisão*)] &#124; segundo [(*intervalo-líderes de campo de precisão*  [, (*intervalo de--segundos-precisão fracionária*)]  
  
 *campo de data e hora* :: = *campo Data e hora que não é segundo* &#124; segundo  
  
 *campo Data e hora que não é segundo* :: = ano &#124; mês &#124; dia &#124; hora &#124; minuto  
  
 *intervalo de--segundos-precisão fracionária* :: = *inteiro não assinado*  
  
 *intervalo-líderes de campo de precisão* :: = *inteiro não assinado*  
  
 *cotação* :: = '  
  
 *inteiro sem sinal* :: = *dígito...*
