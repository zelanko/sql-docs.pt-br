---
title: "Resiliência de Conexão no Driver ODBC do Windows | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 614fa0b4-e9fd-4c68-aab3-183f9b9df143
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9b19c5190d6256b0a5fd5d71976c5078ea86dee8
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="connection-resiliency-in-the-windows-odbc-driver"></a>Resiliência de conexão no driver ODBC do Windows
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

  Para garantir que os aplicativos permaneçam conectados a um [!INCLUDE[ssAzure](../../../includes/ssazure_md.md)], o driver ODBC no Windows pode restaurar conexões ociosas.  
  
> [!IMPORTANT]  
>  O recurso de resiliência de conexão tem suporte em versões de servidor do Banco de Dados SQL do Microsoft Azure e do SQL Server 2014 (e posteriores).  
  
 Para obter informações adicionais sobre a resiliência de conexão ociosa, consulte [artigo técnico – resiliência de Conexão ociosa](http://go.microsoft.com/fwlink/?LinkId=393996).  
  
 Para controlar o comportamento de reconexão, o ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] no Windows tem duas opções:  
  
-   Contagem de repetições de conexão.  
  
     A contagem de repetições de reconexão controla o número de tentativas de reconexão se houver uma falha de conexão. Os valores válidos variam de 0 a 255. Zero (0) significa que não haverá tentativa de reconexão. O valor padrão é uma tentativa de reconexão.  
  
     Você pode modificar o número de repetições de conexão ao:  
  
    -   Definir ou modificar uma fonte de dados que use o ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] com o controle de **Contagem de Repetições de Conexão** .  
  
    -   Usar a palavra-chave de cadeia de conexão **ConnectRetryCount** .  
  
     Para recuperar o número de tentativas de conexão, use o **SQL_COPT_SS_CONNECT_RETRY_COUNT** (somente leitura) atributo de conexão. Se um aplicativo se conecta a um servidor que não oferece suporte a resiliência de conexão, **SQL_COPT_SS_CONNECT_RETRY_COUNT** retorna 0.  
  
-   Intervalo de repetição de conexão.  
  
     O intervalo de repetição de conexão especifica o número de segundos entre cada tentativa de conexão. Os valores válidos são de 1 a 60. O tempo total para reconectar não pode exceder o tempo limite da conexão (SQL_ATTR_QUERY_TIMEOUT em SQLSetStmtAttr). O valor padrão é 10 segundos.  
  
     Você pode modificar o intervalo de repetição de conexão ao:  
  
    -   Definir ou modificar uma fonte de dados que use o ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] com o controle de **Intervalo de Repetição de Conexão** .  
  
    -   Usar a palavra-chave de cadeia de conexão **ConnectRetryInterval** .  
  
     Para recuperar o comprimento do intervalo de repetição de conexão, use o **SQL_COPT_SS_CONNECT_RETRY_INTERVAL** (somente leitura) atributo de conexão.  
  
 Se um aplicativo estabelecer uma conexão com SQL_DRIVER_COMPLETE_REQUIRED e posteriormente tentar executar uma instrução em uma conexão interrompida, o driver ODBC não exibirá a caixa de diálogo novamente. Além disso, durante a recuperação em andamento:  
  
-   Durante a recuperação, qualquer chamada para **sqlgetconnectattr (sql_copt_ss_connection_dead)**, deve retornar **SQL_CD_TRUE**.  
  
-   Se recuperação falhar, qualquer chamada para **sqlgetconnectattr (sql_copt_ss_connection_dead)**, deve retornar **SQL_CD_FALSE**.  
  
 Os seguintes códigos de estado são retornados por qualquer função que execute um comando no servidor:  
  
|Estado|Mensagem|  
|-----------|-------------|  
|IMC01|A conexão foi interrompida e a recuperação não é possível. O driver do cliente tentou recuperar a conexão uma ou mais vezes, e todas as tentativas de conexão falharam. Aumente o valor de ConnectRetryCount para aumentar o número de tentativas de recuperação.|  
|IMC02|O servidor não reconheceu uma tentativa de recuperação; a recuperação da conexão não é possível.|  
|IMC03|O servidor não preservou a versão exata do protocolo TDS do cliente solicitada durante uma tentativa de recuperação; a recuperação da conexão não é possível.|  
|IMC04|O servidor não preservou a versão principal do servidor exata solicitada durante uma tentativa de recuperação; a recuperação da conexão não é possível.|  
|IMC05|A conexão foi interrompida e a recuperação não é possível. A conexão foi marcada pelo servidor como não recuperável. Não foi feita nenhuma tentativa de restaurar a conexão.|  
|IMC06|A conexão foi interrompida e a recuperação não é possível. A conexão foi marcada pelo driver do cliente como não recuperável. Não foi feita nenhuma tentativa de restaurar a conexão.|  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir contém duas funções. **Func1** mostra como você pode se conectar com um nome de fonte de dados (DSN) que usa o Driver ODBC para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] no Windows. O DSN usa a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] e especifica a ID de usuário. **Func1** , em seguida, recupera o número de tentativas de conexão com **SQL_COPT_SS_CONNECT_RETRY_COUNT**.  
  
 **func2** usa **SQLDriverConnect**, a palavra-chave de cadeia de conexão **ConnectRetryCount** e atributos de conexão para recuperar a configuração de repetições de conexão e o intervalo de repetição.  
  
```  
// Connection_resiliency.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <stdio.h>  
#include <sqlext.h>  
#include <msodbcsql.h>  
  
void func1() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
   SQLSMALLINT i = 21;  

   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            // Connect to data source  
            retcode = SQLConnect(hdbc, (SQLCHAR*) "MyDSN", SQL_NTS, (SQLCHAR*) "userID", SQL_NTS, (SQLCHAR*) "password_for_userID", SQL_NTS);  
            retcode = SQLGetConnectAttr(hdbc, SQL_COPT_SS_CONNECT_RETRY_COUNT, &i, SQL_IS_INTEGER, NULL);  
  
            // Allocate statement handle  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
  
               // Process data  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               }  
  
               SQLDisconnect(hdbc);  
            }  
  
            SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
         }  
      }  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
   }  
}
  
void func2() {  
   SQLHENV henv;  
   SQLHDBC hdbc1;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
   SQLSMALLINT i = 21;  
  
#define MAXBUFLEN 255  
  
   SQLCHAR ConnStrIn[MAXBUFLEN] = "DRIVER={ODBC Driver 13 for SQL Server};SERVER=server_that_supports_connection_resiliency;UID=userID;PWD= password_for_userID;ConnectRetryCount=2";
   SQLCHAR ConnStrOut[MAXBUFLEN];

   SQLSMALLINT cbConnStrOut = 0;  
 
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3_80, SQL_IS_INTEGER);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            // SQLSetConnectAttr(hdbc1, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            retcode = SQLDriverConnect(hdbc1, NULL, ConnStrIn, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
         }  
         retcode = SQLGetConnectAttr(hdbc1, SQL_COPT_SS_CONNECT_RETRY_COUNT, &i, SQL_IS_INTEGER, NULL);  
         retcode = SQLGetConnectAttr(hdbc1, SQL_COPT_SS_CONNECT_RETRY_INTERVAL, &i, SQL_IS_INTEGER, NULL);  
      }  
   }  
}  
  
int main() {  
   func1();  
   func2();  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Microsoft ODBC Driver for SQL Server no Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
  
  

