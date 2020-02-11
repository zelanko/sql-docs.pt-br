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
ms.openlocfilehash: 69d88aebe25f6cfa5490cce736c05780b87eee6e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67926643"
---
# <a name="microsoft-ole-db-provider-for-microsoft-jet-overview"></a>Visão geral do provedor do Microsoft OLE DB para Microsoft Jet
O provedor de OLE DB para Microsoft Jet permite que o ADO acesse bancos de dados Microsoft Jet.

## <a name="connection-string-parameters"></a>Parâmetros da cadeia de conexão
 Para se conectar a esse provedor, defina o argumento do *provedor* da propriedade [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) para o seguinte:

```vb
Microsoft.Jet.OLEDB.4.0
```

 Ler a propriedade do [provedor](../../../ado/reference/ado-api/provider-property-ado.md) também retornará essa cadeia de caracteres.

## <a name="typical-connection-string"></a>Cadeia de conexão típica
 Uma cadeia de conexão típica para esse provedor é:

```vb
"Provider=Microsoft.Jet.OLEDB.4.0;Data Source=databaseName;User ID=MyUserID;Password=MyPassword;"
```

 A cadeia de caracteres consiste nessas palavras-chave:

|Palavra-chave|DESCRIÇÃO|
|-------------|-----------------|
|**Provedor**|Especifica o provedor de OLE DB para o Microsoft Jet.|
|**Fonte de Dados**|Especifica o caminho do banco de dados e o nome do `c:\Northwind.mdb`arquivo (por exemplo,).|
|**ID de usuário**|Especifica um nome de usuário. Se essa palavra-chave não for especificada, a cadeia`admin`de caracteres, "", será usada por padrão.|
|**Senha**|Especifica a senha do usuário. Se essa palavra-chave não for especificada, a cadeia de caracteres vazia ("") será usada por padrão.|

> [!NOTE]
>  Se você estiver se conectando a um provedor de fonte de dados que dá suporte à autenticação do Windows, especifique **Trusted_Connection = Sim** ou **segurança integrada = SSPI** , em vez de ID de usuário e informações de senha na cadeia de conexão.

## <a name="provider-specific-connection-parameters"></a>Parâmetros de conexão específicos do provedor
 O provedor de OLE DB para Microsoft Jet dá suporte a várias propriedades dinâmicas específicas de provedor além daquelas definidas pelo ADO. Assim como acontece com todos os outros parâmetros de **conexão** , eles podem ser definidos usando a coleção **Properties** do objeto **Connection** ou como parte da cadeia de conexão.

 A tabela a seguir lista essas propriedades junto com o nome da propriedade OLE DB correspondente entre parênteses.

