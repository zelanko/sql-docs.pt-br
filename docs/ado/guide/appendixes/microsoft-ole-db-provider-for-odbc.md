---
title: Provedor Microsoft OLE DB para ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 25db7fdb20ceb2dd24f819e1db7077d40f7e7e3f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926633"
---
# <a name="microsoft-ole-db-provider-for-odbc-overview"></a>Provedor Microsoft OLE DB para visão geral do ODBC
Para um programador do ADO ou RDS, um mundo ideal seria um no qual todos os dados fonte expõe uma interface OLE DB, para que o ADO pode chamar diretamente na fonte de dados. Embora cada vez mais fornecedores de banco de dados estiver implementando interfaces OLE DB, algumas fontes de dados não são ainda expostos dessa maneira. No entanto, a maioria dos sistemas DBMS em uso atualmente podem ser acessados por meio de ODBC.

 Drivers ODBC estão disponíveis para cada DBMS principais em uso hoje em dia, incluindo o Microsoft SQL Server, Microsoft Access (mecanismo de banco de dados Microsoft Jet) e Microsoft FoxPro, além dos produtos de banco de dados não são da Microsoft, como Oracle.

 O provedor do Microsoft ODBC, no entanto, permite que o ADO para conectar-se a qualquer fonte de dados ODBC. O provedor é de thread livre e Unicode habilitado.

 O provedor oferece suporte a transações, embora os mecanismos de DBMS diferentes oferecem diferentes tipos de suporte a transações. Por exemplo, o Microsoft Access dá suporte a transações aninhadas até cinco níveis de profundidade.

 Esse é o provedor padrão para ADO e todos os métodos e propriedades do ADO depende do provedor são suportados.

