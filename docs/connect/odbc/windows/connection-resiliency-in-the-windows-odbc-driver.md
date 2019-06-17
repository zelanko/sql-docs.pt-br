---
title: Resiliência de conexão no driver ODBC do Windows | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 614fa0b4-e9fd-4c68-aab3-183f9b9df143
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 94845da5a211c1f5b3ebf9f27a8a7ba780bc4b71
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66797820"
---
# <a name="connection-resiliency-in-the-windows-odbc-driver"></a>Resiliência de conexão no driver ODBC do Windows
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

  Para garantir que os aplicativos permaneçam conectados a um [!INCLUDE[ssAzure](../../../includes/ssazure_md.md)], o driver ODBC no Windows pode restaurar conexões ociosas.  
  
> [!IMPORTANT]  
>  O recurso de resiliência de conexão tem suporte em versões de servidor do Banco de Dados SQL do Microsoft Azure e do SQL Server 2014 (e posteriores).  
  
 Para saber mais sobre a resiliência de conexão ociosa, veja [Artigo técnico – Resiliência de conexão ociosa](https://download.microsoft.com/download/D/2/0/D20E1C5F-72EA-4505-9F26-FEF9550EFD44/Idle%20Connection%20Resiliency.docx).
  
 Para controlar o comportamento de reconexão, o ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Windows tem duas opções:  
  
-   Contagem de repetições de conexão.  
  
     A contagem de repetições de reconexão controla o número de tentativas de reconexão se houver uma falha de conexão. Os valores válidos variam de 0 a 255. Zero (0) significa que não haverá tentativa de reconexão. O valor padrão é uma tentativa de reconexão.  
  
     Você pode modificar o número de repetições de conexão ao:  
  
    -   Definir ou modificar uma fonte de dados que use o ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com o controle de **Contagem de Repetições de Conexão** .  
  
    -   Usar a palavra-chave de cadeia de conexão **ConnectRetryCount** .  
  
     Para recuperar o número de tentativas de conexão, use o atributo de conexão **SQL_COPT_SS_CONNECT_RETRY_COUNT** (somente leitura). Se um aplicativo se conectar a um servidor não compatível com resiliência de conexão, **SQL_COPT_SS_CONNECT_RETRY_COUNT** retornará 0.  
  
-   Intervalo de repetição de conexão.  
  
     O intervalo de repetição de conexão especifica o número de segundos entre cada tentativa de conexão. Os valores válidos são 1 a 60. O tempo total para reconectar não pode exceder o tempo limite da conexão (SQL_ATTR_QUERY_TIMEOUT em SQLSetStmtAttr). O valor padrão é 10 segundos.  
  
     Você pode modificar o intervalo de repetição de conexão ao:  
  
    -   Definir ou modificar uma fonte de dados que use o ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com o controle de **Intervalo de Repetição de Conexão** .  
  
    -   Usar a palavra-chave de cadeia de conexão **ConnectRetryInterval** .  
  
     Para recuperar a duração do intervalo de repetição de conexão, use o atributo de conexão **SQL_COPT_SS_CONNECT_RETRY_INTERVAL** (somente leitura).  
  
 Se um aplicativo estabelecer uma conexão com SQL_DRIVER_COMPLETE_REQUIRED e posteriormente tentar executar uma instrução em uma conexão interrompida, o driver ODBC não exibirá a caixa de diálogo novamente. Além disso, durante a recuperação em andamento:  
  
-   Durante a recuperação, qualquer chamada para **SQLGetConnectAttr(SQL_COPT_SS_CONNECTION_DEAD)** precisa retornar **SQL_CD_FALSE**.  
  
-   Se a recuperação falhar, qualquer chamada para **SQLGetConnectAttr(SQL_COPT_SS_CONNECTION_DEAD)** precisará retornar **SQL_CD_TRUE**.  
  
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
 O exemplo a seguir contém duas funções. **func1** mostra como você pode se conectar com um DNS (nome de fonte de dados) que usa o ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Windows. O DSN usa a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e especifica a ID de usuário. **Func1** , em seguida, recupera o número de novas tentativas de conexão com **SQL_COPT_SS_CONNECT_RETRY_COUNT**.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Microsoft ODBC Driver for SQL Server no Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
  
  
