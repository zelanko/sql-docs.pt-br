---
description: Visão geral do provedor de OLE DB da Microsoft para ODBC
title: Provedor do Microsoft OLE DB para ODBC | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB provider for ODBC [ADO]
- providers [ADO], OLE DB provider for ODBC
ms.assetid: 2dc0372d-e74d-4d0f-9c8c-04e5a168c148
author: rothja
ms.author: jroth
ms.openlocfilehash: 2dcd280098a5ca4075f424f12b0abdfede6b7653
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806645"
---
# <a name="microsoft-ole-db-provider-for-odbc-overview"></a>Visão geral do provedor de OLE DB da Microsoft para ODBC
Para um programador de ADO ou RDS, um mundo ideal seria aquele em que cada fonte de dados expõe uma interface OLE DB, para que o ADO pudesse chamar diretamente para a fonte de dados. Embora cada vez mais fornecedores de banco de dados estejam implementando interfaces OLE DB, algumas fontes de dados ainda não são expostas dessa maneira. No entanto, a maioria dos sistemas DBMS usados atualmente pode ser acessada por meio do ODBC.

 Os drivers ODBC estão disponíveis para cada DBMS principal em uso atualmente, incluindo Microsoft SQL Server, Microsoft Access (mecanismo de banco de dados do Microsoft Jet) e Microsoft FoxPro, além de produtos de banco de dados que não são da Microsoft, como Oracle.

 O provedor Microsoft ODBC, no entanto, permite que o ADO se conecte a qualquer fonte de dados ODBC. O provedor está livre de threads e Unicode habilitado.

 O provedor oferece suporte a transações, embora diferentes mecanismos DBMS ofereçam tipos diferentes de suporte a transações. Por exemplo, o Microsoft Access dá suporte a transações aninhadas de até cinco níveis de profundidade.

 Esse é o provedor padrão para ADO, e há suporte para todos os métodos e propriedades ADO dependentes do provedor.

## <a name="connection-string-parameters"></a>Parâmetros de cadeia de conexão
 Para se conectar a esse provedor, defina o **provedor =** argumento da propriedade [ConnectionString](../../reference/ado-api/connectionstring-property-ado.md) como:

```
MSDASQL
```

 A leitura da propriedade [Provider](../../reference/ado-api/provider-property-ado.md) retornará essa cadeia de caracteres também.

## <a name="typical-connection-string"></a>Cadeia de conexão típica
 Uma cadeia de conexão típica para esse provedor é:

```
"Provider=MSDASQL;DSN=dsnName;UID=MyUserID;PWD=MyPassword;"
```

 A cadeia de caracteres consiste nessas palavras-chave:

|Palavra-chave|Descrição|
|-------------|-----------------|
|**Provedor**|Especifica o provedor de OLE DB para ODBC.|
|**DSN**|Especifica o nome da fonte de dados.|
|**UID**|Especifica um nome de usuário.|
|**PWD**|Especifica a senha do usuário.|
|**URL**|Especifica a URL de um arquivo ou diretório publicado em uma pasta da Web.|

 Como esse é o provedor padrão do ADO, se você omitir o parâmetro **Provider =** da cadeia de conexão, o ADO tentará estabelecer uma conexão com esse provedor.

> [!NOTE]
>  Se você estiver se conectando a um provedor de fonte de dados que dá suporte à autenticação do Windows, especifique **Trusted_Connection = Sim** ou **segurança integrada = SSPI** , em vez de ID de usuário e informações de senha na cadeia de conexão.

 O provedor não oferece suporte a parâmetros de conexão específicos além daqueles definidos pelo ADO. No entanto, o provedor passará quaisquer parâmetros de conexão não ADO para o Gerenciador de driver ODBC.

 Como você pode omitir o parâmetro do **provedor** , você pode, portanto, compor uma cadeia de conexão ADO idêntica a uma cadeia de conexão ODBC para a mesma fonte de dados. Use os mesmos nomes de parâmetro (**Driver =**, **Database =**, **DSN =** e assim por diante), valores e sintaxe como você faria ao compor uma cadeia de conexão ODBC. Você pode se conectar com ou sem um nome de fonte de dados (DSN) predefinido ou FileDSN.

## <a name="syntax-with-a-dsn-or-filedsn"></a>Sintaxe com um DSN ou FileDSN:

