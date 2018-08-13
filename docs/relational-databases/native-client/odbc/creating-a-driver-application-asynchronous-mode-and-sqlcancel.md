---
title: Modo assíncrono e SQLCancel | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client|ODBC
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
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
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: d387f7c6183017799845aeb748aa0b54da57c7f3
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39561256"
---
# <a name="creating-a-driver-application---asynchronous-mode-and-sqlcancel"></a>Criar um aplicativo de driver – Modo assíncrono e SQLCancel
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

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
  
 Às vezes um comando fica pendente por muito tempo. Se o aplicativo precisar cancelar o comando sem aguardar uma resposta, ele pode fazer isso chamando **SQLCancel** com a mesma instrução tratar do comando pendente. Esta é a única vez **SQLCancel** deve ser usado. Alguns programadores usam **SQLCancel** quando eles têm parte do processamento por um resultado definido e quiser cancelar o restante do conjunto de resultados. [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md) ou [SQLCloseCursor](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md) deve ser usado para cancelar o restante de um conjunto de resultados, não **SQLCancel**.  
  
## <a name="see-also"></a>Consulte também  
 [Criando um aplicativo de driver ODBC do SQL Server Native Client](../../../relational-databases/native-client/odbc/creating-a-driver-application.md)  
  
  
