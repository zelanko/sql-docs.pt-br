---
title: ENTRE o predicado | Microsoft Docs
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
- BETWEEN predicate [ODBC]
- SQL grammar [ODBC], between predicate
ms.assetid: 0cc7464b-d788-4720-98d8-411e1169185f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e8daaa0e1c26f00acbff2e6f7788eab8ee5ac8ce
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="between-predicate"></a>ENTRE o predicado
A sintaxe:  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 retornará true se somente *expression1* é maior que ou igual a *expression2* e *expression1* é menor que ou igual a *expression3*.  
  
 A semântica dessa sintaxe é diferente para os Drivers de banco de dados de área de trabalho e o Microsoft Jet. No SQL do Microsoft Jet, *expression2* pode ser maior que *expression3* para que a instrução retornará TRUE somente se *expression1* é maior que ou igual a *expression3*, e *expression1* é menor que ou igual a *expression2*.