```
"[Provider=MSDASQL;] { DSN=name | FileDSN=filename } ;
[DATABASE=database;] UID=user; PWD=password"
```

## <a name="syntax-without-a-dsn-dsn-less-connection"></a>Sintaxe sem um DSN (conexão com acesso sem DSN):

```
"[Provider=MSDASQL;] DRIVER=driver; SERVER=server;
DATABASE=database; UID=MyUserID; PWD=MyPassword"
```

## <a name="remarks"></a>Comentários
 Se você usar um **DSN** ou **FileDSN**, ele deverá ser definido por meio do administrador de fonte de dados ODBC no painel de controle do Windows. No Microsoft Windows 2000, o Administrador ODBC está localizado em ferramentas administrativas. Nas versões anteriores do Windows, o ícone do administrador do ODBC é chamado de **ODBC de 32 bits** ou apenas **ODBC**.

 Como alternativa à definição de um **DSN**, você pode especificar o driver ODBC (**Driver =**), como "SQL Server;" o nome do servidor (**Server =**); e o nome do banco de dados (**Database =**).

 Você também pode especificar um nome de conta de usuário (**UID =**) e a senha da conta de usuário (**pwd =**) nos parâmetros específicos do ODBC ou nos parâmetros de *senha* e de *usuário* definidos pelo ADO padrão.

 Embora uma definição de **DSN** já especifique um banco de dados, você pode especificar *um* parâmetro de *banco de dados* além de um **DSN** para se conectar a um banco de dados diferente. É uma boa ideia sempre incluir o parâmetro *de banco de* *dados* ao usar um **DSN**. Isso garantirá que você se conecte ao banco de dados correto se outro usuário alterou o parâmetro de banco de dados padrão desde a última vez que você verificou a definição de **DSN** .

## <a name="provider-specific-connection-properties"></a>Propriedades de conexão específicas do provedor
 O provedor de OLE DB para ODBC adiciona várias propriedades à coleção de [Propriedades](../../reference/ado-api/properties-collection-ado.md) do objeto de **conexão** . A tabela a seguir lista essas propriedades com o nome da propriedade OLE DB correspondente entre parênteses.

|Nome da propriedade|Descrição|
|-------------------|-----------------|
|Procedimentos acessíveis (KAGPROP_ACCESSIBLEPROCEDURES)|Indica se o usuário tem acesso aos procedimentos armazenados.|
|Tabelas acessíveis (KAGPROP_ACCESSIBLETABLES)|Indica se o usuário tem permissão para executar instruções SELECT em relação às tabelas de banco de dados.|
|Instruções ativas (KAGPROP_ACTIVESTATEMENTS)|Indica o número de identificadores que um driver ODBC pode dar suporte em uma conexão.|
|Nome do driver (KAGPROP_DRIVERNAME)|Indica o nome do arquivo do driver ODBC.|
|Versão do ODBC do driver (KAGPROP_DRIVERODBCVER)|Indica a versão do ODBC à qual este driver dá suporte.|
|Uso do arquivo (KAGPROP_FILEUSAGE)|Indica como o driver trata um arquivo em uma fonte de dados; como uma tabela ou como um catálogo.|
|Cláusula LIKE escape (KAGPROP_LIKEESCAPECLAUSE)|Indica se o driver dá suporte à definição e ao uso de um caractere de escape para o caractere de porcentagem (%) e sublinhar caractere (_) no predicado LIKE de uma cláusula WHERE.|
|Máximo de colunas em Group by (KAGPROP_MAXCOLUMNSINGROUPBY)|Indica o número máximo de colunas que podem ser listadas na cláusula GROUP BY de uma instrução SELECT.|
|Máximo de colunas no índice (KAGPROP_MAXCOLUMNSININDEX)|Indica o número máximo de colunas que podem ser incluídas em um índice.|
|Máximo de colunas na ordem por (KAGPROP_MAXCOLUMNSINORDERBY)|Indica o número máximo de colunas que podem ser listadas na cláusula ORDER BY de uma instrução SELECT.|
|Máximo de colunas em Select (KAGPROP_MAXCOLUMNSINSELECT)|Indica o número máximo de colunas que podem ser listadas na parte SELECT de uma instrução SELECT.|
|Máximo de colunas na tabela (KAGPROP_MAXCOLUMNSINTABLE)|Indica o número máximo de colunas permitido em uma tabela.|
|Funções numéricas (KAGPROP_NUMERICFUNCTIONS)|Indica quais funções numéricas são suportadas pelo driver ODBC. Para obter uma lista de nomes de função e os valores associados usados nesta bitmask, consulte o [apêndice e: funções escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md), na documentação ODBC.|
|Recursos de junção externa (KAGPROP_OJCAPABILITY)|Indica os tipos de junções externas com suporte no provedor.|
|Junções externas (KAGPROP_OUTERJOINS)|Indica se o provedor oferece suporte a junções externas.|
|Caracteres especiais (KAGPROP_SPECIALCHARACTERS)|Indica quais caracteres têm um significado especial para o driver ODBC.|
|Procedimentos armazenados (KAGPROP_PROCEDURES)|Indica se os procedimentos armazenados estão disponíveis para uso com este driver ODBC.|
|Funções de cadeia de caracteres (KAGPROP_STRINGFUNCTIONS)|Indica quais funções de cadeia de caracteres são suportadas pelo driver ODBC. Para obter uma lista de nomes de função e os valores associados usados nesta bitmask, consulte o [apêndice e: funções escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md), na documentação ODBC.|
|Funções do sistema (KAGPROP_SYSTEMFUNCTIONS)|Indica quais funções do sistema são suportadas pelo driver ODBC. Para obter uma lista de nomes de função e os valores associados usados nesta bitmask, consulte o [apêndice e: funções escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md), na documentação ODBC.|
|Funções de data/hora (KAGPROP_TIMEDATEFUNCTIONS)|Indica quais funções de data e hora são suportadas pelo driver ODBC. Para obter uma lista de nomes de função e os valores associados usados nesta bitmask, consulte o [apêndice e: funções escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md), na documentação ODBC.|
|Suporte à gramática do SQL (KAGPROP_ODBCSQLCONFORMANCE)|Indica a gramática SQL à qual o driver ODBC dá suporte.|

