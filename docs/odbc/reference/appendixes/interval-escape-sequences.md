---
description: Sequências de escape de intervalo
title: Sequências de escape de intervalo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interval literals [ODBC]
- escape sequences [ODBC], interval
- ODBC escape sequences [ODBC], interval
ms.assetid: 303e8dab-8f13-4fa5-857f-15cc1f75bdd6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e2ef792403352568ce5f8d92c07a5b0e1027b507
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483289"
---
# <a name="interval-escape-sequences"></a>Sequências de escape de intervalo
O ODBC usa sequências de escape para literais de intervalo. A sintaxe dessa sequência de escape é a seguinte:  
  
 {*Interval-literal*}  
  
 Para obter a sintaxe BNF do *Interval-literal*, consulte a seção [sintaxe de literal de intervalo](../../../odbc/reference/appendixes/interval-literal-syntax.md) mais adiante neste apêndice.  
  
 A sequência de escape de literal de intervalo terá suporte se os tipos de dados de intervalo forem suportados pela fonte de dados. Um aplicativo deve chamar **SQLGetTypeInfo** para determinar se esses tipos de dados têm suporte.
