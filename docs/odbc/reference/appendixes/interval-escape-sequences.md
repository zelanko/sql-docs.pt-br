---
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
ms.openlocfilehash: 9fe7f6941e9ec9fba8b6698faaa18a678732dd6f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304951"
---
# <a name="interval-escape-sequences"></a>Sequências de escape de intervalo
O ODBC usa sequências de escape para literais de intervalo. A sintaxe dessa sequência de escape é a seguinte:  
  
 {*Interval-literal*}  
  
 Para obter a sintaxe BNF do *Interval-literal*, consulte a seção [sintaxe de literal de intervalo](../../../odbc/reference/appendixes/interval-literal-syntax.md) mais adiante neste apêndice.  
  
 A sequência de escape de literal de intervalo terá suporte se os tipos de dados de intervalo forem suportados pela fonte de dados. Um aplicativo deve chamar **SQLGetTypeInfo** para determinar se esses tipos de dados têm suporte.
