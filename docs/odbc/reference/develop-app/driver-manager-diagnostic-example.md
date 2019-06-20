---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6ad253c2d0603846d6d1f795f6115e7bb727b3da
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63238049"
---
# <a name="driver-manager-diagnostic-example"></a>Exemplo de diagnóstico do Gerenciador de Driver
O Gerenciador de Driver também pode gerar mensagens de diagnóstico. Por exemplo, se um aplicativo passou uma opção de direção inválida para **SQLDataSources**, o Gerenciador de Driver pode formatar e retornar os seguintes valores de **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY103"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Driver Manager]Direction option out of range"  
```  
  
 Como o erro ocorreu no Gerenciador de Driver, adicionado prefixos para a mensagem de diagnóstico para seu fornecedor ([Microsoft]) e seu identificador ([ODBC Driver Manager]).
