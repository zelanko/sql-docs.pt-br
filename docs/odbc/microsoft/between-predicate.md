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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1f3ff800938574bec81e9cbb86839e014085a2a8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81283846"
---
# <a name="between-predicate"></a>Predicado BETWEEN
A sintaxe:  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 retornará true somente se *expressão1* for maior ou igual a *expression2* e *expression1* for menor ou igual a *expression3*.  
  
 A semântica dessa sintaxe é diferente para os drivers do banco de dados da área de trabalho e o mecanismo do Microsoft Jet. No Microsoft Jet SQL, *expression2* pode ser maior que *expression3* , de modo que a instrução retornará true somente se *expressão1* for maior ou igual a *expression3*, e *expression1* for menor ou igual a *expression2*.
