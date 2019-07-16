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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138123"
---
# <a name="between-predicate"></a>Predicado BETWEEN
A sintaxe:  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 retornará true somente se *expression1* é maior que ou igual a *expression2* e *expression1* é menor que ou igual a *expression3*.  
  
 A semântica dessa sintaxe é diferente para os Drivers de banco de dados de área de trabalho e o mecanismo Microsoft Jet. No SQL do Microsoft Jet *expression2* pode ser maior que *expression3* para que a instrução retornará TRUE somente se *expression1* é maior que ou igual a *expression3*, e *expression1* é menor que ou igual a *expression2*.
