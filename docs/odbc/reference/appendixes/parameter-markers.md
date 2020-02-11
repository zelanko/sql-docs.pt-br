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
ms.openlocfilehash: acb8d5f9687798bc0efa514ee8646b16140fcd36
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68100581"
---
# <a name="parameter-markers"></a>Marcadores de parâmetro
De acordo com a especificação do SQL-92, um aplicativo não pode posicionar os marcadores de parâmetro nos locais a seguir. Para obter uma lista mais abrangente, consulte a especificação do SQL-92.  
  
-   Em uma lista de **seleção**  
  
-   Como as duas *expressões* em um *predicado de comparação*  
  
-   Como ambos os operandos de um operador binário  
  
-   Como o primeiro e o segundo operandos de uma operação **between**  
  
-   Como o primeiro e terceiro operandos de uma operação **between**  
  
-   Como a expressão e o primeiro valor de uma operação **in**  
  
-   Como o operando de uma operação unário + or  
  
-   Como o argumento de uma *referência de set-Function*  
  
 Para obter mais informações sobre marcadores de parâmetro, consulte a especificação do SQL-92. Para obter mais informações sobre parâmetros, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md).
