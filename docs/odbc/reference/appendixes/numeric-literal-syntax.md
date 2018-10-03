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
manager: craigg
ms.openlocfilehash: 18b1c144e84bf0be5aaeb68b66660f7bc7865ade
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47601534"
---
# <a name="numeric-literal-syntax"></a>Sintaxe literal numérica
A sintaxe a seguir é usada para literais numéricos no ODBC:  
  
 *numérico literal* :: = *literal assinados de numeric &#124; literal não assinado de numérico*  
  
 *literal assinados de numérico* :: = [*sinal*] *literal não assinado de numérico*  
  
 *literal não assinado de numérico* :: = *exato numérico-literal &#124; literal aproximar de numérico*  
  
 *exato numérico-literal* :: = *inteiro não assinado* [*período*[*inteiro sem sinal*]]  *&#124;Períoda inteira não assinada*  
  
 *sinal* :: = *sinal &#124; sinal de subtração*  
  
 *aproximar-numeric-literal* :: = *expoente mantissa E*  
  
 *mantissa* :: = *literal exato de numérico*  
  
 *expoente* :: = *inteiro assinado*  
  
 *inteiro assinado* :: = [*sinal*] *inteiro não assinado*  
  
 *inteiro sem sinal* :: = *dígito...*  
  
 *sinal de adição* :: = *+*  
  
 *sinal de subtração* :: = -  
  
 *Dígito* :: = 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; 0  
  
 *período* :: =.
