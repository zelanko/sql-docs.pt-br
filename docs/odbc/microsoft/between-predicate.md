---
title: ENTRE Predicado | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- BETWEEN predicate [ODBC]
- SQL grammar [ODBC], between predicate
ms.assetid: 0cc7464b-d788-4720-98d8-411e1169185f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1f3ff800938574bec81e9cbb86839e014085a2a8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283846"
---
# <a name="between-predicate"></a>Predicado BETWEEN
A sintaxe:  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 retorna verdadeiro somente se *a expressão1* for maior ou igual à *expressão2* e a *expressão1* for menor ou igual à *expressão3*.  
  
 A semântica desta sintaxe é diferente para os Drivers de banco de dados de desktop e o motor Microsoft Jet. No Microsoft Jet SQL, *a expressão2* pode ser maior que a *expressão3* de modo que a declaração retorne TRUE somente se a *expressão1* for maior ou igual à *expressão3*, e *a expressão1* for menor ou igual à *expressão2*.
