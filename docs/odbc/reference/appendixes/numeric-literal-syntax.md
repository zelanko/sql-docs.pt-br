---
title: Sintaxe Literal Numérica | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC literals [ODBC], numeric
- numeric literals [ODBC]
- literals [ODBC], numeric
ms.assetid: fb17498d-4f1d-4b3d-b33d-1e62c7d3c32d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e035e3ec53c5b5494c029d6840b9f5c836821209
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299856"
---
# <a name="numeric-literal-syntax"></a>Sintaxe literal numérica
A seguinte sintaxe é usada para literais numéricos em ODBC:  
  
 *numérico-literal* ::= *assinado-numérico-literal &#124; não assinado-numérico-literal*  
  
 *assinado-numérico-literal* ::= [*sinal*] *não assinado-numérico-literal*  
  
 *unsigned-numeric-literal* ::= *exact-numeric-literal &#124; aproxima-numérico-literal*  
  
 *exato-numérico-literal* ::= *não-assinado-inteiro* [*período**[não assinado-inteiro*]] *&#124;período sem inteiro assinado*  
  
 *sinal* ::= *mais-sinal &#124; menos-sinal*  
  
 expoente *aproxima-numérico-literal* ::= *expoente mantissa E*  
  
 *mantissa* ::= *exata-numérica-literal*  
  
 *expoente* ::= *inteiro assinado*  
  
 *inteiro assinado* ::= [*sinal*] *inassinado-inteiro*  
  
 *indeferido-inteiro* ::= *dígito...*  
  
 *plus-sign* ::=*+*  
  
 *menos sinal* ::= -  
  
 *dígito* ::= 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; 0  
  
 *período* ::= .
