---
title: "Exemplo de diagnóstico do Gerenciador de driver | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- driver manager [ODBC], diagnostic messages
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: af8f2d35-d1bf-495c-af25-630654542b7d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3f373fe012c2b791329fea35ca853021e70274eb
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="driver-manager-diagnostic-example"></a>Exemplo de diagnóstico do Gerenciador de driver
O Gerenciador de Driver também pode gerar mensagens de diagnóstico. Por exemplo, se um aplicativo passada uma opção de direção inválida para **SQLDataSources**, o Gerenciador de Driver pode formatar e retornar os seguintes valores de **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY103"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Driver Manager]Direction option out of range"  
```  
  
 Devido ao erro no Gerenciador de Driver, adicionado prefixos à mensagem de diagnóstico para seu fornecedor ([Microsoft]) e seu identificador ([ODBC Driver Manager]).
