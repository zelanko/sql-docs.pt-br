---
description: Sintaxe literal numérica
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be87238f1663bcf9b12d40cb90521bb404a25af3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88425008"
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