## <a name="connection-string-parameters"></a>Parâmetros de cadeia de caracteres de Conexão
 Para se conectar ao provedor, defina as **provedor =** argumento do [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propriedade para:

```
MSDASQL
```

 Lendo a [provedor](../../../ado/reference/ado-api/provider-property-ado.md) propriedade retornará essa cadeia de caracteres.

## <a name="typical-connection-string"></a>Cadeia de caracteres de Conexão típica
 Uma cadeia de caracteres de conexão típica para esse provedor é:

```
"Provider=MSDASQL;DSN=dsnName;UID=MyUserID;PWD=MyPassword;"
```

 A cadeia de caracteres consiste nessas palavras-chave:

|Palavra-chave|Descrição|
|-------------|-----------------|
|**Provedor**|Especifica o provedor OLE DB para ODBC.|
|**DSN**|Especifica o nome da fonte de dados.|
|**UID**|Especifica o nome de usuário.|
|**PWD**|Especifica a senha do usuário.|
|**URL**|Especifica a URL de um arquivo ou diretório publicado em uma pasta da Web.|

 Como esse é o provedor padrão para ADO, se você omitir a **provedor =** parâmetro da cadeia de conexão, o ADO tentará estabelecer uma conexão para esse provedor.

> [!NOTE]
>  Se você estiver se conectando a um provedor de fonte de dados que dá suporte à autenticação do Windows, você deve especificar **Trusted_Connection = yes** ou **Integrated Security = SSPI** em vez de ID de usuário e senha informações na cadeia de conexão.

 O provedor não dá suporte a parâmetros específicos de conexão, além daqueles definidos pelo ADO. No entanto, o provedor passará quaisquer parâmetros de conexão não ADO para o Gerenciador de driver ODBC.

 Porque você pode omitir as **provedor** parâmetro, portanto você pode compor uma cadeia de caracteres de conexão ADO que é idêntica de uma cadeia de caracteres de conexão ODBC para a mesma fonte de dados. Use os mesmos nomes de parâmetro (**DRIVER =** , **banco de dados =** , **DSN =** e assim por diante), valores e a sintaxe de como você faria ao compor uma cadeia de caracteres de conexão do ODBC. Você pode se conectar com ou sem um nome de fonte de dados predefinidos (DSN) ou FileDSN.

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

## <a name="remarks"></a>Comentários
 Se você usar um **DSN** ou **FileDSN**, ela deve ser definida por meio do administrador de fonte de dados do ODBC no painel de controle do Windows. No Microsoft Windows 2000, o administrador de ODBC está localizado em Ferramentas administrativas. Em versões anteriores do Windows, o ícone de administrador de ODBC é denominado **ODBC de 32 bits** ou apenas **ODBC**.

 Como uma alternativa à configuração de um **DSN**, você pode especificar o driver ODBC (**DRIVER =** ), como "SQL Server"; o nome do servidor (**SERVER =** ); e o nome do banco de dados (**Banco de dados =** ).

 Você também pode especificar um nome de conta de usuário (**UID =** ) e a senha da conta de usuário (**PWD =** ) nos parâmetros de ODBC específico ou no padrão definido pelo ADO *usuário* e *senha* parâmetros.

 Embora uma **DSN** definição já especifica um banco de dados, você pode especificar *um* *banco de dados* parâmetro além uma **DSN** para se conectar para um banco de dados diferente. É uma boa ideia sempre inclua *as* *banco de dados* parâmetro quando você usa um **DSN**. Isso garantirá que você se conectar ao banco de dados correto se outro usuário alterou o parâmetro de banco de dados padrão, uma vez que você verificou se o **DSN** definição.

## <a name="provider-specific-connection-properties"></a>Propriedades de Conexão específicas do provedor
 O provedor OLE DB para ODBC adiciona várias propriedades para o [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção da **Conexão** objeto. A tabela a seguir lista essas propriedades com o nome de propriedade do OLE DB correspondente entre parênteses.

|Nome da Propriedade|Descrição|
|-------------------|-----------------|
|Procedimentos acessíveis (KAGPROP_ACCESSIBLEPROCEDURES)|Indica se o usuário tem acesso a procedimentos armazenados.|
|Tabelas acessíveis (KAGPROP_ACCESSIBLETABLES)|Indica se o usuário tem permissão para executar instruções SELECT nas tabelas de banco de dados.|
|Instruções ativas (KAGPROP_ACTIVESTATEMENTS)|Indica o número de identificadores de que um driver ODBC pode dar suporte a uma conexão.|
|Nome do driver (KAGPROP_DRIVERNAME)|Indica o nome do arquivo do driver ODBC.|
|Versão do ODBC driver (KAGPROP_DRIVERODBCVER)|Indica a versão do ODBC que dá suporte a este driver.|
|Uso de arquivos (KAGPROP_FILEUSAGE)|Indica como o driver trata um arquivo em uma fonte de dados; como uma tabela ou como um catálogo.|
|Como a cláusula de Escape (KAGPROP_LIKEESCAPECLAUSE)|Indica se o driver dá suporte a definição e o uso de um caractere de escape para o caractere de porcentagem (%) e sublinhado (_) de caractere no predicado LIKE de uma cláusula WHERE.|
|Máximo de colunas em Group By (KAGPROP_MAXCOLUMNSINGROUPBY)|Indica o número máximo de colunas que podem ser listadas na cláusula GROUP BY de uma instrução SELECT.|
|Máximo de colunas no índice (KAGPROP_MAXCOLUMNSININDEX)|Indica o número máximo de colunas que podem ser incluídos em um índice.|
|Máximo de colunas em Order By (KAGPROP_MAXCOLUMNSINORDERBY)|Indica o número máximo de colunas que podem ser listadas na cláusula ORDER BY de uma instrução SELECT.|
|Máximo de colunas em Select (KAGPROP_MAXCOLUMNSINSELECT)|Indica o número máximo de colunas que podem ser listados na parte SELECT de uma instrução SELECT.|
|Máximo de colunas na tabela (KAGPROP_MAXCOLUMNSINTABLE)|Indica o número máximo de colunas permitido em uma tabela.|
|Funções numéricas (KAGPROP_NUMERICFUNCTIONS)|Indica quais funções numéricas são suportadas pelo driver ODBC. Para obter uma lista de nomes de função e os valores associados usados nessa máscara de bits, consulte [apêndice e: Funções escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md), na documentação do ODBC.|
|Recursos de junção externa (KAGPROP_OJCAPABILITY)|Indica os tipos de junções externas suportadas pelo provedor.|
|Junções externas (KAGPROP_OUTERJOINS)|Indica se o provedor dá suporte a junções externas.|
|Caracteres especiais (KAGPROP_SPECIALCHARACTERS)|Indica quais caracteres têm significado especial para o driver ODBC.|
|Procedimentos armazenados (KAGPROP_PROCEDURES)|Indica se os procedimentos armazenados estão disponíveis para uso com esse driver ODBC.|
|Funções de cadeia de caracteres (KAGPROP_STRINGFUNCTIONS)|Indica quais funções de cadeia de caracteres são suportadas pelo driver ODBC. Para obter uma lista de nomes de função e os valores associados usados nessa máscara de bits, consulte [apêndice e: Funções escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md), na documentação do ODBC.|
|Funções do sistema (KAGPROP_SYSTEMFUNCTIONS)|Indica quais funções de sistema são suportadas pelo driver ODBC. Para obter uma lista de nomes de função e os valores associados usados nessa máscara de bits, consulte [apêndice e: Funções escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md), na documentação do ODBC.|
|Funções de data/hora (KAGPROP_TIMEDATEFUNCTIONS)|Indica quais funções de data e hora são suportadas pelo driver ODBC. Para obter uma lista de nomes de função e os valores associados usados nessa máscara de bits, consulte [apêndice e: Funções escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md), na documentação do ODBC.|
|Suporte à gramática SQL (KAGPROP_ODBCSQLCONFORMANCE)|Indica a gramática SQL compatíveis com o driver ODBC.|

## <a name="provider-specific-recordset-and-command-properties"></a>Conjunto de registros específicos do provedor e propriedades de comando
 O provedor OLE DB para ODBC adiciona várias propriedades para o **propriedades** coleção da **conjunto de registros** e **comando** objetos. A tabela a seguir lista essas propriedades com o nome de propriedade do OLE DB correspondente entre parênteses.

|Nome da Propriedade|Descrição|
|-------------------|-----------------|
|Consulta com base em atualizações/exclusões/inserções (KAGPROP_QUERYBASEDUPDATES)|Indica se as atualizações, exclusões e inserções podem ser executadas por meio de consultas SQL.|
|Tipo de simultaneidade ODBC (KAGPROP_CONCURRENCY)|Indica o método usado para reduzir possíveis problemas causados por dois usuários tentam acessar os mesmos dados da fonte de dados simultaneamente.|
|Acessibilidade BLOB no cursor somente de avanço (KAGPROP_BLOBSONFOCURSOR)|Indica se o BLOB **campos** podem ser acessados ao usar um cursor de somente avanço.|
|Incluir SQL_FLOAT, SQL_DOUBLE e SQL_REAL em cláusulas WHERE QBU (KAGPROP_INCLUDENONEXACT)|Indica se valores SQL_FLOAT, SQL_DOUBLE e SQL_REAL podem ser incluídos em uma cláusula WHERE QBU.|
|Posição na última linha após a inserção (KAGPROP_POSITIONONNEWROW)|Indica que depois que um novo registro tiver sido inserido em uma tabela, a última linha na tabela será vêm da linha atual.|
|IRowsetChangeExtInfo (KAGPROP_IROWSETCHANGEEXTINFO)|Indica se o **IRowsetChange** interface oferece suporte de informações estendidas.|
|Tipo de Cursor ODBC (KAGPROP_CURSOR)|Indica o tipo de cursor usado pelas **conjunto de registros**.|
|Gerar um conjunto de linhas que pode ser empacotado (KAGPROP_MARSHALLABLE)|Indica que o driver ODBC gera um conjunto de registros pode ser empacotado|

## <a name="command-text"></a>Texto do comando
 Como você usa o [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto depende principalmente da fonte de dados e que tipo de instrução de consulta ou um comando que ele aceitará.

 O ODBC fornece uma sintaxe específica para chamar procedimentos armazenados. Para o [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) propriedade de uma **comando** objeto, o *CommandText* argumento para o **Execute** método em um [ Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto, ou o *fonte* argumento para o **abra** método em uma [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto, passa uma cadeia de caracteres com esta sintaxe:

```
"{ [ ? = ] call procedure [ ( ? [, ? [ , ... ]] ) ] }"
```

 Cada **?** faz referência a um objeto na [parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md) coleção. A primeira **?** as referências **parâmetros**(0), a próxima **?** as referências **parâmetros**(1), e assim por diante.

 As referências de parâmetro são opcionais e dependem da estrutura do procedimento armazenado. Se você quiser chamar um procedimento armazenado que define sem parâmetros, sua cadeia de caracteres seria a seguinte aparência:

```
"{ call procedure }"
```

 Se você tiver dois parâmetros de consulta, sua cadeia de caracteres seria semelhante ao seguinte:

```
"{ call procedure ( ?, ? ) }"
```

 Se o procedimento armazenado retornará um valor, o valor retornado será tratado como outro parâmetro. Se você tiver sem parâmetros de consulta, mas você tem um valor de retorno, sua cadeia de caracteres seria semelhante ao seguinte:

```
"{ ? = call procedure }"
```

 Por fim, se você tiver um valor de retorno e dois parâmetros de consulta, sua cadeia de caracteres seria semelhante ao seguinte:

```
"{ ? = call procedure ( ?, ? ) }"
```

## <a name="recordset-behavior"></a>Comportamento do conjunto de registros
 As tabelas seguintes listam os métodos do ADO padrão e propriedades disponíveis em um **Recordset** objeto aberto com esse provedor.

 Para obter mais informações sobre **conjunto de registros** comportamento para a sua configuração de provedor, execute o [dá suporte à](../../../ado/reference/ado-api/supports-method.md) método e enumerar os **propriedades** coleção da **Recordset** para determinar se as propriedades dinâmicas específicas do provedor estão presentes.

 Disponibilidade do ADO padrão **Recordset** propriedades:

|Propriedade|ForwardOnly|Dinâmico|Keyset|Estático|
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
|[Filtrar](../../../ado/reference/ado-api/filter-property.md)|leitura/gravação|leitura/gravação|leitura/gravação|leitura/gravação|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|leitura/gravação|leitura/gravação|leitura/gravação|leitura/gravação|
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|leitura/gravação|leitura/gravação|leitura/gravação|leitura/gravação|
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|leitura/gravação|leitura/gravação|leitura/gravação|leitura/gravação|
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|leitura/gravação|não disponível|somente leitura|somente leitura|
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|leitura/gravação|leitura/gravação|leitura/gravação|leitura/gravação|
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|leitura/gravação|não disponível|somente leitura|somente leitura|
|[Source](../../../ado/reference/ado-api/source-property-ado-recordset.md)|leitura/gravação|leitura/gravação|leitura/gravação|leitura/gravação|
|[Estado](../../../ado/reference/ado-api/state-property-ado.md)|somente leitura|somente leitura|somente leitura|somente leitura|
|[Status](../../../ado/reference/ado-api/status-property-ado-recordset.md)|somente leitura|somente leitura|somente leitura|somente leitura|

 O [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) e [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) propriedades são somente gravação ao ADO é usado com a versão 1.0 do Microsoft OLE DB Provider para ODBC.

 Disponibilidade do ADO padrão **Recordset** métodos:

|Método|ForwardOnly|Dinâmico|Keyset|Estático|
|------------|-----------------|-------------|------------|------------|
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|Sim|Sim|Sim|Sim|
|[Cancelar](../../../ado/reference/ado-api/cancel-method-ado.md)|Sim|Sim|Sim|Sim|
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|Sim|Sim|Sim|Sim|
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|Sim|Sim|Sim|Sim|
|[Clone](../../../ado/reference/ado-api/clone-method-ado.md)|Não|Não|Sim|Sim|
|[Fechar](../../../ado/reference/ado-api/close-method-ado.md)|Sim|Sim|Sim|Sim|
|[Excluir](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|Sim|Sim|Sim|Sim|
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|Sim|Sim|Sim|Sim|
|[Moverr](../../../ado/reference/ado-api/move-method-ado.md)|Sim|Sim|Sim|Sim|
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Sim|Sim|Sim|Sim|
|[MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Não|Sim|Sim|Sim|
|[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Sim|Sim|Sim|Sim|
|[MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Não|Sim|Sim|Sim|
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)*|Sim|Sim|Sim|Sim|
|[Abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md)|Sim|Sim|Sim|Sim|
|[Requery](../../../ado/reference/ado-api/requery-method.md)|Sim|Sim|Sim|Sim|
|[Resync](../../../ado/reference/ado-api/resync-method.md)|Não|Não|Sim|Sim|
|[Suporta](../../../ado/reference/ado-api/supports-method.md)|Sim|Sim|Sim|Sim|
|[Update (atualizar)](../../../ado/reference/ado-api/update-method.md)|Sim|Sim|Sim|Sim|
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|Sim|Sim|Sim|Sim|

 \* Não há suportada para bancos de dados do Microsoft Access.

## <a name="dynamic-properties"></a>Propriedades Dinâmicas
 O Microsoft OLE DB Provider for ODBC insere várias propriedades dinâmicas para o **propriedades** coleção da não abertos [Conexão](../../../ado/reference/ado-api/connection-object-ado.md), [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md)e [Comando](../../../ado/reference/ado-api/command-object-ado.md) objetos.

 As tabelas a seguir são um cross-index dos nomes de ADO e OLE DB para cada propriedade dinâmica. O referência do programador DB OLE se refere a um nome de propriedade ADO usando o termo, "Description". Você pode encontrar mais informações sobre essas propriedades na referência do OLE DB do programador. Pesquise o nome da propriedade do OLE DB no índice ou consulte [apêndice c: Propriedades OLE DB](https://msdn.microsoft.com/deded3ff-f508-4e1b-b2b1-fd9afd3bd292).

## <a name="connection-dynamic-properties"></a>Propriedades dinâmicas da Conexão
 As propriedades a seguir são adicionadas para o **Conexão** do objeto **propriedades** coleção.

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
|Location|DBPROP_INIT_LOCATION|
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
|Serviços do OLE DB|DBPROP_INIT_OLEDBSERVICES|
|Versão do OLE DB|DBPROP_PROVIDEROLEDBVER|
|Suporte do objeto OLE|DBPROP_OLEOBJECTS|
|Suporte de conjunto de linhas aberto|DBPROP_OPENROWSETSUPPORT|
|Colunas ORDER BY na lista de seleção|DBPROP_ORDERBYCOLUMNSINSELECT|
|Disponibilidade do parâmetro de saída|DBPROP_OUTPUTPARAMETERAVAILABILITY|
|Senha|DBPROP_AUTH_PASSWORD|
|Acessadores passe por referência|DBPROP_BYREFACCESSORS|
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
 As propriedades a seguir são adicionadas para o **conjunto de registros** do objeto **propriedades** coleção.

|Nome da propriedade ADO|Nome da propriedade do OLE DB|
|-----------------------|--------------------------|
|Ordem de acesso|DBPROP_ACCESSORDER|
|Bloquear objetos de armazenamento|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Tipo de indicador|DBPROP_BOOKMARKTYPE|
|Possíveis de indicação|DBPROP_IROWSETLOCATE|
|Modificar linhas inseridas|DBPROP_CHANGEINSERTEDROWS|
|Privilégios de coluna|DBPROP_COLUMNRESTRICT|
|Notificação de conjunto de coluna|DBPROP_NOTIFYCOLUMNSET|
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
|IRowsetResynch||
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
|Linhas exclusivas|DBPROP_UNIQUEROWS|
|Capacidade de atualização|DBPROP_UPDATABILITY|
|Usar indicadores|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>Propriedades dinâmicas do comando
 As propriedades a seguir são adicionadas para o **comando** do objeto **propriedades** coleção.

|Nome da propriedade ADO|Nome da propriedade do OLE DB|
|-----------------------|--------------------------|
|Ordem de acesso|DBPROP_ACCESSORDER|
|Bloquear objetos de armazenamento|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Tipo de indicador|DBPROP_BOOKMARKTYPE|
|Possíveis de indicação|DBPROP_IROWSETLOCATE|
|Modificar linhas inseridas|DBPROP_CHANGEINSERTEDROWS|
|Privilégios de coluna|DBPROP_COLUMNRESTRICT|
|Notificação de conjunto de coluna|DBPROP_NOTIFYCOLUMNSET|
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
|IRowsetResynch||
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
|Ignorar marcadores apagados|DBPROP_BOOKMARKSKIP|
|Identidade de linha forte|DBPROP_STRONGIDENTITY|
|Capacidade de atualização|DBPROP_UPDATABILITY|
|Usar indicadores|DBPROP_BOOKMARKS|

 Para obter detalhes sobre a implementação específica e funcionais informações sobre o Microsoft OLE DB Provider para ODBC, consulte a [referência do programador DB OLE](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8) ou visite o site de acesso a dados e da Web do armazenamento Developer Center no MSDN.

## <a name="see-also"></a>Consulte também
 [Comando (ADO) do objeto](../../../ado/reference/ado-api/command-object-ado.md) [propriedade CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md) [o objeto de Conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) [propriedade ConnectionString (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [executar Método (comando ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md) [(conjunto de registros ADO) do método Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) [coleção Parameters (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md) [coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) [Propriedade provider (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [dá suporte ao método](../../../ado/reference/ado-api/supports-method.md)
