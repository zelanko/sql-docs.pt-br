---
title: Provedor de OLE DB da Microsoft para SQL Server | Microsoft Docs
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
ms.openlocfilehash: bd28ece0e82c4551409920c876d54fbd7dc501ff
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926614"
---
# <a name="microsoft-ole-db-provider-for-sql-server-overview"></a>Visão geral do provedor do Microsoft OLE DB para SQL Server
O provedor de OLE DB da Microsoft para SQL Server, SQLOLEDB, permite que o ADO acesse Microsoft SQL Server.

> [!IMPORTANT]
> O provedor de OLE DB da Microsoft para SQL Server (SQLOLEDB) permanece preterido e não é recomendável usá-lo para novos trabalhos de desenvolvimento. Em vez disso, use o novo [Driver do Microsoft OLE DB para SQL Server](../../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL), que será atualizado com os recursos de servidor mais recentes.

## <a name="connection-string-parameters"></a>Parâmetros de cadeia de conexão
 Para se conectar a esse provedor, defina o argumento do *provedor* como a propriedade [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) como:

```vb
SQLOLEDB
```

 Esse valor também pode ser definido ou lido usando a propriedade [Provider](../../../ado/reference/ado-api/provider-property-ado.md) .

## <a name="typical-connection-string"></a>Cadeia de conexão típica
 Uma cadeia de conexão típica para esse provedor é:

```vb
"Provider=SQLOLEDB;Data Source=serverName;"
Initial Catalog=databaseName;
User ID=MyUserID;Password=MyPassword;"
```

 A cadeia de caracteres consiste nessas palavras-chave:

|Palavra-chave|Descrição|
|-------------|-----------------|
|**Provedor**|Especifica o provedor de OLE DB para SQL Server.|
|**Fonte de dados** ou **servidor**|Especifica o nome de um servidor.|
|**Catálogo inicial** ou **banco de dados**|Especifica o nome de um banco de dados no servidor.|
|**ID de usuário** ou **UID**|Especifica o nome de usuário (para SQL Server autenticação).|
|**Senha** ou **pwd**|Especifica a senha do usuário (para SQL Server autenticação).|

> [!NOTE]
>  Se você estiver se conectando a um provedor de fonte de dados que dá suporte à autenticação do Windows, especifique **Trusted_Connection = Sim** ou **segurança integrada = SSPI** , em vez de ID de usuário e informações de senha na cadeia de conexão.

## <a name="provider-specific-connection-parameters"></a>Parâmetros de conexão específicos do provedor
 O provedor dá suporte a vários parâmetros de conexão específicos do provedor, além daqueles definidos pelo ADO. Assim como acontece com as propriedades de conexão ADO, essas propriedades específicas do provedor podem ser definidas por meio da coleção [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) de uma [conexão](../../../ado/reference/ado-api/connection-object-ado.md) ou podem ser definidas como parte de **ConnectionString**.

