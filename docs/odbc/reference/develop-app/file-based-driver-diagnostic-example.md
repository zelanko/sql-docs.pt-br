---
title: Exemplo de diagnóstico de driver baseado em arquivo | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6f09e4f4758b6276836b08f02b24fb31dd1fadc7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305634"
---
# <a name="file-based-driver-diagnostic-example"></a>Exemplo de diagnóstico de driver baseado em arquivo
Um driver baseado em arquivos atua tanto como um driver ODBC quanto como uma fonte de dados. Portanto, pode gerar erros e avisos tanto como um componente em uma conexão ODBC quanto como fonte de dados. Como também é o componente que faz interface com o Driver Manager, ele formata e retorna argumentos para **SQLGetDiagRec**.  
  
 Por exemplo, se um driver ® Microsoft para dBASE não puder alocar memória suficiente, ele poderá retornar os seguintes valores do **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY001"  
Native Error:      42052  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver]Unable to allocate sufficient memory."  
```  
  
 Como esse erro não estava relacionado à fonte de dados, o driver adicionou apenas prefixos à mensagem de diagnóstico para o fornecedor ([Microsoft]) e para o driver ([Driver odBC dBASE]).  
  
 Se o driver não conseguiu encontrar o arquivo Employee.dbf, ele pode retornar os seguintes valores do **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1305  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver][dBASE]No such table or object"  
```  
  
 Como esse erro estava relacionado à fonte de dados, o driver adicionou o formato de arquivo da fonte de dados ([dBASE]) como um prefixo para a mensagem de diagnóstico. Como o driver também era o componente que interagia com a fonte de dados, ele adicionava prefixos para o fornecedor ([Microsoft]) e o driver ([ODBC dBASE Driver]).
