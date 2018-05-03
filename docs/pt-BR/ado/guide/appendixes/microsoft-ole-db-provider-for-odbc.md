---
title: Provedor Microsoft OLE DB para ODBC | Microsoft Docs
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
- OLE DB provider for ODBC [ADO]
- providers [ADO], OLE DB provider for ODBC
ms.assetid: 2dc0372d-e74d-4d0f-9c8c-04e5a168c148
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 965316983f7ef425d068253c6770beecfa2afe41
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="microsoft-ole-db-provider-for-odbc-overview"></a>Provedor Microsoft OLE DB para visão geral ODBC
Para um programador ADO ou RDS, um mundo ideal seria um no qual todos os dados de origem expõe uma interface OLE DB, para que o ADO poderia chamar diretamente na fonte de dados. Embora cada vez mais fornecedores de banco de dados estiver implementando interfaces OLE DB, algumas fontes de dados não são ainda expostos dessa maneira. No entanto, a maioria dos sistemas DBMS em uso hoje podem ser acessados por meio de ODBC.

 Drivers ODBC estão disponíveis para todos os principais DBMS em uso hoje, incluindo o Microsoft SQL Server, Microsoft Access (mecanismo de banco de dados do Microsoft Jet) e Microsoft FoxPro, além de produtos de banco de dados não Microsoft, como Oracle.

 O provedor do Microsoft ODBC, no entanto, permite que o ADO conectar-se a qualquer fonte de dados ODBC. O provedor é de thread livre e Unicode habilitado.

 O provedor oferece suporte a transações, embora diferentes mecanismos DBMS oferecem tipos diferentes de suporte a transações. Por exemplo, o Microsoft Access dá suporte a transações aninhadas até cinco níveis de profundidade.

 Este é o provedor padrão para ADO e todos os métodos e propriedades do ADO depende do provedor são suportados.

