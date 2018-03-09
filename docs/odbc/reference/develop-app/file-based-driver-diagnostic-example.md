---
title: "Exemplo de diagnóstico do Driver baseada em arquivo | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- file-based driver diagnostic [ODBC]
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: 0575fccd-4641-478d-a3cc-5a764e35bae2
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c8b4fab8c7d39acbffc73959ec06adb830716003
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="file-based-driver-diagnostic-example"></a>Exemplo de diagnóstico baseada em arquivo de Driver
Um driver baseada em arquivo atua como um driver ODBC e uma fonte de dados. Portanto, ele pode gerar erros e avisos, como um componente em uma conexão ODBC e como uma fonte de dados. Como também é o componente que faz interface com o Gerenciador de Driver, formatos e retorna os argumentos para **SQLGetDiagRec**.  
  
 Por exemplo, se um driver de Microsoft® para dBASE não foi possível alocar memória suficiente, ele pode retornar os seguintes valores de **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY001"  
Native Error:      42052  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver]Unable to allocate sufficient memory."  
```  
  
 Como esse erro não foi relacionado à fonte de dados, o driver somente adicionadas prefixos à mensagem de diagnóstico do fornecedor ([Microsoft]) e o driver ([ODBC Driver dBASE]).  
  
 Se o driver não foi possível encontrar o arquivo Employee. dbf, ele pode retornar os seguintes valores de **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1305  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver][dBASE]No such table or object"  
```  
  
 Como esse erro foi relacionado à fonte de dados, o driver adicionado o formato de arquivo da fonte de dados ([dBASE]) como um prefixo para a mensagem de diagnóstica. Como o driver também era o componente de interagir com a fonte de dados, ele adicionou prefixos para o fornecedor ([Microsoft]) e o driver ([ODBC Driver dBASE]).
