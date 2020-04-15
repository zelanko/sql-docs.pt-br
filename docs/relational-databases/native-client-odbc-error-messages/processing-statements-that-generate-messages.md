---
title: Processamento de declarações que geram mensagens | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9820e202f5032423292c4306aa63b175bce550b6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304687"
---
# <a name="processing-statements-that-generate-messages"></a>Processando instruções que geram mensagens
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  As opções STATISTICS TIME e STATISTICS IO da instrução SET do [!INCLUDE[tsql](../../includes/tsql-md.md)] são usadas para obter informações que auxiliem a diagnosticar consultas de longa execução. As versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também dão suporte à opção SHOWPLAN para analisar planos de consulta. Um aplicativo ODBC pode definir essas opções executando as seguintes instruções:  
  
```  
SQLExecDirect(hstmt, "SET SHOWPLAN ON", SQL_NTS);  
SQLExecDirect(hstmt, "SET STATISTICS TIME ON", SQL_NTS90  
);  
SQLExecDirect(hstmt, "SET STATISTICS IO ON", SQL_NTS);  
```  
  
 Quando set STATISTICS TIME ou SET SHOWPLAN estiverem ligados, **SQLExecute** e **SQLExecDirect** retornarSQL_SUCCESS_WITH_INFO e, nesse ponto, o aplicativo pode recuperar a saída SHOWPLAN ou STATISTICS TIME ligando para **SQLGetDiagRec** até que ele retorne SQL_NO_DATA. Cada linha de dados de SHOWPLAN volta no formato:  
  
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
  
 A saída de SET STATISTICS IO não está disponível até o final de um conjunto de resultados. Para obter a saída de IO estatístico, o aplicativo chama **SQLGetDiagRec** no momento em que **SQLFetchScroll** retorna SQL_NO_DATA. [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) A saída de STATISTICS IO volta no formato:  
  
```  
szSqlState="01000", *pfNativeError= 3615,  
szErrorMsg="[Microsoft][ SQL Server Native Client][SQL Server]  
   Table: testshow  scan count 1,  logical reads: 1,  
   physical reads: 0."  
```  
  
## <a name="using-dbcc-statements"></a>Usando instruções DBCC  
 As instruções DBCC retornam seus dados como mensagens, não como conjuntos de resultados. **SQLExecDirect** ou **SQLExecute** retorno SQL_SUCCESS_WITH_INFO, e o aplicativo recupera a saída ligando para **SQLGetDiagRec** até que ele retorne SQL_NO_DATA.  
  
 Por exemplo, a instrução a seguir retorna SQL_SUCCESS_WITH_INFO:  
  
```  
SQLExecDirect(hstmt, "DBCC CHECKTABLE(Authors)", SQL_NTS);  
```  
  
 Chamadas para **retorno do SQLGetDiagRec:**  
  
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
 [!INCLUDE[tsql](../../includes/tsql-md.md)]As instruções PRINT e RAISERROR também retornam dados ligando para **sqlGetDiagRec**. As demonstrações print fazem com que a execução da declaração SQL retorne SQL_SUCCESS_WITH_INFO, e uma chamada subseqüente para **o SQLGetDiagRec** retorna um *SQLState* de 01000. Um RAISERROR com uma severidade de dez ou menor se comporta da mesma forma que PRINT. Um ERRO RAIS com uma gravidade de 11 ou mais faz com que a execução retorne SQL_ERROR, e uma chamada subseqüente para **SQLGetDiagRec** retorna *SQLState* 42000. Por exemplo, a instrução a seguir retorna SQL_SUCCESS_WITH_INFO:  
  
```  
SQLExecDirect (hstmt, "PRINT  'Some message' ", SQL_NTS);  
```  
  
 Chamando **o retorno do SQLGetDiagRec:**  
  
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
  
 Chamando **o retorno do SQLGetDiagRec:**  
  
```  
szSQLState = "01000", *pfNative Error = 50000,  
szErrorMsg= "[Microsoft] [SQL Server Native Client][SQL Server]  
   Sample error 1."  
```  
  
 A instrução a seguir retorna SQL_ERROR:  
  
```  
SQLExecDirect (hstmt, "RAISERROR ('Sample error 2.', 11, -1)", SQL_NTS)  
```  
  
 Chamando **o retorno do SQLGetDiagRec:**  
  
```  
szSQLState = "42000", *pfNative Error = 50000,  
szErrorMsg= "[Microsoft] [SQL Server Native Client][SQL Server]  
   Sample error 2."  
```  
  
 O tempo de chamada **sqlGetDiagRec** é crítico quando a saída das instruções PRINT ou RAISERROR é incluída em um conjunto de resultados. A chamada para **sqlGetDiagRec** para recuperar a saída PRINT ou RAISERROR deve ser feita imediatamente após a declaração que recebe SQL_ERROR ou SQL_SUCCESS_WITH_INFO. Isto é direto quando apenas uma única instrução SQL é executada, como nos exemplos acima. Nesses casos, a chamada para **SQLExecDirect** ou **SQLExecute** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO e **SQLGetDiagRec** pode então ser chamada. Isso é menos direto quando ao codificar loops para tratar a saída de um lote de instruções SQL ou ao executar procedimentos armazenados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Neste caso, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna um conjunto de resultados para cada instrução SELECT executada em um lote ou um procedimento armazenado. Se o lote ou o procedimento contiver instruções PRINT ou RAISERROR, sua saída será intercalada com os conjuntos de resultados da instrução SELECT. Se a primeira declaração no lote ou procedimento for um PRINT ou RAISERROR, o **SQLExecute** ou **O SQLExecDirect** retornarSQL_SUCCESS_WITH_INFO ou SQL_ERROR, e o aplicativo precisar ligar para **o SQLGetDiagRec** até que ele retorne SQL_NO_DATA para recuperar as informações DE PRINT ou RAISERROR.  
  
 Se a declaração PRINT ou RAISERROR vier após uma declaração SQL (como uma declaração SELECT), então as informações PRINT ou RAISERROR serão retornadas quando o [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)for colocado no conjunto de resultados que contém o erro. **SQLMoreResults** retorna SQL_SUCCESS_WITH_INFO ou SQL_ERROR dependendo da gravidade da mensagem. As mensagens são recuperadas ligando para **sqlGetDiagRec** até que ela retorne SQL_NO_DATA.  
  
## <a name="see-also"></a>Consulte Também  
 [Tratando de erros e mensagens](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
