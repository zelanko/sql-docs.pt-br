---
title: Exemplo de diagnóstico de driver baseado em DBMS | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBMS-based driver diagnostic [ODBC]
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: a80d54b0-43ff-4dfd-b6cb-f4694a5ed765
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 117f43548d2b57233dea6f7423e6bad67b6233b0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304347"
---
# <a name="dbms-based-driver-diagnostic-example"></a>Exemplo de diagnóstico de driver baseado em DBMS
Um driver baseado em DBMS envia solicitações a um DBMS e retorna informações ao aplicativo através do Driver Manager. Como o driver é o componente que interage com o Driver Manager, ele formata e retorna argumentos para **SQLGetDiagRec**.  
  
 Por exemplo, se, usando SQL/Services, um driver Microsoft para Oracle Rdb encontrou um nome de cursor inválido, ele poderá retornar os seguintes valores do **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "34000"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver]Invalid cursor name: EMPLOYEE_CURSOR."  
```  
  
 Como o erro ocorreu no driver, ele adicionou prefixos à mensagem de diagnóstico para o fornecedor ([Microsoft]) e para o driver ([Driver ODBC Rdb]).  
  
 Se o DBMS não conseguiu encontrar a tabela EMPLOYEE, o driver pode formatar e retornar os seguintes valores do **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver][Rdb] %SQL-F-RELNOTDEF, Table EMPLOYEE "  
                  "is not defined in schema."  
```  
  
 Como o erro ocorreu na fonte de dados, o driver adicionou um prefixo para o identificador de origem de dados ([Rdb]) à mensagem de diagnóstico. Como o driver era o componente que interagia com a fonte de dados, ele adicionou prefixos para seu fornecedor ([Microsoft]) e identificador ([ODBC Rdb Driver]) à mensagem de diagnóstico.
