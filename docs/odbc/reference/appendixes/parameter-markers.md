---
description: Marcadores de parâmetro
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
ms.openlocfilehash: a585fb983a8f1662cdd42d361f106a76bfd47cb6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483229"
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
