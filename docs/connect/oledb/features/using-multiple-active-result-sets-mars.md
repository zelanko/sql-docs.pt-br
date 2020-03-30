---
title: Usando MARS (vários conjuntos de resultados ativos) | Microsoft Docs
description: Usando MARS (vários conjuntos de resultados ativos)
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, MARS
- MSOLEDBSQL, MARS
- data access [OLE DB Driver for SQL Server], MARS
- Multiple Active Result Sets
- OLE DB Driver for SQL Server, MARS
- MARS [SQL Server]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 8174333abc11b47d62c154171726afebee24824f
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67988814"
---
# <a name="using-multiple-active-result-sets-mars"></a>Usando MARS (vários conjuntos de resultados ativos)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

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
>  Por padrão, a funcionalidade de MARS não é habilitada. Para usar o MARS ao conectar-se ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com o Driver do OLE DB para SQL Server, você precisa habilitá-lo especificamente em uma cadeia de conexão. Para obter mais informações, confira as seções do Driver do OLE DB para SQL Server, mais adiante neste tópico.  
  
 O Driver do OLE DB para SQL Server não limita o número de instruções ativas em uma conexão.  
  
 Os aplicativos típicos que não precisam ter mais de um lote de várias instruções ou de um procedimento armazenado em execução ao mesmo tempo se beneficiarão do MARS mesmo que não saibam como é feita sua implementação. Porém, aplicativos com requisitos mais complexos devem levar isso em conta.  
  
 O MARS habilita a execução intercalada de várias solicitações em uma única conexão. Isto é, ele permite que um lote seja executado e, dentro de sua execução, permite a execução de outras solicitações. Observe, porém, que o MARS é definido em termos de intercalação, e não em termos de execução paralela.  
  
 A infraestrutura do MARS permite que vários lotes sejam executados de uma maneira intercalada, embora a execução só possa ser alternada em pontos bem definidos. Além disso, a maioria das instruções deve ser executada atomicamente dentro de um lote. As instruções que retornam linhas para o cliente, que às vezes são chamadas de *pontos de produção*, têm permissão para intercalar a execução antes da conclusão, enquanto as linhas estão sendo enviadas para o cliente, por exemplo:  
  
-   SELECT  
  
-   FETCH  
  
-   RECEIVE  
  
 Qualquer outra instrução que seja executada como parte de um procedimento armazenado ou lote deve ser executada até a conclusão, antes que a execução possa ser alterada para outras solicitações do MARS.  
  
 A maneira exata que os lotes são intercalados na execução é influenciada por vários fatores e é difícil prever a sequência exata em que os comandos de vários lotes que contêm pontos de produção será executada. Tenha cuidado para evitar efeitos colaterais indesejáveis devido a execução intercalada desses lotes complexos.  
  
 Evite problemas usando chamadas de API, em vez de instruções do [!INCLUDE[tsql](../../../includes/tsql-md.md)], para gerenciar o estado de conexão (SET, USE) e as transações (BEGIN TRAN, COMMIT, ROLLBACK), não incluindo essas instruções em lotes de várias instruções que contenham pontos de produção e serializando a execução de tais lotes consumindo ou cancelando todos os resultados.  
  