|Parâmetro|DESCRIÇÃO|
|---------------|-----------------|
|Jet OLEDB: compactar valor de espaço recuperado (DBPROP_JETOLEDB_COMPACTFREESPACESIZE)|Indica uma estimativa da quantidade de espaço, em bytes, que pode ser recuperada compactando o banco de dados. Esse valor só é válido depois que uma conexão de banco de dados é estabelecida.|
|Jet OLEDB: controle de conexão (DBPROP_JETOLEDB_CONNECTIONCONTROL)|Indica se os usuários podem se conectar ao banco de dados.|
|Jet OLEDB: criar banco de dados do sistema (DBPROP_JETOLEDB_CREATESYSTEMDATABASE)|Indica se um banco de dados do sistema deve ser criado durante a criação de uma nova fonte.|
|Jet OLEDB: modo de bloqueio de banco de dados (DBPROP_JETOLEDB_DATABASELOCKMODE)|Indica o modo de bloqueio para este banco de dados. O primeiro usuário a abrir o banco de dados determina o modo usado enquanto o banco de dados está aberto.|
|Jet OLEDB: senha do banco de dados (DBPROP_JETOLEDB_DATABASEPASSWORD)|Indica a senha do banco de dados.|
|Jet OLEDB: não copie a localidade no Compact (DBPROP_JETOLEDB_COMPACT_DONTCOPYLOCALE)|Indica se o Jet deve copiar informações de localidade ao compactar um banco de dados.|
|Jet OLEDB: criptografar banco de dados (DBPROP_JETOLEDB_ENCRYPTDATABASE)|Indica se um banco de dados compactado deve ser criptografado. Se essa propriedade não for definida, o banco de dados compactado será criptografado se o banco de dados original também tiver sido criptografado.|
|Jet OLEDB: tipo de mecanismo (DBPROP_JETOLEDB_ENGINE)|Indica o mecanismo de armazenamento usado para acessar o armazenamento de dados atual.|
|Jet OLEDB: atraso assíncrono exclusivo (DBPROP_JETOLEDB_EXCLUSIVEASYNCDELAY)|Indica o período máximo de tempo, em milissegundos, que o Jet pode atrasar gravações assíncronas no disco quando o banco de dados é aberto exclusivamente.<br /><br /> Essa propriedade é ignorada a menos que o **Jet OLEDB: liberar o tempo limite da transação** esteja definido como 0.|
|Jet OLEDB: liberar tempo limite da transação (DBPROP_JETOLEDB_FLUSHTRANSACTIONTIMEOUT)|Indica a quantidade de tempo de espera antes que os dados armazenados em um cache para gravação assíncrona sejam realmente gravados no disco. Essa configuração substitui os valores para **Jet OLEDB: atraso assíncrono compartilhado** e **Jet OLEDB: atraso assíncrono exclusivo**.|
|Jet OLEDB: transações em massa globais (DBPROP_JETOLEDB_GLOBALBULKNOTRANSACTIONS)|Indica se as transações em massa do SQL são transacionadas.|
|Jet OLEDB: operações em massa parciais globais (DBPROP_JETOLEDB_GLOBALBULKPARTIAL)|Indica a senha usada para abrir o banco de dados.|
|Jet OLEDB: sincronização de confirmação implícita (DBPROP_JETOLEDB_IMPLICITCOMMITSYNC)|Indica se as alterações feitas em transações implícitas internas são gravadas no modo síncrono ou assíncrono.|
|Jet OLEDB: atraso de bloqueio (DBPROP_JETOLEDB_LOCKDELAY)|Indica o número de milissegundos a aguardar antes de tentar adquirir um bloqueio após a falha de uma tentativa anterior.|
|Jet OLEDB: tentar novamente o bloqueio (DBPROP_JETOLEDB_LOCKRETRY)|Indica quantas vezes uma tentativa de acessar uma página bloqueada é repetida.|
|Jet OLEDB: tamanho máximo do buffer (DBPROP_JETOLEDB_MAXBUFFERSIZE)|Indica a quantidade máxima de memória, em quilobytes, que o Jet pode usar antes de iniciar a liberação de alterações no disco.|
|Jet OLEDB: máximo de bloqueios por arquivo (DBPROP_JETOLEDB_MAXLOCKSPERFILE)|Indica o número máximo de bloqueios que o Jet pode fazer em um banco de dados. O valor padrão é 9500.|
|Jet OLEDB: nova senha de banco de dados (DBPROP_JETOLEDB_NEWDATABASEPASSWORD)|Indica a nova senha a ser definida para este banco de dados. A senha antiga é armazenada em **Jet OLEDB: senha do banco de dados**.|
|Jet OLEDB: tempo limite do comando ODBC (DBPROP_JETOLEDB_ODBCCOMMANDTIMEOUT)|Indica o número de milissegundos antes de uma consulta ODBC remota do Jet atingir o tempo limite.|
|Jet OLEDB: bloqueios de página para bloqueio de tabela (DBPROP_JETOLEDB_PAGELOCKSTOTABLELOCK)|Indica quantas páginas devem ser bloqueadas em uma transação antes que o Jet tente promover o bloqueio para um bloqueio de tabela. Se esse valor for 0, o bloqueio nunca será promovido.|
|Jet OLEDB: tempo limite da página (DBPROP_JETOLEDB_PAGETIMEOUT)|Indica o número de milissegundos que o Jet aguardará antes de verificar se seu cache está desatualizado com o arquivo de banco de dados.|
|Jet OLEDB: Reciclar páginas de valor longo (DBPROP_JETOLEDB_RECYCLELONGVALUEPAGES)|Indica se o Jet deve tentar rereivindicar páginas de BLOB de forma agressiva quando elas forem liberadas.|
|Jet OLEDB: caminho do registro (DBPROP_JETOLEDB_REGPATH)|Indica a chave do registro do Windows que contém valores para o mecanismo de banco de dados Jet.|
|Jet OLEDB: redefinir estatísticas de ISAM (DBPROP_JETOLEDB_RESETISAMSTATS)|Indica se o **conjunto de registros** de esquema DBSCHEMA_JETOLEDB_ISAMSTATS deve redefinir seus contadores de desempenho depois de retornar informações de desempenho.|
|Jet OLEDB: atraso assíncrono compartilhado (DBPROP_JETOLEDB_SHAREDASYNCDELAY)|Indica a quantidade máxima de tempo, em milissegundos, que o Jet pode atrasar gravações assíncronas no disco quando o banco de dados é aberto no modo multiusuário.|
|Jet OLEDB: banco de dados do sistema (DBPROP_JETOLEDB_SYSDBPATH)|Indica o caminho e o nome do arquivo para o arquivo de informações do grupo de trabalho (banco de dados do sistema).|
|Jet OLEDB: modo de confirmação da transação (DBPROP_JETOLEDB_TXNCOMMITMODE)|Indica se o Jet grava dados em disco de forma síncrona ou assíncrona quando uma transação é confirmada.|
|Jet OLEDB: sincronização de confirmação do usuário (DBPROP_JETOLEDB_USERCOMMITSYNC)|Indica se as alterações feitas em transações são gravadas no modo síncrono ou assíncrono.|

