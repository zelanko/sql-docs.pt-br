---
title: Usando vários conjuntos de resultados ativos (MARS) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, MARS
- SQLNCLI, MARS
- data access [SQL Server Native Client], MARS
- Multiple Active Result Sets
- SQL Server Native Client, MARS
- MARS [SQL Server]
- SQL Server Native Client ODBC driver, MARS
ms.assetid: ecfd9c6b-7d29-41d8-af2e-89d7fb9a1d83
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2d0b85fcded8ca6758447795fa23f18fc03e315c
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43082829"
---
# <a name="using-multiple-active-result-sets-mars"></a>Usando MARS (vários conjuntos de resultados ativos)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  O [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] introduziu o suporte ao MARS (conjuntos de resultados ativos múltiplos) nos aplicativos que acessem o [!INCLUDE[ssDE](../../../includes/ssde-md.md)]. Em versões mais antigas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], os aplicativos de banco de dados não podiam manter várias instruções ativas em uma conexão. Ao usar os conjuntos de resultados padrão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o aplicativo tinha que processar ou cancelar todos os conjuntos de resultados de um lote antes de executar outro lote nessa conexão. O [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] introduziu um novo atributo de conexão que permite que os aplicativos tenham mais que uma solicitação pendente por conexão e, especificamente, tenham mais que um conjunto de resultados padrão ativo por conexão.  
  
 O MARS simplifica o design de aplicativo com os seguintes novos recursos:  
  
-   Os aplicativos podem ter vários conjuntos de resultados padrão abertos e intercalar a leitura a partir deles.  
  
-   Os aplicativos podem executar outras instruções (por exemplo, INSERT, UPDATE, DELETE e chamadas de procedimento armazenado) enquanto os conjuntos de resultados padrão estiverem abertos.  
  
 Os aplicativos que usam o MARS considerarão as seguintes diretrizes vantajosas:  
  
-   Os conjuntos de resultados padrão devem ser usados para conjuntos de curta duração ou resultados breves gerados por instruções exclusivas do SQL (SELECT, DML com OUTPUT, RECEIVE, READ TEXT etc).  
  
-   Cursores de servidor devem ser usados para conjuntos de resultados grandes ou de duração mais longa gerados por instruções exclusivas do SQL.  
  
-   Sempre leia os resultados até o fim para obter solicitações de procedimento – independentemente de os resultados serem retornados ou não – e de lotes que retornem vários resultados.  
  
