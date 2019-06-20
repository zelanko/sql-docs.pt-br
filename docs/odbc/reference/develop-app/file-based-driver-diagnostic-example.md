---
title: Exemplo de diagnóstico de Driver baseado em arquivo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- file-based driver diagnostic [ODBC]
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: 0575fccd-4641-478d-a3cc-5a764e35bae2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: decb09098cee4b9ab6473e3c622b9917a89e9b09
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63061524"
---
# <a name="file-based-driver-diagnostic-example"></a>Exemplo de diagnóstico de driver baseado em arquivo
Um driver com base em arquivo atua como um driver ODBC e como uma fonte de dados. Portanto ele pode gerar erros e avisos, tanto como um componente em uma conexão ODBC e como uma fonte de dados. Como também é o componente que faz interface com o Gerenciador de Driver, formata e retorna os argumentos para **SQLGetDiagRec**.  
  
 Por exemplo, se um driver Microsoft® para dBASE não foi possível alocar memória suficiente, ele pode retornar os seguintes valores **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY001"  
Native Error:      42052  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver]Unable to allocate sufficient memory."  
```  
  
 Como esse erro não era relacionado à fonte de dados, o driver adicionado somente prefixos para a mensagem de diagnóstico para o fornecedor ([Microsoft]) e o driver ([ODBC Driver do dBASE]).  
  
 Se o driver não foi possível encontrar o arquivo Employee. dbf, ela pode retornar os seguintes valores **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1305  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver][dBASE]No such table or object"  
```  
  
 Como esse erro foi relacionado à fonte de dados, o driver adicionado o formato de arquivo da fonte de dados ([dBASE]) como um prefixo para a mensagem de diagnóstico. Como o driver também foi o componente que interagir com a fonte de dados, ele adicionou prefixos para o fornecedor ([Microsoft]) e o driver ([ODBC Driver do dBASE]).