## <a name="provider-specific-recordset-and-command-properties"></a>Conjunto de registros e propriedades de comando específicas do provedor
 O provedor Jet também dá suporte a várias propriedades de **conjuntos de registros** e **comandos** específicas do provedor. Essas propriedades são acessadas e definidas por meio da coleção **Properties** do **conjunto de registros** ou do objeto **Command** . A tabela lista o nome da propriedade ADO e seu nome de propriedade OLE DB correspondente entre parênteses.

|Nome da propriedade|DESCRIÇÃO|
|-------------------|-----------------|
|Jet OLEDB: transações em massa (DBPROP_JETOLEDB_BULKNOTRANSACTIONS)|Indica se as operações em massa do SQL são transacionadas. Grandes operações em massa podem falhar quando transacionadas, devido a atrasos de recursos.|
|Jet OLEDB: habilitar cursores de FAT (DBPROP_JETOLEDB_ENABLEFATCURSOR)|Indica se o Jet deve armazenar em cache várias linhas ao preencher um conjunto de registros para fontes de linha remotas.|
|Jet OLEDB: tamanho do cache do cursor FAT (DBPROP_JETOLEDB_FATCURSORMAXROWS)|Indica o número de linhas a serem armazenadas em cache ao usar o cache de linha do repositório de dados remoto. Esse valor é ignorado a menos que o **Jet OLEDB: habilitar cursores de Fat** seja verdadeiro.|
|Jet OLEDB: inconsistente (DBPROP_JETOLEDB_INCONSISTENT)|Indica se os resultados da consulta permitem atualizações inconsistentes.|
|Jet OLEDB: granularidade de bloqueio (DBPROP_JETOLEDB_LOCKGRANULARITY)|Indica se uma tabela é aberta usando o bloqueio em nível de linha.|
|Jet OLEDB: instrução de passagem ODBC (DBPROP_JETOLEDB_ODBCPASSTHROUGH)|Indica que o Jet deve passar o texto SQL em um objeto de **comando** para o back-end inalterado.|
|Jet OLEDB: operações em massa parciais (DBPROP_JETOLEDB_BULKPARTIAL)|Indica o comportamento do Jet quando as operações DML do SQL falham.|
|Jet OLEDB: operação de passagem em massa de consulta (DBPROP_JETOLEDB_PASSTHROUGHBULKOP)|Indica se as consultas que não retornam um **conjunto de registros** são passadas inalteradas para a fonte de dados.|
|Jet OLEDB: cadeia de conexão de passagem de consulta (DBPROP_JETOLEDB_ODBCPASSTHROUGHCONNECTSTRING)|Indica a cadeia de conexão Jet usada para se conectar a um armazenamento de dados remoto. Esse valor é ignorado, a menos que o **Jet OLEDB: instrução de passagem ODBC** seja true.|
|Jet OLEDB: consulta armazenada (DBPROP_JETOLEDB_STOREDQUERY)|Indica se o texto do comando deve ser interpretado como uma consulta armazenada em vez de um comando SQL.|
|Jet OLEDB: validar regras no conjunto (DBPROP_JETOLEDB_VALIDATEONSET)|Indica se as regras de validação do Jet são avaliadas quando os dados da coluna são definidos ou quando as alterações são confirmadas no banco de dado.|

 Por padrão, o provedor de OLE DB para o Microsoft Jet abre bancos de dados do Microsoft Jet no modo de leitura/gravação. Para abrir um banco de dados no modo somente leitura, defina a propriedade [Mode](../../../ado/reference/ado-api/mode-property-ado.md) no objeto de **conexão** ADO como **adModeRead**.