-   Sempre que possível, dê preferência ao uso de chamadas de API para alterar as propriedades de conexão e gerenciar transações em detrimento das instruções do [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
-   No MARS, a representação de escopo por sessão é proibida durante a execução dos lotes simultâneos.  
  
> [!NOTE]  
>  Por padrão, a funcionalidade de MARS não é habilitada. Para usar o MARS ao conectar-se ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, você deve habilitá-lo especificamente em uma cadeia de conexão. Para obter mais informações, consulte o provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e as seções sobre o driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, mais adiante neste tópico.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client não limita o número de instruções ativas em uma conexão.  
  
 Aplicativos típicos que não precisam ter mais de um lote de várias instruções ou de um procedimento armazenado em execução ao mesmo tempo se beneficiarão do MARS mesmo que não saibam como é feita sua implementação. Porém, aplicativos com requisitos mais complexos devem levar isso em conta.  
  
 O MARS habilita a execução intercalada de várias solicitações em uma única conexão. Isto é, ele permite que um lote seja executado e, dentro de sua execução, permite a execução de outras solicitações. Observe, porém, que o MARS é definido em termos de intercalação, e não em termos de execução paralela.  
  
 A infraestrutura do MARS permite que vários lotes sejam executados de uma maneira intercalada, embora a execução só possa ser alterada em pontos bem definidos. Além disso, a maioria das instruções deve ser executada atomicamente dentro de um lote. As instruções que retornam linhas para o cliente, que às vezes são chamados de *pontos de produção*, têm permissão para intercalar execução antes da conclusão, enquanto as linhas estão sendo enviadas ao cliente, por exemplo:  
  
-   SELECT  
  
-   FETCH  
  
-   RECEIVE  
  
 Qualquer outra instrução que seja executada como parte de um procedimento armazenado ou lote deve ser executada até a conclusão, antes que a execução possa ser alterada para outras solicitações do MARS.  
  
 A maneira exata que os lotes são intercalados na execução é influenciada por vários fatores e é difícil prever a sequência exata em que os comandos de vários lotes que contêm pontos de produção será executada. Tenha cuidado para evitar efeitos colaterais indesejáveis devido a execução intercalada desses lotes complexos.  
  
 Evite problemas usando chamadas de API, em vez de instruções do [!INCLUDE[tsql](../../../includes/tsql-md.md)], para gerenciar o estado de conexão (SET, USE) e as transações (BEGIN TRAN, COMMIT, ROLLBACK), não incluindo essas instruções em lotes de várias instruções que contenham pontos de produção e serializando a execução de tais lotes consumindo ou cancelando todos os resultados.  
  
> [!NOTE]  
>  Um lote ou procedimento armazenado que inicie uma transação manual ou implícita quando o MARS está habilitado deve concluir a transação antes de ser encerrado. Se não fizer, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] acumulará todas as alterações feitas pela transação quando o lote for concluído. Essa transação é gerenciada pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como uma transação de escopo em lote. Este é um tipo novo de transação introduzido no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] para habilitar procedimentos armazenados existentes com bom comportamento para uso quando o MARS for habilitado. Para obter mais informações sobre transações no escopo do lote, consulte [instruções de transação &#40;Transact-SQL&#41;](~/t-sql/statements/statements.md).  
  
 Para obter um exemplo de como usar o MARS do ADO, consulte [usando o ADO com SQL Server Native Client](../../../relational-databases/native-client/applications/using-ado-with-sql-server-native-client.md).  
  
## <a name="in-memory-oltp"></a>OLTP na memória  
 OLTP na memória dá suporte a MARS usando consultas e procedimentos armazenados compilados nativamente. O MARS habilita solicitando dados em várias consultas sem a necessidade de se recuperar completamente cada conjunto antes de enviar uma solicitação para buscar linhas em um novo conjunto de resultados de resultados. Para ler com êxito de resultados abertos vários conjuntos, você deve usar um MARS habilitado conexão.  
  
 MARS está desabilitado por padrão, portanto, você deve habilitá-la explicitamente adicionando `MultipleActiveResultSets=True` para uma cadeia de caracteres de conexão. O exemplo a seguir demonstra como se conectar a uma instância do SQL Server e especificar que o MARS está habilitado:  
  
```  
Data Source=MSSQL; Initial Catalog=AdventureWorks; Integrated Security=SSPI; MultipleActiveResultSets=True  
```  
  
 MARS com o OLTP na memória é essencialmente o mesmo que o MARS no restante do mecanismo do SQL. O exemplo a seguir lista as diferenças ao usar MARS em tabelas com otimização de memória e nativamente procedimentos armazenados compilados.  
  
 **Tabelas com otimização de memória e MARS**  
  
 A seguir está as diferenças entre as tabelas baseadas em disco e com otimização de memória ao usar um MARS habilitado a conexão:  
  
-   Duas instruções podem modificar os dados no mesmo objeto de destino, mas se ambos tentarem modificar o mesmo registro de um conflito de gravação-gravação fará com que a nova operação falhe. No entanto, se as duas operações modificam diferentes registros, as operações terão êxito.  
  
-   Cada instrução é executada em isolamento de instantâneo para que novas operações não é possível ver as alterações feitas pelas instruções existentes. Mesmo se as instruções simultâneas são executadas na mesma transação SQL engine cria transações no escopo do lote para cada instrução que são isoladas uns dos outros. No entanto, no escopo do lote de transações ainda são associadas juntos para que a reversão de uma transação no escopo do lote afeta outros no mesmo lote.  
  
-   Não são permitidas operações de DDL em transações de usuário para que eles falharão imediatamente.  
  
 **MARS e procedimentos armazenados compilados nativamente**  
  
 Procedimentos armazenados compilados nativamente podem ser executados em conexões de MARS habilitado e podem gerar outra instrução da execução somente quando um ponto de suspensão é encontrado. Um ponto de suspensão requer uma instrução SELECT, que é a única instrução em um procedimento armazenado compilado nativamente que pode suspender a execução para outra instrução. Se uma instrução SELECT não está presente no procedimento não produzirá, ele será executado até a conclusão antes de começam a outras instruções.  
  
 **Transações de OLTP na memória e MARS**  
  
 As alterações feitas por instruções e blocos atômicos são intercalados são isoladas uns dos outros. Por exemplo, se uma instrução ou bloco atômico faz algumas alterações e, em seguida, gera a execução para outra instrução, a nova instrução não verão as alterações feitas pela primeira instrução. Além disso, quando a primeira instrução retoma a execução, ele não verá as alterações feitas por quaisquer outras instruções. Instruções só verá as alterações que são terminadas e confirmadas antes que a instrução se inicia.  
  
 Uma nova transação de usuário pode ser iniciada dentro da transação do usuário atual usando a instrução BEGIN TRANSACTION – isso é suportado apenas no modo de interoperabilidade para que BEGIN TRANSACTION só pode ser chamado em uma instrução T-SQL e não de dentro de um nativamente armazenado procedimento. Você pode criar uma consulta salva em uma transação usando SAVE TRANSACTION ou uma chamada à API a transação do ponto. Save(save_point_name) para reverter ao ponto de salvamento. Esse recurso também é habilitado somente de instruções T-SQL e não de dentro de procedimentos armazenados compilados nativamente.  
  
 **Índices columnstore e MARS**  
  
 SQL Server (começando com o 2016) dá suporte a MARS com índices columnstore. O SQL Server 2014 usa o MARS para conexões somente leitura com tabelas que contenham um índice columnstore.    No entanto, o SQL Server 2014 não é compatível com o MARS para operações de DML (linguagem de manipulação de dados) simultâneas em uma tabela com um índice columnstore. Quando isso ocorrer, o SQL Server encerrará as conexões e anulará as transações.   SQL Server 2012 tem índices columnstore de somente leitura e o MARS não se aplica a eles.  
  
## <a name="sql-server-native-client-ole-db-provider"></a>Provedor OLE DB do SQL Server Native Client  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client dá suporte a MARS por meio da adição da propriedade de inicialização de SSPROP_INIT_MARSCONNECTION dados fonte, que é implementada no conjunto de propriedades DBPROPSET_SQLSERVERDBINIT. Além disso, uma nova palavra-chave de cadeia de conexão, **MarsConn**, foi adicionada. Ele aceita **verdadeira** ou **falso** valores; **falsos** é o padrão.  
  
 A propriedade da fonte de dados DBPROP_MULTIPLECONNECTIONS é padronizada como VARIANT_TRUE. Isto significa que o provedor gerará várias conexões para oferecer suporte a vários objetos simultâneos do conjunto de linhas e do comando. Quando MARS está habilitado, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client pode dar suporte a vários objetos de comando e o conjunto de linhas em uma única conexão, portanto MULTIPLE_CONNECTIONS é definido como VARIANT_FALSE por padrão.  
  
 Para obter mais informações sobre os aprimoramentos feitos no conjunto de propriedades DBPROPSET_SQLSERVERDBINIT, consulte [propriedades de inicialização e autorização](../../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
### <a name="sql-server-native-client-ole-db-provider-example"></a>Exemplo de provedor OLE DB do SQL Server Native Client  
 Neste exemplo, um objeto de fonte de dados é criado usando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor OLE DB nativo e o MARS é habilitado usando a de propriedades DBPROPSET_SQLSERVERDBINIT antes que o objeto de sessão é criado.  
  
```  
#include <sqlncli.h>  
  
IDBInitialize *pIDBInitialize = NULL;  
IDBCreateSession *pIDBCreateSession = NULL;  
IDBProperties *pIDBProperties = NULL;  
  
// Create the data source object.  
hr = CoCreateInstance(CLSID_SQLNCLI10, NULL,  
   CLSCTX_INPROC_SERVER,  
   IID_IDBInitialize,   
    (void**)&pIDBInitialize);  
  
hr = pIDBInitialize->QueryInterface(IID_IDBProperties, (void**)&pIDBProperties);  
  
// Set the MARS property.  
DBPROP rgPropMARS;  
  
// The following is necessary since MARS is off by default.  
rgPropMARS.dwPropertyID = SSPROP_INIT_MARSCONNECTION;  
rgPropMARS.dwOptions = DBPROPOPTIONS_REQUIRED;  
rgPropMARS.dwStatus = DBPROPSTATUS_OK;  
rgPropMARS.colid = DB_NULLID;  
V_VT(&(rgPropMARS.vValue)) = VT_BOOL;  
V_BOOL(&(rgPropMARS.vValue)) = VARIANT_TRUE;  
  
// Create the structure containing the properties.  
DBPROPSET PropSet;  
PropSet.rgProperties = &rgPropMARS;  
PropSet.cProperties = 1;  
PropSet.guidPropertySet = DBPROPSET_SQLSERVERDBINIT;  
  
// Get an IDBProperties pointer and set the initialization properties.  
pIDBProperties->SetProperties(1, &PropSet);  
pIDBProperties->Release();  
  
// Initialize the data source object.  
hr = pIDBInitialize->Initialize();  
  
//Create a session object from a data source object.  
IOpenRowset * pIOpenRowset = NULL;  
hr = IDBInitialize->QueryInterface(IID_IDBCreateSession, (void**)&pIDBCreateSession));  
hr = pIDBCreateSession->CreateSession(  
   NULL,             // pUnkOuter  
   IID_IOpenRowset,  // riid  
  &pIOpenRowset ));  // ppSession  
  
// Create a rowset with a firehose mode cursor.  
IRowset *pIRowset = NULL;  
DBPROP rgRowsetProperties[2];  
  
// To get a firehose mode cursor request a   
// forward only read only rowset.  
rgRowsetProperties[0].dwPropertyID = DBPROP_IRowsetLocate;  
rgRowsetProperties[0].dwOptions = DBPROPOPTIONS_REQUIRED;  
rgRowsetProperties[0].dwStatus = DBPROPSTATUS_OK;  
rgRowsetProperties[0].colid = DB_NULLID;  
VariantInit(&(rgRowsetProperties[0].vValue));  
rgRowsetProperties[0].vValue.vt = VARIANT_BOOL;  
rgRowsetProperties[0].vValue.boolVal = VARIANT_FALSE;  
  
rgRowsetProperties[1].dwPropertyID = DBPROP_IRowsetChange;  
rgRowsetProperties[1].dwOptions = DBPROPOPTIONS_REQUIRED;  
rgRowsetProperties[1].dwStatus = DBPROPSTATUS_OK;  
rgRowsetProperties[1].colid = DB_NULLID;  
VariantInit(&(rgRowsetProperties[1].vValue));  
rgRowsetProperties[1].vValue.vt = VARIANT_BOOL;  
rgRowsetProperties[1].vValue.boolVal = VARIANT_FALSE;  
  
DBPROPSET rgRowsetPropSet[1];  
rgRowsetPropSet[0].rgProperties = rgRowsetProperties  
rgRowsetPropSet[0].cProperties = 2  
rgRowsetPropSet[0].guidPropertySet = DBPROPSET_ROWSET;  
  
hr = pIOpenRowset->OpenRowset (NULL,  
   &TableID,  
   NULL,  
   IID_IRowset,  
   1,  
   rgRowsetPropSet  
   (IUnknown**)&pIRowset);  
```  
  
## <a name="sql-server-native-client-odbc-driver"></a>Driver ODBC do SQL Server Native Client  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client dá suporte a MARS por meio de adições para o [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) e [SQLGetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) funções. SQL_COPT_SS_MARS_ENABLED foi adicionada para aceitar SQL_MARS_ENABLED_YES ou SQL_MARS_ENABLED_NO, com SQL_MARS_ENABLED_NO sendo o padrão. Além disso, uma conexão nova palavra-chave, em sequência **Mars_Connection**, foi adicionada. Ela aceita valores “yes” ou “no”; “no” é o padrão.  
  
### <a name="sql-server-native-client-odbc-driver-example"></a>Exemplo do driver ODBC do SQL Server Native Client  
 Neste exemplo, o **SQLSetConnectAttr** função é usada para habilitar o MARS antes de chamar o **SQLDriverConnect** função para conectar-se o banco de dados. Depois que a conexão é feita, duas **SQLExecDirect** funções são chamadas para criar dois conjuntos de resultados separados na mesma conexão.  
  
```  
#include <sqlncli.h>  
  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_MARS_ENABLED, SQL_MARS_ENABLED_YES, SQL_IS_UINTEGER);  
SQLDriverConnect(hdbc, hwnd,   
   "DRIVER=SQL Server Native Client 10.0;  
   SERVER=(local);trusted_connection=yes;", SQL_NTS, szOutConn,   
   MAX_CONN_OUT, &cbOutConn, SQL_DRIVER_COMPLETE);  
  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt1);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt2);  
  
// The 2nd execute would have failed with connection busy error if  
// MARS were not enabled.  
SQLExecDirect(hstmt1, L”SELECT * FROM Authors”, SQL_NTS);  
SQLExecDirect(hstmt2, L”SELECT * FROM Titles”, SQL_NTS);  
  
// Result set processing can interleave.  
SQLFetch(hstmt1);  
SQLFetch(hstmt2);  
```  
  
## <a name="see-also"></a>Consulte também  
 [Recursos do SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [Usando conjuntos de resultados padrão do SQL Server](../../../relational-databases/native-client-odbc-cursors/implementation/using-sql-server-default-result-sets.md)  
  
  
