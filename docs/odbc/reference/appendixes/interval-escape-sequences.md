---
title: Sequências de Escape de intervalo | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 81481db74d973da0e54bc6bf9e70550fa3cc0c81
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47767814"
---
# <a name="interval-escape-sequences"></a>Sequências de escape de intervalo
ODBC usa sequências de escape para literais de intervalo. A sintaxe dessa sequência de escape é da seguinte maneira:  
  
 {*literal de intervalo*}  
  
 Para obter a sintaxe BNF da *literal de intervalo*, consulte o [sintaxe Literal de intervalo](../../../odbc/reference/appendixes/interval-literal-syntax.md) seção mais adiante neste apêndice.  
  
 A sequência de escape de literal de intervalo tem suporte se os tipos de dados de intervalo têm suporte pela fonte de dados. Um aplicativo deve chamar **SQLGetTypeInfo** para determinar se esses tipos de dados têm suporte.