## <a name="command-object-usage"></a>Uso do objeto Command
 O texto do comando no objeto de [comando](../../../ado/reference/ado-api/command-object-ado.md) usa o dialeto SQL do Microsoft Jet. Você pode especificar consultas de retorno de linha, consultas de ação e nomes de tabela no texto do comando; no entanto, não há suporte para procedimentos armazenados e eles não devem ser especificados.

## <a name="recordset-behavior"></a>Comportamento do conjunto de registros
 O mecanismo de banco de dados Microsoft Jet não oferece suporte a cursores dinâmicos. Portanto, o provedor de OLE DB do Microsoft Jet não oferece suporte ao tipo de cursor **adLockDynamic** . Quando um cursor dinâmico é solicitado, o provedor retornará um cursor do conjunto de chaves e redefinirá a propriedade [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) para indicar o tipo de [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) retornado. Além disso, se um **conjunto de registros** atualizável for solicitado (**LockType** for **adLockOptimistic**, **adLockBatchOptimistic**ou **adLockPessimistic**), o provedor também retornará um cursor do conjunto de chaves e redefinirá a propriedade **CursorType** .

## <a name="dynamic-properties"></a>Propriedades Dinâmicas
 O provedor de OLE DB do Microsoft Jet insere várias propriedades dinâmicas na coleção **Properties** dos objetos [Connection](../../../ado/reference/ado-api/connection-object-ado.md), [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)e [Command](../../../ado/reference/ado-api/command-object-ado.md) não abertos.

 As tabelas a seguir são um índice cruzado dos nomes do ADO e do OLE DB para cada propriedade dinâmica. A referência do programador de OLE DB refere-se a um nome de propriedade ADO pelo termo "Descrição". Você pode encontrar mais informações sobre essas propriedades na referência do programador de OLE DB.

## <a name="connection-dynamic-properties"></a>Propriedades dinâmicas da conexão
 As propriedades a seguir são adicionadas à coleção **Properties** do objeto **Connection** .