## <a name="connection-string-parameters"></a>Parâmetros de cadeia de caracteres de Conexão
 Para se conectar ao provedor, defina o **provedor =** argumento o [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propriedade para:

```
MSDASQL
```

 Lendo o [provedor](../../../ado/reference/ado-api/provider-property-ado.md) propriedade retornará essa cadeia de caracteres.

## <a name="typical-connection-string"></a>Cadeia de caracteres de Conexão típica
 Uma cadeia de conexão típica para esse provedor é:

```
"Provider=MSDASQL;DSN=dsnName;UID=MyUserID;PWD=MyPassword;"
```

 A cadeia de caracteres consiste nessas palavras-chave:

|Palavra-chave|Description|
|-------------|-----------------|
|**Provedor**|Especifica o provedor OLE DB para ODBC.|
|**DSN**|Especifica o nome da fonte de dados.|
|**UID**|Especifica o nome de usuário.|
|**PWD**|Especifica a senha do usuário.|
|**URL**|Especifica a URL de um arquivo ou diretório publicada em uma pasta da Web.|

 Como esse é o provedor padrão para ADO, se você omitir o **provedor =** parâmetro da cadeia de conexão, o ADO tentará estabelecer uma conexão ao provedor.

> [!NOTE]
>  Se você estiver se conectando a um provedor de fonte de dados que oferece suporte à autenticação do Windows, você deve especificar **Trusted_Connection = yes** ou **segurança integrada = SSPI** em vez de ID de usuário e senha informações na cadeia de conexão.

 O provedor não oferece suporte para os parâmetros de conexão específicos além daqueles definidos pelo ADO. No entanto, o provedor passará os parâmetros de conexão ADO não para o Gerenciador de driver ODBC.

 Porque você pode omitir o **provedor** parâmetro, portanto, você pode compor uma cadeia de caracteres de conexão ADO que seja idêntica de uma cadeia de caracteres de conexão ODBC para a mesma fonte de dados. Use os mesmos nomes de parâmetro (**DRIVER =**, **banco de dados =**, **DSN =**, e assim por diante), valores e sintaxe como você fossem ao compor uma cadeia de caracteres de conexão do ODBC. Você pode se conectar com ou sem um nome de fonte de dados predefinidos (DSN) ou FileDSN.

## <a name="syntax-with-a-dsn-or-filedsn"></a>Sintaxe com um DSN ou FileDSN:

```
"[Provider=MSDASQL;] { DSN=name | FileDSN=filename } ;
[DATABASE=database;] UID=user; PWD=password"
```

## <a name="syntax-without-a-dsn-dsn-less-connection"></a>Sintaxe sem um DSN (conexão sem DSN):

```
"[Provider=MSDASQL;] DRIVER=driver; SERVER=server;
DATABASE=database; UID=MyUserID; PWD=MyPassword"
```

## <a name="remarks"></a>Remarks
 Se você usar um **DSN** ou **FileDSN**, ele deverá ser definido por meio de administrador de fonte de dados do ODBC no painel de controle do Windows. No Microsoft Windows 2000, o administrador ODBC está localizado em Ferramentas administrativas. Em versões anteriores do Windows, o ícone de administrador de ODBC é denominado **ODBC de 32 bits** ou apenas **ODBC**.

 Como alternativa à configuração de um **DSN**, você pode especificar o driver ODBC (**DRIVER =**), como "SQL Server"; o nome do servidor (**SERVER =**); e o nome do banco de dados (**Banco de dados =**).

 Você também pode especificar um nome de conta de usuário (**UID =**) e a senha da conta de usuário (**PWD =**) nos parâmetros de ODBC específico ou no padrão definido pelo ADO *usuário* e *senha* parâmetros.

 Embora um **DSN** definição já especifica um banco de dados, você pode especificar *um* *banco de dados* parâmetro além um **DSN** para se conectar para um banco de dados diferente. É uma boa ideia sempre incluir *o* *banco de dados* parâmetro quando você usa um **DSN**. Isso garantirá que você se conectar ao banco de dados correto se outro usuário alterar o parâmetro de banco de dados padrão, desde que você verificou se o **DSN** definição.

## <a name="provider-specific-connection-properties"></a>Propriedades de Conexão específicos do provedor
 O provedor OLE DB para ODBC adiciona várias propriedades para o [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção do **Conexão** objeto. A tabela a seguir lista essas propriedades com o nome de propriedade OLE DB correspondente entre parênteses.

|Nome da propriedade|Description|
|-------------------|-----------------|
|Procedimentos acessíveis (KAGPROP_ACCESSIBLEPROCEDURES)|Indica se o usuário tem acesso a procedimentos armazenados.|
|Tabelas acessíveis (KAGPROP_ACCESSIBLETABLES)|Indica se o usuário tem permissão para executar instruções SELECT nas tabelas de banco de dados.|
|Instruções ativas (KAGPROP_ACTIVESTATEMENTS)|Indica o número de identificadores de que um driver ODBC pode dar suporte a uma conexão.|
|Nome do driver (KAGPROP_DRIVERNAME)|Indica o nome do arquivo do driver ODBC.|
|Versão do driver ODBC (KAGPROP_DRIVERODBCVER)|Indica a versão do ODBC que dá suporte a este driver.|
|Uso do arquivo (KAGPROP_FILEUSAGE)|Indica como o driver trata um arquivo em uma fonte de dados; como uma tabela ou um catálogo.|
|Como a cláusula de Escape (KAGPROP_LIKEESCAPECLAUSE)|Indica se o driver dá suporte a definição e o uso de um caractere de escape de caractere de porcentagem (%) e o caractere de sublinhado (_) no predicado LIKE de uma cláusula WHERE.|
|Máximo de colunas em Group By (KAGPROP_MAXCOLUMNSINGROUPBY)|Indica o número máximo de colunas que pode ser listado na cláusula GROUP BY de uma instrução SELECT.|
|Máximo de colunas no índice (KAGPROP_MAXCOLUMNSININDEX)|Indica o número máximo de colunas que podem ser incluídos em um índice.|
|Máximo de colunas em Order By (KAGPROP_MAXCOLUMNSINORDERBY)|Indica o número máximo de colunas que pode ser listado na cláusula ORDER BY de uma instrução SELECT.|
|Máximo de colunas em Select (KAGPROP_MAXCOLUMNSINSELECT)|Indica o número máximo de colunas que pode ser listado na parte SELECT de uma instrução SELECT.|
|Máximo de colunas na tabela (KAGPROP_MAXCOLUMNSINTABLE)|Indica o número máximo de colunas permitido em uma tabela.|
|Funções numéricas (KAGPROP_NUMERICFUNCTIONS)|Indica quais funções numéricas são suportadas pelo driver ODBC. Para obter uma lista de nomes de função e os valores associados usados nessa máscara de bits, consulte [apêndice e: escalar funções](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md), na documentação do ODBC.|
|Recursos de junção externa (KAGPROP_OJCAPABILITY)|Indica os tipos de junções externas têm suporte do provedor.|
|Junções externas (KAGPROP_OUTERJOINS)|Indica se o provedor oferece suporte a junções externas.|
|Caracteres especiais (KAGPROP_SPECIALCHARACTERS)|Indica se os caracteres que têm significado especial para o driver ODBC.|
|Procedimentos armazenados (KAGPROP_PROCEDURES)|Indica se os procedimentos armazenados estão disponíveis para uso com esse driver ODBC.|
|Funções de cadeia de caracteres (KAGPROP_STRINGFUNCTIONS)|Indica quais funções de cadeia de caracteres têm suporte pelo driver ODBC. Para obter uma lista de nomes de função e os valores associados usados nessa máscara de bits, consulte [apêndice e: escalar funções](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md), na documentação do ODBC.|
|Funções do sistema (KAGPROP_SYSTEMFUNCTIONS)|Indica quais funções de sistema são suportadas pelo driver ODBC. Para obter uma lista de nomes de função e os valores associados usados nessa máscara de bits, consulte [apêndice e: escalar funções](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md), na documentação do ODBC.|
|Funções de data/hora (KAGPROP_TIMEDATEFUNCTIONS)|Indica quais funções data e hora são suportadas pelo driver ODBC. Para obter uma lista de nomes de função e os valores associados usados nessa máscara de bits, consulte [apêndice e: escalar funções](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md), na documentação do ODBC.|
|Suporte à gramática SQL (KAGPROP_ODBCSQLCONFORMANCE)|Indica que o driver ODBC dá suporte à gramática do SQL.|

## <a name="provider-specific-recordset-and-command-properties"></a>Conjunto de registros específicos do provedor e as propriedades de comando
 O provedor OLE DB para ODBC adiciona várias propriedades para o **propriedades** coleção do **registros** e **comando** objetos. A tabela a seguir lista essas propriedades com o nome de propriedade OLE DB correspondente entre parênteses.

|Nome da propriedade|Description|
|-------------------|-----------------|
|Consulta com base em atualizações/exclusões/inserções (KAGPROP_QUERYBASEDUPDATES)|Indica se as inserções, exclusões e atualizações podem ser executadas por meio de consultas SQL.|
|Tipo de simultaneidade ODBC (KAGPROP_CONCURRENCY)|Indica o método usado para reduzir problemas potenciais causados por dois usuários tentando acessar os mesmos dados da fonte de dados simultaneamente.|
|Acessibilidade do BLOB no cursor somente de avanço (KAGPROP_BLOBSONFOCURSOR)|Indica se o BLOB **campos** podem ser acessados ao usar um cursor somente de avanço.|
|Incluir SQL_FLOAT, SQL_DOUBLE e SQL_REAL em cláusulas WHERE QBU (KAGPROP_INCLUDENONEXACT)|Indica se os valores SQL_FLOAT, SQL_DOUBLE e SQL_REAL podem ser incluídos em uma cláusula WHERE QBU.|
|Posição na última linha após a inserção (KAGPROP_POSITIONONNEWROW)|Indica que depois que um novo registro foi inserido em uma tabela, a última linha na tabela será vêm da linha atual.|
|IRowsetChangeExtInfo (KAGPROP_IROWSETCHANGEEXTINFO)|Indica se o **IRowsetChange** interface oferece suporte a informações estendidas.|
|Tipo de Cursor ODBC (KAGPROP_CURSOR)|Indica o tipo de cursor usado pelo **registros**.|
|Gerar um conjunto de linhas pode ser empacotado (KAGPROP_MARSHALLABLE)|Indica que o driver ODBC gera um conjunto de registros que pode ser empacotado|

## <a name="command-text"></a>Texto de comando
 Como usar o [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto depende principalmente da fonte de dados e o tipo de instrução de consulta ou um comando serão aceitas.

 ODBC fornece uma sintaxe específica para chamar procedimentos armazenados. Para o [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) propriedade de um **comando** objeto, o *CommandText* argumento para o **Execute** método em um [ Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto, ou o *fonte* argumento para o **abrir** método em um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto, passa em uma cadeia de caracteres com esta sintaxe:

```
"{ [ ? = ] call procedure [ ( ? [, ? [ , … ]] ) ] }"
```

 Cada **?** faz referência a um objeto de [parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md) coleção. A primeira **?** referências **parâmetros**(0), a próxima **?** referências **parâmetros**(1), e assim por diante.

 As referências de parâmetro são opcionais e dependem da estrutura do procedimento armazenado. Se você quiser chamar um procedimento armazenado que define sem parâmetros, a cadeia de caracteres seria semelhante ao seguinte:

```
"{ call procedure }"
```

 Se você tiver dois parâmetros de consulta, sua cadeia de caracteres seria semelhante à seguinte:

```
"{ call procedure ( ?, ? ) }"
```

 Se o procedimento armazenado retornará um valor, o valor de retorno será tratado como outro parâmetro. Se você tiver sem parâmetros de consulta, mas você tem um valor de retorno, sua cadeia de caracteres seria semelhante à seguinte:

```
"{ ? = call procedure }"
```

 Por fim, se você tiver um valor de retorno e dois parâmetros de consulta, sua cadeia de caracteres seria semelhante à seguinte:

```
"{ ? = call procedure ( ?, ? ) }"
```

## <a name="recordset-behavior"></a>Comportamento do conjunto de registros
 As tabelas seguintes listam os métodos padrão do ADO e propriedades disponíveis em um **registros** objeto aberto com este provedor.

 Para obter mais informações sobre **registros** comportamento para a sua configuração de provedor, execute o [dá suporte a](../../../ado/reference/ado-api/supports-method.md) método e enumerar o **propriedades** coleção da **Registros** para determinar se as propriedades dinâmicas específicos do provedor estão presentes.

 Disponibilidade do ADO padrão **registros** propriedades:

|Propriedade|ForwardOnly|Dinâmicos|Keyset|Estático|
|--------------|-----------------|-------------|------------|------------|
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|não disponível|não disponível|leitura/gravação|leitura/gravação|
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|não disponível|não disponível|leitura/gravação|leitura/gravação|
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|leitura/gravação|leitura/gravação|leitura/gravação|leitura/gravação|
|[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|somente leitura|somente leitura|somente leitura|somente leitura|
|[Indicador](../../../ado/reference/ado-api/bookmark-property-ado.md)|não disponível|não disponível|leitura/gravação|leitura/gravação|
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|leitura/gravação|leitura/gravação|leitura/gravação|leitura/gravação|
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|leitura/gravação|leitura/gravação|leitura/gravação|leitura/gravação|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|leitura/gravação|leitura/gravação|leitura/gravação|leitura/gravação|
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|somente leitura|somente leitura|somente leitura|somente leitura|
|[Filtro](../../../ado/reference/ado-api/filter-property.md)|leitura/gravação|leitura/gravação|leitura/gravação|leitura/gravação|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|leitura/gravação|leitura/gravação|leitura/gravação|leitura/gravação|
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|leitura/gravação|leitura/gravação|leitura/gravação|leitura/gravação|
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|leitura/gravação|leitura/gravação|leitura/gravação|leitura/gravação|
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|leitura/gravação|não disponível|somente leitura|somente leitura|
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|leitura/gravação|leitura/gravação|leitura/gravação|leitura/gravação|
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|leitura/gravação|não disponível|somente leitura|somente leitura|
|[Origem](../../../ado/reference/ado-api/source-property-ado-recordset.md)|leitura/gravação|leitura/gravação|leitura/gravação|leitura/gravação|
|[Estado](../../../ado/reference/ado-api/state-property-ado.md)|somente leitura|somente leitura|somente leitura|somente leitura|
|[Status](../../../ado/reference/ado-api/status-property-ado-recordset.md)|somente leitura|somente leitura|somente leitura|somente leitura|

 O [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) e [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) propriedades são somente gravação quando ADO é usado com a versão 1.0 do Microsoft OLE DB Provider para ODBC.

 Disponibilidade do ADO padrão **registros** métodos:

|Método|ForwardOnly|Dinâmicos|Keyset|Estático|
|------------|-----------------|-------------|------------|------------|
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|Sim|Sim|Sim|Sim|
|[Cancelar](../../../ado/reference/ado-api/cancel-method-ado.md)|Sim|Sim|Sim|Sim|
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|Sim|Sim|Sim|Sim|
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|Sim|Sim|Sim|Sim|
|[Clone](../../../ado/reference/ado-api/clone-method-ado.md)|não|Não|Sim|Sim|
|[Fechar](../../../ado/reference/ado-api/close-method-ado.md)|Sim|Sim|Sim|Sim|
|[Delete (excluir) (excluir)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|Sim|Sim|Sim|Sim|
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|Sim|Sim|Sim|Sim|
|[Migrar](../../../ado/reference/ado-api/move-method-ado.md)|Sim|Sim|Sim|Sim|
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Sim|Sim|Sim|Sim|
|[MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|não|Sim|Sim|Sim|
|[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Sim|Sim|Sim|Sim|
|[MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|não|Sim|Sim|Sim|
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)*|Sim|Sim|Sim|Sim|
|[Abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md)|Sim|Sim|Sim|Sim|
|[Repetir](../../../ado/reference/ado-api/requery-method.md)|Sim|Sim|Sim|Sim|
|[Ressincronização](../../../ado/reference/ado-api/resync-method.md)|não|Não|Sim|Sim|
|[Suporta](../../../ado/reference/ado-api/supports-method.md)|Sim|Sim|Sim|Sim|
|[Update (atualizar)](../../../ado/reference/ado-api/update-method.md)|Sim|Sim|Sim|Sim|
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|Sim|Sim|Sim|Sim|

 * Não há suportada para bancos de dados do Microsoft Access.

## <a name="dynamic-properties"></a>Propriedades Dinâmicas
 O provedor Microsoft OLE DB para ODBC insere várias propriedades dinâmicas no **propriedades** coleção de não o aberta [Conexão](../../../ado/reference/ado-api/connection-object-ado.md), [registros](../../../ado/reference/ado-api/recordset-object-ado.md)e [Comando](../../../ado/reference/ado-api/command-object-ado.md) objetos.

 As tabelas a seguir são um cross-index dos nomes de ADO e OLE DB para cada propriedade dinâmica. O referência do programador DB OLE refere-se a um nome de propriedade ADO, o termo "Descrição". Você pode encontrar mais informações sobre essas propriedades na referência do OLE DB do programador. Procure o nome da propriedade OLE DB no índice ou consulte [apêndice c: OLE DB Properties](http://msdn.microsoft.com/en-us/deded3ff-f508-4e1b-b2b1-fd9afd3bd292).

## <a name="connection-dynamic-properties"></a>Propriedades de Conexão dinâmica
 As propriedades a seguir são adicionadas para o **Conexão** do objeto **propriedades** coleção.

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
|Local|DBPROP_INIT_LOCATION|
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
|Serviços do OLE DB|DBPROP_INIT_OLEDBSERVICES|
|Versão do banco de dados OLE|DBPROP_PROVIDEROLEDBVER|
|Suporte do objeto OLE|DBPROP_OLEOBJECTS|
|Suporte de conjunto de linhas aberto|DBPROP_OPENROWSETSUPPORT|
|Colunas ORDER BY na lista de seleção|DBPROP_ORDERBYCOLUMNSINSELECT|
|Disponibilidade de parâmetro de saída|DBPROP_OUTPUTPARAMETERAVAILABILITY|
|Senha|DBPROP_AUTH_PASSWORD|
|Acessadores passe por referência|DBPROP_BYREFACCESSORS|
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
 As propriedades a seguir são adicionadas para o **registros** do objeto **propriedades** coleção.

|Nome da propriedade ADO|Nome de propriedade do OLE DB|
|-----------------------|--------------------------|
|Ordem de acesso|DBPROP_ACCESSORDER|
|Bloqueio de objetos de armazenamento|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Tipo de indicador|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|Alterar as linhas inseridas|DBPROP_CHANGEINSERTEDROWS|
|Privilégios de coluna|DBPROP_COLUMNRESTRICT|
|Notificação de conjunto de coluna|DBPROP_NOTIFYCOLUMNSET|
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
|IRowsetResynch||
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
|Linhas exclusivas|DBPROP_UNIQUEROWS|
|Capacidade de atualização|DBPROP_UPDATABILITY|
|Usar indicadores|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>Propriedades dinâmicas do comando
 As propriedades a seguir são adicionadas para o **comando** do objeto **propriedades** coleção.

|Nome da propriedade ADO|Nome de propriedade do OLE DB|
|-----------------------|--------------------------|
|Ordem de acesso|DBPROP_ACCESSORDER|
|Bloqueio de objetos de armazenamento|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Tipo de indicador|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|Alterar as linhas inseridas|DBPROP_CHANGEINSERTEDROWS|
|Privilégios de coluna|DBPROP_COLUMNRESTRICT|
|Notificação de conjunto de coluna|DBPROP_NOTIFYCOLUMNSET|
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
|IRowsetResynch||
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
|Ignorar excluído indicadores|DBPROP_BOOKMARKSKIP|
|Identidade de linha forte|DBPROP_STRONGIDENTITY|
|Capacidade de atualização|DBPROP_UPDATABILITY|
|Usar indicadores|DBPROP_BOOKMARKS|

 Para obter detalhes sobre a implementação específica e funcionais informações sobre o Microsoft OLE DB Provider para ODBC, consulte o [referência do programador de DB OLE](http://msdn.microsoft.com/en-us/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8) ou visite o site de acesso a dados e Storage Developer Center Web no MSDN.

## <a name="see-also"></a>Consulte também
 [Comando de objeto (ADO)](../../../ado/reference/ado-api/command-object-ado.md) [propriedade CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md) [o objeto de Conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) [propriedade ConnectionString (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [executar Método (comando ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md) [(conjunto de registros ADO) do método Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) [a coleção de parâmetros (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md) [a coleção de propriedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) [(ADO) de propriedade do provedor](../../../ado/reference/ado-api/provider-property-ado.md) [o objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [dá suporte ao método](../../../ado/reference/ado-api/supports-method.md)
