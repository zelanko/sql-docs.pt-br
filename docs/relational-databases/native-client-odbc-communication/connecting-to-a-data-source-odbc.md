---
title: Conectando a uma fonte de dados (ODBC) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-communication
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- checking connection states
- ODBC data sources, connections
- data sources [SQL Server Native Client]
- SQLBrowseConnect function
- ODBC applications, connections
- ODBC applications, data sources
- connections [SQL Server Native Client]
- SQLConnect function
- SQLDriveConnect function
- verifying connection states
- SQL Server Native Client ODBC driver, data sources
- SQL Server Native Client ODBC driver, connections
ms.assetid: ae30dd1d-06ae-452b-9618-8fd8cd7ba074
caps.latest.revision: "37"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 19e4b1839d09ccbbca99bfa5992d25531a170571
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="connecting-to-a-data-source-odbc"></a>Conectando-se a uma fonte de dados (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Depois de alocar os identificadores de ambiente e conexão e definir quaisquer atributos de conexão, o aplicativo se conectará à fonte de dados ou driver. Há três funções que você pode usar para se conectar:  
  
-   **SQLConnect**  
  
-   **SQLDriverConnect**  
  
-   **SQLBrowseConnect**  
  
 Para obter mais informações sobre como estabelecer conexões com uma fonte de dados, incluindo as várias opções de cadeia de caracteres de conexão disponíveis, consulte [usando Conexão String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
## <a name="sqlconnect"></a>SQLConnect  
 **SQLConnect** é a função de conexão mais simples. Ela aceita três parâmetros: um nome da fonte de dados, uma ID de usuário e uma senha. Use **SQLConnect** quando esses três parâmetros contiverem todas as informações necessárias para se conectar ao banco de dados. Para fazer isso, crie uma lista de fontes de dados usando **SQLDataSources**; avisar o usuário para uma fonte de dados, ID de usuário e senha; e, em seguida, chamar **SQLConnect**.  
  
 **SQLConnect** supõe que um nome de fonte de dados, ID de usuário e senha são suficientes para se conectar a uma fonte de dados e a fonte de dados ODBC contém todas as outras informações necessárias ao driver ODBC para fazer a conexão. Ao contrário de [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) e [SQLBrowseConnect](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md), **SQLConnect** não usa uma cadeia de caracteres de conexão.  
  
## <a name="sqldriverconnect"></a>SQLDriverConnect  
 **SQLDriverConnect** é usada quando informações mais do que o nome da fonte de dados, a ID de usuário e a senha são necessárias. Um dos parâmetros para **SQLDriverConnect** é uma cadeia de caracteres de conexão que contém informações específicas de driver. Você pode usar **SQLDriverConnect** em vez de **SQLConnect** pelos seguintes motivos:  
  
-   Para especificar informações específicas de driver no tempo de conexão.  
  
-   Para solicitar que o driver instrua o usuário a fornecer informações de conexão.  
  
-   Para se conectar sem usar uma fonte de dados ODBC.  
  
 O **SQLDriverConnect** cadeia de caracteres de conexão contém uma série de pares de valor de palavra-chave que especificam todas as informações de conexão suportadas pelo driver ODBC. Cada driver suporta as palavras-chave ODBC padrão (DSN, FILEDSN, DRIVER, UID, PWD e SAVEFILE), além das palavras-chave específicas de driver para todas as informações de conexão suportadas pelo driver. **SQLDriverConnect** pode ser usado para se conectar sem uma fonte de dados. Por exemplo, um aplicativo que é projetado para tornar uma conexão "Sem-DSN" para uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode chamar **SQLDriverConnect** com uma cadeia de caracteres de conexão que define a ID de logon, a senha, a biblioteca de rede, o nome do servidor para se conectem e banco de dados para usar o padrão.  
  
 Ao usar **SQLDriverConnect**, há duas opções para avisar o usuário para qualquer necessárias informações de conexão:  
  
-   Caixa de diálogo de aplicativo  
  
     Você pode criar uma caixa de diálogo do aplicativo que solicita informações de conexão e, em seguida, chama **SQLDriverConnect** com um identificador de janela NULL e *DriverCompletion* definido como SQL_DRIVER_NOPROMPT. Essas configurações de parâmetro impedem que o driver ODBC abra sua própria caixa de diálogo. Esse método é usado quando é importante controlar a interface do usuário do aplicativo.  
  
-   Caixa de diálogo de driver  
  
     Você pode codificar o aplicativo para passar um identificador de janela válido para **SQLDriverConnect** e defina o *DriverCompletion* parâmetro SQL_DRIVER_COMPLETE, SQL_DRIVER_PROMPT ou SQL_DRIVER_COMPLETE_ Necessário. O driver gera uma caixa de diálogo para solicitar o usuário a fornecer as informações de conexão. Esse método simplifica o código do aplicativo.  
  
## <a name="sqlbrowseconnect"></a>SQLBrowseConnect  
 **SQLBrowseConnect**, como **SQLDriverConnect**, usa uma cadeia de caracteres de conexão. No entanto, usando **SQLBrowseConnect**, um aplicativo pode construir uma cadeia de caracteres de conexão completa iterativamente com a fonte de dados em tempo de execução. Isso permite que o aplicativo faça duas tarefas:  
  
-   Crie as próprias caixas de diálogo para solicitar essas informações, assim mantendo o controle da interface do usuário.  
  
-   Procure no sistema por fontes de dados que possam ser usadas por um driver específico, possivelmente em várias etapas.  
  
     Por exemplo, primeiro o usuário pode procurar servidores na rede e, depois de escolher um, procurar no servidor pelos bancos de dados acessíveis pelo driver.  
  
 Quando **SQLBrowseConnect** conclui uma conexão bem-sucedida, ela retorna uma cadeia de caracteres de conexão que pode ser usada em chamadas subsequentes para **SQLDriverConnect**.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client sempre retorna SQL_SUCCESS_WITH_INFO em um bem-sucedida **SQLConnect**, **SQLDriverConnect**, ou **SQLBrowseConnect**. Quando um aplicativo ODBC chama **SQLGetDiagRec** depois de obter SQL_SUCCESS_WITH_INFO, ele pode receber as seguintes mensagens:  
  
 5701  
 Indica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] colocou o contexto do usuário no banco de dados padrão definido na fonte de dados, ou no banco de dados padrão definido para o ID de logon usado na conexão se a fonte de dados não tinha um banco de dados padrão.  
  
 5703  
 Indica o idioma usado no servidor.  
  
 O exemplo a seguir mostra a mensagem retornada em uma conexão bem-sucedida pelo administrador do sistema:  
  
```  
szSqlState = "01000", *pfNativeError = 5701,  
szErrorMsg="[Microsoft][SQL Server Native Client][SQL Server]  
       Changed database context to 'pubs'."  
szSqlState = "01000", *pfNativeError = 5703,  
szErrorMsg="[Microsoft][SQL Server Native Client][SQL Server]  
       Changed language setting to 'us_english'."  
```  
  
 Você pode ignorar as mensagens 5701 e 5703; elas são meramente informativas. Entretanto, você não deve ignorar um código de retorno de SQL_SUCCESS_WITH_INFO porque podem ser retornadas mensagens diferentes de 5701 ou 5703. Por exemplo, se um driver se conecta a um servidor executando uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com procedimentos armazenados de catálogo obsoletos, um dos erros retornados por meio de **SQLGetDiagRec** após um SQL_SUCCESS_WITH_INFO será:  
  
```  
SqlState:   01000  
pfNative:   0  
szErrorMsg: "[Microsoft][SQL Server Native Client]The ODBC  
            catalog stored procedures installed on server  
            my65server are version 06.50.0193; version 07.00.0205  
            or later is required to ensure proper operation.  
            Please contact your system administrator."  
```  
  
 A função de um aplicativo de tratamento de erros [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conexões devem chamar **SQLGetDiagRec** até ele retornar SQL_NO_DATA. Ele deve, em seguida, agir em todas as mensagens diferentes com um *pfNative* código de 5701 ou 5703.  
  
## <a name="see-also"></a>Consulte também  
 [Comunicação com o SQL Server &#40; ODBC &#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
