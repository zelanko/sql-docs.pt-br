---
title: Conectando-se a uma fonte de dados (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: fe7f86c2ca53ef4534abd1024d317eee0c1b3c99
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705787"
---
# <a name="connecting-to-a-data-source-odbc"></a>Conectando-se a uma fonte de dados (ODBC)
  Depois de alocar os identificadores de ambiente e conexão e definir quaisquer atributos de conexão, o aplicativo se conectará à fonte de dados ou driver. Há três funções que você pode usar para se conectar:  
  
-   **SQLConnect**  
  
-   **SQLDriverConnect**  
  
-   **SQLBrowseConnect**  
  
 Para obter mais informações sobre como fazer conexões com uma fonte de dados, incluindo as várias opções de cadeia de conexão disponíveis, consulte [usando palavras-chave de cadeia de conexão com SQL Server Native Client](../native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
## <a name="sqlconnect"></a>SQLConnect  
 O **SQLConnect** é a função de conexão mais simples. Ela aceita três parâmetros: um nome da fonte de dados, uma ID de usuário e uma senha. Use o **SQLConnect** quando esses três parâmetros contiverem todas as informações necessárias para se conectar ao banco de dados. Para fazer isso, crie uma lista de fontes de dados usando **Sqlsources**; solicitar ao usuário uma fonte de dados, ID de usuário e senha; e, em seguida, chame o **SQLConnect**.  
  
 O **SQLConnect** pressupõe que um nome de fonte de dados, ID de usuário e senha são suficientes para se conectar a uma fonte de dados e que a fonte de dados ODBC contém todas as outras informações que o driver ODBC precisa para fazer a conexão. Ao contrário de [SQLDriverConnect](../native-client-odbc-api/sqldriverconnect.md) e [SQLBrowseConnect](../native-client-odbc-api/sqlbrowseconnect.md), o **SQLConnect** não usa uma cadeia de conexão.  
  
## <a name="sqldriverconnect"></a>SQLDriverConnect  
 **SQLDriverConnect** é usado quando mais informações do que o nome da fonte de dados, a ID de usuário e a senha são necessárias. Um dos parâmetros para **SQLDriverConnect** é uma cadeia de conexão que contém informações específicas do driver. Você pode usar **SQLDriverConnect** em vez de **SQLConnect** pelos seguintes motivos:  
  
-   Para especificar informações específicas de driver no tempo de conexão.  
  
-   Para solicitar que o driver instrua o usuário a fornecer informações de conexão.  
  
-   Para se conectar sem usar uma fonte de dados ODBC.  
  
 A cadeia de conexão **SQLDriverConnect** contém uma série de pares de valor de palavra-chave que especificam todas as informações de conexão suportadas por um driver ODBC. Cada driver suporta as palavras-chave ODBC padrão (DSN, FILEDSN, DRIVER, UID, PWD e SAVEFILE), além das palavras-chave específicas de driver para todas as informações de conexão suportadas pelo driver. **SQLDriverConnect** pode ser usado para se conectar sem uma fonte de dados. Por exemplo, um aplicativo projetado para fazer uma conexão "sem DSN" com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode chamar **SQLDriverConnect** com uma cadeia de conexão que define a ID de logon, a senha, a biblioteca de rede, o nome do servidor para se conectar e o banco de dados padrão a ser usado.  
  
 Ao usar o **SQLDriverConnect**, há duas opções para solicitar ao usuário qualquer informação de conexão necessária:  
  
-   Caixa de diálogo de aplicativo  
  
     Você pode criar uma caixa de diálogo de aplicativo que solicita informações de conexão e, em seguida, chama **SQLDriverConnect** com um identificador de janela nulo e *DriverCompletion* definido como SQL_DRIVER_NOPROMPT. Essas configurações de parâmetro impedem que o driver ODBC abra sua própria caixa de diálogo. Esse método é usado quando é importante controlar a interface do usuário do aplicativo.  
  
-   Caixa de diálogo de driver  
  
     Você pode codificar o aplicativo para passar um identificador de janela válido para **SQLDriverConnect** e definir o parâmetro *DriverCompletion* como SQL_DRIVER_COMPLETE, SQL_DRIVER_PROMPT ou SQL_DRIVER_COMPLETE_REQUIRED. O driver gera uma caixa de diálogo para solicitar o usuário a fornecer as informações de conexão. Esse método simplifica o código do aplicativo.  
  
## <a name="sqlbrowseconnect"></a>SQLBrowseConnect  
 **SQLBrowseConnect**, como **SQLDriverConnect**, usa uma cadeia de conexão. No entanto, usando **SQLBrowseConnect**, um aplicativo pode construir uma cadeia de conexão completa iterativamente com a fonte de dados em tempo de execução. Isso permite que o aplicativo faça duas tarefas:  
  
-   Crie as próprias caixas de diálogo para solicitar essas informações, assim mantendo o controle da interface do usuário.  
  
-   Procure no sistema por fontes de dados que possam ser usadas por um driver específico, possivelmente em várias etapas.  
  
     Por exemplo, primeiro o usuário pode procurar servidores na rede e, depois de escolher um, procurar no servidor pelos bancos de dados acessíveis pelo driver.  
  
 Quando o **SQLBrowseConnect** conclui uma conexão bem-sucedida, ele retorna uma cadeia de conexão que pode ser usada em chamadas subsequentes para **SQLDriverConnect**.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client sempre retorna SQL_SUCCESS_WITH_INFO em um **SQLConnect**, **SQLDriverConnect**ou **SQLBrowseConnect**bem-sucedido. Quando um aplicativo ODBC chama **SQLGetDiagRec** depois de obter SQL_SUCCESS_WITH_INFO, ele pode receber as seguintes mensagens:  
  
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
  
 Você pode ignorar as mensagens 5701 e 5703; elas são meramente informativas. Entretanto, você não deve ignorar um código de retorno de SQL_SUCCESS_WITH_INFO porque podem ser retornadas mensagens diferentes de 5701 ou 5703. Por exemplo, se um driver se conectar a um servidor que executa uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com procedimentos armazenados de catálogo desatualizados, um dos erros retornados por meio de **SQLGetDiagRec** após um SQL_SUCCESS_WITH_INFO é:  
  
```  
SqlState:   01000  
pfNative:   0  
szErrorMsg: "[Microsoft][SQL Server Native Client]The ODBC  
            catalog stored procedures installed on server  
            my65server are version 06.50.0193; version 07.00.0205  
            or later is required to ensure proper operation.  
            Please contact your system administrator."  
```  
  
 A função de tratamento de erros de um aplicativo para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conexões deve chamar **SQLGetDiagRec** até que ela retorne SQL_NO_DATA. Em seguida, ele deve agir em qualquer mensagem além daquelas com um código *pfNative* de 5701 ou 5703.  
  
## <a name="see-also"></a>Consulte Também  
 [Comunicando-se com SQL Server &#40;ODBC&#41;](communicating-with-sql-server-odbc.md)  
  
  