## <a name="provider-specific-recordset-and-command-properties"></a>Conjunto de registros e propriedades de comando específicas do provedor
 O provedor de OLE DB para ODBC adiciona várias propriedades à coleção **Properties** dos objetos **Recordset** e **Command** . A tabela a seguir lista essas propriedades com o nome da propriedade OLE DB correspondente entre parênteses.

|Nome da propriedade|Descrição|
|-------------------|-----------------|
|Atualizações/exclusões/inserções baseadas em consulta (KAGPROP_QUERYBASEDUPDATES)|Indica se as atualizações, as exclusões e as inserções podem ser executadas usando consultas SQL.|
|Tipo de simultaneidade ODBC (KAGPROP_CONCURRENCY)|Indica o método usado para reduzir possíveis problemas causados por dois usuários tentando acessar os mesmos dados da fonte de dados simultaneamente.|
|Acessibilidade de BLOB no cursor de somente avanço (KAGPROP_BLOBSONFOCURSOR)|Indica se os **campos** de blob podem ser acessados ao usar um cursor de somente avanço.|
|Incluir SQL_FLOAT, SQL_DOUBLE e SQL_REAL em QBU WHERE cláusulas (KAGPROP_INCLUDENONEXACT)|Indica se os valores SQL_FLOAT, SQL_DOUBLE e SQL_REAL podem ser incluídos em uma cláusula WHERE QBU.|
|Posição na última linha após a inserção (KAGPROP_POSITIONONNEWROW)|Indica que, depois que um novo registro for inserido em uma tabela, a última linha da tabela será a linha atual.|
|IRowsetChangeExtInfo (KAGPROP_IROWSETCHANGEEXTINFO)|Indica se a interface **IRowsetChange** fornece suporte estendido a informações.|
|Tipo de cursor ODBC (KAGPROP_CURSOR)|Indica o tipo de cursor usado pelo **conjunto de registros**.|
|Gerar um conjunto de linhas que pode ser empacotado (KAGPROP_MARSHALLABLE)|Indica que o driver ODBC gera um conjunto de registros que pode ser empacotado|

