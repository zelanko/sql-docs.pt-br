---
title: Alocar identificadores e conecte-se ao SQL Server (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- handles [ODBC]
- handles [ODBC], connection
- handles [ODBC], about handles
ms.assetid: 6172cd52-9c9a-467d-992f-def07f3f3bb1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 322120624c612371b56029c2cf29c9ab457c81b5
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53376349"
---
# <a name="allocate-handles-and-connect-to-sql-server-odbc"></a>Alocar identificadores e se conectar ao SQL Server (ODBC)
    
### <a name="to-allocate-handles-and-connect-to-sql-server"></a>Para alocar identificadores e se conectar ao SQL Server  
  
1.  Inclua o arquivos de cabeçalho ODBC Sql.h, Sqlext.h, Sqltypes.h.  
  
2.  Inclua o arquivo de cabeçalho específico do driver do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Odbcss.h.  
  
3.  Chame [SQLAllocHandle](https://go.microsoft.com/fwlink/?LinkId=58396) com um `HandleType` SQL_HANDLE_ENV para inicializar o ODBC e alocar um identificador de ambiente.  
  
4.  Chame [SQLSetEnvAttr](../native-client-odbc-api/sqlsetenvattr.md) com `Attribute` definido como SQL_ATTR_ODBC_VERSION e `ValuePtr` definido como SQL_OV_ODBC3 para indicar que o aplicativo irá usar chamadas de função ODBC 3. x-format.  
  
5.  Opcionalmente, chame [SQLSetEnvAttr](../native-client-odbc-api/sqlsetenvattr.md) para definir outro ambiente de opções ou chamada [SQLGetEnvAttr](https://go.microsoft.com/fwlink/?LinkId=58403) para obter opções de ambiente.  
  
6.  Chame [SQLAllocHandle](https://go.microsoft.com/fwlink/?LinkId=58396) com um `HandleType` SQL_HANDLE_DBC para alocar um identificador de conexão.  
  
7.  Opcionalmente, chame [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) para definir opções de conexão ou chamada [SQLGetConnectAttr](../native-client-odbc-api/sqlgetconnectattr.md) para obter opções de conexão.  
  
8.  Chamar SQLConnect para usar uma fonte de dados existente para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Ou  
  
     Chame [SQLDriverConnect](../native-client-odbc-api/sqldriverconnect.md) usar uma cadeia de conexão para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Uma cadeia de conexão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] completa mínima tem uma de duas formas:  
  
    ```  
    DSN=dsn_name;Trusted_connection=yes;  
    DRIVER={SQL Server Native Client 10.0};SERVER=server;Trusted_connection=yes;  
    ```  
  
     Se a cadeia de conexão não estiver completa, o `SQLDriverConnect` poderá solicitar as informações necessárias. Isso é controlado pelo valor especificado para o *DriverCompletion* parâmetro.  
  
     \- ou –  
  
     Chame [SQLBrowseConnect](../native-client-odbc-api/sqlbrowseconnect.md) várias vezes de forma iterativa para criar a cadeia de conexão e conecte-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
9. Opcionalmente, chame [SQLGetInfo](../native-client-odbc-api/sqlgetinfo.md) para obter atributos de driver e o comportamento para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fonte de dados.  
  
10. Aloque e use instruções.  
  
11. Chamar SQLDisconnect para se desconectar do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e tornar o lidar com a conexão disponível para uma nova conexão.  
  
12. Chame [SQLFreeHandle](../native-client-odbc-api/sqlfreehandle.md) com um `HandleType` SQL_HANDLE_DBC para liberar o identificador de conexão.  
  
13. Chame `SQLFreeHandle` com um `HandleType` SQL_HANDLE_ENV para liberar o identificador de ambiente.  
  
> [!IMPORTANT]  
>  Quando possível, use a Autenticação do Windows. Se a Autenticação do Windows não estiver disponível, solicite aos usuários que digitem suas credenciais em tempo de execução. Evite armazenar as credenciais em um arquivo. Se for necessário manter as credenciais, criptografe-as com a [Win32 crypto API](https://go.microsoft.com/fwlink/?LinkId=64532)(em inglês).  
  
## <a name="example"></a>Exemplo  
 Este exemplo mostra uma chamada de `SQLDriverConnect` para conectar-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sem exigir uma fonte de dados ODBC existente. A passagem de uma cadeia de conexão incompleta a `SQLDriverConnect`, faz o driver ODBC solicitar que o usuário digite as informações ausentes.  
  
```  
#define MAXBUFLEN   255  
  
SQLHENV      henv = SQL_NULL_HENV;  
SQLHDBC      hdbc1 = SQL_NULL_HDBC;  
SQLHSTMT      hstmt1 = SQL_NULL_HSTMT;  
  
SQLCHAR      ConnStrIn[MAXBUFLEN] =  
         "DRIVER={SQL Server Native Client 10.0};SERVER=MyServer";  
  
SQLCHAR      ConnStrOut[MAXBUFLEN];  
SQLSMALLINT   cbConnStrOut = 0;  
  
// Make connection without data source. Ask that driver   
// prompt if insufficient information. Driver returns  
// SQL_ERROR and application prompts user  
// for missing information. Window handle not needed for  
// SQL_DRIVER_NOPROMPT.  
retcode = SQLDriverConnect(hdbc1,      // Connection handle  
                  NULL,         // Window handle  
                  ConnStrIn,      // Input connect string  
                  SQL_NTS,         // Null-terminated string  
                  ConnStrOut,      // Address of output buffer  
                  MAXBUFLEN,      // Size of output buffer  
                  &cbConnStrOut,   // Address of output length  
                  SQL_DRIVER_PROMPT);  
```  
  
  
