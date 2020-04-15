---
title: Exemplo de diagnóstico do driver manager | Microsoft Docs
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
ms.openlocfilehash: 839095e5544cab73cdddd4f4b17a3d8d52136c9c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305807"
---
# <a name="driver-manager-diagnostic-example"></a>Exemplo de diagnóstico do Gerenciador de Driver
O Driver Manager também pode gerar mensagens de diagnóstico. Por exemplo, se um aplicativo passou uma opção de direção inválida para **SQLDataSources,** o Gerenciador de driver pode formatar e retornar os seguintes valores do **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY103"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Driver Manager]Direction option out of range"  
```  
  
 Como o erro ocorreu no Driver Manager, ele adicionou prefixos à mensagem de diagnóstico para seu fornecedor ([Microsoft]) e seu identificador ([ODBC Driver Manager]).
