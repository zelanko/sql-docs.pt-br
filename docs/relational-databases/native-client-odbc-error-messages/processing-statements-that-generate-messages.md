---
title: Processando instruções que geram mensagens | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- PRINT statement
- messages [ODBC], statements generating messages
- statements [ODBC], message generation
- errors [ODBC], statements generating messages
- SQL Server Native Client ODBC driver, errors
- STATISTICS IO option
- STATISTICS TIME option
- DBCC statements
- SQLExecute function
- RAISERROR statement
- SQLGetDiagRec function
- ODBC error handling, statements generating messages
- SQLExecDirect function
ms.assetid: 672ebdc5-7fa1-4ceb-8d52-fd25ef646654
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5ff2141bb8b84fa27d9aefe00f3a48281d5c017e
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2018
ms.locfileid: "35703737"
---
# <a name="processing-statements-that-generate-messages"></a>Processando instruções que geram mensagens
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  As opções STATISTICS TIME e STATISTICS IO da instrução SET do [!INCLUDE[tsql](../../includes/tsql-md.md)] são usadas para obter informações que auxiliem a diagnosticar consultas de longa execução. As versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também dão suporte à opção SHOWPLAN para analisar planos de consulta. Um aplicativo ODBC pode definir essas opções executando as seguintes instruções:  
  
```  
SQLExecDirect(hstmt, "SET SHOWPLAN ON", SQL_NTS);  
SQLExecDirect(hstmt, "SET STATISTICS TIME ON", SQL_NTS90  
);  
SQLExecDirect(hstmt, "SET STATISTICS IO ON", SQL_NTS);  
```  
  
 Quando SET STATISTICS TIME ou SET SHOWPLAN forem ON, **SQLExecute** e **SQLExecDirect** retornar SQL_SUCCESS_WITH_INFO e, nesse ponto, o aplicativo pode recuperar a saída SHOWPLAN ou STATISTICS TIME chamando **SQLGetDiagRec** até ele retornar SQL_NO_DATA. Cada linha de dados de SHOWPLAN volta no formato:  
  
```  
szSqlState="01000", *pfNativeError=6223,  
szErrorMsg="[Microsoft][SQL Server Native Client][SQL Server]   
              Table Scan"  
```  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versão 7.0 substituiu a opção SHOWPLAN por SHOWPLAN_ALL e SHOWPLAN_TEXT, que retornam a saída como um conjunto de resultados e não um conjunto de mensagens.  
  
 Cada linha de STATISTICS TIME volta no formato:  
  
```  
szSqlState="01000", *pfNativeError= 3613,  
szErrorMsg="[Microsoft][SQL Server Native Client][SQL Server]  
   SQL Server Parse and Compile Time: cpu time = 0 ms."  
```  
  
 A saída de SET STATISTICS IO não está disponível até o final de um conjunto de resultados. Para obter estatísticas de e/s de saída, o aplicativo chama **SQLGetDiagRec** no momento **SQLFetch** ou [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) retorna SQL_NO_DATA. A saída de STATISTICS IO volta no formato:  
  
```  
szSqlState="01000", *pfNativeError= 3615,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   Table: testshow  scan count 1,  logical reads: 1,  
   physical reads: 0."  
```  
  
## <a name="using-dbcc-statements"></a>Usando instruções DBCC  
 As instruções DBCC retornam seus dados como mensagens, não como conjuntos de resultados. **SQLExecDirect** ou **SQLExecute** retornar SQL_SUCCESS_WITH_INFO e o aplicativo recupera a saída chamando **SQLGetDiagRec** até ele retornar SQL_NO_DATA.  
  
 Por exemplo, a instrução a seguir retorna SQL_SUCCESS_WITH_INFO:  
  
```  
SQLExecDirect(hstmt, "DBCC CHECKTABLE(Authors)", SQL_NTS);  
```  
  
 Chamadas para **SQLGetDiagRec** retornar:  
  
```  
szSqlState = "01000", *pfNativeError = 2536,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   Checking authors"  
szSqlState = "01000", *pfNativeError = 2579,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   The total number of data pages in this table is 1."  
szSqlState = "01000", *pfNativeError = 7929,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   Table has 23 data rows."  
szSqlState = "01000", *pfNativeError = 2528  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   DBCC execution completed. If DBCC printed error messages,  
   see your System Administrator."  
```  
  
