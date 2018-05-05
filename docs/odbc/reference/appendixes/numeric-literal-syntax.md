---
title: Sintaxe de literais numérico | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC literals [ODBC], numeric
- numeric literals [ODBC]
- literals [ODBC], numeric
ms.assetid: fb17498d-4f1d-4b3d-b33d-1e62c7d3c32d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 95fd850239c0ad3894105c94e3f8ff05459394ff
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="numeric-literal-syntax"></a>Sintaxe de literais numérico
A sintaxe a seguir é usada para literais numéricos em ODBC:  
  
 *literal numérico* :: = *assinado numeric-literal &#124; literal não assinado de numérico*  
  
 *literal assinado de numérico* :: = [*sinal*] *literal não assinado de numérico*  
  
 *sem sinal numérico-literal* :: = *exato numérico-literal &#124; aproximado numérico-literal*  
  
 *exato numérico-literal* :: = *inteiro não assinado* [*período*[*inteiro não assinado*]]  *&#124;Períoda inteira não assinada*  
  
 *sinal de* :: = *sinal &#124; sinal de subtração*  
  
 *literal aproximado de numérico* :: = *expoente mantissa E*  
  
 *mantissa* :: = *exato numérico-literal*  
  
 *expoente* :: = *inteiro assinado*  
  
 *inteiro assinado* :: = [*sinal*] *inteiro não assinado*  
  
 *inteiro não assinado* :: = *dígitos...*  
  
 *sinal de adição* :: = *+*  
  
 *sinal de menos* :: = -  
  
 *Dígito* :: = 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; 0  
  
 *período* :: =.
