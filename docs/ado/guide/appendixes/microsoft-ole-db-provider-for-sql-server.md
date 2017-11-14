---
title: Provedor Microsoft OLE DB para SQL Server | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- providers [ADO], OLE DB provider for SQL Server
- OLE DB provider for SQL Server [ADO]
- SQLOLEDB [ADO]
ms.assetid: 99bc40c4-9181-4ca1-a06f-9a1a914a0b7b
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 11f9d1d69332e1d32b1d6bbabd804ed222b620e1
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="microsoft-ole-db-provider-for-sql-server-overview"></a>Provedor Microsoft OLE DB para visão geral do SQL Server
O Microsoft OLE DB Provider para SQL Server, SQLOLEDB, permite que o ADO para acessar o Microsoft SQL Server.

## <a name="connection-string-parameters"></a>Parâmetros de cadeia de caracteres de Conexão
 Para se conectar ao provedor, defina o *provedor* argumento para o [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propriedade para:

```
SQLOLEDB
```

 Esse valor também pode ser definido ou lidos usando o [provedor](../../../ado/reference/ado-api/provider-property-ado.md) propriedade.

## <a name="typical-connection-string"></a>Cadeia de caracteres de Conexão típica
 Uma cadeia de conexão típica para esse provedor é:

```
"Provider=SQLOLEDB;Data Source=serverName;"
Initial Catalog=databaseName;
User ID=MyUserID;Password=MyPassword;"
```

 A cadeia de caracteres consiste nessas palavras-chave:

|Palavra-chave|Description|
|-------------|-----------------|
|**Provedor**|Especifica o provedor OLE DB para SQL Server.|
|**Fonte de dados** ou **Server**|Especifica o nome de um servidor.|
|**Catálogo inicial** ou **banco de dados**|Especifica o nome de um banco de dados no servidor.|
|**ID de usuário** ou **uid**|Especifica o nome de usuário (para autenticação do SQL Server).|
|**Senha** ou **pwd**|Especifica a senha do usuário (para autenticação do SQL Server).|

> [!NOTE]
>  Se você estiver se conectando a um provedor de fonte de dados que oferece suporte à autenticação do Windows, você deve especificar **Trusted_Connection = yes** ou **segurança integrada = SSPI** em vez de ID de usuário e senha informações na cadeia de conexão.

## <a name="provider-specific-connection-parameters"></a>Parâmetros de Conexão específicos do provedor
 O provedor oferece suporte a vários parâmetros de conexão específica do provedor, além daqueles definidos pelo ADO. Como com as propriedades de conexão ADO, essas propriedades específicas do provedor podem ser definidas por meio de [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção de um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) ou pode ser definido como parte do **ConnectionString**.

|Parâmetro|Description|
|---------------|-----------------|
|Trusted_Connection|Indica o modo de autenticação do usuário. Isso pode ser definido como **Sim** ou **não**. O valor padrão é **não**. Se essa propriedade é definida como **Sim**, SQLOLEDB usa o modo de autenticação do Microsoft Windows NT para autorizar o acesso de usuário no banco de dados do SQL Server especificada pelo **local** e [a fonte de dados ](../../../ado/reference/ado-api/datasource-property-ado.md) valores de propriedade. Se essa propriedade é definida como **não**, SQLOLEDB usa modo misto para autorizar o acesso de usuário no banco de dados do SQL Server. O logon do SQL Server e a senha são especificadas no **Id de usuário** e **senha** propriedades.|
|Idioma Atual|Indica um nome de idioma do SQL Server. Identifica o idioma usado para seleção de mensagem de sistema e formatação. O idioma deve ser instalado no SQL Server, caso contrário, abrir a conexão falhará.|
|Endereço de Rede|Indica o endereço de rede do SQL Server especificada pelo **local** propriedade.|
|Biblioteca de rede|Indica o nome da biblioteca de rede (DLL) usado para se comunicar com o SQL Server. O nome não deve incluir o caminho ou a extensão de nome de arquivo .dll. O padrão é fornecido pela configuração de cliente do SQL Server.|
|Use o procedimento para preparar|Determina se o SQL Server cria os procedimentos armazenados temporários quando os comandos são preparados (pelo **preparado** propriedade).|
|Tradução automática|Indica se caracteres OEM/ANSI são convertidos. Essa propriedade pode ser definida como **True** ou **False**. O valor padrão é **True**. Se essa propriedade é definida como **True**, SQLOLEDB executa a conversão de caracteres ANSI/OEM quando cadeias de caracteres de vários bytes são recuperadas do ou enviadas, o SQL Server. Se essa propriedade é definida como **False**, SQLOLEDB não executar a conversão de caracteres OEM/ANSI nos dados da cadeia de caracteres de bytes múltiplos.|
|Tamanho do Pacote|Indica um tamanho de pacote de rede em bytes. O valor de propriedade de tamanho de pacote deve estar entre 512 e 32767. O tamanho de pacote de rede SQLOLEDB padrão é 4096.|
|Nome do Aplicativo|Indica o nome do aplicativo cliente.|
|ID da Estação de Trabalho|Uma cadeia de caracteres que identifica a estação de trabalho.|

## <a name="command-object-usage"></a>Uso do objeto de comando
 SQLOLEDB aceita uma mistura de ODBC, ANSI e específicas do SQL Server Transact-SQL como sintaxe válida. Por exemplo, a seguinte instrução SQL usa uma sequência de escape do ODBC SQL para especificar a função de cadeia de caracteres LCASE:

```
SELECT customerid={fn LCASE(CustomerID)} FROM Customers

```

 LCASE retorna uma cadeia de caracteres, convertendo todos os caracteres em maiúscula aos seus equivalentes em minúsculas. A função de cadeia de caracteres SQL ANSI inferior executa a mesma operação, portanto, a seguinte instrução SQL é um ANSI equivalente à instrução ODBC apresentada anteriormente:

```
SELECT customerid=LOWER(CustomerID) FROM Customers

```

 SQLOLEDB processa qualquer formulário de instrução quando especificado como o texto de um comando com êxito.

## <a name="stored-procedures"></a>Procedimentos armazenados
 Ao executar um SQL Server procedimento armazenado usando um comando SQLOLEDB, use a sequência de escape de chamada de procedimento ODBC no texto do comando. SQLOLEDB, em seguida, usa o mecanismo de chamada de procedimento remoto do SQL Server para otimizar o processamento do comando. Por exemplo, a seguinte instrução SQL ODBC é o texto do comando preferencial sobre o formulário de Transact-SQL:

## <a name="odbc-sql"></a>ODBC SQL

```
{call SalesByCategory('Produce', '1995')}

```

## <a name="transact-sql"></a>Transact-SQL

```
EXECUTE SalesByCategory 'Produce', '1995'

```

## <a name="sql-server-features"></a>Recursos do SQL Server
 Com o SQL Server, o ADO pode usar XML para **comando** de entrada e recuperar resultados em formato de fluxo XML em vez de usar **registros** objetos. Para obter mais informações, consulte [usando fluxos de entrada de comando](../../../ado/guide/data/command-streams.md) e [recuperar conjuntos de resultados em fluxos](../../../ado/guide/data/retrieving-resultsets-into-streams.md).

### <a name="accessing-sqlvariant-data-using-mdac-27-mdac-28-or-windows-dac-60"></a>Acessando dados sql_variant usando MDAC 2.7, MDAC 2.8 ou Windows DAC 6.0
 Microsoft SQL Server tem um tipo de dados chamado **sql_variant**. Semelhante ao OLE DB **DBTYPE_VARIANT**, o **sql_variant** tipo de dados pode armazenar dados de vários tipos diferentes. No entanto, há algumas diferenças importantes entre **DBTYPE_VARIANT** e **sql_variant**. ADO também lida com dados armazenados como um **sql_variant** Diferentemente de como ele trata a outros tipos de dados de valor. A lista a seguir descreve os aspectos a serem considerados quando você acessa dados do SQL Server armazenados em colunas do tipo **sql_variant**.

-   No MDAC 2.7, MDAC 2.8 e Windows Data Access Components (Windows DAC) 6.0, o provedor OLE DB para SQL Server oferece suporte a **sql_variant** tipo. O provedor OLE DB para ODBC não aceita.

-   O **sql_variant** tipo corresponde exatamente a **DBTYPE_VARIANT** tipo de dados.  O **sql_variant** tipo oferece suporte a alguns novos subtipos não tem suportados por **DBTYPE_VARIANT,** incluindo **GUID**, **ANSI** (não UNICODE) cadeias de caracteres, e **BIGINT**. Uso de subtipos diferente daqueles listados anteriormente funcionará corretamente.

-   O **sql_variant** subtipo **NUMÉRICO** não coincide com o **DBTYPE_DECIMAL** em tamanho.

-   Várias coerções de tipo de dados resultará em tipos que não correspondem. Por exemplo, forçando uma **sql_variant** com um subtipo de **GUID** para um **DBTYPE_VARIANT** resultará em um subtipo de **safearray**(bytes) . Esse tipo de conversão de volta para um **sql_variant** resultará em um novo subtipo **matriz**(bytes).

-   **Conjunto de registros** campos que contêm **sql_variant** dados podem ser remotos (empacotado) ou persistente somente se o **sql_variant** contém subtipos específicos. A tentativa de remoto ou persistir dados com o seguinte sem suporte subtipos causará um erro de tempo de execução (não há suporte para conversão) do provedor de persistência de Microsoft (MSPersist): **VT_VARIANT**, **VT_RECORD**, **VT_ILLEGAL**, **VT_UNKNOWN**, **VT_BSTR**, e **VT_DISPATCH.**

-   O provedor OLE DB para SQL Server no MDAC 2.7, MDAC 2.8 e 6.0 do Windows DAC tem uma propriedade dinâmica chamada **permitir nativo variantes** que, como o nome sugere, permite aos desenvolvedores o acesso a **sql_variant** em seu formulário nativo em vez de um **DBTYPE_VARIANT**. Se essa propriedade for definida e um **registros** é aberta com o mecanismo de Cursor do cliente (**adUseClient**), o **Recordset.Open** chamada falhará. Se essa propriedade for definida e uma **registros** é aberto com cursores de servidor (**adUseServer**), o **Recordset.Open** chamada será bem-sucedida, mas acessando as colunas do tipo **sql_variant** produzirá um erro.

-   Em aplicativos cliente que usam MDAC 2.5, **sql_variant** dados podem ser usados com consultas no Microsoft SQL Server. No entanto, os valores de **sql_variant** dados são tratados como cadeias de caracteres. Tais aplicativos cliente devem ser atualizados para o MDAC 2.7, MDAC 2.8 ou Windows DAC 6.0.

## <a name="recordset-behavior"></a>Comportamento do conjunto de registros
 SQLOLEDB não é possível usar cursores do SQL Server para dar suporte o vários-resultados gerado por muitos comandos. Se um consumidor solicitar um conjunto de registros que requerem suporte de cursor do SQL Server, ocorrerá um erro se o texto do comando usado mais de um único conjunto de registros gera como resultado.

 Conjuntos de registros SQLOLEDB roláveis há suporte para cursores do SQL Server. SQL Server impõe limitações sobre cursores que são sensíveis às alterações feitas por outros usuários do banco de dados. Especificamente, as linhas em alguns cursores não podem ser ordenadas e tentar criar um conjunto de registros usando um comando que contém uma cláusula SQL ORDER BY pode falhar.

## <a name="dynamic-properties"></a>Propriedades Dinâmicas
 O Microsoft OLE DB Provider para SQL Server insere várias propriedades dinâmicas no **propriedades** coleção de não o aberta [Conexão](../../../ado/reference/ado-api/connection-object-ado.md), [registros](../../../ado/reference/ado-api/recordset-object-ado.md)e [ Comando](../../../ado/reference/ado-api/command-object-ado.md) objetos.

 As tabelas a seguir são um cross-index dos nomes de ADO e OLE DB para cada propriedade dinâmica. O referência do programador DB OLE refere-se a um nome de propriedade ADO, o termo "Descrição". Você pode encontrar mais informações sobre essas propriedades na referência do OLE DB do programador. Procure o nome da propriedade OLE DB no índice ou consulte [apêndice c: OLE DB Properties](http://msdn.microsoft.com/en-us/deded3ff-f508-4e1b-b2b1-fd9afd3bd292).

## <a name="connection-dynamic-properties"></a>Propriedades de Conexão dinâmica
 As propriedades a seguir são adicionadas para o **propriedades** coleção do **Conexão** objeto.

|Nome da propriedade ADO|Nome de propriedade do OLE DB|
|-----------------------|--------------------------|
|Sessões ativas|DBPROP_ACTIVESESSIONS|
|Anulação de Asynchable|DBPROP_ASYNCTXNABORT|
|Confirmação Asynchable|DBPROP_ASYNCTNXCOMMIT|
|Níveis de isolamento de confirmação automática|DBPROP_SESS_AUTOCOMMITISOLEVELS|
|Local do catálogo|DBPROP_CATALOGLOCATION|
|Termo do catálogo|DBPROP_CATALOGTERM|
|Definição de coluna|DBPROP_COLUMNDEFINITION|
|Connect Timeout|DBPROP_INIT_TIMEOUT|
|Catálogo atual|DBPROP_CURRENTCATALOG|
|Fonte de dados|DBPROP_INIT_DATASOURCE|
|Nome da Fonte de Dados|DBPROP_DATASOURCENAME|
|Modelo de Threading do objeto de fonte de dados|DBPROP_DSOTHREADMODEL|
|Nome do DBMS|DBPROP_DBMSNAME|
|Versão do DBMS|DBPROP_DBMSVER|
|Propriedades estendidas|DBPROP_INIT_PROVIDERSTRING|
|GRUPO de suporte|DBPROP_GROUPBY|
|Suporte a tabelas heterogêneos|DBPROP_HETEROGENEOUSTABLES|
|Diferenciação de maiusculas e minúsculas identificador|DBPROP_IDENTIFIERCASE|
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
|Atualização de várias tabela|DBPROP_MULTITABLEUPDATE|
|Ordem de agrupamento NULL|DBPROP_NULLCOLLATION|
|Comportamento de concatenação de nulos|DBPROP_CONCATNULLBEHAVIOR|
|Versão do banco de dados OLE|DBPROP_PROVIDEROLEDBVER|
|Suporte do objeto OLE|DBPROP_OLEOBJECTS|
|Suporte de conjunto de linhas aberto|DBPROP_OPENROWSETSUPPORT|
|Colunas ORDER BY na lista de seleção|DBPROP_ORDERBYCOLUMNSINSELECT|
|Disponibilidade de parâmetro de saída|DBPROP_OUTPUTPARAMETERAVAILABILITY|
|Acessadores passe por referência|DBPROP_BYREFACCESSORS|
|Senha|DBPROP_AUTH_PASSWORD|
|Informações de Persistência de Segurança|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|
|ID do tipo|DBPROP_PERSISTENTIDTYPE|
|Preparar o comportamento de anulação|DBPROP_PREPAREABORTBEHAVIOR|
|Preparar o comportamento de confirmação|DBPROP_PREPARECOMMITBEHAVIOR|
|Termo do procedimento|DBPROP_PROCEDURETERM|
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
|Suporte de subconsulta|DBPROP_SUBQUERIES|
|Termo de tabela|DBPROP_TABLETERM|
|Transação de DDL|DBPROP_SUPPORTEDTXNDDL|
|ID de usuário|DBPROP_AUTH_USERID|
|Nome do Usuário|DBPROP_USERNAME|
|Identificador de janela|DBPROP_INIT_HWND|

## <a name="recordset-dynamic-properties"></a>Propriedades do conjunto de registros dinâmicos
 As propriedades a seguir são adicionadas para o **propriedades** coleção do **registros** objeto.

|Nome da propriedade ADO|Nome de propriedade do OLE DB|
|-----------------------|--------------------------|
|Ordem de acesso|DBPROP_ACCESSORDER|
|Bloqueio de objetos de armazenamento|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Tipo de indicador|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|Alterar as linhas inseridas|DBPROP_CHANGEINSERTEDROWS|
|Privilégios de coluna|DBPROP_COLUMNRESTRICT|
|Notificação de conjunto de coluna|DBPROP_NOTIFYCOLUMNSET|
|Tempo limite de comando|DBPROP_COMMANDTIMEOUT|
|Adiar a coluna|DBPROP_DEFERRED|
|Atualizações de objetos de armazenamento de atraso|DBPROP_DELAYSTORAGEOBJECTS|
|Buscar com versões anteriores|DBPROP_CANFETCHBACKWARDS|
|Manter linhas|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|Linhas immobile|DBPROP_IMMOBILEROWS|
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
|Indicadores literal|DBPROP_LITERALBOOKMARKS|
|Identidade de linha literal|DBPROP_LITERALIDENTITY|
|Máximo de linhas aberto|DBPROP_MAXOPENROWS|
|Máximo de linhas pendentes|DBPROP_MAXPENDINGROWS|
|Máximo de linhas|DBPROP_MAXROWS|
|Granularidade de notificação|DBPROP_NOTIFICATIONGRANULARITY|
|Fases de notificação|DBPROP_NOTIFICATIONPHASES|
|Objetos transacionados|DBPROP_TRANSACTEDOBJECT|
|Outros alterações visíveis|DBPROP_OTHERUPDATEDELETE|
|Outros inserções visíveis|DBPROP_OTHERINSERT|
|Possui alterações visíveis|DBPROP_OWNUPDATEDELETE|
|Próprias inserções visíveis|DBPROP_OWNINSERT|
|Preservar a anulação|DBPROP_ABORTPRESERVE|
|Preservar a confirmação|DBPROP_COMMITPRESERVE|
|Reinicialização rápida|DBPROP_QUICKRESTART|
|Eventos reentrantes|DBPROP_REENTRANTEVENTS|
|Remover linhas excluídas|DBPROP_REMOVEDELETED|
|Várias alterações de relatórios|DBPROP_REPORTMULTIPLECHANGES|
|Retornar inserções pendentes|DBPROP_RETURNPENDINGINSERTS|
|Notificação de exclusão de linha|DBPROP_NOTIFYROWDELETE|
|Primeira notificação de alteração de linha|DBPROP_NOTIFYROWFIRSTCHANGE|
|Notificação de inserção de linha|DBPROP_NOTIFYROWINSERT|
|Privilégios de linha|DBPROP_ROWRESTRICT|
|Notificação de ressincronização de linha|DBPROP_NOTIFYROWRESYNCH|
|Modelo de Threading de linha|DBPROP_ROWTHREADMODEL|
|Notificação de alteração de desfazer de linha|DBPROP_NOTIFYROWUNDOCHANGE|
|Notificação de desfazer deleção de linha|DBPROP_NOTIFYROWUNDODELETE|
|Notificação desfazer inserção de linha|DBPROP_NOTIFYROWUNDOINSERT|
|Notificação de atualização de linha|DBPROP_NOTIFYROWUPDATE|
|Notificação de alteração de posição de busca do conjunto de linhas|DBPROP_NOTIFYROWSETFETCHPOSISIONCHANGE|
|Notificação de versão do conjunto de linhas|DBPROP_NOTIFYROWSETRELEASE|
|Rolar para trás|DBPROP_CANSCROLLBACKWARDS|
|Cursor de servidor|DBPROP_SERVERCURSOR|
|Ignorar excluído indicadores|DBPROP_BOOKMARKSKIPPED|
|Identidade de linha forte|DBPROP_STRONGITDENTITY|
|Linhas exclusivas|DBPROP_UNIQUEROWS|
|Capacidade de atualização|DBPROP_UPDATABILITY|
|Usar indicadores|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>Propriedades dinâmicas do comando
 As propriedades a seguir são adicionadas para o **propriedades** coleção do **comando** objeto.

|Nome da propriedade ADO|Nome de propriedade do OLE DB|
|-----------------------|--------------------------|
|Ordem de acesso|DBPROP_ACCESSORDER|
|Caminho de base|SSPROP_STREAM_BASEPATH|
|Bloqueio de objetos de armazenamento|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Tipo de indicador|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|Alterar as linhas inseridas|DBPROP_CHANGEINSERTEDROWS|
|Privilégios de coluna|DBPROP_COLUMNRESTRICT|
|Notificação de conjunto de coluna|DBPROP_NOTIFYCOLUMNSET|
|Tipo de Conteúdo|SSPROP_STREAM_CONTENTTYPE|
|Busca do cursor automaticamente|SSPROP_CURSORAUTOFETCH|
|Adiar a coluna|DBPROP_DEFERRED|
|Adiar Preparação|SSPROP_DEFERPREPARE|
|Atualizações de objetos de armazenamento de atraso|DBPROP_DELAYSTORAGEOBJECTS|
|Buscar com versões anteriores|DBPROP_CANFETCHBACKWARDS|
|Manter linhas|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|Linhas immobile|DBPROP_IMMOBILEROWS|
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
|Indicadores literal|DBPROP_LITERALBOOKMARKS|
|Identidade de linha literal|DBPROP_LITERALIDENTITY|
|Modo de bloqueio|DBPROP_LOCKMODE|
|Máximo de linhas aberto|DBPROP_MAXOPENROWS|
|Máximo de linhas pendentes|DBPROP_MAXPENDINGROWS|
|Máximo de linhas|DBPROP_MAXROWS|
|Granularidade de notificação|DBPROP_NOTIFICATIONGRANULARITY|
|Fases de notificação|DBPROP_NOTIFICATIONPHASES|
|Objetos transacionados|DBPROP_TRANSACTEDOBJECT|
|Outros alterações visíveis|DBPROP_OTHERUPDATEDELETE|
|Outros inserções visíveis|DBPROP_OTHERINSERT|
|Propriedade de codificação de saída|DBPROP_OUTPUTENCODING|
|Propriedade de fluxo de saída|DBPROP_OUTPUTSTREAM|
|Possui alterações visíveis|DBPROP_OWNUPDATEDELETE|
|Próprias inserções visíveis|DBPROP_OWNINSERT|
|Preservar a anulação|DBPROP_ABORTPRESERVE|
|Preservar a confirmação|DBPROP_COMMITPRESERVE|
|Reinicialização rápida|DBPROP_QUICKRESTART|
|Eventos reentrantes|DBPROP_REENTRANTEVENTS|
|Remover linhas excluídas|DBPROP_REMOVEDELETED|
|Várias alterações de relatórios|DBPROP_REPORTMULTIPLECHANGES|
|Retornar inserções pendentes|DBPROP_RETURNPENDINGINSERTS|
|Notificação de exclusão de linha|DBPROP_NOTIFYROWDELETE|
|Primeira notificação de alteração de linha|DBPROP_NOTIFYROWFIRSTCHANGE|
|Notificação de inserção de linha|DBPROP_NOTIFYROWINSERT|
|Privilégios de linha|DBPROP_ROWRESTRICT|
|Notificação de ressincronização de linha|DBPROP_NOTIFYROWRESYNCH|
|Modelo de Threading de linha|DBPROP_ROWTHREADMODEL|
|Notificação de alteração de desfazer de linha|DBPROP_NOTIFYROWUNDOCHANGE|
|Notificação de desfazer deleção de linha|DBPROP_NOTIFYROWUNDODELETE|
|Notificação desfazer inserção de linha|DBPROP_NOTIFYROWUNDOINSERT|
|Notificação de atualização de linha|DBPROP_NOTIFYROWUPDATE|
|Notificação de alteração de posição de busca do conjunto de linhas|DBPROP_NOTIFYROWSETFETCHPOSITIONCHANGE|
|Notificação de versão do conjunto de linhas|DBPROP_NOTIFYROWSETRELEASE|
|Rolar para trás|DBPROP_CANSCROLLBACKWARDS|
|Cursor de servidor|DBPROP_SERVERCURSOR|
|Dados de servidor na inserção|DBPROP_SERVERDATAONINSERT|
|Ignorar excluído indicadores|DBPROP_BOOKMARKSKIP|
|Identidade de linha forte|DBPROP_STRONGIDENTITY|
|Capacidade de atualização|DBPROP_UPDATABILITY|
|Usar indicadores|DBPROP_BOOKMARKS|
|Raiz XML|SSPROP_STREAM_XMLROOT|
|XSL|SSPROP_STREAM_XSL|

 Para detalhes específicos de implementação e funcionais informações sobre o Microsoft SQL Server OLE DB Provider, consulte o [provedor do SQL Server](http://msdn.microsoft.com/en-us/adf1d6c4-5930-444a-9248-ff1979729635).

## <a name="see-also"></a>Consulte também
 [Propriedade ConnectionString (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [propriedade do provedor (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [o objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)

