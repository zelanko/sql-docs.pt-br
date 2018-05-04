---
title: Funções numéricas (Driver ODBC do Visual FoxPro) | Microsoft Docs
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
- ODBC numeric functions [ODBC]
- Visual FoxPro ODBC driver [ODBC], numeric functions
- numeric functions [ODBC]
- FoxPro ODBC driver [ODBC], numeric functions
ms.assetid: 7caab48e-cbb5-4bbc-a09b-5cf902e5bc45
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 42d494823cf1792bbec78ff3de1d70d4f8f75046
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="numeric-functions-visual-foxpro-odbc-driver"></a>Funções numéricas (Driver ODBC do Visual FoxPro)
A tabela a seguir descreve as funções de numérica ODBC com suporte do Visual FoxPro ODBC Driver; Quando a gramática do Visual FoxPro para a mesma função difere da sintaxe de ODBC, o Visual FoxPro equivalente é listado.  
  
|Gramática ODBC|Gramática do Visual FoxPro|  
|------------------|---------------------------|  
|ABS *(numeric_exp)*||  
|ACOS *(float_exp)*||  
|ASIN *(float_exp)*||  
|ATAN *(float_exp)*||  
|ATAN2 *(float_exp1, float_exp2)*|ATN2 (*float_exp1, float_exp2*)|  
|CEILING *(numeric_exp)*||  
|COS *(float_exp)*||  
|COT *(float_exp)*||  
|GRAUS *(numeric_exp)*|RTOD *(numeric_exp)*|  
|EXP *(float_exp)*||  
|FLOOR *(numeric_exp)*||  
|LOG *(float_exp)*||  
|LOG10 *(float_exp)*||  
|MOD *(integer_exp1, integer_exp2)*||  
|PI *)*||  
|RADIANOS *(numeric_exp)*|DTOR *(numeric_exp)*|  
|RAND *([integer_exp])*||  
|ROUND *(numeric_exp, integer_exp)*||  
|SINAL de *(numeric_exp)*||  
|SIN *(float_exp)*||  
|SQRT *(float_exp)*||  
|TAN *(float_exp)*||  
  
 Não há suporte para as funções numéricas seguintes:  
  
 ENERGIA *(numeric_exp, integer_exp)*  
  
 Truncar *(numeric_exp, integer_exp)*
