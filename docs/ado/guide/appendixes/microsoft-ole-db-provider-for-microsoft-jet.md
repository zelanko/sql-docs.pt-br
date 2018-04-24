---
title: Provedor Microsoft OLE DB para Microsoft Jet | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Jet provider for OLE DB [ADO]
- providers [ADO], OLE DB provider for Microsoft Jet
- OLE DB provider for Microsoft Jet [ADO]
ms.assetid: fd956da1-5203-40af-aa7e-fc13a6c6581f
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 253de8c53055269efb6a9e15c9d9a5ca940606e8
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="microsoft-ole-db-provider-for-microsoft-jet-overview"></a>Provedor Microsoft OLE DB para visão geral do Microsoft Jet
O OLE DB Provider for Microsoft Jet permite que o ADO acessar bancos de dados Microsoft Jet.

## <a name="connection-string-parameters"></a>Parâmetros de cadeia de caracteres de Conexão
 Para se conectar ao provedor, defina o *provedor* argumento o [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propriedade para o seguinte:

```
Microsoft.Jet.OLEDB.4.0
```

 Lendo o [provedor](../../../ado/reference/ado-api/provider-property-ado.md) propriedade também retornará essa cadeia de caracteres.

## <a name="typical-connection-string"></a>Cadeia de caracteres de Conexão típica
 Uma cadeia de conexão típica para esse provedor é:

```
"Provider=Microsoft.Jet.OLEDB.4.0;Data Source=databaseName;User ID=MyUserID;Password=MyPassword;"
```

 A cadeia de caracteres consiste nessas palavras-chave:

|Palavra-chave|Description|
|-------------|-----------------|
|**Provedor**|Especifica o provedor OLE DB para Microsoft Jet.|
|**Fonte de dados**|Especifica o nome de arquivo e caminho do banco de dados (por exemplo, `c:\Northwind.mdb`).|
|**ID de usuário**|Especifica o nome de usuário. Se essa palavra-chave não for especificada, a cadeia de caracteres "`admin`", é usado por padrão.|
|**Senha**|Especifica a senha do usuário. Se essa palavra-chave não for especificada, a cadeia de caracteres vazia (""), é usado por padrão.|

> [!NOTE]
>  Se você estiver se conectando a um provedor de fonte de dados que oferece suporte à autenticação do Windows, você deve especificar **Trusted_Connection = yes** ou **segurança integrada = SSPI** em vez de ID de usuário e senha informações na cadeia de conexão.

## <a name="provider-specific-connection-parameters"></a>Parâmetros de Conexão específicos do provedor
 O OLE DB Provider for Microsoft Jet dá suporte a várias propriedades de dinâmicas específica do provedor, além daqueles definidos pelo ADO. Assim como acontece com todos os outros **Conexão** parâmetros, eles podem ser definidos usando o **propriedades** coleção do **Conexão** objeto ou como parte da cadeia de conexão.

 A tabela a seguir lista essas propriedades junto com o nome da propriedade OLE DB correspondente entre parênteses.

|Parâmetro|Description|
|---------------|-----------------|
|Quantidade de espaço recuperado do Jet OLEDB:Compact (DBPROP_JETOLEDB_COMPACTFREESPACESIZE)|Indica uma estimativa da quantidade de espaço, em bytes, que pode ser recuperado pela compactação de banco de dados. Esse valor só é válido após o estabelecimento de uma conexão de banco de dados.|
|Controle de OLEDB:Connection Jet (DBPROP_JETOLEDB_CONNECTIONCONTROL)|Indica se os usuários podem se conectar ao banco de dados.|
|Jet OLEDB: criar o banco de dados do sistema (DBPROP_JETOLEDB_CREATESYSTEMDATABASE)|Indica se um banco de dados do sistema deve ser criado durante a criação de uma nova fonte de dados.|
|Modo de bloqueio do Jet OLEDB:Database (DBPROP_JETOLEDB_DATABASELOCKMODE)|Indica o modo de bloqueio para este banco de dados. O primeiro usuário abrir o banco de dados determina o modo usado enquanto o banco de dados está aberto.|
|Senha do Jet OLEDB:Database (DBPROP_JETOLEDB_DATABASEPASSWORD)|Indica a senha do banco de dados.|
|Jet OLEDB: não copie localidade no CD (DBPROP_JETOLEDB_COMPACT_DONTCOPYLOCALE)|Indica se o Jet deve copiar as informações de localidade ao compactar um banco de dados.|
|Jet OLEDB: criptografar o banco de dados (DBPROP_JETOLEDB_ENCRYPTDATABASE)|Indica se um banco de dados compactado deve ser criptografado. Se essa propriedade não é definida, o banco de dados compactado será criptografado se o banco de dados original também foi criptografado.|
|Tipo de OLEDB:Engine Jet (DBPROP_JETOLEDB_ENGINE)|Indica que o mecanismo de armazenamento usado para acessar o repositório de dados atual.|
|Jet OLEDB: intervalo assíncrono (DBPROP_JETOLEDB_EXCLUSIVEASYNCDELAY)|Indica o comprimento máximo de tempo, em milissegundos, que pode atrasar o Jet gravações assíncronas em disco quando o banco de dados é aberto exclusivamente.<br /><br /> Essa propriedade será ignorada, a menos que **tempo limite de transação do Jet OLEDB** é definido como 0.|
|Tempo limite da transação Jet OLEDB (DBPROP_JETOLEDB_FLUSHTRANSACTIONTIMEOUT)|Indica a quantidade de tempo de espera antes que os dados armazenados em um cache de gravação assíncrona realmente são gravados no disco. Essa configuração substitui os valores de **Jet OLEDB: compartilhado Async atraso** e **Jet OLEDB: intervalo assíncrono**.|
|Jet OLEDB: Global de grandes volumes transações (DBPROP_JETOLEDB_GLOBALBULKNOTRANSACTIONS)|Indica se as transações do SQL em massa são transacionadas.|
|Jet OLEDB: operações em massa de parcial Global (DBPROP_JETOLEDB_GLOBALBULKPARTIAL)|Indica a senha usada para abrir o banco de dados.|
|Jet OLEDB: sincronização de confirmação implícita (DBPROP_JETOLEDB_IMPLICITCOMMITSYNC)|Indica se as alterações feitas em transações implícitas internas são gravadas no modo síncrono ou assíncrono.|
|Jet OLEDB: intervalo (DBPROP_JETOLEDB_LOCKDELAY)|Indica o número de milissegundos de espera antes de tentar adquirir um bloqueio após uma tentativa anterior falhou.|
|Jet OLEDB: repetição (DBPROP_JETOLEDB_LOCKRETRY)|Indica quantas vezes uma tentativa de acessar uma página bloqueada é repetida.|
|Tamanho do Buffer do Jet OLEDB (DBPROP_JETOLEDB_MAXBUFFERSIZE)|Indica a quantidade máxima de memória, em quilobytes, Jet pode usar antes de começar a liberar alterações para o disco.|
|Jet OLEDB: proteção por arquivo (DBPROP_JETOLEDB_MAXLOCKSPERFILE)|Indica o número máximo de bloqueios que Jet pode colocar em um banco de dados. O valor padrão é 9500.|
|Jet OLEDB: nova senha de banco de dados (DBPROP_JETOLEDB_NEWDATABASEPASSWORD)|Indica a nova senha a ser definido para este banco de dados. A senha antiga é armazenada em **Jet OLEDB:Database senha**.|
|Jet OLEDB:ODBC comando tempo limite (DBPROP_JETOLEDB_ODBCCOMMANDTIMEOUT)|Indica que o número de milissegundos antes de uma consulta remota de ODBC do Jet atingirá o tempo limite.|
|Jet OLEDB bloqueios para bloqueio de tabela (DBPROP_JETOLEDB_PAGELOCKSTOTABLELOCK)|Indica quantas páginas devem ser bloqueadas dentro de uma transação antes de Jet tenta promover o bloqueio em um bloqueio de tabela. Se esse valor for 0, o bloqueio é promovido nunca.|
|Tempo limite do Jet OLEDB (DBPROP_JETOLEDB_PAGETIMEOUT)|Indica o número de milissegundos que Jet aguardará antes de verificar se o cache está desatualizada com o arquivo de banco de dados.|
|Jet OLEDB: reciclar com valor Long páginas (DBPROP_JETOLEDB_RECYCLELONGVALUEPAGES)|Indica se Jet agressivamente deve tentar recuperar as páginas BLOB quando eles são liberados.|
|Caminho de OLEDB:Registry Jet (DBPROP_JETOLEDB_REGPATH)|Indica a chave de registro do Windows que contém valores para o mecanismo de banco de dados Jet.|
|Estatísticas ISAM do Jet OLEDB:Reset (DBPROP_JETOLEDB_RESETISAMSTATS)|Indica se o esquema **registros** DBSCHEMA_JETOLEDB_ISAMSTATS devem redefinir os contadores de desempenho depois que ele retorna informações sobre o desempenho.|
|Jet OLEDB: intervalo assíncrono (DBPROP_JETOLEDB_SHAREDASYNCDELAY) compartilhado|Indica a quantidade máxima de tempo, em milissegundos, Jet pode atrasar gravações assíncronas em disco quando o banco de dados é aberto no modo de multiusuário.|
|Banco de dados do Jet OLEDB (DBPROP_JETOLEDB_SYSDBPATH)|Indica o nome de arquivo e caminho para o arquivo de informações do grupo de trabalho (banco de dados do sistema).|
|Modo de confirmação do Jet OLEDB:Transaction (DBPROP_JETOLEDB_TXNCOMMITMODE)|Indica se o Jet grava dados em disco de forma síncrona ou assíncrona quando uma transação for confirmada.|
|Sincronização de confirmação do Jet OLEDB (DBPROP_JETOLEDB_USERCOMMITSYNC)|Indica se as alterações feitas em transações são gravadas no modo síncrono ou assíncrono.|

## <a name="provider-specific-recordset-and-command-properties"></a>Conjunto de registros específicos do provedor e as propriedades de comando
 O provedor Jet também oferece suporte a vários específica do provedor **registros** e **comando** propriedades. Essas propriedades são acessadas e definidas por meio de **propriedades** coleção do **registros** ou **comando** objeto. A tabela lista o nome da propriedade ADO e o nome de propriedade OLE DB correspondente entre parênteses.

|Nome da propriedade|Description|
|-------------------|-----------------|
|Transações de OLEDB:Bulk Jet (DBPROP_JETOLEDB_BULKNOTRANSACTIONS)|Indica se as operações em massa SQL são transacionadas. Operações em massa grande podem falhar quando transacionado, devido a atrasos de recurso.|
|Cursores do Jet OLEDB:Enable Fat (DBPROP_JETOLEDB_ENABLEFATCURSOR)|Indica se Jet deve armazenar em cache várias linhas ao preencher um conjunto de registros para fontes de linha remota.|
|Tamanho de Cache de Cursor do Jet OLEDB:Fat (DBPROP_JETOLEDB_FATCURSORMAXROWS)|Indica o número de linhas em cache ao usar o cache de linha do repositório de dados remotos. Esse valor é ignorado, a menos que **Jet OLEDB:Enable Fat cursores** for True.|
|Jet OLEDB: inconsistente (DBPROP_JETOLEDB_INCONSISTENT)|Indica se os resultados da consulta permitem atualizações inconsistentes.|
|Jet OLEDB: bloqueio de granularidade (DBPROP_JETOLEDB_LOCKGRANULARITY)|Indica se uma tabela é aberta usando o bloqueio em nível de linha.|
|Instrução de passagem do Jet OLEDB:ODBC (DBPROP_JETOLEDB_ODBCPASSTHROUGH)|Indica que o Jet deve passar o texto SQL em um **comando** objeto para o back-end inalterado.|
|Operações em massa de OLEDB:Partial Jet (DBPROP_JETOLEDB_BULKPARTIAL)|Indica o comportamento do Jet quando operações DML SQL falharem.|
|Jet OLEDB:Pass por meio de consulta Bulk-Op (DBPROP_JETOLEDB_PASSTHROUGHBULKOP)|Indica se consultas que não retornam um **registros** são passados inalterados para a fonte de dados.|
|Jet OLEDB:Pass por meio de consulta se conectar a cadeia de caracteres (DBPROP_JETOLEDB_ODBCPASSTHROUGHCONNECTSTRING)|Indica a cadeia de conexão do Jet usada para se conectar a um repositório de dados remoto. Esse valor é ignorado, a menos que **declaração de passagem do Jet OLEDB:ODBC** for True.|
|Jet OLEDB: armazenados consulta (DBPROP_JETOLEDB_STOREDQUERY)|Indica se o texto do comando deve ser interpretado como uma consulta armazenada em vez de um comando SQL.|
|Jet OLEDB: validar regras em conjunto (DBPROP_JETOLEDB_VALIDATEONSET)|Indica se as regras de validação de Jet são avaliadas quando dados de coluna está definido ou quando as alterações são confirmadas no banco de dados.|

 Por padrão, o OLE DB Provider for Microsoft Jet abre bancos de dados Microsoft Jet no modo de leitura/gravação. Para abrir um banco de dados no modo somente leitura, defina a [modo](../../../ado/reference/ado-api/mode-property-ado.md) propriedade ADO **Conexão** do objeto para **adModeRead**.

## <a name="command-object-usage"></a>Uso do objeto de comando
 Texto de comando do [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto usa o dialeto SQL do Microsoft Jet. Você pode especificar nomes de tabela, consultas ação e consultas retornam linhas no texto do comando; No entanto, os procedimentos armazenados não são suportados e não devem ser especificados.

## <a name="recordset-behavior"></a>Comportamento do conjunto de registros
 O mecanismo de banco de dados Microsoft Jet não suporta cursores dinâmicos. Portanto, o OLE DB Provider for Microsoft Jet não suporta o **adLockDynamic** tipo de cursor. Quando um cursor dinâmico é solicitado, o provedor retornará um cursor de conjunto de chaves e redefinir o [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) propriedade para indicar o tipo de [registros](../../../ado/reference/ado-api/recordset-object-ado.md) retornado. Além disso, se um atualizável **registros** é solicitada (**LockType** é **adLockOptimistic**, **adLockBatchOptimistic**, ou **adLockPessimistic**) o provedor também retornará um cursor de conjunto de chaves e redefinir o **CursorType** propriedade.

## <a name="dynamic-properties"></a>Propriedades Dinâmicas
 O OLE DB Provider for Microsoft Jet insere várias propriedades dinâmicas no **propriedades** coleção de não o aberta [Conexão](../../../ado/reference/ado-api/connection-object-ado.md), [registros](../../../ado/reference/ado-api/recordset-object-ado.md)e [Comando](../../../ado/reference/ado-api/command-object-ado.md) objetos.

 As tabelas a seguir são um cross-index dos nomes de ADO e OLE DB para cada propriedade dinâmica. O referência do programador DB OLE refere-se a um nome de propriedade ADO, o termo "Descrição". Você pode encontrar mais informações sobre essas propriedades na referência do OLE DB do programador.

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
|Catálogo atual|DBPROP_CURRENTCATALOG|
|Fonte de dados|DBPROP_INIT_DATASOURCE|
|Nome da Fonte de Dados|DBPROP_DATASOURCENAME|
|Modelo de Threading do objeto de fonte de dados|DBPROP_DSOTHREADMODEL|
|Nome do DBMS|DBPROP_DBMSNAME|
|Versão do DBMS|DBPROP_DBMSVER|
|GRUPO de suporte|DBPROP_GROUPBY|
|Suporte a tabelas heterogêneos|DBPROP_HETEROGENEOUSTABLES|
|Diferenciação de maiusculas e minúsculas identificador|DBPROP_IDENTIFIERCASE|
|Níveis de isolamento|DBPROP_SUPPORTEDTXNISOLEVELS|
|Retenção de isolamento|DBPROP_SUPPORTEDTXNISORETAIN|
|Identificador de Localidade|DBPROP_INIT_LCID|
|Tamanho máximo de índice|DBPROP_MAXINDEXSIZE|
|Tamanho máximo da linha|DBPROP_MAXROWSIZE|
|Tamanho máximo de linha inclui BLOB|DBPROP_MAXROWSIZEINCLUDESBLOB|
|Máximo de tabelas em SELECT|DBPROP_MAXTABLESINSELECT|
|Modo|DBPROP_INIT_MODE|
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
|Conjunto de linhas somente de acréscimo|DBPROP_APPENDONLY|
|Bloqueio de objetos de armazenamento|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Tipo de indicador|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|Indicadores ordenados|DBPROP_ORDEREDBOOKMARKS|
|Cache adiada colunas|DBPROP_CACHEDEFERRED|
|Alterar as linhas inseridas|DBPROP_CHANGEINSERTEDROWS|
|Privilégios de coluna|DBPROP_COLUMNRESTRICT|
|Notificação de conjunto de coluna|DBPROP_NOTIFYCOLUMNSET|
|Coluna gravável|DBPROP_MAYWRITECOLUMN|
|Adiar a coluna|DBPROP_DEFERRED|
|Atualizações de objetos de armazenamento de atraso|DBPROP_DELAYSTORAGEOBJECTS|
|Buscar com versões anteriores|DBPROP_CANFETCHBACKWARDS|
|Manter linhas|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|ILockBytes|DBPROP_ILockBytes|
|Linhas immobile|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetIndex|DBPROP_IRowsetIndex|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsestLocate|
|IRowsetResynch||
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|IStorage|DBPROP_IStorage|
|IStream|DBPROP_IStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|Indicadores literal|DBPROP_LITERALBOOKMARKS|
|Identidade de linha literal|DBPROP_LITERALIDENTITY|
|Máximo de linhas aberto|DBPROP_MAXOPENROWS|
|Máximo de linhas pendentes|DBPROP_MAXPENDINGROWS|
|Máximo de linhas|DBPROP_MAXROWS|
|Uso de Memória|DBPROP_MEMORYUSAGE|
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
|Ignorar excluído indicadores|DBPROP_BOOKMARKSKIPPED|
|Identidade de linha forte|DBPROP_STRONGITDENTITY|
|Capacidade de atualização|DBPROP_UPDATABILITY|
|Usar indicadores|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>Propriedades dinâmicas do comando
 As propriedades a seguir são adicionadas para o **propriedades** coleção do **comando** objeto.

|Nome da propriedade ADO|Nome de propriedade do OLE DB|
|-----------------------|--------------------------|
|Ordem de acesso|DBPROP_ACCESSORDER|
|Conjunto de linhas somente de acréscimo|DBPROP_APPENDONLY|
|Bloqueio de objetos de armazenamento|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Tipo de indicador|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|Alterar as linhas inseridas|DBPROP_CHANGEINSERTEDROWS|
|Privilégios de coluna|DBPROP_COLUMNRESTRICT|
|Notificação de conjunto de coluna|DBPROP_NOTIFYCOLUMNSET|
|Adiar a coluna|DBPROP_DEFERRED|
|Atualizações de objetos de armazenamento de atraso|DBPROP_DELAYSTORAGEOBJECTS|
|Buscar com versões anteriores|DBPROP_CANFETCHBACKWARDS|
|Manter linhas|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|ILockBytes|DBPROP_ILockBytes|
|Linhas immobile|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetIndex|DBPROP_IRowsetIndex|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsetLocate|
|IRowsetResynch||
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|IStorage|DBPROP_IStorage|
|IStream|DBPROP_IStream|
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
|Dados de servidor na inserção|DBPROP_SERVERDATAONINSERT|
|Ignorar excluído indicadores|DBPROP_BOOKMARKSKIP|
|Identidade de linha forte|DBPROP_STRONGIDENTITY|
|Capacidade de atualização|DBPROP_UPDATABILITY|
|Usar indicadores|DBPROP_BOOKMARKS|

 Para detalhes específicos de implementação e funcionais informações sobre o OLE DB Provider for Microsoft Jet, consulte [provedor Jet](https://msdn.microsoft.com/library/windows/desktop/ms722791.aspx) na documentação do OLE DB.
