---
title: Sintaxe de literais numérico | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ODBC literals [ODBC], numeric
- numeric literals [ODBC]
- literals [ODBC], numeric
ms.assetid: fb17498d-4f1d-4b3d-b33d-1e62c7d3c32d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0863af2ae1fef38107a33ea99de330d547d7d2f9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
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