|Parâmetro|Descrição|
|---------------|-----------------|
|Trusted_Connection|Indica o modo de autenticação do usuário. Isso pode ser definido como **Sim** ou **não**. O valor padrão é **no**. Se essa propriedade for definida como **Sim**, SQLOLEDB usará o modo de autenticação do Microsoft Windows NT para autorizar o acesso do usuário ao banco de dados de SQL Server especificado pelos valores de propriedade **local** e [DataSource](../../../ado/reference/ado-api/datasource-property-ado.md) . Se essa propriedade for definida como **não**, SQLOLEDB usará o modo misto para autorizar o acesso do usuário ao banco de dados de SQL Server. O logon de SQL Server e a senha são especificados nas propriedades **ID de usuário** e **senha** .|
|Idioma Atual|Indica um nome de idioma SQL Server. Identifica o idioma usado para seleção de mensagem de sistema e formatação. O idioma deve ser instalado na SQL Server, caso contrário, abrir a conexão falhará.|
|Endereço de Rede|Indica o endereço de rede do SQL Server especificado pela propriedade **Location** .|
|Biblioteca de rede|Indica o nome da biblioteca de rede (DLL) usada para se comunicar com o SQL Server. O nome não deve incluir o caminho ou a extensão de nome de arquivo .dll. O padrão é fornecido pela configuração do cliente SQL Server.|
|Usar procedimento para preparar|Determina se SQL Server cria procedimentos armazenados temporários quando os comandos são preparados (pela propriedade **preparada** ).|
|Tradução automática|Indica se os caracteres OEM/ANSI são convertidos. Essa propriedade pode ser definida como **true** ou **false**. O valor padrão é **True**. Se essa propriedade for definida como **true**, SQLOLEDB executará a conversão de caracteres OEM/ANSI quando as cadeias de caracteres de vários bytes forem recuperadas ou enviadas para o SQL Server. Se essa propriedade for definida como **false**, SQLOLEDB não executará a conversão de caracteres OEM/ANSI em dados de cadeia de caracteres de vários bytes.|
|Tamanho do Pacote|Indica um tamanho de pacote de rede em bytes. O valor da propriedade tamanho do pacote deve estar entre 512 e 32767. O tamanho padrão do pacote de rede SQLOLEDB é 4096.|
|Nome do Aplicativo|Indica o nome do aplicativo cliente.|
|ID da Estação de Trabalho|uma cadeia de caracteres que identifica a estação de trabalho.|

## <a name="command-object-usage"></a>Uso do objeto Command
 SQLOLEDB aceita um mistura de ODBC, ANSI e Transact-SQL específico de SQL Server como sintaxe válida. Por exemplo, a seguinte instrução SQL usa uma sequência de escape do ODBC SQL para especificar a função de cadeia de caracteres LCASE:

```sql
SELECT customerid={fn LCASE(CustomerID)} FROM Customers

```

 LCASE retorna uma cadeia de caracteres, convertendo todos os caracteres em maiúscula aos seus equivalentes em minúsculas. A função de cadeia de caracteres SQL ANSI baixa executa a mesma operação, portanto, a seguinte instrução SQL é um equivalente ANSI para a instrução ODBC apresentada anteriormente:

```sql
SELECT customerid=LOWER(CustomerID) FROM Customers

```

 SQLOLEDB processa com êxito a forma da instrução quando especificado como texto para um comando.

## <a name="stored-procedures"></a>Procedimentos armazenados
 Ao executar um procedimento armazenado SQL Server usando um comando SQLOLEDB, use a sequência de escape de chamada de procedimento ODBC no texto do comando. Em seguida, SQLOLEDB usa o mecanismo de chamada de procedimento remoto de SQL Server para otimizar o processamento de comandos. Por exemplo, a seguinte instrução SQL ODBC é o texto de comando preferencial no formulário Transact-SQL:

## <a name="odbc-sql"></a>ODBC SQL

```vb
{call SalesByCategory('Produce', '1995')}

```

## <a name="transact-sql"></a>Transact-SQL

```sql
EXECUTE SalesByCategory 'Produce', '1995'

```

## <a name="sql-server-features"></a>Recursos de SQL Server
 Com o SQL Server, o ADO pode usar XML para entrada de **comando** e recuperar resultados em formato de fluxo XML em vez de em objetos **Recordset** . Para obter mais informações, consulte [usando fluxos para entrada de comando](../../../ado/guide/data/command-streams.md) e [recuperando conjuntos de resultados em fluxos](../../../ado/guide/data/retrieving-resultsets-into-streams.md).