|Nome da propriedade ADO|Nome da propriedade de OLE DB|
|-----------------------|--------------------------|
|Sessões ativas|DBPROP_ACTIVESESSIONS|
|Anular Asynchable|DBPROP_ASYNCTXNABORT|
|Asynchable confirmação|DBPROP_ASYNCTNXCOMMIT|
|Níveis de isolamento de confirmação automática|DBPROP_SESS_AUTOCOMMITISOLEVELS|
|Local do catálogo|DBPROP_CATALOGLOCATION|
|Termo do catálogo|DBPROP_CATALOGTERM|
|Definição de coluna|DBPROP_COLUMNDEFINITION|
|Catálogo atual|DBPROP_CURRENTCATALOG|
|Fonte de dados|DBPROP_INIT_DATASOURCE|
|Nome da fonte de dados|DBPROP_DATASOURCENAME|
|Modelo de Threading do objeto de fonte de dados|DBPROP_DSOTHREADMODEL|
|Nome do DBMS|DBPROP_DBMSNAME|
|Versão do DBMS|DBPROP_DBMSVER|
|Agrupar por suporte|DBPROP_GROUPBY|
|Suporte a tabelas heterogêneas|DBPROP_HETEROGENEOUSTABLES|
|Diferenciar maiúsculas de minúsculas|DBPROP_IDENTIFIERCASE|
|Níveis de isolamento|DBPROP_SUPPORTEDTXNISOLEVELS|
|Retenção de isolamento|DBPROP_SUPPORTEDTXNISORETAIN|
|Identificador de Localidade|DBPROP_INIT_LCID|
|Tamanho máximo do índice|DBPROP_MAXINDEXSIZE|
|Tamanho máximo da linha|DBPROP_MAXROWSIZE|
|O tamanho máximo da linha inclui o BLOB|DBPROP_MAXROWSIZEINCLUDESBLOB|
|Máximo de tabelas em SELECT|DBPROP_MAXTABLESINSELECT|
|Mode|DBPROP_INIT_MODE|
|Vários conjuntos de parâmetros|DBPROP_MULTIPLEPARAMSETS|
|Vários resultados|DBPROP_MULTIPLERESULTS|
|Vários objetos de armazenamento|DBPROP_MULTIPLESTORAGEOBJECTS|
|Atualização de várias tabelas|DBPROP_MULTITABLEUPDATE|
|Ordem de agrupamento nula|DBPROP_NULLCOLLATION|
|Comportamento de concatenação NULL|DBPROP_CONCATNULLBEHAVIOR|
|Versão do OLE DB|DBPROP_PROVIDEROLEDBVER|
|Suporte a objeto OLE|DBPROP_OLEOBJECTS|
|Abrir suporte a conjunto de linhas|DBPROP_OPENROWSETSUPPORT|
|CLASSIFICAR por colunas na lista de seleção|DBPROP_ORDERBYCOLUMNSINSELECT|
|Disponibilidade do parâmetro de saída|DBPROP_OUTPUTPARAMETERAVAILABILITY|
|Acessadores de passagem por referência|DBPROP_BYREFACCESSORS|
|Senha|DBPROP_AUTH_PASSWORD|
|Tipo de ID persistente|DBPROP_PERSISTENTIDTYPE|
|Preparar comportamento de anulação|DBPROP_PREPAREABORTBEHAVIOR|
|Preparar comportamento de confirmação|DBPROP_PREPARECOMMITBEHAVIOR|
|Termo do procedimento|DBPROP_PROCEDURETERM|
|Prompt|DBPROP_INIT_PROMPT|
|Nome amigável do provedor|DBPROP_PROVIDERFRIENDLYNAME|
|Nome do Provedor|DBPROP_PROVIDERFILENAME|
|Versão do provedor|DBPROP_PROVIDERVER|
|Fonte de dados somente leitura|DBPROP_DATASOURCEREADONLY|
|Conversões de conjunto de linhas no comando|DBPROP_ROWSETCONVERSIONSONCOMMAND|
|Termo do esquema|DBPROP_SCHEMATERM|
|Uso do esquema|DBPROP_SCHEMAUSAGE|
|Suporte a SQL|DBPROP_SQLSUPPORT|
|Armazenamento estruturado|DBPROP_STRUCTUREDSTORAGE|
|Suporte a subconsulta|DBPROP_SUBQUERIES|
|Termo da tabela|DBPROP_TABLETERM|
|DDL de transação|DBPROP_SUPPORTEDTXNDDL|
|Id de Usuário|DBPROP_AUTH_USERID|
|Nome de usuário|DBPROP_USERNAME|
|Identificador de janela|DBPROP_INIT_HWND|

## <a name="recordset-dynamic-properties"></a>Propriedades dinâmicas do conjunto de registros
 As propriedades a seguir são adicionadas à coleção **Properties** do objeto **Recordset** .

