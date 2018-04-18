---
title: Processar códigos de retorno e parâmetros de saída (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-how-to
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- return codes [ODBC]
- output parameters [ODBC]
ms.assetid: 102ae1d0-973d-4e12-992c-d844bf05160d
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e9348b4be3341f3353dcc707ab5cc570e9d49c15
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="running-stored-procedures---process-return-codes-and-output-parameters"></a>Executando procedimentos armazenados - processar códigos de retorno e parâmetros de saída
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suporta a execução de procedimentos armazenados como procedimentos armazenados remotos. Executar um procedimento armazenado como um procedimento armazenado remoto permite que o driver e o servidor otimizem o desempenho da execução do procedimento.  
  
  Os procedimentos armazenados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem ter códigos de retorno e parâmetros de saída inteiros. Os códigos de retorno e parâmetros de saída são enviados no último pacote do servidor e não estão disponíveis para o aplicativo até que [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md) retorna SQL_NO_DATA. Se um erro for retornado por um procedimento armazenado, chame o SQLMoreResults para Avançar para o próximo resultado até que SQL_NO_DATA seja retornado.  
  
> [!IMPORTANT]  
>  Quando possível, use a Autenticação do Windows. Se a Autenticação do Windows não estiver disponível, solicite aos usuários que digitem suas credenciais em tempo de execução. Evite armazenar as credenciais em um arquivo. Se for necessário manter as credenciais, criptografe-as com a [Win32 crypto API](http://go.microsoft.com/fwlink/?LinkId=64532)(em inglês).  
  
### <a name="to-process-return-codes-and-output-parameters"></a>Para processar códigos de retorno e parâmetros de saída  
  
1.  Construa uma instrução SQL que use a sequência de escape ODBC CALL. A instrução deve usar marcadores de parâmetro para cada entrada/saída e parâmetro de saída, e também para o valor de retorno de procedimento (se houver).  
  
2.  Chamar [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) para cada entrada, entrada/saída e parâmetro de saída e para o procedimento retorna o valor (se houver).  
  
3.  Execute a instrução com **SQLExecDirect**.  
  
4.  Processe conjuntos de resultados até que **SQLFetch** ou **SQLFetchScroll** retorne SQL_NO_DATA e processando o último conjunto de resultados ou até que **SQLMoreResults** retorne SQL_NO_DATA. Nesse ponto, as variáveis associadas aos códigos de retorno e parâmetros de saída são preenchidas com valores de dados retornados.  
  
## <a name="example"></a>Exemplo  
 Este exemplo mostra como processar um código de retorno e um parâmetro de saída. Este exemplo não tem suporte em IA64. Esse exemplo foi desenvolvido para o ODBC versão 3.0 ou posterior.  
  
 Será necessária uma fonte de dados ODBC chamada AdventureWorks, cujo banco de dados padrão é o banco de dados de exemplo AdventureWorks. (Você pode baixar o banco de dados de exemplo AdventureWorks na página inicial de [Microsoft SQL Server Samples and Community Projects](http://go.microsoft.com/fwlink/?LinkID=85384) (em inglês)). Essa fonte de dados deve ser baseada no driver ODBC que é fornecido pelo sistema operacional (o nome do driver é "SQL Server"). Se você compilar e executar esse exemplo como um aplicativo de 32 bits em um sistema operacional de 64 bits, deverá criar a fonte de dados ODBC com o Administrador ODBC em %windir%\SysWOW64\odbcad32.exe.  
  
 Esse aplicativo se conecta à instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do computador. Para conectar-se a uma instância nomeada, altere a definição da fonte de dados ODBC para especificar a instância usando o seguinte formato: servidor\instância_nomeada. Por padrão, o [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] é instalado em uma instância nomeada.  
  
 O primeiro ([!INCLUDE[tsql](../../includes/tsql-md.md)]) listagem de código cria um procedimento armazenado usado por este exemplo.  
  
 Compile a segunda listagem de código (C++) com odbc32.lib. Em seguida, execute o programa.  
  
 O terceiro ([!INCLUDE[tsql](../../includes/tsql-md.md)]) listagem de código exclui o procedimento armazenado usado por este exemplo.  
  
```  
use AdventureWorks  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'TestParm')  
   DROP PROCEDURE TestParm  
GO  
  
CREATE PROCEDURE TestParm   
@OutParm int OUTPUT   
AS  
SELECT Name FROM Purchasing.Vendor  
SELECT @OutParm = 88  
RETURN 99  
go  
```  
  
```  
// compile with: odbc32.lib  
#include \<stdio.h>  
#include \<string.h>  
#include \<windows.h>  
#include \<sql.h>  
#include \<sqlext.h>  
#include \<odbcss.h>  
  
#define MAXBUFLEN 255  
  
SQLHENV henv = SQL_NULL_HENV;  
SQLHDBC hdbc1 = SQL_NULL_HDBC;       
SQLHSTMT hstmt1 = SQL_NULL_HSTMT;  
  
void Cleanup() {  
   if (hstmt1 != SQL_NULL_HSTMT)  
      SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
  
   if (hdbc1 != SQL_NULL_HDBC) {  
      SQLDisconnect(hdbc1);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   }  
  
   if (henv != SQL_NULL_HENV)  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
  
int main() {  
   RETCODE retcode;  
   // SQLBindParameter variables.  
   SWORD sParm1 = 0, sParm2 = 1;  
   SQLLEN cbParm1 = SQL_NTS;  
   SQLLEN cbParm2 = SQL_NTS;  
  
   // Allocate the ODBC environment and save handle.  
   retcode = SQLAllocHandle (SQL_HANDLE_ENV, NULL, &henv);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(Env) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Notify ODBC that this is an ODBC 3.0 app.  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetEnvAttr(ODBC version) Failed\n\n");  
      Cleanup();  
      return(9);      
   }  
  
   // Allocate ODBC connection handle and connect.  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // This sample use Integrated Security. Create the SQL Server DSN by using the Windows NT authentication.   
   retcode = SQLConnect(hdbc1, (UCHAR*)"AdventureWorks", SQL_NTS, (UCHAR*)"",SQL_NTS, (UCHAR*)"", SQL_NTS);  
  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Allocate statement handle.  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLAllocHandle(hstmt1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Bind the return code to variable sParm1.  
   retcode = SQLBindParameter(hstmt1, 1, SQL_PARAM_OUTPUT, SQL_C_SSHORT, SQL_INTEGER, 0, 0, &sParm1, 0, &cbParm1);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLBindParameter(sParm1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Bind the output parameter to variable sParm2.  
   retcode = SQLBindParameter(hstmt1, 2, SQL_PARAM_OUTPUT, SQL_C_SSHORT, SQL_INTEGER, 0, 0, &sParm2, 0, &cbParm2);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLBindParameter(sParm2) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Execute the command.   
   retcode = SQLExecDirect(hstmt1, (UCHAR*)"{? = call TestParm(?)}", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLExecDirect Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Show parameters are not filled.  
   printf("Before result sets cleared: RetCode = %d, OutParm = %d.\n", sParm1, sParm2);  
  
   // Clear any result sets generated.  
   while ( ( retcode = SQLMoreResults(hstmt1) ) != SQL_NO_DATA )  
      ;  
  
   // Show parameters are now filled.  
   printf("After result sets drained: RetCode = %d, OutParm = %d.\n", sParm1, sParm2);  
  
   // Clean up.   
   SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
```  
use AdventureWorks  
DROP PROCEDURE TestParm  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
[Chamar procedimentos armazenados & #40; ODBC & #41;](../../relational-databases/native-client-odbc-how-to/running-stored-procedures-call-stored-procedures.md)  
  
  
