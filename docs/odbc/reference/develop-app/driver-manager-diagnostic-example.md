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
ms.openlocfilehash: 95392367b70af3eb820f0943af5dc668783a3fe5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68046966"
---
# <a name="driver-manager-diagnostic-example"></a>Exemplo de diagnóstico do Gerenciador de Driver
O Gerenciador de driver também pode gerar mensagens de diagnóstico. Por exemplo, se um aplicativo passasse uma opção de direção inválida para **SQLDataSources**, o Gerenciador de driver poderá Formatar e retornar os seguintes valores de **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY103"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Driver Manager]Direction option out of range"  
```  
  
 Como o erro ocorreu no Gerenciador de driver, ele adicionou prefixos à mensagem de diagnóstico para seu fornecedor ([Microsoft]) e seu identificador ([ODBC Driver Manager]).
