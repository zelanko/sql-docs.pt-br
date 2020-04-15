---
title: Marcadores de parâmetro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- parameter markers [ODBC]
ms.assetid: 07213d04-cd31-45fd-a8c8-2e16e09eeaf4
author: David-Engel
ms.author: v-daenge
ms.reviewer: ''
ms.openlocfilehash: 132473de586094f79dd34c999d44f6dd59aefaef
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303567"
---
# <a name="parameter-markers"></a>Marcadores de parâmetro
De acordo com a especificação SQL-92, um aplicativo não pode colocar marcadores de parâmetros nos seguintes locais. Para obter uma lista mais abrangente, consulte a especificação SQL-92.  
  
-   Em uma **lista SELECT**  
  
-   Como ambas as *expressões* em um *predicado de comparação*  
  
-   Como ambos os operands de um operador binário  
  
-   Como o primeiro e o segundo operands de uma operação **BETWEEN**  
  
-   Como o primeiro e o terceiro operands de uma operação **BETWEEN**  
  
-   Como a expressão e o primeiro valor de uma operação **IN**  
  
-   Como o operand de uma unary + ou - operação  
  
-   Como o argumento de uma *referência de função de set*  
  
 Para obter mais informações sobre marcadores de parâmetros, consulte a especificação SQL-92. Para obter mais informações sobre parâmetros, consulte [Parâmetros de declaração](../../../odbc/reference/develop-app/statement-parameters.md).
