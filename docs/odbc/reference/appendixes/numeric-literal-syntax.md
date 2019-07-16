---
title: Sintaxe de literais numéricos | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9daa81e2e0c2e927ee7407d4a00d5d48c333bd54
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990722"
---
# <a name="numeric-literal-syntax"></a>Sintaxe literal numérica
A sintaxe a seguir é usada para literais numéricos no ODBC:  
  
 *numeric-literal* ::= *signed-numeric-literal &#124; unsigned-numeric-literal*  
  
 *signed-numeric-literal* ::= [*sign*] *unsigned-numeric-literal*  
  
 *unsigned-numeric-literal* ::= *exact-numeric-literal &#124; approximate-numeric-literal*  
  
 *exact-numeric-literal* ::= *unsigned-integer* [*period*[*unsigned-integer*]] *&#124;period unsigned-integer*  
  
 *sign* ::= *plus-sign &#124; minus-sign*  
  
 *aproximar-numeric-literal* :: = *expoente mantissa E*  
  
 *mantissa* ::= *exact-numeric-literal*  
  
 *exponent* ::= *signed-integer*  
  
 *signed-integer* ::= [*sign*] *unsigned-integer*  
  
 *unsigned-integer* ::= *digit...*  
  
 *plus-sign* ::= *+*  
  
 *minus-sign* ::= -  
  
 *digit* ::= 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; 0  
  
 *período* :: =.
