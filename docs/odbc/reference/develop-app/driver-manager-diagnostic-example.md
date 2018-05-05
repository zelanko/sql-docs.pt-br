---
title: Exemplo de diagnóstico do Gerenciador de driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC], diagnostic messages
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: af8f2d35-d1bf-495c-af25-630654542b7d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8c383dda247d3309ed38744609afb5ca12e3c38f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="driver-manager-diagnostic-example"></a>Exemplo de diagnóstico do Gerenciador de driver
O Gerenciador de Driver também pode gerar mensagens de diagnóstico. Por exemplo, se um aplicativo passada uma opção de direção inválida para **SQLDataSources**, o Gerenciador de Driver pode formatar e retornar os seguintes valores de **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY103"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Driver Manager]Direction option out of range"  
```  
  
 Devido ao erro no Gerenciador de Driver, adicionado prefixos à mensagem de diagnóstico para seu fornecedor ([Microsoft]) e seu identificador ([ODBC Driver Manager]).
