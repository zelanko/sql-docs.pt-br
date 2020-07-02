---
title: Cópia em massa usando um arquivo de formato (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bulk copy using format file [ODBC]
- ODBC, bulk copy operations
ms.assetid: 970fd3af-f918-4fc3-a5b1-92596515d4de
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 01221bcb23dea7dc78777620fe580bcf0e1287c2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85725155"
---
# <a name="bulk-copy-by-using-a-format-file-odbc"></a>Copiar em massa usando um arquivo de formato (ODBC)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  Este exemplo mostra como usar a função ODBC bcp_init com um arquivo de formato.  
  
### <a name="to-bulk-copy-by-using-a-format-file"></a>Para copiar em massa usando um arquivo de formato  
  
1.  Aloque um identificador de ambiente e um identificador de conexão.  
  
2.  Defina SQL_COPT_SS_BCP e SQL_BCP_ON para habilitar operações de cópia em massa.  
  
3.  Conecte ao Microsoft® SQL Server™.  
  
4.  Chame [bcp_init](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) para definir as seguintes informações:  
  
    -   O nome da tabela ou da exibição da qual ou para a qual será feita a cópia em massa.  
  
    -   O nome do arquivo de dados que contém os dados a serem copiados para o banco de dados ou que recebe os dados ao copiar do banco de dados.  
  
    -   O nome de um arquivo de dados que receberá qualquer mensagem de erro de cópia em massa (especifique NULL se não desejar um arquivo de mensagens).  
  
    -   A direção da cópia: DB_IN do arquivo para a tabela ou exibição.  
  
5.  Chame [bcp_readfmt](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md) para ler o arquivo de formato que descreve o arquivo de dados a ser usado pela operação de cópia em massa.  
  
6.  Chame [bcp_exec](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md) para executar a operação de cópia em massa.  
  
## <a name="example"></a>Exemplo  
 Este exemplo não tem suporte em IA64.  
  
 Será necessária uma fonte de dados ODBC chamada AdventureWorks, cujo banco de dados padrão é o banco de dados de exemplo AdventureWorks. (Você pode baixar o banco de dados de exemplo AdventureWorks do [Microsoft SQL Server exemplos e projetos da comunidade](https://go.microsoft.com/fwlink/?LinkID=85384) Home Page.) Essa fonte de dados deve ser baseada no driver ODBC fornecido pelo sistema operacional (o nome do driver é "SQL Server"). Se você compilar e executar esse exemplo como um aplicativo de 32 bits em um sistema operacional de 64 bits, deverá criar a fonte de dados ODBC com o Administrador ODBC em %windir%\SysWOW64\odbcad32.exe.  
  
 Esse aplicativo se conecta à instância padrão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do computador. Para conectar-se a uma instância nomeada, altere a definição da fonte de dados ODBC para especificar a instância usando o seguinte formato: servidor\instância_nomeada. Por padrão, o [!INCLUDE[ssExpress](../../../includes/ssexpress-md.md)] é instalado em uma instância nomeada.  
  
 Execute a primeira [!INCLUDE[tsql](../../../includes/tsql-md.md)] listagem de código () para criar a tabela que será usada pelo exemplo.  
  
 Copie a segunda listagem de código e cole-a em um arquivo denominado Bcpfmt.fmt. Cada coluna na tabela é separada por um caractere de tabulação.  
  
 Copie a terceira listagem de código e cole-a em um arquivo denominado Bcpodbc.bcp. Um caractere de tabulação precede cada retorno de carro no arquivo.  
  
 Compile a quarta listagem de código (C++) com odbc32.lib e odbcbcp.lib. Se você compilou com o MSBuild.exe, copie primeiro o Bcpfmt.fmt e o Bcpodbc.bcp do diretório do projeto no diretório com o .exe e, em seguida, invoque o .exe.  
  
 Execute a quinta [!INCLUDE[tsql](../../../includes/tsql-md.md)] listagem de código () para excluir a tabela usada pelo exemplo.  
  
```  
use AdventureWorks  
CREATE TABLE BCPDate (cola int, colb datetime)  
```  
  
```  
8.0  
2  
1SQLCHAR04"\t"1colaSQL_Latin1_General_Cp437_Bin  
2SQLCHAR08"\r\n"2colbSQL_Latin1_General_Cp437_Bin  
```  
  
```  
1  
2  
  
```  
  
```  
// compile with: odbc32.lib odbcbcp.lib  
#include <stdio.h>  
#include <windows.h>  
#include <sql.h>  
#include <sqlext.h>  
#include <odbcss.h>  
  
SQLHENV henv = SQL_NULL_HENV;  
HDBC hdbc1 = SQL_NULL_HDBC;   
  
void Cleanup() {  
   if (hdbc1 != SQL_NULL_HDBC) {  
      SQLDisconnect(hdbc1);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   }  
  
   if (henv != SQL_NULL_HENV)  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
  
int main() {  
   RETCODE retcode;  
   SDWORD cRows;  
  
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
  
   // Allocate ODBC connection handle, set BCP mode, and connect.  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   retcode = SQLSetConnectAttr(hdbc1, SQL_COPT_SS_BCP, (void *)SQL_BCP_ON, SQL_IS_INTEGER);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetConnectAttr(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Sample uses Integrated Security. Create SQL Server DSN using Windows NT authentication.  
   retcode = SQLConnect(hdbc1, (UCHAR*)"AdventureWorks", SQL_NTS, (UCHAR*)"", SQL_NTS, (UCHAR*)"", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Initialize the bulk copy.  
   retcode = bcp_init(hdbc1, "BCPDate", "BCPODBC.bcp", NULL, DB_IN);  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_init(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Read the format file.  
   retcode = bcp_readfmt(hdbc1, "BCPFMT.fmt");  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_readfmt(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Execute the bulk copy.  
   retcode = bcp_exec(hdbc1, &cRows);  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_exec(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   printf("Number of rows bulk copied in = %d.\n", cRows);  
  
   // Cleanup  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
```  
use AdventureWorks  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'BCPDate')  
     DROP TABLE BCPDate  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Tópicos de instruções sobre cópia em massa com o SQL Server ODBC Driver &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/bulk-copy/bulk-copying-with-the-sql-server-odbc-driver-how-to-topics-odbc.md)   
 [Usando arquivos de dados e de formato](../../../relational-databases/native-client-odbc-bulk-copy-operations/using-data-files-and-format-files.md)  
  
  
