---
title: Provedor Microsoft OLE DB para Microsoft Jet | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Jet provider for OLE DB [ADO]
- providers [ADO], OLE DB provider for Microsoft Jet
- OLE DB provider for Microsoft Jet [ADO]
ms.assetid: fd956da1-5203-40af-aa7e-fc13a6c6581f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 71df952769ae509ba25b256ecdc9ddef3a54ebe5
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702844"
---
# <a name="microsoft-ole-db-provider-for-microsoft-jet-overview"></a>Provedor Microsoft OLE DB para visão geral do Microsoft Jet
O provedor OLE DB para Microsoft Jet permite que o ADO para acessar bancos de dados Microsoft Jet.

## <a name="connection-string-parameters"></a>Parâmetros de cadeia de caracteres de Conexão
 Para se conectar ao provedor, defina as *provedor* argumento do [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propriedade para o seguinte:

```vb
Microsoft.Jet.OLEDB.4.0
```

 Lendo a [provedor](../../../ado/reference/ado-api/provider-property-ado.md) propriedade também retornará essa cadeia de caracteres.

## <a name="typical-connection-string"></a>Cadeia de caracteres de Conexão típica
 Uma cadeia de caracteres de conexão típica para esse provedor é:

```vb
"Provider=Microsoft.Jet.OLEDB.4.0;Data Source=databaseName;User ID=MyUserID;Password=MyPassword;"
```

 A cadeia de caracteres consiste nessas palavras-chave:

|Palavra-chave|Descrição|
|-------------|-----------------|
|**Provedor**|Especifica o provedor OLE DB para Microsoft Jet.|
|**Fonte de dados**|Especifica o nome de arquivo e caminho do banco de dados (por exemplo, `c:\Northwind.mdb`).|
|**ID de usuário**|Especifica o nome de usuário. Se essa palavra-chave não for especificado, a cadeia de caracteres "`admin`", é usado por padrão.|
|**Senha**|Especifica a senha do usuário. Se essa palavra-chave não for especificado, a cadeia de caracteres vazia (""), é usado por padrão.|

> [!NOTE]
>  Se você estiver se conectando a um provedor de fonte de dados que dá suporte à autenticação do Windows, você deve especificar **Trusted_Connection = yes** ou **Integrated Security = SSPI** em vez de ID de usuário e senha informações na cadeia de conexão.

## <a name="provider-specific-connection-parameters"></a>Parâmetros de Conexão específicas do provedor
 O provedor OLE DB para Microsoft Jet dá suporte a várias propriedades de dinâmicas específica do provedor, além das que são definidos pelo ADO. Assim como acontece com todos os outros **Conexão** parâmetros, eles podem ser definidos usando o **Properties** coleção do **Conexão** objeto ou como parte da cadeia de conexão.

 A tabela a seguir lista essas propriedades junto com o nome de propriedade do OLE DB correspondente entre parênteses.

|Parâmetro|Descrição|
|---------------|-----------------|
|Quantidade de espaço recuperado do Jet OLEDB:Compact (DBPROP_JETOLEDB_COMPACTFREESPACESIZE)|Indica uma estimativa da quantidade de espaço, em bytes, que pode ser recuperado pela compactação de banco de dados. Esse valor só é válido após o estabelecimento de uma conexão de banco de dados.|
|Controle de OLEDB:Connection Jet (DBPROP_JETOLEDB_CONNECTIONCONTROL)|Indica se os usuários podem se conectar ao banco de dados.|
|Jet OLEDB:Create System Database (DBPROP_JETOLEDB_CREATESYSTEMDATABASE)|Indica se um banco de dados do sistema deve ser criado durante a criação de uma nova fonte de dados.|
|Modo de bloqueio do Jet OLEDB (DBPROP_JETOLEDB_DATABASELOCKMODE)|Indica o modo de bloqueio para esse banco de dados. O primeiro usuário para abrir o banco de dados determina o modo usado enquanto o banco de dados é aberto.|
|Jet OLEDB:Database Password (DBPROP_JETOLEDB_DATABASEPASSWORD)|Indica a senha do banco de dados.|
|Jet OLEDB: não copie localidade no CD (DBPROP_JETOLEDB_COMPACT_DONTCOPYLOCALE)|Indica se o Jet deve copiar as informações de localidade ao compactar um banco de dados.|
|Jet OLEDB:Encrypt Database (DBPROP_JETOLEDB_ENCRYPTDATABASE)|Indica se um banco de dados compactado deve ser criptografado. Se essa propriedade não for definida, o banco de dados compactado será criptografado se o banco de dados original também foi criptografado.|
|Tipo de OLEDB:Engine Jet (DBPROP_JETOLEDB_ENGINE)|Indica que o mecanismo de armazenamento usado para acessar o armazenamento de dados atual.|
|Jet OLEDB: intervalo assíncrono (DBPROP_JETOLEDB_EXCLUSIVEASYNCDELAY)|Indica o comprimento máximo de tempo, em milissegundos, que pode atrasar o Jet gravações assíncronas em disco quando o banco de dados fica aberto exclusivamente.<br /><br /> Essa propriedade será ignorada, a menos que **tempo limite de transação do Jet OLEDB** é definido como 0.|
|Tempo limite da transação Jet OLEDB (DBPROP_JETOLEDB_FLUSHTRANSACTIONTIMEOUT)|Indica a quantidade de tempo de espera antes que os dados armazenados em um cache de gravação assíncrona, na verdade, são gravados no disco. Essa configuração substitui os valores para **Jet OLEDB: atraso de Async compartilhados** e **Jet OLEDB: intervalo assíncrono**.|
|Jet OLEDB: Global de grandes volumes transações (DBPROP_JETOLEDB_GLOBALBULKNOTRANSACTIONS)|Indica se as transações em massa SQL são transacionadas.|
|Jet OLEDB: operações em massa de parcial Global (DBPROP_JETOLEDB_GLOBALBULKPARTIAL)|Indica a senha usada para abrir o banco de dados.|
|Jet OLEDB: sincronização de Commit implícito (DBPROP_JETOLEDB_IMPLICITCOMMITSYNC)|Indica se as alterações que foram feitas em transações implícitas internas são gravadas no modo síncrono ou assíncrono.|
|Jet OLEDB: intervalo (DBPROP_JETOLEDB_LOCKDELAY)|Indica o número de milissegundos de espera antes de tentar adquirir um bloqueio após uma tentativa anterior falhou.|
|Jet OLEDB: repetição (DBPROP_JETOLEDB_LOCKRETRY)|Indica quantas vezes uma tentativa de acessar uma página bloqueada é repetida.|
|Tamanho do Buffer do Jet OLEDB (DBPROP_JETOLEDB_MAXBUFFERSIZE)|Indica a quantidade máxima de memória, em quilobytes, Jet pode usar antes de começar a liberar alterações para o disco.|
|Jet OLEDB: proteção por arquivo (DBPROP_JETOLEDB_MAXLOCKSPERFILE)|Indica o número máximo de bloqueios que Jet pode colocar em um banco de dados. O valor padrão é 9500.|
|Jet OLEDB:New Database Password (DBPROP_JETOLEDB_NEWDATABASEPASSWORD)|Indica a nova senha a ser definido para esse banco de dados. A senha antiga é armazenada no **Jet OLEDB: senha**.|
|Jet OLEDB:ODBC comando atingir o tempo limite (DBPROP_JETOLEDB_ODBCCOMMANDTIMEOUT)|Indica que o número de milissegundos antes que uma consulta remota de ODBC do Jet atingirá o tempo limite.|
|Jet OLEDB bloqueios para bloqueio de tabela (DBPROP_JETOLEDB_PAGELOCKSTOTABLELOCK)|Indica quantas páginas devem ser bloqueadas em uma transação antes de Jet tenta promover o bloqueio em um bloqueio de tabela. Se esse valor for 0, o bloqueio é promovido nunca.|
|Tempo limite do Jet OLEDB (DBPROP_JETOLEDB_PAGETIMEOUT)|Indica o número de milissegundos que Jet aguardará antes de verificar se o seu cache está desatualizado, com o arquivo de banco de dados.|
|Jet OLEDB: reciclar com valor Long páginas (DBPROP_JETOLEDB_RECYCLELONGVALUEPAGES)|Indica se Jet agressivamente deve tentar recuperar as páginas BLOB quando eles são liberados.|
|Caminho de OLEDB:Registry Jet (DBPROP_JETOLEDB_REGPATH)|Indica a chave de registro do Windows que contém valores para o mecanismo de banco de dados Jet.|
|Jet OLEDB:Reset ISAM Stats (DBPROP_JETOLEDB_RESETISAMSTATS)|Indica se o esquema **Recordset** DBSCHEMA_JETOLEDB_ISAMSTATS deve redefinir seus contadores de desempenho depois que ele retorna informações sobre o desempenho.|
|Jet OLEDB:Shared Async Delay (DBPROP_JETOLEDB_SHAREDASYNCDELAY)|Indica a quantidade máxima de tempo, em milissegundos, o Jet pode atrasar gravações assíncronas em disco quando o banco de dados é aberto no modo de multiusuário.|
|Banco de dados do Jet OLEDB (DBPROP_JETOLEDB_SYSDBPATH)|Indica o nome de arquivo e caminho para o arquivo de informações do grupo de trabalho (banco de dados do sistema).|
|Modo de confirmação do Jet OLEDB:Transaction (DBPROP_JETOLEDB_TXNCOMMITMODE)|Indica se o Jet grava dados no disco de forma síncrona ou assíncrona quando uma transação é confirmada.|
|Sincronização de confirmação do Jet OLEDB (DBPROP_JETOLEDB_USERCOMMITSYNC)|Indica se as alterações que foram feitas em transações são gravadas no modo síncrono ou assíncrono.|

## <a name="provider-specific-recordset-and-command-properties"></a>Conjunto de registros específicos do provedor e propriedades de comando
 O provedor Jet também dá suporte a vários específico do provedor **conjunto de registros** e **comando** propriedades. Essas propriedades são acessadas e definidas por meio de **propriedades** coleção da **conjunto de registros** ou **comando** objeto. A tabela lista o nome da propriedade ADO e o nome de propriedade do OLE DB correspondente entre parênteses.

|Nome da propriedade|Descrição|
|-------------------|-----------------|
|Jet OLEDB:Bulk transações (DBPROP_JETOLEDB_BULKNOTRANSACTIONS)|Indica se as operações em massa SQL são transacionadas. Grandes operações em massa podem falhar quando transacionado, devido a atrasos de recurso.|
|Cursores do Jet OLEDB:Enable Fat (DBPROP_JETOLEDB_ENABLEFATCURSOR)|Indica se Jet deve armazenar em cache várias linhas ao preencher um conjunto de registros para fontes de linha remota.|
|Tamanho do Cache de Cursor OLEDB:Fat Jet (DBPROP_JETOLEDB_FATCURSORMAXROWS)|Indica o número de linhas em cache ao usar o cache de linha de repositório de dados remotos. Esse valor é ignorado, a menos que **Jet OLEDB:Enable Fat cursores** é True.|
|Jet OLEDB:Inconsistent (DBPROP_JETOLEDB_INCONSISTENT)|Indica se os resultados da consulta permitem atualizações inconsistentes.|
|Jet OLEDB: bloqueio de granularidade (DBPROP_JETOLEDB_LOCKGRANULARITY)|Indica se uma tabela é aberta usando o bloqueio em nível de linha.|
|Instrução de passagem do Jet OLEDB:ODBC (DBPROP_JETOLEDB_ODBCPASSTHROUGH)|Indica que o Jet deve passar o texto SQL em uma **comando** objeto para o back-end inalterado.|
|Operações em massa de OLEDB:Partial Jet (DBPROP_JETOLEDB_BULKPARTIAL)|Indica o comportamento do Jet quando operações DML SQL falhar.|
|Jet OLEDB:Pass por meio de consulta Bulk-Op (DBPROP_JETOLEDB_PASSTHROUGHBULKOP)|Indica se consultas que não retornam um **Recordset** são passados inalterados para a fonte de dados.|
|Jet OLEDB:Pass por meio de consulta se conectar a cadeia de caracteres (DBPROP_JETOLEDB_ODBCPASSTHROUGHCONNECTSTRING)|Indica a cadeia de conexão do Jet usada para se conectar a um armazenamento de dados remoto. Esse valor é ignorado, a menos que **declaração de passagem do Jet OLEDB:ODBC** é True.|
|Jet OLEDB: armazenados consulta (DBPROP_JETOLEDB_STOREDQUERY)|Indica se o texto do comando deve ser interpretado como uma consulta armazenada em vez de um comando SQL.|
|Jet OLEDB: validar regras em conjunto (DBPROP_JETOLEDB_VALIDATEONSET)|Indica se as regras de validação de Jet são avaliadas quando dados de coluna são definidos ou quando as alterações são confirmadas no banco de dados.|

 Por padrão, o provedor OLE DB para Microsoft Jet abre bancos de dados Microsoft Jet no modo de leitura/gravação. Para abrir um banco de dados no modo somente leitura, defina a [modo](../../../ado/reference/ado-api/mode-property-ado.md) propriedade em ADO **Conexão** objeto **adModeRead**.

## <a name="command-object-usage"></a>Uso do objeto Command
 Texto de comando do [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto usa o dialeto SQL do Microsoft Jet. Você pode especificar consultas que retornam a linha, consultas de ação e os nomes de tabela no texto do comando; No entanto, os procedimentos armazenados não têm suporte e não devem ser especificados.

## <a name="recordset-behavior"></a>Comportamento do conjunto de registros
 O mecanismo de banco de dados Microsoft Jet não oferece suporte a cursores dinâmicos. Portanto, o provedor OLE DB para Microsoft Jet não suporta o **adLockDynamic** tipo de cursor. Quando um cursor dinâmico é solicitado, o provedor retornará um cursor keyset e redefinir o [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) propriedade para indicar o tipo de [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) retornado. Além disso, se um atualizável **conjunto de registros** é solicitada (**LockType** está **adLockOptimistic**, **adLockBatchOptimistic**, ou **adLockPessimistic**) o provedor também retornará um cursor keyset e redefinir o **CursorType** propriedade.

## <a name="dynamic-properties"></a>Propriedades Dinâmicas
 O provedor OLE DB para Microsoft Jet insere várias propriedades dinâmicas para o **propriedades** coleção da não abertos [Conexão](../../../ado/reference/ado-api/connection-object-ado.md), [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md)e [Comando](../../../ado/reference/ado-api/command-object-ado.md) objetos.

 As tabelas a seguir são um cross-index dos nomes de ADO e OLE DB para cada propriedade dinâmica. O referência do programador DB OLE se refere a um nome de propriedade ADO usando o termo, "Description". Você pode encontrar mais informações sobre essas propriedades na referência do OLE DB do programador.

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
|Catálogo atual|DBPROP_CURRENTCATALOG|
|fonte de dados|DBPROP_INIT_DATASOURCE|
|Nome da Fonte de Dados|DBPROP_DATASOURCENAME|
|Objeto de fonte de dados modelo de Threading|DBPROP_DSOTHREADMODEL|
|Nome do DBMS|DBPROP_DBMSNAME|
|Versão do DBMS|DBPROP_DBMSVER|
|Suporte GROUP BY|DBPROP_GROUPBY|
|Suporte a tabelas heterogêneas|DBPROP_HETEROGENEOUSTABLES|
|Maiusculas e minúsculas do identificador|DBPROP_IDENTIFIERCASE|
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
|Conjunto de linhas somente de acréscimo|DBPROP_APPENDONLY|
|Bloquear objetos de armazenamento|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Tipo de indicador|DBPROP_BOOKMARKTYPE|
|Possíveis de indicação|DBPROP_IROWSETLOCATE|
|Marcadores ordenados|DBPROP_ORDEREDBOOKMARKS|
|Armazenar em cache colunas adiadas|DBPROP_CACHEDEFERRED|
|Modificar linhas inseridas|DBPROP_CHANGEINSERTEDROWS|
|Privilégios de coluna|DBPROP_COLUMNRESTRICT|
|Notificação de conjunto de coluna|DBPROP_NOTIFYCOLUMNSET|
|Coluna gravável|DBPROP_MAYWRITECOLUMN|
|Adiar a coluna|DBPROP_DEFERRED|
|Atualizações de objetos de armazenamento de atraso|DBPROP_DELAYSTORAGEOBJECTS|
|Buscar na ordem inversa|DBPROP_CANFETCHBACKWARDS|
|Manter linhas|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|ILockBytes|DBPROP_ILockBytes|
|Linhas imóveis|DBPROP_IMMOBILEROWS|
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
|Marcadores literais|DBPROP_LITERALBOOKMARKS|
|Identidade de linha literal|DBPROP_LITERALIDENTITY|
|Máximo de linhas abertas|DBPROP_MAXOPENROWS|
|Máximo de linhas pendentes|DBPROP_MAXPENDINGROWS|
|Máximo de linhas|DBPROP_MAXROWS|
|Uso de Memória|DBPROP_MEMORYUSAGE|
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
|Ignorar marcadores apagados|DBPROP_BOOKMARKSKIPPED|
|Identidade de linha forte|DBPROP_STRONGITDENTITY|
|Capacidade de atualização|DBPROP_UPDATABILITY|
|Usar indicadores|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>Propriedades dinâmicas do comando
 As propriedades a seguir são adicionadas para o **propriedades** coleção da **comando** objeto.

|Nome da propriedade ADO|Nome da propriedade do OLE DB|
|-----------------------|--------------------------|
|Ordem de acesso|DBPROP_ACCESSORDER|
|Conjunto de linhas somente de acréscimo|DBPROP_APPENDONLY|
|Bloquear objetos de armazenamento|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Tipo de indicador|DBPROP_BOOKMARKTYPE|
|Possíveis de indicação|DBPROP_IROWSETLOCATE|
|Modificar linhas inseridas|DBPROP_CHANGEINSERTEDROWS|
|Privilégios de coluna|DBPROP_COLUMNRESTRICT|
|Notificação de conjunto de coluna|DBPROP_NOTIFYCOLUMNSET|
|Adiar a coluna|DBPROP_DEFERRED|
|Atualizações de objetos de armazenamento de atraso|DBPROP_DELAYSTORAGEOBJECTS|
|Buscar na ordem inversa|DBPROP_CANFETCHBACKWARDS|
|Manter linhas|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|ILockBytes|DBPROP_ILockBytes|
|Linhas imóveis|DBPROP_IMMOBILEROWS|
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
|Dados de servidor na inserção|DBPROP_SERVERDATAONINSERT|
|Ignorar marcadores apagados|DBPROP_BOOKMARKSKIP|
|Identidade de linha forte|DBPROP_STRONGIDENTITY|
|Capacidade de atualização|DBPROP_UPDATABILITY|
|Usar indicadores|DBPROP_BOOKMARKS|

 Para detalhes específicos de implementação e funcionais informações sobre o provedor OLE DB para Microsoft Jet, consulte [provedor Jet](https://msdn.microsoft.com/library/windows/desktop/ms722791.aspx) na documentação do OLE DB.
