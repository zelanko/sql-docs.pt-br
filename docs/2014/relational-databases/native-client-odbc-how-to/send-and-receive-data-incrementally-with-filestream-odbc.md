---
title: Enviar e receber dados de forma incremental com FILESTREAM (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: b82ecf4c-f151-4a99-8717-a73ee5ec994f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac4965e665013cad4cd17068633a812cc5813826
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68205531"
---
# <a name="send-and-receive-data-incrementally-with-filestream-odbc"></a>Enviar e receber dados de forma incremental com FILESTREAM (ODBC)
  Este exemplo mostra como usar o recurso FILESTREAM para enviar e receber dados de forma incremental com SQLPutData e SQLGetData.  
  
 Para obter mais informações sobre o recurso FILESTREAM, consulte [suporte a filestream &#40;&#41;ODBC ](../native-client/odbc/filestream-support-odbc.md).  
  
## <a name="example"></a>Exemplo  
 Antes de compilar e executar este exemplo, habilite o suporte a FILESTREAM ([Habilitar e configurar o FILESTREAM](../blob/enable-and-configure-filestream.md)).  
  
 A primeira listagem de código ([!INCLUDE[tsql](../../includes/tsql-md.md)]) cria um banco de dados usado por este exemplo. Sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ter acesso de gravação para executar este script (por exemplo, faça logon como uma conta de sistema local).  
  
 A segunda listagem de código é o código C++. Especifique um servidor; na listagem de código C++, altere "MyServer" para um nome de servidor válido. Verifique se a variável de ambiente INCLUDE inclui o diretório que contém sqlncli.h. Compile a listagem de código C++ com odbc32.lib, user32.lib, /D "_UNICODE", /D "UNICODE", odbc32.lib e /EHsc.  
  
 A terceira listagem de código ([!INCLUDE[tsql](../../includes/tsql-md.md)]) exclui o banco de dados usado por este exemplo.  
  
```  
USE master  
GO  
  
-- enable file stream  
exec sp_configure 'filestream access level', 2  
GO  
  
-- create directory for filestream database  
EXEC sp_configure 'show advanced options', 1  
GO  
RECONFIGURE  
GO  
EXEC sp_configure 'xp_cmdshell', 1  
GO  
RECONFIGURE  
GO  
EXEC xp_cmdshell 'md c:\filestreamdemo'  
GO  
  
-- Drop the filestream demo database  
IF EXISTS (SELECT name FROM master..sysdatabases WHERE name = 'myfilestreamdb')  
    DROP DATABASE [myfilestreamdb]  
GO  
  
-- Create filestream demo database  
CREATE DATABASE [myfilestreamdb] ON PRIMARY  
    (NAME=[myfilestreamdbprimary], FILENAME='c:\filestreamdemo\dbf.mdf'),  
    FILEGROUP [fsgrp] CONTAINS FILESTREAM (NAME=[fscnt],FILENAME='c:\filestreamdemo\fscnt')  
    LOG ON (NAME=[dblog], FILENAME='c:\filestreamdemo\db1.ldf', SIZE=5MB, MAXSIZE=3000MB, FILEGROWTH=5MB)  
GO  
  
-- Create table that contain filestream column  
CREATE TABLE [myfilestreamdb]..[mydocs]  
(  
    id UNIQUEIDENTIFIER ROWGUIDCOL NOT NULL UNIQUE,  
    doc VARBINARY(MAX) FILESTREAM  
)  
GO  
```  
  
```  
// compile with: /D "_UNICODE" /D "UNICODE" odbc32.lib /EHsc  
#pragma once  
#define WIN32_LEAN_AND_MEAN  
#include <tchar.h>  
#include <windows.h>  
#include <stdio.h>  
#include <sql.h>  
#include <sqlext.h>  
  
#define _SQLNCLI_ODBC_  
#include <sqlncli.h>  
  
#define SUCCESS(x) (!((x) & 0xFFFE))  
  
#define CHKRC(stmt) do { \  
                        rc = (stmt); \  
                        if (!SUCCESS(rc)) \  
                            throw (RETCODE) rc; \  
                    } while(0);  
  
void PrintError(SQLSMALLINT HandleType, SQLHANDLE Handle) {  
    RETCODE rc = SQL_SUCCESS;  
    SQLTCHAR szSqlState[6], szMessage[1024];  
    SQLSMALLINT i = 1, msgLen = 0;  
    SQLINTEGER NativeError;  
  
    do {  
       i = 1;  
       while (SQL_NO_DATA != (rc = SQLGetDiagRec(HandleType, Handle, i, szSqlState, &NativeError, szMessage, sizeof(szMessage)/sizeof(SQLTCHAR), &msgLen)) && SUCCESS(rc)) {  
            _tprintf(_T("SQLState=%s, NativeError=%ld, Message=%s\r\n"), szSqlState, NativeError, szMessage);  
            i++;  
        }  
    }   
    while (SQL_NO_DATA != (rc = SQLMoreResults(Handle)) && SUCCESS(rc));  
}  
  
int _tmain(int argc, _TCHAR* argv[]) {  
    RETCODE rc = SQL_SUCCESS;  
    HENV henv = SQL_NULL_HENV;  
    HDBC hdbc = SQL_NULL_HDBC;  
    SQLHSTMT hstmt = SQL_NULL_HSTMT;  
    SQLTCHAR * pszConnection = _T("DRIVER={SQL Server Native Client 10.0};")  
                               _T("Server=MyServer;")  
                               _T("Trusted_Connection=Yes;");  
    SQLLEN cbBuffer = SQL_DATA_AT_EXEC;  
    BYTE rgbDoc[1024];  
    SQLLEN cbDoc;  
  
    try {  
        CHKRC(SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HENV, &henv));  
        CHKRC(SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER)SQL_OV_ODBC3, 0));  
        CHKRC(SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc));  
        CHKRC(SQLDriverConnect(hdbc, NULL, pszConnection, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT));  
  
        CHKRC(SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt));  
        CHKRC(SQLPrepare(hstmt,  (SQLTCHAR *)_T("INSERT INTO [myfilestreamdb]..[mydocs] VALUES(newid(), ?)"), SQL_NTS));  
        CHKRC(SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_BINARY, SQL_VARBINARY, SQL_SS_LENGTH_UNLIMITED, 0, (SQLPOINTER)1, 0, &cbBuffer));  
  
        rc = ::SQLExecute(hstmt);  
        if (SQL_NEED_DATA == rc) {  
            SQLPOINTER pParam = NULL;  
            while (SQL_NEED_DATA == (rc = ::SQLParamData(hstmt, (SQLPOINTER *)&pParam))) {  
                CHKRC(SQLPutData(hstmt, "Hello ", 6));  
                CHKRC(SQLPutData(hstmt, "World!", 6));  
            }  
        }  
  
        CHKRC(SQLFreeStmt(hstmt, SQL_CLOSE));  
        CHKRC(SQLExecDirect(hstmt, _T("SELECT doc FROM [myfilestreamdb]..[mydocs]"), SQL_NTS));  
        CHKRC(SQLBindCol(hstmt, 1, SQL_C_BINARY, (SQLPOINTER)rgbDoc, sizeof(rgbDoc), &cbDoc));  
        CHKRC(SQLFetch(hstmt));  
  
        rgbDoc[cbDoc] = '\0';  
        printf("%s\r\n", (LPSTR)rgbDoc);  
    }  
    catch (RETCODE retcode) {  
        rc = retcode;  
    }  
  
    if (!SUCCESS(rc))  
        if (hstmt)  
            PrintError(SQL_HANDLE_STMT, hstmt);  
        else if (hdbc)  
            PrintError(SQL_HANDLE_DBC, hdbc);  
        else if(henv)  
            PrintError(SQL_HANDLE_ENV, henv);  
  
    if (hstmt)  
        SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
  
    if (hdbc) {  
        SQLDisconnect(hdbc);  
        SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
    }  
  
    if (henv)  
        SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
```  
USE master  
GO  
-- Drop the filestream demo database  
sp_detach_db 'myfilestreamdb'  
IF EXISTS (SELECT name FROM master..sysdatabases WHERE name = 'myfilestreamdb')  
    DROP DATABASE [myfilestreamdb]  
EXEC xp_cmdshell 'rd /s /q c:\filestreamdemo'  
GO  
```  
  
  