|Nome da propriedade ADO|Nome da propriedade de OLE DB|
|-----------------------|--------------------------|
|Ordem de acesso|DBPROP_ACCESSORDER|
|Conjunto de linhas somente acréscimo|DBPROP_APPENDONLY|
|Bloqueando objetos de armazenamento|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Tipo de indicador|DBPROP_BOOKMARKTYPE|
|Indicação|DBPROP_IROWSETLOCATE|
|Indicadores ordenados|DBPROP_ORDEREDBOOKMARKS|
|Colunas adiadas do cache|DBPROP_CACHEDEFERRED|
|Alterar linhas inseridas|DBPROP_CHANGEINSERTEDROWS|
|Privilégios de coluna|DBPROP_COLUMNRESTRICT|
|Notificação de conjunto de colunas|DBPROP_NOTIFYCOLUMNSET|
|Coluna gravável|DBPROP_MAYWRITECOLUMN|
|Adiar coluna|DBPROP_DEFERRED|
|Atrasar atualizações de objeto de armazenamento|DBPROP_DELAYSTORAGEOBJECTS|
|Buscar versões anteriores|DBPROP_CANFETCHBACKWARDS|
|Linhas de espera|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|ILockBytes|DBPROP_ILockBytes|
|Linhas irmóveis|DBPROP_IMMOBILEROWS|
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
|Indicadores literais|DBPROP_LITERALBOOKMARKS|
|Identidade de linha literal|DBPROP_LITERALIDENTITY|
|Máximo de linhas abertas|DBPROP_MAXOPENROWS|
|Máximo de linhas pendentes|DBPROP_MAXPENDINGROWS|
|Máximo de linhas|DBPROP_MAXROWS|
|Uso de Memória|DBPROP_MEMORYUSAGE|
|Granularidade da notificação|DBPROP_NOTIFICATIONGRANULARITY|
|Fases de notificação|DBPROP_NOTIFICATIONPHASES|
|Objetos transacionados|DBPROP_TRANSACTEDOBJECT|
|Alterações de outros visíveis|DBPROP_OTHERUPDATEDELETE|
|Inserções de outros visíveis|DBPROP_OTHERINSERT|
|Próprias alterações visíveis|DBPROP_OWNUPDATEDELETE|
|Próprias inserções visíveis|DBPROP_OWNINSERT|
|Preservar ao abortar|DBPROP_ABORTPRESERVE|
|Preservar ao confirmar|DBPROP_COMMITPRESERVE|
|Reinicialização rápida|DBPROP_QUICKRESTART|
|Eventos reentrante|DBPROP_REENTRANTEVENTS|
|Remover linhas excluídas|DBPROP_REMOVEDELETED|
|Relatar várias alterações|DBPROP_REPORTMULTIPLECHANGES|
|Retornar inserções pendentes|DBPROP_RETURNPENDINGINSERTS|
|Notificação de exclusão de linha|DBPROP_NOTIFYROWDELETE|
|Notificação da primeira alteração da linha|DBPROP_NOTIFYROWFIRSTCHANGE|
|Notificação de inserção de linha|DBPROP_NOTIFYROWINSERT|
|Privilégios de linha|DBPROP_ROWRESTRICT|
|Notificação de ressincronização de linha|DBPROP_NOTIFYROWRESYNCH|
|Modelo de threading de linha|DBPROP_ROWTHREADMODEL|
|Notificação de desfazer alteração de linha|DBPROP_NOTIFYROWUNDOCHANGE|
|Notificação de desfazer exclusão de linha|DBPROP_NOTIFYROWUNDODELETE|
|Notificação de desfazer inserção de linha|DBPROP_NOTIFYROWUNDOINSERT|
|Notificação de atualização de linha|DBPROP_NOTIFYROWUPDATE|
|Notificação de alteração de posição de busca de conjunto de linhas|DBPROP_NOTIFYROWSETFETCHPOSISIONCHANGE|
|Notificação de liberação de conjunto de linhas|DBPROP_NOTIFYROWSETRELEASE|
|Rolar para trás|DBPROP_CANSCROLLBACKWARDS|
|Ignorar indicadores excluídos|DBPROP_BOOKMARKSKIPPED|
|Identidade de linha forte|DBPROP_STRONGITDENTITY|
|Capacidade|DBPROP_UPDATABILITY|
|Usar indicadores|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>Propriedades dinâmicas do comando
 As propriedades a seguir são adicionadas à coleção **Properties** do objeto **Command** .

