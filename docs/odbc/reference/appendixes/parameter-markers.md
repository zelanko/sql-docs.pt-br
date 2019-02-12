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
author: MightyPen
ms.author: genemi
ms.reviewer: ''
manager: craigg
ms.openlocfilehash: cda6719eb46a4a05222bd54062e6cab98459d7dc
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56042877"
---
# <a name="parameter-markers"></a>Marcadores de parâmetro
Acordo com a especificação SQL-92, um aplicativo não é possível colocar os marcadores de parâmetro nos seguintes locais. Para obter uma lista mais abrangente, consulte a especificação SQL-92.  
  
-   Em um **selecionar** lista  
  
-   Como ambos *expressões* em um *predicado de comparação*  
  
-   Como ambos os operandos de um operador binário  
  
-   Como ambos os operandos primeiros e segundo de um **BETWEEN** operação  
  
-   Como o primeiro e o terceiro operandos de uma **BETWEEN** operação  
  
-   Como a expressão e o primeiro valor de uma **IN** operação  
  
-   Como o operando de um unário + ou - operação  
  
-   Como o argumento de um *referência da função de conjunto*  
  
 Para obter mais informações sobre marcadores de parâmetro, consulte a especificação SQL-92. Para obter mais informações sobre parâmetros, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md).
