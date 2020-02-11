---
title: Sintaxe de literal numérico | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67990722"
---
# <a name="numeric-literal-syntax"></a>Sintaxe literal numérica
A sintaxe a seguir é usada para literais numéricos no ODBC:  
  
 *numeric-literal* :: = *sinal-numérico-literal &#124; não assinado-numeric-literal*  
  
 *sinal-numérico-literal* :: = [*Sign*] não *assinado-numeric-literal*  
  
 *não atribuído-numérico-literal* :: = *Exact-numeric-literal &#124; aproximado numérico-literal*  
  
 *exatos-numérico-literal* :: *= não assinado-inteiro* [*período*[*sem sinal-inteiro*]] *&#124;período sem sinal-inteiro*  
  
 *Sign* :: = sinal *de mais &#124; sinal de menos-sinal*  
  
 *aproximado-numérico-literal* :: = *mantissa E expoente*  
  
 *mantissa* :: = *Exact-numeric-literal*  
  
 *expoente* :: = *com sinal inteiro*  
  
 sinal *inteiro* :: = [*sinal*] *não assinado-inteiro*  
  
 *sem sinal-inteiro* :: = *dígito..* .  
  
 sinal *de mais* :: =*+*  
  
 sinal *de subtração* :: =-  
  
 *dígito* :: = 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; 0  
  
 *período* :: =.
