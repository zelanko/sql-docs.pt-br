---
title: Provedor Microsoft OLE DB para SQL Server | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB provider for SQL Server
- OLE DB provider for SQL Server [ADO]
- SQLOLEDB [ADO]
ms.assetid: 99bc40c4-9181-4ca1-a06f-9a1a914a0b7b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 17146ee01a2e4b99dbe50b1d81aedaf0ad7e0b94
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65095883"
---
# <a name="microsoft-ole-db-provider-for-sql-server-overview"></a>Provedor Microsoft OLE DB para visão geral do SQL Server
O Microsoft OLE DB Provider para SQL Server, SQLOLEDB, permite que o ADO para acessar o Microsoft SQL Server.

> [!IMPORTANT]
> O Microsoft OLE DB Provider for SQL Server (SQLOLEDB) permanece preterido e não é recomendável usá-lo para o novo trabalho de desenvolvimento. Em vez disso, use a nova [Microsoft Driver do OLE DB para SQL Server](../../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL) que será atualizado com os recursos mais recentes do servidor.

## <a name="connection-string-parameters"></a>Parâmetros de cadeia de caracteres de Conexão
 Para se conectar ao provedor, defina as *provedor* argumento para o [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propriedade para:

```vb
SQLOLEDB
```

 Esse valor também pode ser definido ou lidos usando o [provedor](../../../ado/reference/ado-api/provider-property-ado.md) propriedade.

## <a name="typical-connection-string"></a>Cadeia de caracteres de Conexão típica
 Uma cadeia de caracteres de conexão típica para esse provedor é:

```vb
"Provider=SQLOLEDB;Data Source=serverName;"
Initial Catalog=databaseName;
User ID=MyUserID;Password=MyPassword;"
```

 A cadeia de caracteres consiste nessas palavras-chave:

|Palavra-chave|Descrição|
|-------------|-----------------|
|**Provedor**|Especifica o provedor OLE DB para SQL Server.|
|**Fonte de dados** ou **Server**|Especifica o nome de um servidor.|
|**Catálogo inicial** ou **banco de dados**|Especifica o nome de um banco de dados no servidor.|
|**ID de usuário** ou **uid**|Especifica o nome de usuário (para autenticação do SQL Server).|
|**Senha** ou **pwd**|Especifica a senha do usuário (para autenticação do SQL Server).|

> [!NOTE]
>  Se você estiver se conectando a um provedor de fonte de dados que dá suporte à autenticação do Windows, você deve especificar **Trusted_Connection = yes** ou **Integrated Security = SSPI** em vez de ID de usuário e senha informações na cadeia de conexão.

## <a name="provider-specific-connection-parameters"></a>Parâmetros de Conexão específicas do provedor
 O provedor oferece suporte a vários parâmetros de conexão específica do provedor além daqueles definidos pelo ADO. Como com as propriedades de conexão ADO, essas propriedades específicas do provedor podem ser definidas por meio de [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção de um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) ou pode ser definido como parte do **ConnectionString**.

|Parâmetro|Descrição|
|---------------|-----------------|
|Trusted_Connection|Indica o modo de autenticação do usuário. Isso pode ser definido como **Yes** ou **não**. O valor padrão é **não**. Se essa propriedade é definida como **Yes**, SQLOLEDB usa o modo de autenticação do Microsoft Windows NT para autorizar o acesso de usuário no banco de dados do SQL Server especificado pela **local** e [fonte de dados ](../../../ado/reference/ado-api/datasource-property-ado.md) valores de propriedade. Se essa propriedade é definida como **não**, SQLOLEDB usa modo misto para autorizar o acesso de usuário no banco de dados do SQL Server. O logon do SQL Server e a senha são especificadas na **Id de usuário** e **senha** propriedades.|
|Idioma Atual|Indica um nome de idioma do SQL Server. Identifica o idioma usado para seleção de mensagem de sistema e formatação. O idioma deve ser instalado no SQL Server, caso contrário, abertura a conexão falhará.|
|Endereço de Rede|Indica o endereço de rede do SQL Server especificado pela **local** propriedade.|
|Biblioteca de rede|Indica o nome da biblioteca de rede (DLL) usado para se comunicar com o SQL Server. O nome não deve incluir o caminho ou a extensão de nome de arquivo .dll. O padrão é fornecido pela configuração de cliente do SQL Server.|
|Usar procedimento para preparar|Determina se o SQL Server cria procedimentos armazenados temporários quando os comandos são preparados (pela **preparado** propriedade).|
|Tradução automática|Indica se os caracteres OEM/ANSI são convertidos. Essa propriedade pode ser definida como **verdadeira** ou **falso**. O valor padrão é **True**. Se essa propriedade é definida como **verdadeira**, SQLOLEDB executa a conversão de caracteres OEM/ANSI quando cadeias de caracteres multibyte são recuperadas de ou enviadas para o SQL Server. Se essa propriedade é definida como **falsos**, SQLOLEDB não faz a conversão de caracteres OEM/ANSI em dados de cadeia de caracteres de vários bytes.|
|Tamanho do Pacote|Indica um tamanho de pacote de rede em bytes. O valor de propriedade de tamanho de pacote deve estar entre 512 e 32767. O tamanho de pacote de rede SQLOLEDB padrão é 4096.|
|Nome do Aplicativo|Indica o nome do aplicativo cliente.|
|ID da Estação de Trabalho|Uma cadeia de caracteres que identifica a estação de trabalho.|

## <a name="command-object-usage"></a>Uso do objeto Command
 SQLOLEDB aceita uma amálgama de ODBC, ANSI e específicas do SQL Server Transact-SQL como sintaxe válida. Por exemplo, a seguinte instrução SQL usa uma sequência de escape do ODBC SQL para especificar a função de cadeia de caracteres LCASE:

```sql
SELECT customerid={fn LCASE(CustomerID)} FROM Customers

```

 LCASE retorna uma cadeia de caracteres, convertendo todos os caracteres em maiúscula aos seus equivalentes em minúsculas. A função de cadeia de caracteres SQL ANSI inferior executa a mesma operação, portanto, a seguinte instrução SQL é um ANSI equivalente à instrução ODBC apresentada anteriormente:

```sql
SELECT customerid=LOWER(CustomerID) FROM Customers

```

 SQLOLEDB processa com êxito o formulário da instrução quando especificado como o texto para um comando.

## <a name="stored-procedures"></a>Procedimentos armazenados
 Ao executar um SQL Server armazenado procedimento usando um comando SQLOLEDB, use a sequência de escape ODBC chamada de procedimento no texto do comando. SQLOLEDB, em seguida, usa o mecanismo de chamada de procedimento remoto do SQL Server para otimizar o processamento do comando. Por exemplo, a seguinte instrução SQL ODBC é o texto do comando preferencial sobre o formulário de Transact-SQL:

## <a name="odbc-sql"></a>ODBC SQL

```vb
{call SalesByCategory('Produce', '1995')}

```

## <a name="transact-sql"></a>Transact-SQL

```sql
EXECUTE SalesByCategory 'Produce', '1995'

```

## <a name="sql-server-features"></a>Recursos do SQL Server
 Com o SQL Server, o ADO pode usar XML para **comando** inserir e recuperar os resultados no formato de fluxo XML em vez de usar **Recordset** objetos. Para obter mais informações, consulte [usando fluxos de entrada de comando](../../../ado/guide/data/command-streams.md) e [recuperando conjuntos de resultados em fluxos](../../../ado/guide/data/retrieving-resultsets-into-streams.md).

### <a name="accessing-sqlvariant-data-using-mdac-27-mdac-28-or-windows-dac-60"></a>Acessando dados sql_variant usando MDAC 2.7, o MDAC 2.8 ou o Windows DAC 6.0
 Microsoft SQL Server tem um tipo de dados chamado **sql_variant**. Semelhante do OLE DB **DBTYPE_VARIANT**, o **sql_variant** tipo de dados pode armazenar dados de vários tipos diferentes. No entanto, há algumas diferenças importantes entre **DBTYPE_VARIANT** e **sql_variant**. ADO também lida com dados armazenados como um **sql_variant** Diferentemente de como ele lida com outros tipos de dados de valor. A lista a seguir descreve problemas devem ser consideradas quando você acessa dados do SQL Server armazenados em colunas do tipo **sql_variant**.

-   No MDAC 2.7, MDAC 2.8 e Windows Data Access Components (Windows DAC) 6.0, o provedor OLE DB para SQL Server dá suporte a **sql_variant** tipo. O provedor OLE DB para ODBC, não.

-   O **sql_variant** tipo corresponde exatamente a **DBTYPE_VARIANT** tipo de dados.  O **sql_variant** tipo dá suporte a alguns novos subtipos não tem suportados pelo **DBTYPE_VARIANT,** incluindo **GUID**, **ANSI** (não-UNICODE) cadeias de caracteres, e **BIGINT**. Usando subtipos diferente daqueles listados anteriormente funcionará corretamente.

-   O **sql_variant** subtipo **NUMÉRICO** não coincide com o **DBTYPE_DECIMAL** de tamanho.

-   Várias coerções de tipo de dados resultará em tipos que não correspondem. Por exemplo, a coerção uma **sql_variant** com um subtipo do **GUID** para um **DBTYPE_VARIANT** resultará em um subtipo do **safearray**(bytes) . Conversão desse tipo de volta para um **sql_variant** resultará em um novo subtipo **matriz**(bytes).

-   **Conjunto de registros** campos que contêm **sql_variant** dados podem ser remotos (empacotado) ou persistente somente se o **sql_variant** contiver subtipos específicos. A tentativa de remoto ou manter os dados com o seguinte sem suporte subtipos causará um erro de tempo de execução (não há suporte para conversão) do provedor de persistência de Microsoft (MSPersist): **VT_VARIANT**, **VT_RECORD**, **VT_ILLEGAL**, **VT_UNKNOWN**, **VT_BSTR**, and **VT_DISPATCH.**

-   O provedor OLE DB para SQL Server no MDAC 2.7, MDAC 2.8 e 6.0 do Windows DAC tem uma propriedade dinâmica chamada **permitir variantes nativas** que, como o nome sugere, permite que os desenvolvedores acessem os **sql_variant** em seu formulário nativo em vez de um **DBTYPE_VARIANT**. Se essa propriedade for definida e um **conjunto de registros** é aberta com o mecanismo de Cursor do cliente (**adUseClient**), o **Recordset.Open** chamada falhará. Se essa propriedade é definida e uma **conjunto de registros** é aberto com cursores de servidor (**adUseServer**), o **Recordset.Open** chamada terá êxito, mas acessando as colunas do tipo **sql_variant** produzirá um erro.

-   Em aplicativos cliente que usam MDAC 2.5 **sql_variant** dados podem ser usados com consultas no Microsoft SQL Server. No entanto, os valores de **sql_variant** dados são tratados como cadeias de caracteres. Tais aplicativos cliente devem ser atualizados para MDAC 2.7, o MDAC 2.8 ou o Windows DAC 6.0.

## <a name="recordset-behavior"></a>Comportamento do conjunto de registros
 SQLOLEDB não é possível usar cursores do SQL Server para suportar o resultado de vários gerado por muitos comandos. Se um consumidor solicitar um conjunto de registros que exigem suporte de cursor do SQL Server, ocorrerá um erro se o texto do comando usado mais de um único conjunto de registros gera como resultado.

 Conjuntos de registros SQLOLEDB roláveis são compatíveis com cursores do SQL Server. SQL Server impõe limitações sobre cursores que são sensíveis às alterações feitas por outros usuários do banco de dados. Especificamente, as linhas em alguns cursores não podem ser ordenadas e tentar criar um conjunto de registros usando um comando que contém uma cláusula SQL ORDER BY pode falhar.

## <a name="dynamic-properties"></a>Propriedades Dinâmicas
 O Microsoft OLE DB Provider para SQL Server insere várias propriedades dinâmicas para o **propriedades** coleção da não abertos [Conexão](../../../ado/reference/ado-api/connection-object-ado.md), [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md)e [ Comando](../../../ado/reference/ado-api/command-object-ado.md) objetos.

 As tabelas a seguir são um cross-index dos nomes de ADO e OLE DB para cada propriedade dinâmica. O referência do programador DB OLE se refere a um nome de propriedade ADO usando o termo "Descrição". Você pode encontrar mais informações sobre essas propriedades na referência do OLE DB do programador. Pesquise o nome da propriedade do OLE DB no índice ou consulte [apêndice c: Propriedades OLE DB](https://msdn.microsoft.com/deded3ff-f508-4e1b-b2b1-fd9afd3bd292).

## <a name="connection-dynamic-properties"></a>Propriedades dinâmicas da Conexão
 As propriedades a seguir são adicionadas para o **propriedades** coleção da **Conexão** objeto.

|Nome da propriedade ADO|Nome da propriedade do OLE DB|
|-----------------------|--------------------------|
|Sessões ativas|DBPROP_ACTIVESESSIONS|
|Anulação Asynchable|DBPROP_ASYNCTXNABORT|
|Confirmação de Asynchable|DBPROP_ASYNCTNXCOMMIT|
|Níveis de isolamento de confirmação automática|DBPROP_SESS_AUTOCOMMITISOLEVELS|
|Local do catálogo|DBPROP_CATALOGLOCATION|
|Termo do catálogo|DBPROP_CATALOGTERM|
|Definição de coluna|DBPROP_COLUMNDEFINITION|
|Connect Timeout|DBPROP_INIT_TIMEOUT|
|Catálogo atual|DBPROP_CURRENTCATALOG|
|fonte de dados|DBPROP_INIT_DATASOURCE|
|Nome da Fonte de Dados|DBPROP_DATASOURCENAME|
|Objeto de fonte de dados modelo de Threading|DBPROP_DSOTHREADMODEL|
|Nome do DBMS|DBPROP_DBMSNAME|
|Versão do DBMS|DBPROP_DBMSVER|
|Propriedades estendidas|DBPROP_INIT_PROVIDERSTRING|
|Suporte GROUP BY|DBPROP_GROUPBY|
|Suporte a tabelas heterogêneas|DBPROP_HETEROGENEOUSTABLES|
|Maiusculas e minúsculas do identificador|DBPROP_IDENTIFIERCASE|
|Catálogo Inicial|DBPROP_INIT_CATALOG|
|Níveis de isolamento|DBPROP_SUPPORTEDTXNISOLEVELS|
|Retenção de isolamento|DBPROP_SUPPORTEDTXNISORETAIN|
|Identificador de Localidade|DBPROP_INIT_LCID|
|Tamanho máximo de índice|DBPROP_MAXINDEXSIZE|
|Tamanho máximo da linha|DBPROP_MAXROWSIZE|
|Tamanho máximo de linha inclui BLOB|DBPROP_MAXROWSIZEINCLUDESBLOB|
|Máximo de tabelas em SELECT|DBPROP_MAXTABLESINSELECT|
|Vários conjuntos de parâmetros|DBPROP_MULTIPLEPARAMSETS|
|Vários resultados|DBPROP_MULTIPLERESULTS|
|Vários objetos de armazenamento|DBPROP_MULTIPLESTORAGEOBJECTS|
|Atualização multi-tabela|DBPROP_MULTITABLEUPDATE|
|Ordem de agrupamento de NULL|DBPROP_NULLCOLLATION|
|Comportamento de concatenação nulo|DBPROP_CONCATNULLBEHAVIOR|
|Versão do OLE DB|DBPROP_PROVIDEROLEDBVER|
|Suporte do objeto OLE|DBPROP_OLEOBJECTS|
|Suporte de conjunto de linhas aberto|DBPROP_OPENROWSETSUPPORT|
|Colunas ORDER BY na lista de seleção|DBPROP_ORDERBYCOLUMNSINSELECT|
|Disponibilidade do parâmetro de saída|DBPROP_OUTPUTPARAMETERAVAILABILITY|
|Acessadores passe por referência|DBPROP_BYREFACCESSORS|
|Senha|DBPROP_AUTH_PASSWORD|
|Informações de Persistência de Segurança|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|
|Tipo de ID persistente|DBPROP_PERSISTENTIDTYPE|
|Preparar comportamento do abortar|DBPROP_PREPAREABORTBEHAVIOR|
|Preparar comportamento da confirmação|DBPROP_PREPARECOMMITBEHAVIOR|
|Termo de procedimento|DBPROP_PROCEDURETERM|
|Aviso|DBPROP_INIT_PROMPT|
|Nome amigável do provedor|DBPROP_PROVIDERFRIENDLYNAME|
|Nome do Provedor|DBPROP_PROVIDERFILENAME|
|Versão do provedor|DBPROP_PROVIDERVER|
|Fonte de dados somente leitura|DBPROP_DATASOURCEREADONLY|
|Conversões de conjunto de linhas no comando|DBPROP_ROWSETCONVERSIONSONCOMMAND|
|Termo do esquema|DBPROP_SCHEMATERM|
|Uso do esquema|DBPROP_SCHEMAUSAGE|
|Suporte do SQL|DBPROP_SQLSUPPORT|
|Armazenamento estruturado|DBPROP_STRUCTUREDSTORAGE|
|Suporte subconsulta|DBPROP_SUBQUERIES|
|Termo de tabela|DBPROP_TABLETERM|
|Transação DDL|DBPROP_SUPPORTEDTXNDDL|
|ID de usuário|DBPROP_AUTH_USERID|
|Nome do Usuário|DBPROP_USERNAME|
|Identificador de janela|DBPROP_INIT_HWND|

## <a name="recordset-dynamic-properties"></a>Propriedades dinâmicas do conjunto de registros
 As propriedades a seguir são adicionadas para o **propriedades** coleção da **Recordset** objeto.

|Nome da propriedade ADO|Nome da propriedade do OLE DB|
|-----------------------|--------------------------|
|Ordem de acesso|DBPROP_ACCESSORDER|
|Bloquear objetos de armazenamento|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Tipo de indicador|DBPROP_BOOKMARKTYPE|
|Possíveis de indicação|DBPROP_IROWSETLOCATE|
|Modificar linhas inseridas|DBPROP_CHANGEINSERTEDROWS|
|Privilégios de coluna|DBPROP_COLUMNRESTRICT|
|Notificação de conjunto de coluna|DBPROP_NOTIFYCOLUMNSET|
|Tempo limite de comando|DBPROP_COMMANDTIMEOUT|
|Adiar a coluna|DBPROP_DEFERRED|
|Atualizações de objetos de armazenamento de atraso|DBPROP_DELAYSTORAGEOBJECTS|
|Buscar na ordem inversa|DBPROP_CANFETCHBACKWARDS|
|Manter linhas|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|Linhas imóveis|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsestLocate|
|IRowsetResynch||
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|Marcadores literais|DBPROP_LITERALBOOKMARKS|
|Identidade de linha literal|DBPROP_LITERALIDENTITY|
|Máximo de linhas abertas|DBPROP_MAXOPENROWS|
|Máximo de linhas pendentes|DBPROP_MAXPENDINGROWS|
|Máximo de linhas|DBPROP_MAXROWS|
|Granularidade de notificação|DBPROP_NOTIFICATIONGRANULARITY|
|Fases de notificação|DBPROP_NOTIFICATIONPHASES|
|Objetos transacionados|DBPROP_TRANSACTEDOBJECT|
|Alterações de outros visíveis|DBPROP_OTHERUPDATEDELETE|
|Inserções de outros visíveis|DBPROP_OTHERINSERT|
|Modificações próprias visíveis|DBPROP_OWNUPDATEDELETE|
|Indicações próprias visíveis|DBPROP_OWNINSERT|
|Preservar no abortar|DBPROP_ABORTPRESERVE|
|Preservar na confirmação|DBPROP_COMMITPRESERVE|
|Reinicialização rápida|DBPROP_QUICKRESTART|
|Eventos reentrantes|DBPROP_REENTRANTEVENTS|
|Remover linhas excluídas|DBPROP_REMOVEDELETED|
|Reportar múltiplas mudanças|DBPROP_REPORTMULTIPLECHANGES|
|Retorna inserções pendentes|DBPROP_RETURNPENDINGINSERTS|
|Notificação de exclusão da linha|DBPROP_NOTIFYROWDELETE|
|Primeira notificação de alteração de linha|DBPROP_NOTIFYROWFIRSTCHANGE|
|Notificação de inserção de linha|DBPROP_NOTIFYROWINSERT|
|Privilégios de linhas|DBPROP_ROWRESTRICT|
|Notificação de ressincronização de linha|DBPROP_NOTIFYROWRESYNCH|
|Modelo de Threading de linha|DBPROP_ROWTHREADMODEL|
|Notificação de alteração de desfazer de linha|DBPROP_NOTIFYROWUNDOCHANGE|
|Notificação de desfazer deleção de linha|DBPROP_NOTIFYROWUNDODELETE|
|Notificação desfazer inserção de linha|DBPROP_NOTIFYROWUNDOINSERT|
|Notificação de atualização de linha|DBPROP_NOTIFYROWUPDATE|
|Notificação de alteração de posição de busca do conjunto de linhas|DBPROP_NOTIFYROWSETFETCHPOSISIONCHANGE|
|Notificação de liberação de conjunto de linhas|DBPROP_NOTIFYROWSETRELEASE|
|Rolar na ordem inversa|DBPROP_CANSCROLLBACKWARDS|
|Cursor de servidor|DBPROP_SERVERCURSOR|
|Ignorar marcadores apagados|DBPROP_BOOKMARKSKIPPED|
|Identidade de linha forte|DBPROP_STRONGITDENTITY|
|Linhas exclusivas|DBPROP_UNIQUEROWS|
|Capacidade de atualização|DBPROP_UPDATABILITY|
|Usar indicadores|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>Propriedades dinâmicas do comando
 As propriedades a seguir são adicionadas para o **propriedades** coleção da **comando** objeto.

|Nome da propriedade ADO|Nome da propriedade do OLE DB|
|-----------------------|--------------------------|
|Ordem de acesso|DBPROP_ACCESSORDER|
|Caminho base|SSPROP_STREAM_BASEPATH|
|Bloquear objetos de armazenamento|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Tipo de indicador|DBPROP_BOOKMARKTYPE|
|Possíveis de indicação|DBPROP_IROWSETLOCATE|
|Modificar linhas inseridas|DBPROP_CHANGEINSERTEDROWS|
|Privilégios de coluna|DBPROP_COLUMNRESTRICT|
|Notificação de conjunto de coluna|DBPROP_NOTIFYCOLUMNSET|
|Tipo de Conteúdo|SSPROP_STREAM_CONTENTTYPE|
|Busca do cursor automaticamente|SSPROP_CURSORAUTOFETCH|
|Adiar a coluna|DBPROP_DEFERRED|
|Adiar Preparação|SSPROP_DEFERPREPARE|
|Atualizações de objetos de armazenamento de atraso|DBPROP_DELAYSTORAGEOBJECTS|
|Buscar na ordem inversa|DBPROP_CANFETCHBACKWARDS|
|Manter linhas|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|Linhas imóveis|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsetLocate|
|IRowsetResynch|DBPROP_IRowsetResynch|
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|Marcadores literais|DBPROP_LITERALBOOKMARKS|
|Identidade de linha literal|DBPROP_LITERALIDENTITY|
|Modo de bloqueio|DBPROP_LOCKMODE|
|Máximo de linhas abertas|DBPROP_MAXOPENROWS|
|Máximo de linhas pendentes|DBPROP_MAXPENDINGROWS|
|Máximo de linhas|DBPROP_MAXROWS|
|Granularidade de notificação|DBPROP_NOTIFICATIONGRANULARITY|
|Fases de notificação|DBPROP_NOTIFICATIONPHASES|
|Objetos transacionados|DBPROP_TRANSACTEDOBJECT|
|Alterações de outros visíveis|DBPROP_OTHERUPDATEDELETE|
|Inserções de outros visíveis|DBPROP_OTHERINSERT|
|Propriedade de codificação de saída|DBPROP_OUTPUTENCODING|
|Propriedade Stream de saída|DBPROP_OUTPUTSTREAM|
|Modificações próprias visíveis|DBPROP_OWNUPDATEDELETE|
|Indicações próprias visíveis|DBPROP_OWNINSERT|
|Preservar no abortar|DBPROP_ABORTPRESERVE|
|Preservar na confirmação|DBPROP_COMMITPRESERVE|
|Reinicialização rápida|DBPROP_QUICKRESTART|
|Eventos reentrantes|DBPROP_REENTRANTEVENTS|
|Remover linhas excluídas|DBPROP_REMOVEDELETED|
|Reportar múltiplas mudanças|DBPROP_REPORTMULTIPLECHANGES|
|Retorna inserções pendentes|DBPROP_RETURNPENDINGINSERTS|
|Notificação de exclusão da linha|DBPROP_NOTIFYROWDELETE|
|Primeira notificação de alteração de linha|DBPROP_NOTIFYROWFIRSTCHANGE|
|Notificação de inserção de linha|DBPROP_NOTIFYROWINSERT|
|Privilégios de linhas|DBPROP_ROWRESTRICT|
|Notificação de ressincronização de linha|DBPROP_NOTIFYROWRESYNCH|
|Modelo de Threading de linha|DBPROP_ROWTHREADMODEL|
|Notificação de alteração de desfazer de linha|DBPROP_NOTIFYROWUNDOCHANGE|
|Notificação de desfazer deleção de linha|DBPROP_NOTIFYROWUNDODELETE|
|Notificação desfazer inserção de linha|DBPROP_NOTIFYROWUNDOINSERT|
|Notificação de atualização de linha|DBPROP_NOTIFYROWUPDATE|
|Notificação de alteração de posição de busca do conjunto de linhas|DBPROP_NOTIFYROWSETFETCHPOSITIONCHANGE|
|Notificação de liberação de conjunto de linhas|DBPROP_NOTIFYROWSETRELEASE|
|Rolar na ordem inversa|DBPROP_CANSCROLLBACKWARDS|
|Cursor de servidor|DBPROP_SERVERCURSOR|
|Dados de servidor na inserção|DBPROP_SERVERDATAONINSERT|
|Ignorar marcadores apagados|DBPROP_BOOKMARKSKIP|
|Identidade de linha forte|DBPROP_STRONGIDENTITY|
|Capacidade de atualização|DBPROP_UPDATABILITY|
|Usar indicadores|DBPROP_BOOKMARKS|
|XML Root|SSPROP_STREAM_XMLROOT|
|XSL|SSPROP_STREAM_XSL|

 Para detalhes específicos de implementação e funcionais informações sobre o Microsoft SQL Server OLE DB Provider, consulte a [provedor do SQL Server](https://msdn.microsoft.com/adf1d6c4-5930-444a-9248-ff1979729635).

## <a name="see-also"></a>Consulte também
 [Propriedade ConnectionString (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [propriedade Provider (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