## <a name="using-print-and-raiserror-statements"></a>Usando as instruções PRINT e RAISERROR  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] Instruções PRINT e RAISERROR também retornam dados chamando **SQLGetDiagRec**. Instruções PRINT fazem a execução da instrução SQL retornar SQL_SUCCESS_WITH_INFO e uma chamada subsequente para **SQLGetDiagRec** retorna um *SQLState* igual a 01000. Um RAISERROR com uma severidade de dez ou menor se comporta da mesma forma que PRINT. Um RAISERROR com severidade de 11 ou maior faz com que a execução retornar SQL_ERROR e uma chamada subsequente para **SQLGetDiagRec** retorna *SQLState* 42000. Por exemplo, a instrução a seguir retorna SQL_SUCCESS_WITH_INFO:  
  
```  
SQLExecDirect (hstmt, "PRINT  'Some message' ", SQL_NTS);  
```  
  
 Chamando **SQLGetDiagRec** retorna:  
  
```  
szSQLState = "01000", *pfNative Error = 0,  
szErrorMsg= "[Microsoft] [SQL Server Native Client][SQL Server]  
   Some message"  
```  
  
 A instrução a seguir retorna SQL_SUCCESS_WITH_INFO:  
  
```  
SQLExecDirect (hstmt, "RAISERROR ('Sample error 1.', 10, -1)",  
   SQL_NTS)  
```  
  
 Chamando **SQLGetDiagRec** retorna:  
  
```  
szSQLState = "01000", *pfNative Error = 50000,  
szErrorMsg= "[Microsoft] [SQL Server Native Client][SQL Server]  
   Sample error 1."  
```  
  
 A instrução a seguir retorna SQL_ERROR:  
  
```  
SQLExecDirect (hstmt, "RAISERROR ('Sample error 2.', 11, -1)", SQL_NTS)  
```  
  
 Chamando **SQLGetDiagRec** retorna:  
  
```  
szSQLState = "42000", *pfNative Error = 50000,  
szErrorMsg= "[Microsoft] [SQL Server Native Client][SQL Server]  
   Sample error 2."  
```  
  
 O tempo da chamada **SQLGetDiagRec** é crítica quando a saída de instruções PRINT ou RAISERROR está incluída em um conjunto de resultados. A chamada para **SQLGetDiagRec** para recuperar o PRINT ou RAISERROR saída deve ser feita imediatamente após a instrução que recebe SQL_ERROR ou SQL_SUCCESS_WITH_INFO. Isto é direto quando apenas uma única instrução SQL é executada, como nos exemplos acima. Nesses casos, a chamada para **SQLExecDirect** ou **SQLExecute** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO e **SQLGetDiagRec** , em seguida, pode ser chamado. Isso é menos direto quando ao codificar loops para tratar a saída de um lote de instruções SQL ou ao executar procedimentos armazenados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Neste caso, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna um conjunto de resultados para cada instrução SELECT executada em um lote ou um procedimento armazenado. Se o lote ou o procedimento contiver instruções PRINT ou RAISERROR, sua saída será intercalada com os conjuntos de resultados da instrução SELECT. Se a primeira instrução no lote ou procedimento for PRINT ou RAISERROR, o **SQLExecute** ou **SQLExecDirect** retorna SQL_SUCCESS_WITH_INFO ou SQL_ERROR e o aplicativo precisa chamar **SQLGetDiagRec** até ele retornar SQL_NO_DATA para recuperar as informações de PRINT ou RAISERROR.  
  
 Se a instrução PRINT ou RAISERROR vem depois de uma instrução SQL (como uma instrução SELECT), as informações de PRINT ou RAISERROR são retornadas quando [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)posições no resultado definido que contém o erro. **SQLMoreResults** retorna SQL_SUCCESS_WITH_INFO ou SQL_ERROR, dependendo da severidade da mensagem. As mensagens são recuperadas chamando **SQLGetDiagRec** até ele retornar SQL_NO_DATA.  
  
## <a name="see-also"></a>Consulte também  
 [Tratando de erros e mensagens](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
