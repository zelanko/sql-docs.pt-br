---
title: Marcadores de parâmetro | Microsoft Docs
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
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- parameter markers [ODBC]
ms.assetid: 07213d04-cd31-45fd-a8c8-2e16e09eeaf4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c307c188deb2b268174130274f665a168aff2a88
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="parameter-markers"></a>Marcadores de parâmetro
Acordo com a especificação de SQL-92, um aplicativo não pode colocar marcadores de parâmetro nos seguintes locais. Para obter uma lista mais completa, consulte a especificação de SQL-92.  
  
-   Em um **selecione** lista  
  
-   Como ambos *expressões* em um *predicado de comparação*  
  
-   Como ambos os operandos de um operador binário  
  
-   Como ambos os operandos de primeiro e segundo de um **entre** operação  
  
-   Como o primeiro e o terceiro operandos de um **entre** operação  
  
-   Como a expressão e o primeiro valor de uma **IN** operação  
  
-   Como o operando de um unário + ou -operação  
  
-   Como o argumento de um *referência de função de conjunto*  
  
 Para obter mais informações sobre os marcadores de parâmetro, consulte a especificação de SQL-92. Para obter mais informações sobre parâmetros, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md).
