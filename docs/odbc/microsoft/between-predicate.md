---
title: ENTRE o predicado | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- BETWEEN predicate [ODBC]
- SQL grammar [ODBC], between predicate
ms.assetid: 0cc7464b-d788-4720-98d8-411e1169185f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 55c86eaca6c79a3e5811223f58a78a9452986800
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="between-predicate"></a>ENTRE o predicado
A sintaxe:  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 retornará true se somente *expression1* é maior que ou igual a *expression2* e *expression1* é menor que ou igual a *expression3*.  
  
 A semântica dessa sintaxe é diferente para os Drivers de banco de dados de área de trabalho e o Microsoft Jet. No SQL do Microsoft Jet, *expression2* pode ser maior que *expression3* para que a instrução retornará TRUE somente se *expression1* é maior que ou igual a *expression3*, e *expression1* é menor que ou igual a *expression2*.
