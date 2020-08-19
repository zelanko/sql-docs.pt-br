---
description: Exemplo de diagnóstico do Gerenciador de Driver
title: Exemplo de diagnóstico do Gerenciador de driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC], diagnostic messages
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: af8f2d35-d1bf-495c-af25-630654542b7d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b1d852436600ffb3ce5258e731d23c4579bf8964
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483059"
---
# <a name="driver-manager-diagnostic-example"></a>Exemplo de diagnóstico do Gerenciador de Driver
O Gerenciador de driver também pode gerar mensagens de diagnóstico. Por exemplo, se um aplicativo passasse uma opção de direção inválida para **SQLDataSources**, o Gerenciador de driver poderá Formatar e retornar os seguintes valores de **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY103"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Driver Manager]Direction option out of range"  
```  
  
 Como o erro ocorreu no Gerenciador de driver, ele adicionou prefixos à mensagem de diagnóstico para seu fornecedor ([Microsoft]) e seu identificador ([ODBC Driver Manager]).
