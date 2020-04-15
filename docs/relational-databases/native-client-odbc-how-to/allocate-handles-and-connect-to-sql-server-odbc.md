---
title: Alocar alças e conectar-se ao SQL Server (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- handles [ODBC]
- handles [ODBC], connection
- handles [ODBC], about handles
ms.assetid: 6172cd52-9c9a-467d-992f-def07f3f3bb1
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5d26af711c07c4ea296d5351d0fcb0d1f9710706
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294446"
---
# <a name="allocate-handles-and-connect-to-sql-server-odbc"></a>Alocar identificadores e se conectar ao SQL Server (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

    
### <a name="to-allocate-handles-and-connect-to-sql-server"></a>Para alocar identificadores e se conectar ao SQL Server  
  
1.  Inclua o arquivos de cabeçalho ODBC Sql.h, Sqlext.h, Sqltypes.h.  
  
2.  Inclua o arquivo de cabeçalho específico do driver do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Odbcss.h.  
  
3.  Ligue para [o SQLAllocHandle](https://go.microsoft.com/fwlink/?LinkId=58396) com um **HandleType** de SQL_HANDLE_ENV para inicializar o ODBC e alocar uma alça de ambiente.  
  
4.  Ligue para [sqlsetenvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md) com **atributo** definido como SQL_ATTR_ODBC_VERSION e **ValuePtr** definido para SQL_OV_ODBC3 para indicar que o aplicativo usará chamadas de função ODBC 3.x.x.  
  
5.  Opcionalmente, ligue para [o SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md) para definir outras opções de ambiente ou ligue para [o SQLGetEnvAttr](https://go.microsoft.com/fwlink/?LinkId=58403) para obter opções de ambiente.  
  
6.  Ligue para [o SQLAllocHandle](https://go.microsoft.com/fwlink/?LinkId=58396) com um **HandleType** de SQL_HANDLE_DBC para alocar uma alça de conexão.  
  
7.  Opcionalmente, ligue para [o SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) para definir opções de conexão ou ligue para [o SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) para obter opções de conexão.  
  
8.  Ligue para o SQLConnect para usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]uma fonte de dados existente para se conectar a .  
  
     Ou  
  
     Ligue para [o SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]usar uma seqüência de conexões para se conectar a .  
  
     Uma cadeia de conexão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] completa mínima tem uma de duas formas:  
  
    ```  
    DSN=dsn_name;Trusted_connection=yes;  
    DRIVER={SQL Server Native Client 10.0};SERVER=server;Trusted_connection=yes;  
    ```  
  
     Se a seqüência de conexões não estiver concluída, **o SQLDriverConnect** pode solicitar as informações necessárias. Isso é controlado pelo valor especificado para o parâmetro *DriverComplet.*  
  
     \- ou –  
  
     Ligue para [o SQLBrowseConnect](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md) várias vezes de forma iterativa para construir a cadeia de conexão e se conectar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
9. Opcionalmente, ligue para [o SQLGetInfo](../../relational-databases/native-client-odbc-api/sqlgetinfo.md) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] obter atributos e comportamentos do driver para a fonte de dados.  
  
10. Aloque e use instruções.  
  
11. Ligue para o SQLDisconnect para se desconectar e disponibilizar a alça de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conexão para uma nova conexão.  
  
12. Ligue para [o SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) com um **HandleType** de SQL_HANDLE_DBC para liberar o cabo de conexão.  
  
13. Ligue para **o SQLFreeHandle** com um **handleType** de SQL_HANDLE_ENV para liberar o cabo do ambiente.  
  
> [!IMPORTANT]  
>  Quando possível, use a Autenticação do Windows. Se a Autenticação do Windows não estiver disponível, solicite aos usuários que digitem suas credenciais em tempo de execução. Evite armazenar as credenciais em um arquivo. Se for necessário manter as credenciais, criptografe-as com a [Win32 crypto API](https://go.microsoft.com/fwlink/?LinkId=64532)(em inglês).  
  
## <a name="example"></a>Exemplo  
 Este exemplo mostra uma chamada ao **SQLDriverConnect** para se conectar a uma instância sem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exigir uma fonte de dados ODBC existente. Ao passar uma seqüência de conexão incompleta para **SQLDriverConnect,** isso faz com que o driver ODBC insira o usuário para inserir as informações faltantes.  
  
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
  
  
