---
title: Predicado BETWEEN | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a4411345d790e64ae9fb21144a7d82ffe4cd45e8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63301954"
---
# <a name="between-predicate"></a>Predicado BETWEEN
A sintaxe:  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 retornará true somente se *expression1* é maior que ou igual a *expression2* e *expression1* é menor que ou igual a *expression3*.  
  
 A semântica dessa sintaxe é diferente para os Drivers de banco de dados de área de trabalho e o mecanismo Microsoft Jet. No SQL do Microsoft Jet *expression2* pode ser maior que *expression3* para que a instrução retornará TRUE somente se *expression1* é maior que ou igual a *expression3*, e *expression1* é menor que ou igual a *expression2*.
