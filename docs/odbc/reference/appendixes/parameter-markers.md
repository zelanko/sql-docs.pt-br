---
title: Marcadores de parâmetro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- parameter markers [ODBC]
ms.assetid: 07213d04-cd31-45fd-a8c8-2e16e09eeaf4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 833e2740e54f07701fb66a894bb5e4798c4a42e2
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52516399"
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