## <a name="command-text"></a>Texto do comando
 A maneira como você usa o objeto de [comando](../../reference/ado-api/command-object-ado.md) depende amplamente da fonte de dados e do tipo de consulta ou instrução de comando que ele aceitará.

 O ODBC fornece uma sintaxe específica para chamar procedimentos armazenados. Para a propriedade [CommandText](../../reference/ado-api/commandtext-property-ado.md) de um objeto **Command** , o *argumento CommandText* para o método **Execute** em um objeto [Connection](../../reference/ado-api/connection-object-ado.md) ou o argumento *Source* para o método **Open** em um objeto [Recordset](../../reference/ado-api/recordset-object-ado.md) , passa uma cadeia de caracteres com essa sintaxe:

```
"{ [ ? = ] call procedure [ ( ? [, ? [ , ... ]] ) ] }"
```

 Cada um **?** faz referência a um objeto na coleção de [parâmetros](../../reference/ado-api/parameters-collection-ado.md) . O primeiro **?** referencia **parâmetros**(0), o próximo **?** referencia **parâmetros**(1) e assim por diante.

 As referências de parâmetro são opcionais e dependem da estrutura do procedimento armazenado. Se você quiser chamar um procedimento armazenado que não define nenhum parâmetro, sua cadeia de caracteres seria semelhante ao seguinte:

```
"{ call procedure }"
```

 Se você tiver dois parâmetros de consulta, sua cadeia de caracteres seria semelhante ao seguinte:

```
"{ call procedure ( ?, ? ) }"
```

 Se o procedimento armazenado retornar um valor, o valor de retorno será tratado como outro parâmetro. Se você não tiver parâmetros de consulta, mas tiver um valor de retorno, sua cadeia de caracteres será semelhante ao seguinte:

```
"{ ? = call procedure }"
```

 Por fim, se você tiver um valor de retorno e dois parâmetros de consulta, sua cadeia de caracteres seria semelhante ao seguinte:

```
"{ ? = call procedure ( ?, ? ) }"
```

## <a name="recordset-behavior"></a>Comportamento do conjunto de registros
 As tabelas a seguir listam os métodos e as propriedades padrão do ADO disponíveis em um objeto **Recordset** aberto com esse provedor.

 Para obter informações mais detalhadas sobre o comportamento do **conjunto de registros** para a configuração do provedor, execute o método de [suporte](../../reference/ado-api/supports-method.md) e enumere a coleção **Properties** do **conjunto de registros** para determinar se as propriedades dinâmicas específicas do provedor estão presentes.

 Disponibilidade das propriedades padrão do **conjunto de registros** ADO:

|Propriedade|ForwardOnly|Dinâmico|Keyset|Estático|
|--------------|-----------------|-------------|------------|------------|
|[AbsolutePage](../../reference/ado-api/absolutepage-property-ado.md)|não disponível|não disponível|leitura/gravação|leitura/gravação|
|[AbsolutePosition](../../reference/ado-api/absoluteposition-property-ado.md)|não disponível|não disponível|leitura/gravação|leitura/gravação|
|[ActiveConnection](../../reference/ado-api/activeconnection-property-ado.md)|leitura/gravação|leitura/gravação|leitura/gravação|leitura/gravação|
|[BOF](../../reference/ado-api/bof-eof-properties-ado.md)|somente leitura|somente leitura|somente leitura|somente leitura|
|[Indicador](../../reference/ado-api/bookmark-property-ado.md)|não disponível|não disponível|leitura/gravação|leitura/gravação|
|[CacheSize](../../reference/ado-api/cachesize-property-ado.md)|leitura/gravação|leitura/gravação|leitura/gravação|leitura/gravação|
|[CursorLocation](../../reference/ado-api/cursorlocation-property-ado.md)|leitura/gravação|leitura/gravação|leitura/gravação|leitura/gravação|
|[CursorType](../../reference/ado-api/cursortype-property-ado.md)|leitura/gravação|leitura/gravação|leitura/gravação|leitura/gravação|
|[EditMode](../../reference/ado-api/editmode-property.md)|somente leitura|somente leitura|somente leitura|somente leitura|
|[Filter](../../reference/ado-api/filter-property.md)|leitura/gravação|leitura/gravação|leitura/gravação|leitura/gravação|
|[LockType](../../reference/ado-api/locktype-property-ado.md)|leitura/gravação|leitura/gravação|leitura/gravação|leitura/gravação|
|[MarshalOptions](../../reference/ado-api/marshaloptions-property-ado.md)|leitura/gravação|leitura/gravação|leitura/gravação|leitura/gravação|
|[MaxRecords](../../reference/ado-api/maxrecords-property-ado.md)|leitura/gravação|leitura/gravação|leitura/gravação|leitura/gravação|
|[PageCount](../../reference/ado-api/pagecount-property-ado.md)|leitura/gravação|não disponível|somente leitura|somente leitura|
|[PageSize](../../reference/ado-api/pagesize-property-ado.md)|leitura/gravação|leitura/gravação|leitura/gravação|leitura/gravação|
|[RecordCount](../../reference/ado-api/recordcount-property-ado.md)|leitura/gravação|não disponível|somente leitura|somente leitura|
|[Origem](../../reference/ado-api/source-property-ado-recordset.md)|leitura/gravação|leitura/gravação|leitura/gravação|leitura/gravação|
|[State](../../reference/ado-api/state-property-ado.md)|somente leitura|somente leitura|somente leitura|somente leitura|
|[Status](../../reference/ado-api/status-property-ado-recordset.md)|somente leitura|somente leitura|somente leitura|somente leitura|

 As propriedades [AbsolutePosition](../../reference/ado-api/absoluteposition-property-ado.md) e [AbsolutePage](../../reference/ado-api/absolutepage-property-ado.md) são somente gravação quando o ADO é usado com a versão 1,0 do provedor do Microsoft OLE DB para ODBC.

 Disponibilidade de métodos **Recordset** padrão do ADO:

|Método|ForwardOnly|Dinâmico|Keyset|Estático|
|------------|-----------------|-------------|------------|------------|
|[AddNew](../../reference/ado-api/addnew-method-ado.md)|Sim|Sim|Sim|Sim|
|[Cancelar](../../reference/ado-api/cancel-method-ado.md)|Sim|Sim|Sim|Sim|
|[CancelBatch](../../reference/ado-api/cancelbatch-method-ado.md)|Sim|Sim|Sim|Sim|
|[CancelUpdate](../../reference/ado-api/cancelupdate-method-ado.md)|Sim|Sim|Sim|Sim|
|[Clone](../../reference/ado-api/clone-method-ado.md)|Não|Não|Sim|Sim|
|[Fechar](../../reference/ado-api/close-method-ado.md)|Sim|Sim|Sim|Sim|
|[Delete (excluir)](../../reference/ado-api/delete-method-ado-recordset.md)|Sim|Sim|Sim|Sim|
|[GetRows](../../reference/ado-api/getrows-method-ado.md)|Sim|Sim|Sim|Sim|
|[Mover](../../reference/ado-api/move-method-ado.md)|Sim|Sim|Sim|Sim|
|[MoveFirst](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Sim|Sim|Sim|Sim|
|[Velas](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Não|Sim|Sim|Sim|
|[MoveNext](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Sim|Sim|Sim|Sim|
|[MovePrevious](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Não|Sim|Sim|Sim|
|[NextRecordset](../../reference/ado-api/nextrecordset-method-ado.md)*|Sim|Sim|Sim|Sim|
|[Abrir](../../reference/ado-api/open-method-ado-recordset.md)|Sim|Sim|Sim|Sim|
|[Repita](../../reference/ado-api/requery-method.md)|Sim|Sim|Sim|Sim|
|[Sincronizar novamente](../../reference/ado-api/resync-method.md)|Não|Não|Sim|Sim|
|[Suporta](../../reference/ado-api/supports-method.md)|Sim|Sim|Sim|Sim|
|[Atualização](../../reference/ado-api/update-method.md)|Sim|Sim|Sim|Sim|
|[UpdateBatch](../../reference/ado-api/updatebatch-method.md)|Sim|Sim|Sim|Sim|

 * Não há suporte para bancos de dados do Microsoft Access.

## <a name="dynamic-properties"></a>Propriedades Dinâmicas
 O provedor Microsoft OLE DB para ODBC insere várias propriedades dinâmicas na coleção **Properties** dos objetos [Connection](../../reference/ado-api/connection-object-ado.md), [Recordset](../../reference/ado-api/recordset-object-ado.md)e [Command](../../reference/ado-api/command-object-ado.md) não abertos.

 As tabelas a seguir são um índice cruzado dos nomes do ADO e do OLE DB para cada propriedade dinâmica. A referência do programador de OLE DB refere-se a um nome de propriedade ADO pelo termo "Descrição". Você pode encontrar mais informações sobre essas propriedades na referência do programador de OLE DB. Procure o nome da propriedade OLE DB no índice ou veja o [Apêndice C: OLE DB Propriedades](/previous-versions/windows/desktop/ms723130(v=vs.85)).

## <a name="connection-dynamic-properties"></a>Propriedades dinâmicas da conexão
 As propriedades a seguir são adicionadas à coleção de **Propriedades** do objeto de **conexão** .

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
|Local|DBPROP_INIT_LOCATION|
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
|Serviços OLE DBs|DBPROP_INIT_OLEDBSERVICES|
|Versão do OLE DB|DBPROP_PROVIDEROLEDBVER|
|Suporte a objeto OLE|DBPROP_OLEOBJECTS|
|Abrir suporte a conjunto de linhas|DBPROP_OPENROWSETSUPPORT|
|CLASSIFICAR por colunas na lista de seleção|DBPROP_ORDERBYCOLUMNSINSELECT|
|Disponibilidade do parâmetro de saída|DBPROP_OUTPUTPARAMETERAVAILABILITY|
|Senha|DBPROP_AUTH_PASSWORD|
|Acessadores de passagem por referência|DBPROP_BYREFACCESSORS|
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
 As propriedades a seguir são adicionadas à coleção de **Propriedades** do objeto **Recordset** .

|Nome da propriedade ADO|Nome da propriedade de OLE DB|
|-----------------------|--------------------------|
|Ordem de acesso|DBPROP_ACCESSORDER|
|Bloqueando objetos de armazenamento|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Tipo de indicador|DBPROP_BOOKMARKTYPE|
|Indicação|DBPROP_IROWSETLOCATE|
|Alterar linhas inseridas|DBPROP_CHANGEINSERTEDROWS|
|Privilégios de coluna|DBPROP_COLUMNRESTRICT|
|Notificação de conjunto de colunas|DBPROP_NOTIFYCOLUMNSET|
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
|IRowsetResynch||
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
|Linhas exclusivas|DBPROP_UNIQUEROWS|
|Capacidade|DBPROP_UPDATABILITY|
|Usar indicadores|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>Propriedades dinâmicas do comando
 As propriedades a seguir são adicionadas à coleção de **Propriedades** do objeto de **comando** .

|Nome da propriedade ADO|Nome da propriedade de OLE DB|
|-----------------------|--------------------------|
|Ordem de acesso|DBPROP_ACCESSORDER|
|Bloqueando objetos de armazenamento|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Tipo de indicador|DBPROP_BOOKMARKTYPE|
|Indicação|DBPROP_IROWSETLOCATE|
|Alterar linhas inseridas|DBPROP_CHANGEINSERTEDROWS|
|Privilégios de coluna|DBPROP_COLUMNRESTRICT|
|Notificação de conjunto de colunas|DBPROP_NOTIFYCOLUMNSET|
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
|IRowsetResynch||
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
|Ignorar indicadores excluídos|DBPROP_BOOKMARKSKIP|
|Identidade de linha forte|DBPROP_STRONGIDENTITY|
|Capacidade|DBPROP_UPDATABILITY|
|Usar indicadores|DBPROP_BOOKMARKS|

 Para obter detalhes sobre a implementação específica e informações funcionais sobre o provedor de OLE DB da Microsoft para ODBC, consulte a [referência do programador de OLE DB](/previous-versions/windows/desktop/ms713643(v=vs.85)) ou visite o site Data Access and Storage Developer Center no msdn.

## <a name="see-also"></a>Consulte Também
 O [objeto Command (ADO)](../../reference/ado-api/command-object-ado.md) [COMMANDTEXT Property (ADO)](../../reference/ado-api/commandtext-property-ado.md) UserProperty [Object](../../reference/ado-api/connection-object-ado.md) (ADO) [ConnectionString](../../reference/ado-api/connectionstring-property-ado.md) [Properties](../../reference/ado-api/properties-collection-ado.md) (ADO) [método execute Method (](../../reference/ado-api/execute-method-ado-command.md) ADO) [o método](../../reference/ado-api/supports-method.md) [Open Method](../../reference/ado-api/open-method-ado-recordset.md) (ADO) (ADO) (ADO) [Propriedade do provedor](../../reference/ado-api/provider-property-ado.md) [de conjunto de](../../reference/ado-api/recordset-object-ado.md) [parâmetros](../../reference/ado-api/parameters-collection-ado.md)