|Nome da propriedade ADO|Nome da propriedade de OLE DB|
|-----------------------|--------------------------|
|Ordem de acesso|DBPROP_ACCESSORDER|
|Conjunto de linhas somente acréscimo|DBPROP_APPENDONLY|
|Bloqueando objetos de armazenamento|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Tipo de indicador|DBPROP_BOOKMARKTYPE|
|Indicação|DBPROP_IROWSETLOCATE|
|Alterar linhas inseridas|DBPROP_CHANGEINSERTEDROWS|
|Privilégios de coluna|DBPROP_COLUMNRESTRICT|
|Notificação de conjunto de colunas|DBPROP_NOTIFYCOLUMNSET|
|Adiar coluna|DBPROP_DEFERRED|
|Atrasar atualizações de objeto de armazenamento|DBPROP_DELAYSTORAGEOBJECTS|
|Buscar versões anteriores|DBPROP_CANFETCHBACKWARDS|
|Linhas de espera|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|ILockBytes|DBPROP_ILockBytes|
|Linhas irmóveis|DBPROP_IMMOBILEROWS|
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
|Indicadores literais|DBPROP_LITERALBOOKMARKS|
|Identidade de linha literal|DBPROP_LITERALIDENTITY|
|Modo de bloqueio|DBPROP_LOCKMODE|
|Máximo de linhas abertas|DBPROP_MAXOPENROWS|
|Máximo de linhas pendentes|DBPROP_MAXPENDINGROWS|
|Máximo de linhas|DBPROP_MAXROWS|
|Granularidade da notificação|DBPROP_NOTIFICATIONGRANULARITY|
|Fases de notificação|DBPROP_NOTIFICATIONPHASES|
|Objetos transacionados|DBPROP_TRANSACTEDOBJECT|
|Alterações de outros visíveis|DBPROP_OTHERUPDATEDELETE|
|Inserções de outros visíveis|DBPROP_OTHERINSERT|
|Próprias alterações visíveis|DBPROP_OWNUPDATEDELETE|
|Próprias inserções visíveis|DBPROP_OWNINSERT|
|Preservar ao abortar|DBPROP_ABORTPRESERVE|
|Preservar ao confirmar|DBPROP_COMMITPRESERVE|
|Reinicialização rápida|DBPROP_QUICKRESTART|
|Eventos reentrante|DBPROP_REENTRANTEVENTS|
|Remover linhas excluídas|DBPROP_REMOVEDELETED|
|Relatar várias alterações|DBPROP_REPORTMULTIPLECHANGES|
|Retornar inserções pendentes|DBPROP_RETURNPENDINGINSERTS|
|Notificação de exclusão de linha|DBPROP_NOTIFYROWDELETE|
|Notificação da primeira alteração da linha|DBPROP_NOTIFYROWFIRSTCHANGE|
|Notificação de inserção de linha|DBPROP_NOTIFYROWINSERT|
|Privilégios de linha|DBPROP_ROWRESTRICT|
|Notificação de ressincronização de linha|DBPROP_NOTIFYROWRESYNCH|
|Modelo de threading de linha|DBPROP_ROWTHREADMODEL|
|Notificação de desfazer alteração de linha|DBPROP_NOTIFYROWUNDOCHANGE|
|Notificação de desfazer exclusão de linha|DBPROP_NOTIFYROWUNDODELETE|
|Notificação de desfazer inserção de linha|DBPROP_NOTIFYROWUNDOINSERT|
|Notificação de atualização de linha|DBPROP_NOTIFYROWUPDATE|
|Notificação de alteração de posição de busca de conjunto de linhas|DBPROP_NOTIFYROWSETFETCHPOSITIONCHANGE|
|Notificação de liberação de conjunto de linhas|DBPROP_NOTIFYROWSETRELEASE|
|Rolar para trás|DBPROP_CANSCROLLBACKWARDS|
|Dados do servidor ao inserir|DBPROP_SERVERDATAONINSERT|
|Ignorar indicadores excluídos|DBPROP_BOOKMARKSKIP|
|Identidade de linha forte|DBPROP_STRONGIDENTITY|
|Capacidade|DBPROP_UPDATABILITY|
|Usar indicadores|DBPROP_BOOKMARKS|

 Para obter detalhes de implementação específicos e informações funcionais sobre o provedor de OLE DB do Microsoft Jet, consulte [provedor Jet](https://msdn.microsoft.com/library/windows/desktop/ms722791.aspx) na documentação do OLE DB.
