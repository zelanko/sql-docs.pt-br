---
title: Sequências de Escape de intervalo | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- interval literals [ODBC]
- escape sequences [ODBC], interval
- ODBC escape sequences [ODBC], interval
ms.assetid: 303e8dab-8f13-4fa5-857f-15cc1f75bdd6
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a9ef232521850dbf6007942d7758ce2b5820a335
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="interval-escape-sequences"></a>Sequências de Escape de intervalo
ODBC usa sequências de escape para literais de intervalo. A sintaxe dessa sequência de escape é da seguinte maneira:  
  
 {*intervalo literal*}  
  
 Para obter a sintaxe BNF de *intervalo literal*, consulte o [sintaxe de literais de intervalo](../../../odbc/reference/appendixes/interval-literal-syntax.md) seção mais adiante neste apêndice.  
  
 A sequência de escape literal do intervalo é suportada se os tipos de dados de intervalo são suportados pela fonte de dados. Um aplicativo deve chamar **SQLGetTypeInfo** para determinar se esses tipos de dados têm suporte.
