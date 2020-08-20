---
description: Predicado BETWEEN
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
ms.openlocfilehash: 2f2283f5824e4be0c9702bfe8feef9fe3109849a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500379"
---
# <a name="between-predicate"></a>Predicado BETWEEN
A sintaxe:  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 retornará true somente se *expressão1* for maior ou igual a *expression2* e *expression1* for menor ou igual a *expression3*.  
  
 A semântica dessa sintaxe é diferente para os drivers do banco de dados da área de trabalho e o mecanismo do Microsoft Jet. No Microsoft Jet SQL, *expression2* pode ser maior que *expression3* , de modo que a instrução retornará true somente se *expressão1* for maior ou igual a *expression3*, e *expression1* for menor ou igual a *expression2*.