> [!NOTE]  
>  Um lote ou procedimento armazenado que inicie uma transação manual ou implícita quando o MARS está habilitado deve concluir a transação antes de ser encerrado. Se não fizer, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] acumulará todas as alterações feitas pela transação quando o lote for concluído. Essa transação é gerenciada pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como uma transação de escopo em lote. Este é um tipo novo de transação introduzido no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] para habilitar procedimentos armazenados existentes com bom comportamento para uso quando o MARS for habilitado. Para obter mais informações sobre transações com escopo do lote, confira [Instruções de transação &#40;Transact-SQL&#41;](../../../t-sql/statements/statements.md).  
  
 Para obter um exemplo de como usar MARS do ADO, confira [Como usar o ADO com o Driver do OLE DB para SQL Server](../../oledb/applications/using-ado-with-oledb-driver-for-sql-server.md).  
  
## <a name="in-memory-oltp"></a>OLTP na memória  
 O OLTP in-memory dá suporte a MARS usando consultas e procedimentos armazenados compilados nativamente. O MARS permite solicitar dados de várias consultas sem a necessidade de recuperar completamente cada conjunto de resultados antes de enviar uma solicitação para buscar linhas de um novo conjunto de resultados. Para ler com êxito de vários conjuntos de resultados abertos, você precisa usar uma conexão habilitada para MARS.  
  
 O MARS é desabilitado por padrão, portanto, você precisa habilitá-lo explicitamente adicionando `MultipleActiveResultSets=True` a uma cadeia de conexão. O seguinte exemplo demonstra como se conectar a uma instância do SQL Server e como especificar que o MARS está habilitado:  
  
```  
Data Source=MSSQL; Initial Catalog=AdventureWorks; Integrated Security=SSPI; MultipleActiveResultSets=True  
```  
  
 O MARS com OLTP in-memory é essencialmente o mesmo que o MARS no restante do mecanismo do SQL. O conteúdo a seguir lista as diferenças ao usar o MARS em tabelas com otimização de memória e nos procedimentos armazenados compilados de modo nativo.  
  
 **MARS e tabelas com otimização de memória**  
  
 Veja abaixo as diferenças entre as tabelas baseadas em disco e as tabelas com otimização de memória ao usar uma conexão habilitada para MARS:  
  
-   Duas instruções podem modificar dados no mesmo objeto de destino, mas se as duas tentarem modificar o mesmo registro, um conflito de gravação/gravação fará com que a nova operação falhe. No entanto, se ambas as operações modificarem registros diferentes, as operações terão êxito.  
  
-   Cada instrução é executada em isolamento de SNAPSHOT para que novas operações não possam ver as alterações feitas pelas instruções existentes. Mesmo que as instruções simultâneas sejam executadas na mesma transação, o mecanismo do SQL cria transações com escopo do lote para cada instrução isolada das outras. No entanto, as transações com escopo do lote ainda estão associadas para que a reversão de uma transação com escopo do lote afete outras no mesmo lote.  
  
-   As operações DDL não são permitidas em transações de usuário, então elas falharão imediatamente.  
  
 **MARS e procedimentos armazenados compilados nativamente**  
  
 Os procedimentos armazenados compilados nativamente podem ser executados em conexões MARS habilitadas e podem suspender a execução, passando para outra instrução, o que ocorre somente quando um ponto de suspensão é encontrado. Um ponto de suspensão requer uma instrução SELECT, que é a única instrução em um procedimento armazenado compilado nativamente que pode suspender a execução e passar para outra instrução. Se uma instrução SELECT não estiver presente no procedimento ele não será suspenso, mas sim executado até concluir, para que depois outras instruções comecem.  
  
 **MARS e transações OLTP in-memory**  
  
 As alterações feitas por instruções e blocos atômicos intercalados são isoladas umas das outras. Por exemplo, se uma instrução ou um bloco atômico fizer algumas alterações e, em seguida, suspender a execução e passar para outra instrução, a nova instrução não verá as alterações feitas pela primeira instrução. Além disso, quando a primeira instrução retomar a execução, ela não verá nenhuma alteração feita por outras instruções. As instruções verão apenas as alterações que foram concluídas e confirmadas antes da instrução em questão ser iniciada.  
  
 Uma nova transação de usuário pode ser iniciada dentro da transação de usuário atual usando a instrução BEGIN TRANSACTION – esse procedimento é compatível somente no modo de interoperabilidade, de modo que a BEGIN TRANSACTION só pode ser chamada por meio de uma instrução T-SQL e não de dentro de um procedimento armazenado compilado nativamente. Você pode criar um ponto de salvamento em uma transação usando SAVE TRANSACTION ou uma chamada à API para transaction.Save(save_point_name) para reverter para o ponto de salvamento. Esse recurso também é habilitado apenas de instruções T-SQL e não de dentro de procedimentos armazenados compilados nativamente.  
  
 **MARS e índices columnstore**  
  
 O SQL Server (do 2016 em diante) dá suporte ao MARS com índices columnstore. O SQL Server 2014 usa o MARS para conexões somente leitura com tabelas que contenham um índice columnstore.    No entanto, o SQL Server 2014 não é compatível com o MARS para operações de DML (linguagem de manipulação de dados) simultâneas em uma tabela com um índice columnstore. Quando isso ocorrer, o SQL Server encerrará as conexões e anulará as transações.   O SQL Server 2012 tem índices columnstore somente leitura e o MARS não se aplica a eles.  
  
## <a name="ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server  
 O OLE DB Driver for SQL Server dá suporte ao MARS por meio da adição da propriedade de inicialização de fonte de dados SSPROP_INIT_MARSCONNECTION, que é implementada no conjunto de propriedades DBPROPSET_SQLSERVERDBINIT. Além disso, uma nova palavra-chave de cadeia de conexão, **MarsConn**, foi adicionada. Ele aceita valores **true** ou **false**, sendo **false** o padrão.  
  
 A propriedade da fonte de dados DBPROP_MULTIPLECONNECTIONS é padronizada como VARIANT_TRUE. Isto significa que o provedor gerará várias conexões para oferecer suporte a vários objetos simultâneos do conjunto de linhas e do comando. Quando o MARS está habilitado, o OLE DB Driver for SQL Server pode dar suporte a vários objetos do conjunto de linhas e do comando em uma única conexão e, portanto, MULTIPLE_CONNECTIONS é definido como VARIANT_FALSE por padrão.  
  
 Para obter mais informações sobre aprimoramentos realizados no conjunto de propriedades DBPROPSET_SQLSERVERDBINIT, confira [Propriedades de inicialização e autorização](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
### <a name="ole-db-driver-for-sql-server-example"></a>Exemplo do OLE DB Driver for SQL Server  
 Neste exemplo, um objeto de fonte de dados foi criado usando o OLE DB Driver for SQL Server e o MARS foi habilitado usando o conjunto de propriedades DBPROPSET_SQLSERVERDBINIT antes da criação do objeto da sessão.  
  
```  
#include <msoledbsql.h>  
  
IDBInitialize *pIDBInitialize = NULL;  
IDBCreateSession *pIDBCreateSession = NULL;  
IDBProperties *pIDBProperties = NULL;  
  
// Create the data source object.  
hr = CoCreateInstance(CLSID_MSOLEDBSQL, NULL,  
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

  
## <a name="see-also"></a>Consulte Também  
 [Recursos do Driver do OLE DB para SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)   
 
  
  
