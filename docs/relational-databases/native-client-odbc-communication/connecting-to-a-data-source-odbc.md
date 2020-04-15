---
title: Conectando-se a uma Fonte de Dados (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ae59e0bdb005d296341970f4582100b15a0dfdf7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307707"
---
# <a name="connecting-to-a-data-source-odbc"></a>Conectando-se a uma fonte de dados (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Depois de alocar os identificadores de ambiente e conexão e definir quaisquer atributos de conexão, o aplicativo se conectará à fonte de dados ou driver. Há três funções que você pode usar para se conectar:  
  
-   **SQLConnect**  
  
-   **SQLDriverConnect**  
  
-   **SQLBrowseConnect**  
  
 Para obter mais informações sobre como fazer conexões a uma fonte de dados, incluindo as várias opções de seqüência de conexões disponíveis, consulte [Usando palavras-chave de string de conexão com o Cliente Nativo do Servidor SQL](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
## <a name="sqlconnect"></a>SQLConnect  
 **SQLConnect** é a função de conexão mais simples. Ela aceita três parâmetros: um nome da fonte de dados, uma ID de usuário e uma senha. Use **o SQLConnect** quando esses três parâmetros contiverem todas as informações necessárias para se conectar ao banco de dados. Para isso, crie uma lista de fontes de dados usando **o SQLDataSources;** solicitar ao usuário uma fonte de dados, ID do usuário e senha; e, em seguida, chamar **SQLConnect**.  
  
 **O SQLConnect** assume que um nome de origem de dados, iD de usuário e senha são suficientes para se conectar a uma fonte de dados e que a fonte de dados ODBC contém todas as outras informações que o driver ODBC precisa para fazer a conexão. Ao contrário [do SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) e [do SQLBrowseConnect,](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md) **o SQLConnect** não usa uma seqüência de conexões.  
  
## <a name="sqldriverconnect"></a>SQLDriverConnect  
 **O SQLDriverConnect** é usado quando mais informações do que o nome de origem dos dados, o ID de usuário e a senha são necessários. Um dos parâmetros do **SQLDriverConnect** é uma seqüência de conexão que contém informações específicas do driver. Você pode usar **o SQLDriverConnect** em vez do **SQLConnect** pelas seguintes razões:  
  
-   Para especificar informações específicas de driver no tempo de conexão.  
  
-   Para solicitar que o driver instrua o usuário a fornecer informações de conexão.  
  
-   Para se conectar sem usar uma fonte de dados ODBC.  
  
 A seqüência de conexão **SQLDriverConnect** contém uma série de pares de valor de palavras-chave que especificam todas as informações de conexão suportadas por um driver ODBC. Cada driver suporta as palavras-chave ODBC padrão (DSN, FILEDSN, DRIVER, UID, PWD e SAVEFILE), além das palavras-chave específicas de driver para todas as informações de conexão suportadas pelo driver. **O SQLDriverConnect** pode ser usado para se conectar sem uma fonte de dados. Por exemplo, um aplicativo projetado para fazer uma conexão "sem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DSN" a uma instância de pode chamar **sqldriverConnect** com uma seqüência de conexão que define o ID de login, senha, biblioteca de rede, nome do servidor para se conectar e banco de dados padrão para usar.  
  
 Ao usar **o SQLDriverConnect,** existem duas opções para solicitar ao usuário qualquer informação de conexão necessária:  
  
-   Caixa de diálogo de aplicativo  
  
     Você pode criar uma caixa de diálogo de aplicativo que solicita informações de conexão e, em seguida, chama **SQLDriverConnect** com uma alça de janela NULL e *DriverComplet* definido para SQL_DRIVER_NOPROMPT. Essas configurações de parâmetro impedem que o driver ODBC abra sua própria caixa de diálogo. Esse método é usado quando é importante controlar a interface do usuário do aplicativo.  
  
-   Caixa de diálogo de driver  
  
     Você pode codificar o aplicativo para passar uma alça de janela válida para **SQLDriverConnect** e definir o parâmetro *DriverComplet* para SQL_DRIVER_COMPLETE, SQL_DRIVER_PROMPT ou SQL_DRIVER_COMPLETE_REQUIRED. O driver gera uma caixa de diálogo para solicitar o usuário a fornecer as informações de conexão. Esse método simplifica o código do aplicativo.  
  
## <a name="sqlbrowseconnect"></a>SQLBrowseConnect  
 **SQLBrowseConnect**, como **SQLDriverConnect,** usa uma seqüência de conexão. No entanto, usando **o SQLBrowseConnect,** um aplicativo pode construir uma seqüência de conexão completa iterativamente com a fonte de dados em tempo de execução. Isso permite que o aplicativo faça duas tarefas:  
  
-   Crie as próprias caixas de diálogo para solicitar essas informações, assim mantendo o controle da interface do usuário.  
  
-   Procure no sistema por fontes de dados que possam ser usadas por um driver específico, possivelmente em várias etapas.  
  
     Por exemplo, primeiro o usuário pode procurar servidores na rede e, depois de escolher um, procurar no servidor pelos bancos de dados acessíveis pelo driver.  
  
 Quando **o SQLBrowseConnect** completa uma conexão bem-sucedida, ele retorna uma seqüência de conexão que pode ser usada em chamadas subseqüentes para **SQLDriverConnect**.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do cliente nativo sempre retorna SQL_SUCCESS_WITH_INFO em um **SQLConnect,** **SQLDriverConnect**ou **SQLBrowseConnect**de sucesso. Quando um aplicativo ODBC chama **o SQLGetDiagRec** depois de receber SQL_SUCCESS_WITH_INFO, ele pode receber as seguintes mensagens:  
  
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
  
 Você pode ignorar as mensagens 5701 e 5703; elas são meramente informativas. Entretanto, você não deve ignorar um código de retorno de SQL_SUCCESS_WITH_INFO porque podem ser retornadas mensagens diferentes de 5701 ou 5703. Por exemplo, se um driver se conectar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a um servidor executando uma instância com procedimentos armazenados em catálogo desatualizados, um dos erros retornados através do **SQLGetDiagRec** após um SQL_SUCCESS_WITH_INFO é:  
  
```  
SqlState:   01000  
pfNative:   0  
szErrorMsg: "[Microsoft][SQL Server Native Client]The ODBC  
            catalog stored procedures installed on server  
            my65server are version 06.50.0193; version 07.00.0205  
            or later is required to ensure proper operation.  
            Please contact your system administrator."  
```  
  
 A função de manipulação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de erros de um aplicativo para conexões deve ligar para **o SQLGetDiagRec** até que ele retorne SQL_NO_DATA. Em seguida, deve agir em qualquer mensagem que não seja aquela com um código *pfNative* de 5701 ou 5703.  
  
## <a name="see-also"></a>Consulte Também  
 [Comunicando-se com o SQL Server &#40;o ODBC&#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