### <a name="accessing-sql_variant-data-using-mdac-27-mdac-28-or-windows-dac-60"></a>Acessando dados sql_variant usando MDAC 2,7, MDAC 2,8 ou Windows DAC 6,0
 Microsoft SQL Server tem um tipo de dados chamado **sql_variant**. Semelhante ao **DBTYPE_VARIANT**do OLE DB, o tipo de dados **sql_variant** pode armazenar dados de vários tipos diferentes. No entanto, há algumas diferenças importantes entre **DBTYPE_VARIANT** e **sql_variant**. O ADO também manipula os dados armazenados como um valor **sql_variant** de forma diferente de como ele lida com outros tipos de dados. A lista a seguir descreve os problemas a serem considerados quando você acessa SQL Server dados armazenados em colunas do tipo **sql_variant**.

-   No MDAC 2,7, no MDAC 2,8 e no Windows Data Access Components (Windows DAC) 6,0, o provedor de OLE DB para SQL Server dá suporte ao tipo de **sql_variant** . O provedor de OLE DB para ODBC não faz isso.

-   O tipo de **sql_variant** não corresponde exatamente ao tipo de dados **DBTYPE_VARIANT** .  O tipo de **sql_variant** dá suporte a alguns novos subtipos, o que não é suportado pelo **DBTYPE_VARIANT,** incluindo cadeias de caracteres **GUID**, **ANSI** (não Unicode) e **bigint**. O uso de subtipos diferentes daqueles listados anteriormente funcionará corretamente.

-   O **numérico** de subtipo **sql_variant** não corresponde ao **DBTYPE_DECIMAL** de tamanho.

-   Várias coerçãos de tipo de dados resultarão em tipos que não correspondem. Por exemplo, a coerção de um **sql_variant** com um subtipo de **GUID** para um **DBTYPE_VARIANT** resultará em um subtipo de **SafeArray**(bytes). Converter esse tipo de volta para um **sql_variant** resultará em um novo subtipo de **matriz**(bytes).

-   Os campos do **conjunto de registros** que contêm **sql_variant** dados poderão ser remotos (empacotados) ou persistidos somente se o **sql_variant** contiver subtipos específicos. A tentativa de manter os dados remotos ou persistentes com os seguintes subtipos sem suporte causará um erro em tempo de execução (conversão sem suporte) do provedor de persistência da Microsoft (MSPersist): **VT_VARIANT**, **VT_RECORD**, **VT_ILLEGAL**, **VT_UNKNOWN**, **VT_BSTR**e **VT_DISPATCH.**

-   O provedor de OLE DB para SQL Server no MDAC 2,7, no MDAC 2,8 e no Windows DAC 6,0 tem uma propriedade dinâmica chamada **permitir variantes nativas** , que, como o nome sugere, permite que os desenvolvedores acessem o **sql_variant** em sua forma nativa, em oposição a um **DBTYPE_VARIANT**. Se essa propriedade for definida e um **conjunto de registros** for aberto com o mecanismo de cursor do cliente (**adUseClient**), a chamada **Recordset. Open** falhará. Se essa propriedade for definida e um **conjunto de registros** for aberto com cursores de servidor (**adUseServer**), a chamada **Recordset. Open** terá sucesso, mas o acesso às colunas do tipo **sql_variant** produzirá um erro.

-   Em aplicativos cliente que usam o MDAC 2,5, **sql_variant** dados podem ser usados com consultas no Microsoft SQL Server. No entanto, os valores dos dados de **sql_variant** são tratados como cadeias de caracteres. Esses aplicativos cliente devem ser atualizados para MDAC 2,7, MDAC 2,8 ou Windows DAC 6,0.

## <a name="recordset-behavior"></a>Comportamento do conjunto de registros
 SQLOLEDB não pode usar cursores SQL Server para dar suporte a vários resultados gerados por muitos comandos. Se um consumidor solicitar um conjunto de registros exigindo SQL Server suporte a cursor, ocorrerá um erro se o texto do comando usado gerar mais de um único conjunto de registros como resultado.

 Os conjuntos de registros SQLOLEDB que podem ser rolados são suportados pelos cursores SQL Server. SQL Server impõe limitações em cursores que são sensíveis a alterações feitas por outros usuários do banco de dados. Especificamente, as linhas em alguns cursores não podem ser ordenadas e a tentativa de criar um conjunto de registros usando um comando que contém uma cláusula SQL ORDER BY pode falhar.

