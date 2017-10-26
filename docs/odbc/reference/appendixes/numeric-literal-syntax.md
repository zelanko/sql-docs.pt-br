---
title: "Sintaxe de literais numérico | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC literals [ODBC], numeric
- numeric literals [ODBC]
- literals [ODBC], numeric
ms.assetid: fb17498d-4f1d-4b3d-b33d-1e62c7d3c32d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 64a772d8a04015060aa717e4153bf6f36e5b74de
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="numeric-literal-syntax"></a>Sintaxe de literais numérico
A sintaxe a seguir é usada para literais numéricos em ODBC:  
  
 *literal numérico* :: = *literal assinado de numérico &#124; sem sinal numérico-literal*  
  
 *literal assinado de numérico* :: = [*sinal*] *literal não assinado de numérico*  
  
 *sem sinal numérico-literal* :: = *literal exato de numérico &#124; aproximado numérico-literal*  
  
 *exato numérico-literal* :: = *inteiro não assinado* [*período*[*inteiro não assinado*]] *&#124; Períoda inteira não assinada*  
  
 *sinal de* :: = *sinal de adição &#124; o sinal de subtração*  
  
 *literal aproximado de numérico* :: = *expoente mantissa E*  
  
 *mantissa* :: = *exato numérico-literal*  
  
 *expoente* :: = *inteiro assinado*  
  
 *inteiro assinado* :: = [*sinal*] *inteiro não assinado*  
  
 *inteiro não assinado* :: = *dígitos...*  
  
 *sinal de adição* :: =*+*  
  
 *sinal de menos* :: = -  
  
 *Dígito* :: = 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; 0  
  
 *período* :: =.

