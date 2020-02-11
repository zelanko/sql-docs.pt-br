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
ms.openlocfilehash: 1a0ac99729966acdcb03c2aab0175c34bba0c08a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138123"
---
# <a name="between-predicate"></a>Predicado BETWEEN
A sintaxe:  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 retornará true somente se *expressão1* for maior ou igual a *expression2* e *expression1* for menor ou igual a *expression3*.  
  
 A semântica dessa sintaxe é diferente para os drivers do banco de dados da área de trabalho e o mecanismo do Microsoft Jet. No Microsoft Jet SQL, *expression2* pode ser maior que *expression3* , de modo que a instrução retornará true somente se *expressão1* for maior ou igual a *expression3*, e *expression1* for menor ou igual a *expression2*.