## <a name="dynamic-properties"></a>Propriedades Dinâmicas
 O provedor de OLE DB da Microsoft para SQL Server insere várias propriedades dinâmicas na coleção **Properties** dos objetos [Connection](../../../ado/reference/ado-api/connection-object-ado.md), [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)e [Command](../../../ado/reference/ado-api/command-object-ado.md) não abertos.

 As tabelas a seguir são um índice cruzado dos nomes do ADO e do OLE DB para cada propriedade dinâmica. A referência do programador de OLE DB refere-se a um nome de propriedade ADO pelo termo "Descrição". Você pode encontrar mais informações sobre essas propriedades na referência do programador de OLE DB. Procure o nome da propriedade OLE DB no índice ou veja o [Apêndice C: OLE DB Propriedades](https://msdn.microsoft.com/deded3ff-f508-4e1b-b2b1-fd9afd3bd292).

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
|Connect Timeout|DBPROP_INIT_TIMEOUT|
|Catálogo atual|DBPROP_CURRENTCATALOG|
|fonte de dados|DBPROP_INIT_DATASOURCE|
|Nome da Fonte de Dados|DBPROP_DATASOURCENAME|
|Modelo de Threading do objeto de fonte de dados|DBPROP_DSOTHREADMODEL|
|Nome do DBMS|DBPROP_DBMSNAME|
|Versão do DBMS|DBPROP_DBMSVER|
|Propriedades estendidas|DBPROP_INIT_PROVIDERSTRING|
|Agrupar por suporte|DBPROP_GROUPBY|
|Suporte a tabelas heterogêneas|DBPROP_HETEROGENEOUSTABLES|
|Diferenciar maiúsculas de minúsculas|DBPROP_IDENTIFIERCASE|
|Catálogo Inicial|DBPROP_INIT_CATALOG|
|Níveis de isolamento|DBPROP_SUPPORTEDTXNISOLEVELS|
|Retenção de isolamento|DBPROP_SUPPORTEDTXNISORETAIN|
|Identificador de Localidade|DBPROP_INIT_LCID|
|Tamanho máximo do índice|DBPROP_MAXINDEXSIZE|
|Tamanho máximo da linha|DBPROP_MAXROWSIZE|
|O tamanho máximo da linha inclui o BLOB|DBPROP_MAXROWSIZEINCLUDESBLOB|
|Máximo de tabelas em SELECT|DBPROP_MAXTABLESINSELECT|
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
|Informações de Persistência de Segurança|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|
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
|Nome do Usuário|DBPROP_USERNAME|
|Identificador da Janela|DBPROP_INIT_HWND|

## <a name="recordset-dynamic-properties"></a>Propriedades dinâmicas do conjunto de registros
 As propriedades a seguir são adicionadas à coleção **Properties** do objeto **Recordset** .

|Nome da propriedade ADO|Nome da propriedade de OLE DB|
|-----------------------|--------------------------|
|Ordem de acesso|DBPROP_ACCESSORDER|
|Bloqueando objetos de armazenamento|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Tipo de indicador|DBPROP_BOOKMARKTYPE|
|Indicação|DBPROP_IROWSETLOCATE|
|Alterar linhas inseridas|DBPROP_CHANGEINSERTEDROWS|
|Privilégios de coluna|DBPROP_COLUMNRESTRICT|
|Notificação de conjunto de colunas|DBPROP_NOTIFYCOLUMNSET|
|Tempo limite do comando|DBPROP_COMMANDTIMEOUT|
|Adiar coluna|DBPROP_DEFERRED|
|Atrasar atualizações de objeto de armazenamento|DBPROP_DELAYSTORAGEOBJECTS|
|Buscar versões anteriores|DBPROP_CANFETCHBACKWARDS|
|Linhas de espera|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|Linhas irmóveis|DBPROP_IMMOBILEROWS|
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
|Indicadores literais|DBPROP_LITERALBOOKMARKS|
|Identidade de linha literal|DBPROP_LITERALIDENTITY|
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
|Notificação de alteração de posição de busca de conjunto de linhas|DBPROP_NOTIFYROWSETFETCHPOSISIONCHANGE|
|Notificação de liberação de conjunto de linhas|DBPROP_NOTIFYROWSETRELEASE|
|Rolar para trás|DBPROP_CANSCROLLBACKWARDS|
|Cursor do servidor|DBPROP_SERVERCURSOR|
|Ignorar indicadores excluídos|DBPROP_BOOKMARKSKIPPED|
|Identidade de linha forte|DBPROP_STRONGITDENTITY|
|Linhas exclusivas|DBPROP_UNIQUEROWS|
|Capacidade|DBPROP_UPDATABILITY|
|Usar indicadores|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>Propriedades dinâmicas do comando
 As propriedades a seguir são adicionadas à coleção **Properties** do objeto **Command** .

|Nome da propriedade ADO|Nome da propriedade de OLE DB|
|-----------------------|--------------------------|
|Ordem de acesso|DBPROP_ACCESSORDER|
|Caminho base|SSPROP_STREAM_BASEPATH|
|Bloqueando objetos de armazenamento|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Tipo de indicador|DBPROP_BOOKMARKTYPE|
|Indicação|DBPROP_IROWSETLOCATE|
|Alterar linhas inseridas|DBPROP_CHANGEINSERTEDROWS|
|Privilégios de coluna|DBPROP_COLUMNRESTRICT|
|Notificação de conjunto de colunas|DBPROP_NOTIFYCOLUMNSET|
|Tipo de conteúdo|SSPROP_STREAM_CONTENTTYPE|
|Busca automática do cursor|SSPROP_CURSORAUTOFETCH|
|Adiar coluna|DBPROP_DEFERRED|
|Adiar Preparação|SSPROP_DEFERPREPARE|
|Atrasar atualizações de objeto de armazenamento|DBPROP_DELAYSTORAGEOBJECTS|
|Buscar versões anteriores|DBPROP_CANFETCHBACKWARDS|
|Linhas de espera|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|Linhas irmóveis|DBPROP_IMMOBILEROWS|
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
|Propriedade de codificação de saída|DBPROP_OUTPUTENCODING|
|Propriedade de fluxo de saída|DBPROP_OUTPUTSTREAM|
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
|Cursor do servidor|DBPROP_SERVERCURSOR|
|Dados do servidor ao inserir|DBPROP_SERVERDATAONINSERT|
|Ignorar indicadores excluídos|DBPROP_BOOKMARKSKIP|
|Identidade de linha forte|DBPROP_STRONGIDENTITY|
|Capacidade|DBPROP_UPDATABILITY|
|Usar indicadores|DBPROP_BOOKMARKS|
|Raiz XML|SSPROP_STREAM_XMLROOT|
|XSL|SSPROP_STREAM_XSL|

 Para obter detalhes de implementação específicos e informações funcionais sobre o provedor de OLE DB de Microsoft SQL Server, consulte o [provedor de SQL Server](https://msdn.microsoft.com/adf1d6c4-5930-444a-9248-ff1979729635).

## <a name="see-also"></a>Consulte Também
 Propriedade [ConnectionString (](../../../ado/reference/ado-api/connectionstring-property-ado.md) ADO) provedor de conjunto de [Propriedades](../../../ado/reference/ado-api/provider-property-ado.md) (ADO) [Recordset (](../../../ado/reference/ado-api/recordset-object-ado.md) ADO)
