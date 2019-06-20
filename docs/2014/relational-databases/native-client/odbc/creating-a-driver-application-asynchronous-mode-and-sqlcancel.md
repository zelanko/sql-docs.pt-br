---
title: Modo assíncrono e SQLCancel | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- asynchronous operations [SQL Server Native Client]
- SQLCancel function
- SQLSetConnectAttr function
- SQL Server Native Client, asynchronous operations
- ODBC functions
- ODBC applications, asynchronous operations
- SQL Server Native Client ODBC driver, asynchronous mode
ms.assetid: f31702a2-df76-4589-ac3b-da5412c03dc2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3a4ec4e5d7575fdf5d915c8209999e1285fa79aa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63144317"
---
# <a name="asynchronous-mode-and-sqlcancel"></a>Modo assíncrono e SQLCancel
  Algumas funções ODBC podem operar de forma síncrona ou assíncrona. O aplicativo pode habilitar operações assíncronas para um identificador de instrução ou um identificador de conexão. Se a opção for definida para um identificador de conexão, ela afetará todos os identificadores de instrução do identificador de conexão. O aplicativo usa as seguintes instruções para habilitar ou desabilitar operações assíncronas:  
  
```  
SQLSetConnectAttr(hdbc, SQL_ATTR_ASYNC_ENABLE,  
                        SQL_ASYNC_ENABLE_ON, SQL_IS_INTEGER);  
SQLSetConnectAttr(hdbc, SQL_ATTR_ASYNC_ENABLE,  
                        SQL_ASYNC_ENABLE_OFF, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ASYNC_ENABLE,  
                        SQL_ASYNC_ENABLE_ON, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ASYNC_ENABLE,  
                        SQL_ASYNC_ENABLE_OFF, SQL_IS_INTEGER);  
```  
  
 Quando um aplicativo chama uma função ODBC no modo síncrono, o driver não retorna o controle para o aplicativo antes de ser notificado que o servidor concluiu o comando.  
  
 Na operação assíncrona, o driver retorna o controle para o aplicativo, mesmo antes de enviar o comando ao servidor. O driver define o código de retorno como SQL_STILL_EXECUTING. O aplicativo poderá, então, executar outro trabalho.  
  
 Quando o aplicativo testa para concluir o comando, faz a mesma chamada de função com os mesmos parâmetros para o driver. Se o driver ainda não tiver recebido uma resposta do servidor, novamente retornará SQL_STILL_EXECUTING. O aplicativo deve testar o comando periodicamente até que o código de retorno seja diferente de SQL_STILL_EXECUTING. Quando o aplicativo obtiver algum outro código de retorno, até mesmo SQL_ERROR, ele poderá determinar que o comando foi concluído.  
  
 Às vezes um comando fica pendente por muito tempo. Se o aplicativo precisar cancelar o comando sem aguardar uma resposta, ele pode fazer isso chamando **SQLCancel** com a mesma instrução tratar do comando pendente. Esta é a única vez **SQLCancel** deve ser usado. Alguns programadores usam **SQLCancel** quando eles têm parte do processamento por um resultado definido e quiser cancelar o restante do conjunto de resultados. [SQLMoreResults](../../native-client-odbc-api/sqlmoreresults.md) ou [SQLCloseCursor](../../native-client-odbc-api/sqlclosecursor.md) deve ser usado para cancelar o restante de um conjunto de resultados, não **SQLCancel**.  
  
## <a name="see-also"></a>Consulte também  
 [Criando um aplicativo de driver ODBC do SQL Server Native Client](creating-a-driver-application.md)  
  
  
