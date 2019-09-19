---
title: Criar um provedor de servidor vinculado (Mecanismo de Banco de Dados do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/01/2019
ms.prod: sql
ms.technology: ''
ms.prod_service: database-engine
ms.reviewer: MikeRayMSFT
ms.topic: conceptual
author: pmasl
ms.author: pelopes
manager: rothj
ms.openlocfilehash: 166b55c70cc9b7d1337128b12b78a8ec1f4a1032
ms.sourcegitcommit: 77293fb1f303ccfd236db9c9041d2fb2f64bce42
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70929649"
---
# <a name="microsoft-sql-server-distributed-queries-ole-db-connectivity"></a>Consultas distribuídas do Microsoft SQL Server: Conectividade do OLE DB

Este artigo descreve como o processador de consultas do Microsoft SQL Server interage com um provedor OLE DB para habilitar consultas distribuídas e heterogêneas. Ele se destina principalmente a desenvolvedores do provedor OLE DB e pressupõe uma compreensão sólida da especificação OLE DB. A ênfase está na interface OLE DB entre o processador de consultas do SQL Server e o provedor OLE DB, não na funcionalidade de consulta distribuída em si. Para obter uma descrição completa da funcionalidade de consulta distribuída, confira [Servidores vinculados](../../relational-databases/linked-servers/linked-servers-database-engine.md).

## <a name="overview-and-terminology"></a>Visão geral e terminologia

 No Microsoft SQL Server, as consultas distribuídas permitem que os usuários do SQL Server acessem dados fora de um servidor baseado no SQL Server, seja em outros servidores que executam o SQL Server ou outras fontes de dados que expõem uma interface OLE DB. O OLE DB fornece uma maneira de acessar uniformemente os dados de tabela de fontes de dados heterogêneos.

Uma consulta distribuída, para fins deste artigo, é qualquer instrução `SELECT`, `INSERT`, `UPDATE` ou `DELETE` que referencie tabelas e conjuntos de linhas de uma ou mais fontes de dados OLE DB externas.

Uma tabela remota é uma tabela que é armazenada em uma fonte de dados OLE DB e é externa ao servidor que executa o SQL Server que realiza a consulta. Uma consulta distribuída acessa uma ou mais tabelas remotas.

### <a name="ole-db-provider-categories"></a>Categorias do provedor OLE DB

Veja a seguir uma categorização dos provedores OLE DB com base em suas funcionalidades do ponto de vista da consulta distribuída do SQL Server. Conforme definido, elas não são mutuamente exclusivas; determinado provedor pode pertencer a mais de uma das seguintes categorias:

- Provedores de comando SQL

- Provedores de índice

- Provedores de tabela simples

- Provedores de comando não SQL

#### <a name="sql-command-providers"></a>Provedores de comando SQL

Os provedores que dão suporte ao objeto `Command` com um dialeto padrão SQL reconhecido pelo SQL Server pertencem a essa categoria. Os requisitos específicos para que determinado provedor OLE DB seja tratado como um provedor de comando SQL pelo SQL Server são:

- O provedor precisa dar suporte ao objeto `Command` e a todas as suas interfaces OLE DB obrigatórias: `ICommand`, `ICommandText`, `IColumnsInfo`, `ICommandProperties` e `IAccessor`.

- O dialeto SQL com suporte do provedor precisa ser, pelo menos, Submínimo SQL. O dialeto precisa ser relatado pelo provedor por meio da propriedade `DBPROP_SQLSUPPORT`.

Exemplos de provedores de comando SQL são o Provedor Microsoft OLE DB para SQL Server e o Provedor Microsoft OLE DB para ODBC.

#### <a name="index-providers"></a>Provedores de índice

Os provedores de índice são aqueles que dão suporte a índices e os expõem de acordo com o OLE DB e permitem a pesquisa baseada em índice de tabelas base. Os requisitos específicos para que determinado provedor OLE DB seja tratado como um provedor de índice pelo SQL Server são:

- O provedor precisa dar suporte à interface `IDBSchemaRowset` com os conjuntos de linhas de esquema TABLES, COLUMNS e INDEXES.

- O provedor precisa dar suporte à abertura de um conjunto de linhas em um índice por meio de `IOpenRowset` especificando o nome do índice e o nome da tabela base correspondente.

- O objeto `Index` precisa dar suporte a todas as suas interfaces obrigatórias: `IRowset`, `IRowsetIndex`, `IAccessor`, `IColumnsInfo`, `IRowsetInfo` e `IConvertTypes`.

- Os conjuntos de linhas abertos na tabela base indexada (por meio de `IOpenRowset`) precisam dar suporte à interface `IRowsetLocate` para posicionamento em uma linha com base em um indicador.

Se o provedor OLE DB atender aos requisitos acima, os usuários poderão definir a opção de provedor `Index As Access Path` para permitir que o SQL Server use os índices do provedor para avaliar consultas. Por padrão, o SQL Server não tenta usar os índices do provedor, a menos que essa opção esteja definida.

>[!NOTE]
>O SQL Server dá suporte a várias opções que influenciam como o SQL Server acessa um provedor OLE DB. A caixa de diálogo `Linked Server Properties` do SQL Server Enterprise Manager pode ser usada para definir essas opções.

#### <a name="simple-table-providers"></a>Provedores de tabela simples

Esses são provedores que expõem a abertura de um conjunto de linhas em uma tabela base por meio da interface `IOpenRowset`. Esses provedores não são provedores de comando SQL nem provedores de índice; em vez disso, são a classe mais simples de provedores com os quais as consultas distribuídas do SQL Server podem trabalhar.

Nesses provedores, o SQL Server só pode executar verificações de tabela durante a avaliação da consulta distribuída.

#### <a name="non-sql-command-providers"></a>Provedores de comando não SQL

Os provedores que dão suporte ao objeto `Command` e a suas interfaces obrigatórias, mas que não dão suporte a um dialeto padrão SQL reconhecido pelo SQL Server, se enquadram nessa categoria.

Dois exemplos de provedores de comando não SQL são o Provedor Microsoft OLE DB para serviço de indexação e o [Provedor OLE DB da Microsoft para o serviço Microsoft Active Directory](../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md).

### <a name="transact-sql-subset"></a>Subconjunto Transact-SQL

Haverá suporte para cada uma das classes de instruções Transact-SQL a seguir em consultas distribuídas se o provedor der suporte às interfaces OLE DB necessárias.

- Todas as instruções `SELECT` são permitidas, exceto instruções `SELECT` INTO com uma tabela remota como a tabela de destino.

- As instruções `INSERT` são permitidas em tabelas remotas se o provedor dá suporte às interfaces necessárias para inserção. Para obter mais informações sobre os requisitos do OLE DB para INSERT, confira \"Instrução INSERT\" mais adiante neste artigo.

- As instruções `UPDATE` e DELETE serão permitidas em tabelas remotas se o provedor atender aos requisitos da interface OLE DB na tabela especificada. Para os requisitos da interface OLE DB e as condições sob as quais uma tabela remota pode ser atualizada ou excluída, confira \"Instruções UPDATE e DELETE\" mais adiante neste artigo.

### <a name="cursor-support"></a>Suporte para cursor

Haverá suporte para cursores de instantâneo e conjunto de chaves em consultas distribuídas se o provedor der suporte à funcionalidade OLE DB necessária. Não há suporte para cursores dinâmicos em consultas distribuídas. É feito o downgrade para um cursor de conjunto de chaves de uma solicitação de usuário de um cursor dinâmico em uma consulta distribuída.

Os cursores de instantâneo são populados durante a abertura do cursor e o conjunto de resultados permanece inalterado; as atualizações, as inserções e as exclusões nas tabelas subjacentes não são refletidas no cursor.

Os cursores de conjunto de chaves são populados durante a abertura do cursor e o conjunto de resultados permanece inalterado durante todo o tempo de vida do cursor. No entanto, as atualizações e as exclusões em tabelas subjacentes são visíveis no cursor conforme as linhas são visitadas. As inserções em tabelas subjacentes que podem afetar a associação de cursor não estão visíveis.

Uma tabela remota poderá ser atualizada ou excluída por meio de um cursor que é definido em uma consulta distribuída e referencia a tabela remota se o provedor atender às condições de atualizações e exclusões na tabela remota, por exemplo, a tabela `UPDATE` \| DELETE `<remote-table>` `WHERE` CURRENT OF `<cursor-name>`. Para obter mais informações, confira \"Instruções UPDATE e DELETE\" mais adiante neste artigo.

#### <a name="keyset-cursor-support-requirements"></a>Requisitos de suporte para cursor de conjunto de chaves

Haverá suporte para um cursor de conjunto de chaves em uma consulta distribuída se todos os requisitos da sintaxe Transact-SQL forem atendidos e um dos seguintes existir:

- O provedor OLE DB dá suporte a indicadores reutilizáveis em todas as tabelas remotas na consulta. Os indicadores reutilizáveis podem ser consumidos de um conjunto de linhas em determinada tabela e usados em um conjunto de linhas diferente da mesma tabela. O suporte para indicadores reutilizáveis é indicado por meio do conjunto de linhas de esquema TABLES_INFO de `IDBSchemaRowset` pela definição da coluna BOOKMARK_DURABILITY como BMK_DURABILITY_INTRANSACTION ou com uma durabilidade mais alta.

- Todas as tabelas remotas expõem uma chave exclusiva por meio do conjunto de linhas INDEXES da interface `IDBSchemaRowset`. Deve haver uma entrada de índice com a coluna UNIQUE definida como VARIANT_TRUE.

Não há suporte para cursores de conjunto de chaves em consultas distribuídas que envolvem a função *OpenQuery*.

#### <a name="updatable-keyset-cursor-requirements"></a>Requisitos de cursor de conjunto de chaves atualizável

Uma tabela remota pode ser atualizada ou excluída por meio de um cursor de conjunto de chaves definido em uma consulta distribuída, por exemplo, `UPDATE` \| DELETE `<remote-table>` `WHERE` CURRENT OF `<cursor-name>`. Estas são as condições sob as quais são permitidos cursores atualizáveis em consultas distribuídas:

- Os cursores atualizáveis são permitidos se o provedor também atende às condições de atualizações e exclusões na tabela remota. Para obter mais informações, confira \"Instruções UPDATE e DELETE\" mais adiante neste artigo.

- Todas as operações atualizáveis do cursor de conjunto de chaves precisam estar em uma transação definida pelo usuário com um nível de isolamento de leitura repetida ou um nível de isolamento mais alto. Além disso, o provedor precisa dar suporte a transações distribuídas com a interface `ITransactionJoin`.

## <a name="ole-db-provider-interaction-phases"></a>Fases de interação do provedor OLE DB

 Seis operações são comuns a todos os cenários de execução de consulta distribuída:

- As operações de estabelecimento da conexão e recuperação de propriedade indicam como o SQL Server se conecta a um provedor OLE DB e quais propriedades do provedor são usadas.

- A resolução de nomes de tabela e as operações de recuperação de metadados indicam como o SQL Server resolve o nome da tabela remota (que é especificada de uma das duas maneiras: um nome baseado em servidor vinculado ou um nome ad hoc) para o objeto de dados apropriado no provedor. Isso também inclui os metadados de tabela que o SQL Server recupera do provedor para compilar e otimizar uma consulta distribuída.

- As operações de gerenciamento de transações especificam toda a interação relacionada à transação com o provedor OLE DB.

- As operações de tratamento de tipo de dados indicam como os tipos de dados OLE DB são tratados pelo SQL Server quando ele consome dados de um provedor OLE DB ou exporta dados para ele durante o processamento de uma consulta distribuída.

- As operações de tratamento de erro indicam como o SQL Server usa as informações de erro estendido do provedor.

- As operações de segurança especificam como a segurança do SQL Server interage com a segurança do provedor.

### <a name="connection-establishment-and-property-retrieval"></a>Estabelecimento de conexão e recuperação de propriedade

O SQL Server dá suporte a duas convenções de nomenclatura de objeto de dados remoto: nomes de quatro partes baseados no servidor vinculado e nomes ad hoc que usam a função `OPENROWSET`.

#### <a name="linked-server-based-names"></a>Nomes baseados no servidor vinculado

Um servidor vinculado serve como uma abstração para uma fonte de dados OLE DB. Um nome baseado no servidor vinculado é um nome de quatro partes do formato `<linked-server>.<catalog>`. `<schema>.<object>`, em que `<linked-server>` é o nome do servidor vinculado. O SQL Server interpreta `<linked-server>` para derivar o provedor OLE DB e os atributos de conexão que identificam a fonte de dados para o provedor. As outras três partes do nome são interpretadas pela fonte de dados OLE DB para identificar a tabela remota específica. :::

#### <a name="ad-hoc-names"></a>Nomes ad hoc

Um nome ad hoc é um nome baseado na função `OPENROWSET` ou `OPENDATASOURCE`. Ele inclui todas as informações de conexão (ou seja, o provedor OLE DB a ser usado, os atributos necessários para identificar a fonte de dados, a ID de usuário e a senha) sempre que a tabela remota é referenciada em uma consulta distribuída.

O uso de nomes ad hoc não é permitido por padrão, exceto pelos membros da função sysadmin. Para usar nomes ad hoc em um provedor OLE DB, a opção `DisallowAdhocAccess` do provedor deve ser definida como `0`.

Se um nome de servidor vinculado for usado, o SQL Server extrairá da definição de servidor vinculado o nome do provedor OLE DB e as propriedades de inicialização para o provedor. Se um nome ad hoc for usado, o SQL Server extrairá as mesmas informações dos argumentos da função `OPENROWSET`.

Para obter instruções detalhadas sobre como configurar um servidor vinculado usando um nome de quatro partes e uma sintaxe baseada no nome ad hoc, confira [Criar servidores vinculados](create-linked-servers-sql-server-database-engine.md).

### <a name="connecting-to-an-ole-db-provider"></a>Como se conectar a um provedor OLE DB

Estas são as etapas de alto nível executadas pelo SQL Server ao se conectar a um provedor OLE DB:

1. O SQL Server cria um objeto de fonte de dados.

   O SQL Server usa a `ProgID` do provedor para criar uma instância de seu DSO (objeto de fonte de dados). A ProgID é especificada como o parâmetro `provider_name` de uma configuração de servidor vinculado ou como o primeiro argumento da função `OPENROWSET` no caso de um nome ad hoc.

   O SQL Server cria uma instância do DSO do provedor por meio da interface `IDataInitialize` do componente de serviço OLE DB. Isso permite que o Gerenciador de Componente de Serviço agregue seus serviços, como suporte à atualização e rolagem, acima da funcionalidade nativa do provedor. Além disso, a criação de uma instância do provedor por meio do `IDataInitialize` permite que o componente de serviço OLE DB agrupe conexões com o provedor, reduzindo uma parte da sobrecarga de conexão e inicialização.

   Um provedor especificado pode ser configurado para ter uma instância criada no mesmo processo do SQL Server ou em seu próprio processo. A criação de uma instância em um processo separado protege o processo do SQL Server contra falhas no provedor. Ao mesmo tempo, há uma sobrecarga de desempenho associada ao marshaling das chamadas do OLE DB fora do processo do SQL Server. Um provedor pode ser configurado para ter uma instância criada em processo ou fora do processo pela definição da opção `Allow In Process` do provedor. Para obter mais informações, confira [Como definir as opções do provedor](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md).

   Para saber mais sobre os componentes de serviço do OLE DB e o pooling de sessões, confira a documentação do OLE DB para obter os requisitos do provedor.

2. A fonte de dados é inicializada.

   Depois que o DSO for criado, a interface `IDBProperties` definirá a propriedade de inicialização DBPROP_INIT_TIMEOUT se a opção `remote login timeout` de configuração do servidor for maior que 0; essa é uma propriedade necessária.

   Essas propriedades serão definidas se forem especificadas ou implícitas na definição de servidor vinculado ou no segundo argumento da função `OPENROWSET`:

   - `DBPROP_INIT_PROVIDERSTRING`

   - `DBPROP_INIT_DATASOURCE`

   - `DBPROP_INIT_LOCATION`

   - `DBPROP_INIT_CATALOG`

   - `DBPROP_AUTH_USERID`

   - `DBPROP_AUTH_PASSWORD`

   Depois que essas propriedades forem definidas, `IDBInitialize::Initialize` será chamado para inicializar o DSO com as propriedades especificadas.

3. O SQL Server coleta informações específicas do provedor.

   O SQL Server coleta várias propriedades do provedor a serem usadas na avaliação de consulta distribuída; essas propriedades são recuperadas com uma chamada a `IDBProperties::GetProperties`. Todas essas propriedades são opcionais; no entanto, o suporte a todas as propriedades relevantes permite que o SQL Server aproveite ao máximo as funcionalidades do provedor. Por exemplo, `DBPROP_SQLSUPPORT` é necessário para determinar se o SQL Server pode enviar consultas ao provedor. Se não houver suporte para essa propriedade, o SQL Server não usará o provedor remoto como um provedor de comando SQL, mesmo se ele for um. Na tabela a seguir, a coluna Valor padrão indica qual valor será pressuposto pelo SQL Server se o provedor não der suporte à propriedade.

Propriedade| Valor padrão| Use |
|:----|:----|:----|
|`DBPROP_DBMSNAME`|None|Usado para mensagens de erro.|
|`DBPROP_DBMSVER` |None|Usado para mensagens de erro.|
|`DBPROP_PROVIDERNAME`|None|Usado para mensagens de erro.|
|`DBPROP_PROVIDEROLEDBVER1`|1.5|Usado para determinar a disponibilidade dos recursos do 2.0.
|`DBPROP_CONCATNULLBEHAVIOR`|None|Usado para determinar se o comportamento da concatenação de `NULL` do provedor é o mesmo que o do SQL Server.|
|`DBPROP_NULLCOLLATION`|None|Permite a classificação/o uso do índice somente se `NULLCOLLATION` corresponde ao comportamento de ordenação de nulo da Instância do SQL Server.|
|`DBPROP_OLEOBJECTS`|None|Determina se o provedor dá suporte a interfaces de armazenamento estruturado para colunas de objeto de dados grandes.|
|`DBPROP_STRUCTUREDSTORAGE`|None|Determina quais interfaces de armazenamento estruturado são compatíveis com tipos de objeto grande (entre `ILockBytes`, `Istream` e `ISequentialStream`).|
|`DBPROP_MULTIPLESTORAGEOBJECTS`|Falso|Determina se mais de uma coluna de objeto grande pode ser aberta ao mesmo tempo.|
|`DBPROP_SQLSUPPORT`|None|Determina se as consultas SQL podem ser enviadas ao provedor.|
|`DBPROP_CATALOGLOCATION`|`DBPROPVAL_CL_START`|Usado para construir nomes de tabela com várias partes.
|`SQLPROP_DYNAMICSQL`|Falso|Propriedade específica do SQL Server: se ela retornar `VARIANT_TRUE`, indicará que os marcadores de parâmetro `?` são compatíveis com a execução de consulta parametrizada.
|`SQLPROP_NESTEDQUERIES`|Falso|Propriedade específica do SQL Server: se ela retornar `VARIANT_TRUE`, indicará que o provedor dá suporte a instruções `SELECT` aninhadas na cláusula `FROM`.
|`SQLPROP_GROUPBY`|Falso|Propriedade específica do SQL Server: se ela retornar `VARIANT_TRUE`, indicará que o provedor dá suporte à cláusula GROUP BY na instrução `SELECT`, conforme especificado pelo padrão SQL-92.
|`SQLPROP_DATELITERALS `|Falso|Propriedade específica do SQL Server: se ela retornar `VARIANT_TRUE`, indicará que o provedor dá suporte a literais de datetime de acordo com a sintaxe Transact-SQL do SQL Server.
|`SQLPROP_ANSILIKE `|Falso|Propriedade específica do SQL Server: Essa propriedade é de interesse de um provedor que dá suporte ao nível Mínimo SQL e dá suporte ao operador `LIKE` de acordo com o nível Entrada da SQL-92 (\'%\' e \'_\' como caracteres curinga).
|`SQLPROP_SUBQUERIES `|Falso|Propriedade do SQL Server: Essa propriedade é de interesse de um provedor que dá suporte ao nível Mínimo SQL. Essa propriedade indica que o provedor dá suporte a subconsultas, conforme especificado pelo nível Entrada da SQL-92. Isso inclui as subconsultas na lista `SELECT` e na cláusula `WHERE` com suporte para subconsultas correlacionadas e os operadores `IN`, `EXISTS`, `ALL` e `ANY`.
|`SQLPROP_INNERJOIN`|Falso|Propriedade específica do SQL Server: Essa propriedade é de interesse para provedores que dão suporte ao nível Mínimo SQL. Essa propriedade indica suporte para junções usando várias tabelas na cláusula `FROM`. ------ ---

Os três seguintes literais são recuperados de `IDBInfo::GetLiteralInfo`: `DBLITERAL_CATALOG_SEPARATOR`, `DBLITERAL_SCHEMA_SEPARATOR` (para construir um nome de objeto completo, considerando suas partes de nome de objeto, catálogo e esquema) e `DBLITERAL_QUOTE` (para citar nomes de identificadores em uma consulta SQL enviada ao provedor).

Se o provedor não der suporte aos literais de separadores, o SQL Server usará um ponto final (.) como o caractere separador padrão. Se o provedor der suporte apenas ao caractere separador de catálogo, mas não ao caractere separador de esquema, o SQL Server usará o caractere separador de catálogo como o caractere separador de esquema também. Se o provedor não der suporte ao `DBLITERAL_QUOTE`, o SQL Server usará aspas simples (`'`) como o caractere de aspas.

>[!NOTE]
>Se os literais de separadores de nome do provedor não corresponderem a esses valores padrão, o provedor precisará expô-los por meio de `IDBInfo`, de modo que o SQL Server acesse suas tabelas por meio de nomes de quatro partes. Se esses literais não forem expostos, somente consultas passagem poderão ser usadas nesse provedor.

Para obter informações sobre como expor as propriedades `SQLPROP_DYNAMICSQL` e `SQLPROP_NESTEDQUERIES`, confira [Propriedades específicas do SQL Server](#appendixc).

### <a name="table-name-resolution-and-meta-data-retrieval"></a>Resolução de nomes de tabela e recuperação de metadados

O SQL Server resolve um nome de tabela remota especificado em uma consulta distribuída para uma tabela ou uma exibição específica em uma fonte de dados OLE DB. Ambos os esquemas de nomenclatura ad hoc e de servidor vinculado resultam em um nome de três partes a ser interpretado pelo provedor. No caso do nome baseado no servidor vinculado, as últimas três partes do nome de quatro partes formam os nomes de catálogo, esquema e objeto. No caso do nome ad hoc, o terceiro argumento da função `OPENROWSET` especifica um nome de três partes que descreve os nomes de catálogo, esquema e objeto. Um ou ambos os nomes de catálogo e esquema podem estar vazios. (Um nome de quatro partes com um nome de catálogo vazio e um nome de esquema será semelhante a `<server-name>...<object-name>`.) Nesse caso, o SQL Server usa `NULL` como o valor correspondente a ser procurado nas tabelas de conjunto de linhas de esquema.

As regras de resolução de nomes e as etapas de recuperação de metadados empregadas pelo SQL Server dependem se o provedor dá suporte à interface `IDBSchemaRowset` no objeto `Session`.

Se houver suporte para `IDBSchemaRowset`, os conjuntos de linhas de esquema `TABLES`, `COLUMNS`, `INDEXES` e `TABLES_INFO` serão usados da interface `IDBSchemaRowset`. (O conjunto de linhas de esquema `TABLES_INFO` é definido no OLE DB 2.0.) O SQL Server restringe os conjuntos de linhas de esquema retornados pela interface `IDBSchemaRowset` para procurar as colunas de esquema que correspondem às partes de nome da tabela remota especificadas. Estas são as regras relacionadas às restrições compatíveis com o provedor nos conjuntos de linhas de esquema e como o SQL Server as utiliza para recuperar os metadados de uma tabela remota:

- As restrições nas colunas `TABLE_NAME` e `COLUMN_NAME` são sempre necessárias.

- Se o provedor der suporte a uma restrição `TABLE_CATALOG` (ou `TABLE_SCHEMA`), o SQL Server usará essa restrição em `TABLE_CATALOG` (ou `TABLE_SCHEMA`). Se o nome do catálogo (ou esquema) não for especificado no nome da tabela remota, um valor `NULL` será usado como o valor de restrição correspondente. Se um nome de catálogo (ou esquema) for especificado, o provedor precisará dar suporte à restrição correspondente em `TABLE_CATALOG` (ou `TABLE_SCHEMA`).

- O provedor precisa dar suporte à restrição na coluna `TABLE_SCHEMA` em `TABLES` e `COLUMNS` ou dar suporte a eles em nenhuma delas. O provedor precisa dar suporte à restrição de nome de catálogo nos conjuntos de linhas `TABLES` ou `COLUMNS` ou dar suporte a eles em nenhum deles.

- Se houver suporte para restrições em INDEXES, o provedor precisará dar suporte à restrição de esquema em conjuntos de linhas `TABLES` e INDEXES ou dar suporte a eles em nenhuma delas. O provedor precisa dar suporte à restrição de nome de catálogo em `XES or support them on neither. The provider must either support catalog name restriction on both `TABLES` and `INDEXES` ou dar suporte a eles em nenhuma delas.

No conjunto de linhas de esquema `TABLES`, o SQL Server recupera as colunas `TABLE_CATALOG`, `TABLE_SCHEMA`, `TABLE_NAME`, `TABLE_TYPE` e `TABLE_GUID` definindo as restrições de acordo com as regras acima.

No conjunto de linhas de esquema `COLUMNS`, o SQL Server recupera as colunas `TABLE_CATALOG`, `TABLE_SCHEMA`, `TABLE_NAME`, `COLUMN_NAME`, `COLUMN_GUID`, `ORDINAL_POSITION`, `COLUMN_FLAGS`, `IS_NULLABLE`, `DATA_TYPE`, `TYPE_GUID`, `CHARACTER_MAXIMUM_LENGTH`, `NUMERIC_PRECISION` e `NUMERIC_SCALE`. `COLUMN_NAME`, `DATA_TYPE` e `ORDINAL_POSITION` precisam retornar valores não nulos válidos. Se `DATA_TYPE` for `DBTYPE_NUMERIC` ou `DBTYPE_DECIMAL`, o `NUMERIC_PRECISION` e `NUMERIC_SCALE` correspondentes precisarão ser valores não nulos válidos.

No conjunto de linhas de esquema `INDEXES` opcional, o SQL Server procura índices na tabela remota especificada definindo as restrições de acordo com as regras anteriores. Nas entradas de índice correspondentes assim encontradas, o SQL Server recupera as colunas `TABLE_CATALOG`, `TABLE_SCHEMA`, `TABLE_NAME`, `INDEX_CATALOG`, `INDEX_SCHEMA`, `INDEX_NAME`, `PRIMARY_KEY`, `UNIQUE`, `CLUSTERED`, `FILL_FACTOR`, `ORDINAL_POSITION`, `COLUMN_NAME`, `COLLATION`, `CARDINALITY` e `PAGES`.

No conjunto de linhas `TABLES_INFO` opcional, o SQL Server procura informações adicionais na tabela remota especificada, como suporte a indicadores, o tipo e o tamanho do indicador. Todas as colunas, exceto a coluna `DESCRIPTION` do conjunto de linhas `TABLES_INFO`, são usadas. As informações do conjunto de linhas `TABLES_INFO` são usadas da seguinte maneira:

- A coluna `BOOKMARK_DURABILITY` é usada para implementar cursores de conjunto de chaves mais eficientes. Se essa coluna tiver um valor igual a `BMK_DURABILITY_INTRANSACTION` ou um valor de durabilidade mais alto, o SQL Server usará a recuperação baseada em indicador e as atualizações de linhas da tabela remota para implementar um cursor de conjunto de chaves.

- As colunas `BOOKMARK_TYPE`, `BOOKMARK_DATA TYPE` e `BOOKMARK_MAXIMUM_LENGTH` são usadas para determinar metadados de indicadores durante a compilação da consulta. Se não houver suporte para essas colunas, o SQL Server abrirá o conjunto de linhas da tabela base por meio de `IOpenRowset` durante a compilação para obter as informações de indicador.

Se não houver suporte para `IDBSchemaRowset` e o nome da tabela remota incluir um nome de catálogo ou de esquema, o SQL Server exigirá `IDBSchemaRowset` e retornará um erro. No entanto, se o nome de catálogo nem o nome de esquema forem fornecidos, o SQL Server abrirá o conjunto de linhas que corresponde à tabela remota e recuperará os metadados de coluna da interface `IColumnsInfo` obrigatória do objeto de conjunto de linhas.

O SQL Server abre o conjunto de linhas correspondente à tabela chamando `IOpenRowset::OpenRowset`. O nome da tabela fornecido para `OPENROWSET` é construído com base nas partes do nome de objeto, catálogo e esquema.

- Cada uma das partes do nome (`catalog`, `schema` e `object name`) é colocada entre aspas com o caractere de aspas do provedor (`DBLITERAL_QUOTE`) e, em seguida, concatenada com o caractere `DBLITERAL_CATALOG_SEPARATOR` e o caractere `DBLITERAL_SCHEMA_SEPARATOR` inserido entre eles. A construção de nome segue as regras do OLE DB em `IOpenRowset`.

- Os metadados de coluna para a tabela são recuperados por meio de `IColumnsInfo::GetColumnInfo` depois que o objeto de conjunto de linhas é aberto.

Se não houver suporte para `IDBSchemaRowset` com os conjuntos de linhas TABLES, COLUMNS e TABLES_INFO, o SQL Server abrirá o conjunto de linhas na tabela base duas vezes: uma vez durante a compilação da consulta para recuperar metadados e outra durante a execução da consulta. Os provedores que geram efeitos colaterais por abrir o conjunto de linhas (por exemplo, executar um código que altera o estado de um dispositivo em tempo real, enviar emails, executar um código arbitrário fornecido pelo usuário) precisam estar cientes desse comportamento.

### <a name="statistics-retrieval"></a>Recuperação de estatísticas

Se o provedor der suporte a estatísticas de distribuição nas tabelas base, o SQL Server usará essas estatísticas. Há dois tipos de estatísticas de interesse para o processador de consultas do SQL Server:

- **Cardinalidades de coluna (ou tupla)** . Esse é o número de valores exclusivos que estão em uma coluna (ou uma combinação de colunas) de uma tabela. Isso pode ser usado para estimar a seletividade dos predicados em relação às colunas. Um provedor que dá suporte a estatísticas de distribuição deve dar suporte a, pelo menos, um tipo de cardinalidade.

- **Histogramas**. Se a distribuição de valores não for uniforme, o número de valores exclusivos não será suficiente para estimar precisamente a seletividade dos predicados. Nesse caso, um histograma pode ser fornecido, que gera informações mais refinadas sobre a distribuição de valores de coluna em uma tabela.

A disponibilidade de estatísticas permite que o otimizador de consulta do SQL Server estime melhor as cardinalidades de operações intermediárias em uma consulta, o que possibilita gerar planos de execução melhores para elas.

O provedor OLE DB deve dar suporte a estatísticas de distribuição da seguinte maneira:

- **Obrigatório**. Dá suporte às propriedades (1) `DBPROP_TABLESTATISTICS` que indicam se há suporte para as cardinalidades de coluna ou tupla e se há suporte para histogramas e (2) `DBPROP_OPENROWSETSUPPORT` que indicam o uso do bit `DBPROPVAL_ORS_HISTOGRAM`, caso haja suporte para histogramas.

- **Obrigatório**. O conjunto de linhas de esquema `TABLE_STATISTICS`. O conjunto de linhas de esquema `TABLE_STATISTICS` lista as estatísticas disponíveis em determinado banco de dados. Ele também inclui as cardinalidades de coluna e tupla no próprio conjunto de linhas de esquema e indica se há suporte para histogramas nas colunas específicas. Para que o SQL Server use estatísticas, as colunas `TABLE_NAME`, `STATISTICS_NAME`, `STATISTICS_TYPE`, `COLUMN_NAME` e `ORDINAL_POSITION` são obrigatórias nesse conjunto de linhas de esquema. Pelo menos um `COLUMN_CARDINALITY` ou `TUPLE_CARDINALITY` é obrigatório. Se houver suporte para histogramas, `NO_OF_RANGES` também será obrigatório.

- **Opcional**. Opcionalmente, se o provedor der suporte a histogramas, ele deverá dar suporte a uma melhoria para o método `IOpenRowset::OpenRowset`, que permite abrir um conjunto de linhas de histograma especificando o `DBID` da estatística correspondente.

Para obter informações completas sobre as interfaces de estatísticas, confira a especificação OLE DB 2.6.

### <a name="constraints"></a>Restrições

O otimizador de consulta do SQL Server também usa as restrições `CHECK` definidas nas tabelas base em uma fonte de dados remota se o provedor OLE DB dá suporte ao conjunto de linhas de esquema `CHECK_CONSTRAINTS_BY_TABLE` do OLE DB 2.6. A coluna `CHECK_CLAUSE` do conjunto de linhas de esquema deve retornar o predicado de cláusula `CHECK` na sintaxe em conformidade com a SQL-92. O otimizador de consulta usa informações de restrição para eliminar ou simplificar predicados que são sempre falsos ou sempre verdadeiros devido à presença de uma restrição de verificação na tabela.

### <a name="transaction-management"></a>Gerenciamento de transações

O SQL Server dá suporte ao acesso baseado em transação a dados distribuídos usando as interfaces OLE DB `ITransactionLocal` (para transação local) e `ITransactionJoin` (para transações distribuídas) do provedor. Ao iniciar uma transação local no provedor, o SQL Server garante operações de gravação atômicas. Ao usar transações distribuídas, o SQL Server garante que uma transação que envolva vários nós tenha o mesmo resultado (confirmação ou anulação) em todos os nós. Se o provedor não der suporte às interfaces OLE DB relacionadas à transação obrigatórias, as operações de atualização nesse provedor não serão permitidas, dependendo do contexto de transação local.

A tabela a seguir descreve o que acontece quando o usuário executa uma consulta distribuída, considerando as funcionalidades do provedor e um contexto de transação local. Uma operação de leitura em um provedor refere-se a uma instrução `SELECT` ou quando a tabela remota é lida no lado de entrada de uma instrução `SELECT INTO`, `INSERT`, `UPDATE` ou `DELETE`. Uma operação de gravação em um provedor refere-se a uma instrução `INSERT`, `UPDATE` ou `DELETE` com uma tabela remota como a tabela de destino.

Os resultados de uma consulta distribuída com base nas funcionalidades do provedor e no contexto da transação:

|A consulta distribuída ocorre|O provedor não dá suporte a `ITransactionLocal`|O provedor dá suporte a `ITransactionLocal`, mas não a `ITransactionJoin`|O provedor dá suporte a `ITransactionLocal` e `ITransactionJoin`|
|:-----|:-----|:-----|:-----|
| Em uma transação por si só (sem transação de usuário).|Por padrão, somente operações de leitura são permitidas. Quando a opção `Nontransacted Updates` do nível de provedor está habilitada, as operações de gravação são permitidas. (Quando essa opção está habilitada, o SQL Server não pode garantir a atomicidade e a consistência nos dados do provedor. Isso pode fazer com que os efeitos parciais de uma operação de gravação sejam refletidos na fonte de dados remota sem a capacidade de desfazê-los.)| Todas as instruções são permitidas em dados remotos. Os cursores de conjunto de chaves são somente leitura. A transação local é iniciada no provedor com o nível de isolamento da sessão atual do SQL Server e é confirmada no final de uma avaliação de instrução bem-sucedida. (O nível de isolamento padrão para uma sessão do SQL Server é `READ COMMITTED`, a menos que ele seja modificado com a instrução `SET TRANSACTION ISOLATION LEVEL`. O provedor precisa dar suporte ao nível de isolamento solicitado.) | Todas as instruções são permitidas. Os cursores de conjunto de chaves são somente leitura. A transação local é iniciada no provedor com o nível de isolamento da sessão atual do SQL Server e é confirmada no final de uma avaliação de instrução bem-sucedida. |
| Em uma transação de usuário (ou seja, entre `BEGIN TRAN` ou `BEGIN DISTRIBUTED TRAN` e `COMMIT`). | Se o nível de isolamento da transação for `READ COMMITTED` (o padrão) ou abaixo, as operações de leitura serão permitidas. Se o nível de isolamento for maior, nenhuma consulta distribuída será permitida. | Somente operações de leitura são permitidas. Novas transações distribuídas são iniciadas no provedor com o nível de isolamento da sessão atual do SQL Server. |Todas as instruções são permitidas. A nova transação distribuída é iniciada no provedor com o nível de isolamento da sessão atual do SQL Server e confirmada quando a transação de usuário é confirmada. Para instruções de modificação de dados, por padrão, o SQL Server inicia uma transação aninhada abaixo da transação distribuída, para que a instrução de modificação de dados possa ser interrompida em determinadas condições de erro sem interromper a transação adjacente. Se a opção `XACT_ABORT SET` estiver ativada, o SQL Server não exigirá suporte a transações aninhadas e interromperá a transação adjacente no caso de erros durante a instrução de modificação de dados. |
|  |  |  |

### <a name="data-type-handling-in-distributed-queries"></a>Tratamento de tipo de dados em consultas distribuídas

Os provedores OLE DB expõem seus dados em termos dos tipos de dados definidos pelo OLE DB (indicado por `DBTYPE` no OLE DB). O SQL Server processa dados externos dentro do servidor como tipos nativos do SQL Server; isso resulta em um mapeamento de tipos de dados OLE DB para tipos nativos do SQL Server e vice-versa, pois os dados são consumidos pelo SQL Server ou exportados pelo SQL Server, respectivamente. Esse mapeamento é feito implicitamente, salvo indicação em contrário.

Os tipos de dados em consultas distribuídas são tratados usando um dos dois métodos de mapeamento:

- O mapeamento do lado de consumo mapeia tipos dos tipos de dados OLE DB para os tipos de dados nativos do SQL Server no lado de consumo, quando as tabelas remotas aparecem em instruções `SELECT` e no lado de entrada das instruções INSERT, UPDATE e DELETE.

- O mapeamento do lado da exportação mapeia os tipos dos tipos de dados do SQL Server para tipos de dados OLE DB no lado da exportação, quando uma tabela remota aparece como a tabela de destino de uma instrução `INSERT` ou `UPDATE`.

Tabela de mapeamento de tipo de dados do SQL Server e OLE DB.

| Tipo OLE DB | `DBCOLUMNFLAG` | Tipo de dados do SQL Server |
|-----|-----|-----|
|`DBTYPE_I1`*| |`numeric(3, 0)`|
|`DBTYPE_I2`| |`smallint`|
|`DBTYPE_I4`| |`int`|
|`DBTYPE_I8`| |`numeric(19,0)`|
|`DBTYPE_UI1`| |`tinyint`|
|`DBTYPE_UI2`*| |`numeric(5,0)`|
|`DBTYPE_UI4`*| |`numeric(10,0)`|
|`DBTYPE_UI8`*| |`numeric(20,0)`|
|`DBTYPE_R4`| |`float`|
|`DBTYPE_R8`| |`real`|
|`DBTYPE_NUMERIC`| |`numeric`|
|`DBTYPE_DECIMAL`| |`decimal`|
|`DBTYPE_CY`| |`money`|
|`DBTYPE_BSTR`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=true`<br>ou em<br> Tamanho máx. > 4.000 caracteres|ntext|
|`DBTYPE_BSTR`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=true`|NCHAR|
|`DBTYPE_BSTR`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=false`|NVARCHAR|
|`DBTYPE_IDISPATCH`| |Erro|
|`DBTYPE_ERROR`| |Erro|
|`DBTYPE_BOOL`| |`bit`|
|`DBTYPE_VARIANT`*| |NVARCHAR|
|`DBTYPE_IUNKNOWN`| |Erro|
|`DBTYPE_GUID`| |`uniqueidentifier`|
|`DBTYPE_BYTES`|`DBCOLUMNFLAGS_ISLONG=true` <br>ou em<br> Tamanho máx. > 8.000|`image`|
|`DBTYPE_BYTES`|`DBCOLUMNFLAGS_ISROWVER=true`, `DBCOLUMNFLAGS_ISFIXEDLENGTH=true`, tamanho da coluna = 8 <br>ou em<br> Tamanho máx. não relatado. | `timestamp` |
|`DBTYPE_BYTES`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=true` | `binary` |
|`DBTYPE_BYTES`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=true` | `varbinary`|
|`DBTYPE_STR`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=true` | `char`|
|`DBTYPE_STR`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=true` | `varchar` |
|`DBTYPE_STR`| `DBCOLUMNFLAGS_ISLONG=true` <br>ou em<br> Tamanho máx. > 8.000 caracteres <br>ou em<br>   Tamanho máx. não relatado. | `text`|
|`DBTYPE_WSTR`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=true` |`nchar`|
|`DBTYPE_WSTR` | `DBCOLUMNFLAGS_ISFIXEDLENGTH=false`|`nvarchar`|
|`DBTYPE_WSTR`| `DBCOLUMNFLAGS_ISLONG=true` <br>ou em<br> Tamanho máx. > 4.000 caracteres <br>ou em<br>   Tamanho máx. não relatado. | `ntext`|
|`DBTYPE_UDT`| |Erro|
|`DBTYPE_DATE`* | | `datetime` |
|`DBTYPE_DBDATE` | | `datetime` (conversão explícita necessária)|
|`DBTYPE_DBTIME`| | `datetime` (conversão explícita necessária)|
|`DBTYPE_DBTIMESTAMP`* | | `datetime`|
|`DBTYPE_ARRAY` | |Erro|
|`DBTYPE_BYREF` | | Ignored |
|`DBTYPE_VECTOR` | |Erro|
|`DBTYPE_RESERVED`| |Erro|

\* Indique alguma forma de conversão para a representação do tipo do SQL Server, pois não há nenhum tipo de dados equivalente exato no SQL Server. Essas conversões podem resultar em perda de precisão, estouro ou estouro negativo. Os mapeamentos implícitos padrão poderão ser alterados no futuro se houver suporte para os tipos de dados correspondentes em versões futuras do SQL Server.

>[!NOTE]
>`numeric(p,s)` indica o tipo de dados `numeric` do SQL Server com precisão `p` e escala `s`. A precisão máxima permitida para `DBTYPE_NUMERIC` e `DBTYPE_DECIMAL` é 38. O provedor precisa dar suporte à associação à coluna `DBTYPE_BSTR` como `DBTYPE_WSTR` durante a criação de um acessador. As colunas `DBTYPE_VARIANT` são consumidas como cadeias de caracteres Unicode `nvarchar`. Isso exige suporte para conversão de `DBTYPE_VARIANT` para `DBTYPE_WSTR` do provedor. O provedor deve implementar essa conversão conforme definido no OLE DB. Para obter mais informações, confira [Tipos de dados da especificação OLE DB](#appendixa).

#### <a name="interpreting-data-type-mapping"></a>Como interpretar o mapeamento de tipo de dados

O mapeamento para um tipo do SQL Server é determinado pelo tipo de dados OLE DB e pelos valores DBCOLUMNFLAGS que descrevem a coluna ou o valor escalar. No caso do conjunto de linhas de esquema `COLUMNS`, as colunas `DATA_TYPE` e `COLUMN_FLAGS` representam esses valores. No caso da interface `IColumnsInfo::GetColumnInfo`, os membros `wType` e `dwFlags` da estrutura `DBCOLUMNINFO` representam essas informações.

Para usar o mapeamento do lado de consumo para determinada coluna com um valor `DBTYPE` e `DBCOLUMNFLAG` específico, procure o tipo do SQL Server correspondente na tabela. As regras de tipo para colunas de tabelas remotas em expressões podem ser descritas pela seguinte regra simples:

>Um valor especificado de coluna remota é válido em uma expressão Transact-SQL se o tipo do SQL Server mapeado correspondente na tabela é válido no mesmo contexto.

A tabela e a regra definem:

- Comparações e expressões.

Em geral, `X <op> <remote-column>` é uma expressão válida se `<op>` é um operador válido no tipo de dados de `X` e no tipo de dados para o qual `<remote-column>` é mapeado.

- Conversões explícitas.

`Convert(X, <remote-column>)` é permitido se o `DBTYPE` de `<remote-column>` é mapeado para o tipo de dados nativo `Y` (conforme a tabela acima) e a conversão explícita de `Y` para `X` é permitida.

Se os usuários desejarem que os dados remotos sejam convertidos em um tipo de dados nativo não padrão, eles precisarão usar uma conversão explícita.

Para usar o mapeamento do lado de exportação no caso de instruções `UPDATE` e `INSERT` em tabelas remotas, mapeie os tipos de dados nativos do SQL Server para tipos de dados OLE DB usando a mesma tabela. Um mapeamento de um tipo `S1` do SQL Server para determinado tipo OLE DB `T` será permitido se um dos seguintes existir:

- O mapeamento correspondente pode ser encontrado na tabela de mapeamento diretamente.

- Há uma conversão implícita permitida de `S1` para outro tipo `S2` do SQL Server, de forma que `S2` seja mapeado para o tipo `T` na tabela de mapeamento.

#### <a name="large-object-lob-handling"></a>Tratamento de LOB (Objeto Grande)

Conforme indicado na tabela de mapeamento, se as colunas do tipo `DBTYPE_STR`, `DBTYPE_WSTR` ou `DBTYPE_BSTR` também relatarem `DBCOLUMNFLAGS_ISLONG`, ou se o tamanho máximo exceder 4.000 caracteres (ou se nenhum tamanho máximo for relatado), o SQL Server os tratará como uma coluna `text` ou `ntext`, conforme apropriado. Da mesma forma, para colunas `DBTYPE_BYTES`, se `DBCOLUMNFLAGS_ISLONG` for definido ou se o tamanho máximo for superior a 8.000 bytes (ou se o tamanho máximo não for relatado), as colunas `image` serão tratadas como colunas. As colunas `Text`, `ntext` e `image` são chamadas de colunas LOB.

O SQL Server não expõe a funcionalidade completa de texto e imagem em LOBs de um provedor OLE DB. Não há suporte para `TEXTPTRS` em objetos grandes de um provedor OLE DB; portanto, não há suporte para nenhuma das funcionalidades relacionadas, por exemplo, a função do sistema `TEXTPTR` e as instruções `READTEXT`, `WRITETEXT` e `UPDATETEXT`. Há suporte para instruções `SELECT` que recuperam colunas LOBs inteiras, assim como para instruções `UPDATE` e `INSERT` para colunas inteiras de objeto grande em tabelas remotas.

O SQL Server usará as interfaces de armazenamento estruturado em colunas LOB se o provedor der suporte a elas. As interfaces de armazenamento estruturado em ordem crescente de preferência e as funcionalidades são as seguintes: `ISequentialStream`, `Istream` ou `ILockBytes`. Se houver suporte para uma ou mais dessas interfaces, o provedor precisará retornar DBPROPVAL_OO_BLOB como o valor da propriedade `DBPROP_OLEOBJECTS` quando ela for consultada por meio da interface `IDBProperties`. Além disso, o provedor deve indicar suporte para as interfaces às quais ele dá suporte na propriedade `DBPROP_STRUCTUREDSTORAGE`.

Se o provedor não der suporte a nenhuma das interfaces de armazenamento estruturado em colunas LOB, o SQL Server materializará essa interface por conta própria e ainda as exporá como colunas `text`, `ntext` ou `image`.

#### <a name="accessing-lob-columns"></a>Como acessar colunas LOB

Se o provedor der suporte a uma das interfaces de armazenamento estruturado, o SQL Server executará as seguintes etapas para recuperar colunas LOB durante a execução da consulta:

1. Antes de abrir o conjunto de linhas por meio de `IOpenRowset::OpenRowset`, o SQL Server solicitará suporte para uma ou mais das interfaces de armazenamento estruturado (`ISequentialStream`, `Istream` e `ILockBytes`) nas colunas de objeto grande. A primeira interface compatível com o provedor é necessária; interfaces adicionais são solicitadas como \"set if cheap\" pela definição do elemento *dwOptions* da estrutura DBPROP correspondente como DBPROPOPTIONS_SETIFCHEAP. Por exemplo, se um provedor der suporte a `ISequentialStream` e `ILockBytes`, `ISequentialStream` será obrigatório e `ILockBytes` será solicitado como \"set if cheap\".

4. Depois que o conjunto de linhas é aberto, o SQL Server usa `IRowsetInfo::GetProperties` para identificar as interfaces reais disponíveis no conjunto de linhas. A última interface ou a interface mais preferencial que o provedor retornou é usada. Quando o SQL Server cria um acessador em uma coluna de objeto grande, a coluna é associada como DBTYPE_IUNKNOWN ao elemento *iid* da estrutura DBOBJECT na associação definida como a interface.

#### <a name="reading-from-lob-columns"></a>Como fazer a leitura de colunas LOB

Use o ponteiro de interface para a interface de armazenamento estruturado solicitada retornada no buffer de linha de `IRowset::GetData` para fazer a leitura da coluna de objeto grande. Se o provedor não der suporte a vários LOBs abertos ao mesmo tempo (ou seja, se ele não der suporte a `DBPROP_MULTIPLE_STORAGEOBJECTS`) e se a linha tiver várias colunas de objeto grande, o SQL Server copiará as colunas LOB para uma tabela de trabalho local.

#### <a name="update-and-insert-statements-on-lob-columns"></a>Instruções `UPDATE` e `INSERT` em colunas LOB

O SQL Server passa para o provedor um ponteiro para um novo objeto de armazenamento, em vez de usar a interface fornecida pelo provedor para modificar o objeto de armazenamento. Para cada coluna LOB, o valor que é atualizado ou inserido em um objeto de armazenamento é criado com a interface de armazenamento estruturado escolhida. Dependendo se ela é uma operação `UPDATE` ou `INSERT`, um ponteiro para o objeto de armazenamento é passado para o provedor por meio de `IRowsetChange::SetData` ou `IRowsetChange::InsertRow`, respectivamente.

### <a name="error-handling"></a>Tratamento de erros

Quando uma invocação de método específica em um provedor OLE DB retorna um código de erro, o SQL Server procura as informações de erro estendido do provedor antes de retornar informações sobre a condição de erro para o usuário.

O SQL Server usa o objeto de erro do OLE DB, conforme especificado pelo OLE DB. Algumas das etapas de alto nível são:

1. Quando uma invocação de método retorna um código de erro do provedor, o SQL Server procura a interface `ISupportErrorInfo`. Se houver suporte para essa interface, o SQL Server chamará `ISupportErrorInfo::InterfaceSupportsErrorInfo` para verificar se há suporte para os objetos de erro pela interface que produziu o código de erro.

<!-- -->

5. Se houver suporte para objetos de erro na interface, o SQL Server chamará a função `GetErrorInfo` para obter um ponteiro de interface `IErrorInfo` no objeto de erro atual.

6. O SQL Server usa a interface `IErrorInfo` para obter um ponteiro para a interface `IErrorRecords`.

7. O SQL Server usa `IErrorRecords` para executar um loop em todos os registros de erro no objeto e obter o texto da mensagem de erro correspondente a cada registro.

Para obter mais informações sobre como o objeto de erro do provedor é usado, confira a documentação do OLE DB.

### <a name="security"></a>Segurança

Quando um consumidor se conecta a um provedor OLE DB, o provedor geralmente exige uma ID de usuário e uma senha, a menos que o consumidor deseje ser autenticado como um usuário de segurança integrada. No caso de consultas distribuídas, o SQL Server funciona como o consumidor do provedor OLE DB em nome do logon do SQL Server que executa a consulta distribuída. O SQL Server mapeia o logon atual do SQL Server para uma ID de usuário e uma senha no servidor vinculado.

Esses mapeamentos podem ser especificados pelo usuário para determinado servidor vinculado e podem ser configurados e gerenciados pelos procedimentos armazenados do sistema `sp_addlinkedsrvlogin` e `sp_droplinkedsrvlogin`. Ao definir as propriedades do grupo de inicialização DBPROP_AUTH_USERID e DBPROP_AUTH_PASSWORD por meio de `IDBProperties::SetProperties`, a ID de usuário e a senha determinados pelo mapeamento são passados para o provedor durante o estabelecimento da conexão.

Quando um cliente se conectar ao SQL Server por meio da Autenticação do Windows e se o logon tiver uma configuração de mapeamento `self` usando `sp_addlinkedsrvlogin`, o SQL Server tentará representar o contexto de segurança do cliente e definirá a propriedade `DBPROP_AUTH_INTEGRATED` no provedor durante o estabelecimento da conexão. Esse processo é chamado de *delegação*.

Depois que o contexto de segurança usado para a conexão for determinado, a autenticação desse contexto de segurança e a verificação de permissão para esse contexto em relação aos objetos de dados na fonte de dados ficam inteiramente sob a responsabilidade do provedor OLE DB.

Para obter mais informações, confira [`sp_addlinkedsrvlogin`](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) e [`sp_droplinkedsrvlogin`](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md).

## <a name="query-execution-scenarios"></a>Cenários de execução de consulta

 Ao avaliar uma consulta distribuída, o SQL Server interage com o provedor OLE DB em um ou mais destes cenários:

- Consulta remota

- Acesso indexado

- Verificações de tabela pura

- Instruções `UPDATE` e DELETE

- Instrução `INSERT`

- Consultas passagem

### <a name="remote-query"></a>Remote Query

O SQL Server gera uma consulta SQL que avalia uma parte da consulta original, que pode ser avaliada em sua totalidade pelo provedor. Esse cenário só é possível em provedores de comando SQL. A extensão para a qual o SQL Server envia as operações por push ao provedor pela geração de uma consulta SQL depende da gramática SQL à qual o provedor dá suporte. O provedor deve indicar seu nível de suporte ao SQL por meio do seguinte:

1. Indicando o suporte de nível Entrada da SQL-92, Núcleo ODBC ou SQL Mínimo por meio da propriedade `DBPROP_SQLSUPPORT`. O nível de sintaxe SQL Mínimo é um novo nível compatível com o SQL Server que permite ao SQL Server enviar consultas remotas para provedores simples que dão suporte a um subconjunto simples do SQL. Esse nível abrange uma instrução básica `SELECT` que não inclui subconsultas, várias tabelas na cláusula `FROM` (portanto, sem junções) e GROUP BY. Para que o subconjunto da gramática SQL que é usado pelo SQL Server gere consultas remotas nos provedores de cada um desses níveis de sintaxe, confira [Subconjunto SQL usado para gerar consultas remotas](#appendixb).

1. Dando suporte a várias propriedades específicas do SQL Server para indicar o suporte a recursos individuais do SQL que não são incluídos de outra forma no nível de sintaxe, conforme relatado pelo DBPROP_SQLSUPPORT. A lista de propriedades e como elas são usadas pelo SQL Server é descrito mais adiante nesta seção.

O SQL Server usa a execução de consulta parametrizada com um ponto de interrogação (?) como o marcador de parâmetro na cadeia de caracteres Transact-SQL. A execução de consulta parametrizada é usada nos provedores OLE DB do SQL Server, do Microsoft Jet e do Oracle. Em outros provedores, a execução de consulta parametrizada será usada se o provedor der suporte a `ICommandWithParameters` no objeto `Command` e, pelo menos, uma das seguintes condições for atendida:

- O provedor indica o nível de suporte Núcleo ODBC do SQL Server por meio da propriedade `DBPROP_SQLSUPPORT`.

- O provedor indica suporte para o marcador de parâmetro de ponto de interrogação (?) ao dar suporte à propriedade específica do SQL Server SQLPROP_DYNCMICSQL por meio de `IDBPProperties`. Para obter mais informações, confira a próxima seção sobre propriedades do provedor.

- O administrador define a opção `Dynamic Parameters` do provedor no provedor para fazer com que o SQL Server gere consultas parametrizadas.

Quando o SQL Server gera o texto SQL a ser executado remotamente, os nomes de tabela e coluna são colocados entre aspas com o caractere de aspas do provedor, conforme relatado por meio do literal `DBLITERAL_QUOTE` da interface `IDBInfo`. Se não houver suporte para esse literal, os nomes de tabela e coluna não serão colocados entre aspas.

Se o provedor der suporte à execução de consulta parametrizada, o SQL Server considerará uma estratégia de execução de consulta parametrizada avaliar uma junção de uma tabela remota com uma tabela local. A consulta parametrizada é executada repetidamente para valores de parâmetro gerados de cada linha da tabela local. Essa estratégia reduz o número de linhas recuperadas do provedor e é benéfico quando uma tabela local com um número pequeno de linhas é unida a uma tabela remota com um número grande de linhas. Essa estratégia de junção remota pode ser imposta pela dica do otimizador de junção `REMOTE`. Para obter mais informações sobre a execução de consulta parametrizada, confira [Como: Executar consultas parametrizadas](../../connect/php/how-to-perform-parameterized-queries.md).

Veja a seguir as etapas de nível superior no provedor no cenário de consulta remota.

1. O SQL Server cria um objeto `Command` com base no objeto `Session` usando `IDBCreateCommand::CreateCommand`.

9. Se a opção de configuração de servidor `Remote Query Timeout` for definida com um valor > 0, o SQL Server definirá a propriedade `DBPROP_COMMANDTIMEOUT` no objeto `Command` com o mesmo valor usando `ICommandProperties::SetProperties`. `ICommand::SetCommandText` deve ser chamado para definir o texto de comando para a cadeia de caracteres Transact-SQL gerada.

10. O SQL Server chama `ICommandPrepare::Prepare` para preparar o comando. Se o provedor não der suporte a essa interface, o SQL Server continuará com a etapa 4.

11. Se a consulta gerada for parametrizada, o SQL Server usará `ICommandWithParameters::SetParameterInfo` para descrever os parâmetros e `IAccessor::CreateAccessor` para criar acessadores para os parâmetros.

12. O SQL Server chama `ICommand::Execute` para executar o comando e criar o conjunto de linhas.

13. O SQL Server usa a interface `IRowset` para navegar pelas linhas da tabela e consumi-las. Use `IRowset::GetNextRows` para efetuar fetch de linhas, `IRowset::RestartPosition` para reposicionar o início do conjunto de linhas e `IRowset::ReleaseRows` para liberar linhas.

#### <a name="provider-properties-of-interest-for-remote-query-execution"></a>Propriedades do provedor de interesse para execução de consulta remota

Se o provedor der suporte a recursos do SQL que não são cobertos pelo nível de sintaxe relatado em DBPROP_SQLSUPPORT, ele poderá indicá-los usando várias propriedades específicas do provedor.

- SQLPROP_GROUPBY. Essa propriedade é de interesse de um provedor que dá suporte ao nível Mínimo SQL. Essa propriedade indica que o provedor dá suporte às cláusulas GROUP BY e HAVING na instrução `SELECT`. Além disso, essa propriedade indica que o provedor dá suporte às cinco seguintes funções de agregação: MIN, MAX, SUM, COUNT e AVG. O provedor pode não dar suporte a DISTINCT no argumento dessas funções de agregação.

- SQLPROP_SUBQUERIES. Essa propriedade é de interesse de um provedor que dá suporte ao nível Mínimo SQL. Ela indica que o provedor dá suporte a subconsultas, conforme especificado pelo nível Entrada da SQL-92. Isso inclui as subconsultas na lista `SELECT` e na cláusula `WHERE` com suporte para subconsultas correlacionadas e os operadores `IN`, `EXISTS`, `ALL` e `ANY`.

- SQLPROP_DATELITERALS. Essa propriedade é de interesse de qualquer provedor (incluindo aqueles que dão suporte ao nível Entrada da SQL-92). O suporte para a sintaxe literal padrão para literais datetime não faz parte do nível Entrada da SQL-92. Essa propriedade específica do SQL Server indica que o provedor dá suporte à sintaxe literal datetime, conforme especificado pelo padrão SQL-92.

- SQLPROP_ANSILIKE. De interesse de um provedor que dá suporte ao nível Mínimo SQL. Essa propriedade indica que o provedor dá suporte ao operador `LIKE` de acordo com o nível Entrada da SQL-92 (\'%\' e \'_\' como caracteres curinga). Isso será útil em um provedor que dê suporte ao nível Mínimo SQL, porque o nível Mínimo SQL não inclui o suporte a `LIKE`.

- SQLPROP_INNERJOIN. Essa propriedade é de interesse para provedores que dão suporte ao nível Mínimo SQL. Ela indica suporte para várias tabelas na cláusula `FROM`. Isso será útil em um provedor que dê suporte apenas ao nível Mínimo SQL, porque o nível Mínimo SQL não inclui o suporte a junções. Isso não indica suporte a palavras-chave JOIN explícitas e não indica suporte a junções externas. Ele indica suporte apenas a junções implícitas por meio de uma lista de tabelas na cláusula `FROM`.

- SQLPROP_DYNAMICSQL. Indica suporte para `?` como um marcador de parâmetro. O marcador de parâmetro deve ter suporte no lugar de um item escalar em uma cláusula `WHERE` ou na lista `SELECT`. O suporte para `?` marcadores de parâmetro permite que o SQL Server envie consultas parametrizadas ao provedor.

- SQLPROP_NESTEDQUERIES. Indica suporte para instruções SELECT aninhadas na cláusula `FROM` (por exemplo, `SELECT * FROM (SELECT * FROM T))`. Em muitos casos, o SQL Server usa instruções `SELECT` aninhadas na cláusula `FROM` de uma consulta quando ele gera as cadeias de consulta a serem executadas remotamente. Como o suporte a `SELECT` aninhado não é exigido pelo nível Entrada da SQL-92, o SQL Server não delega consultas com instruções `SELECT` aninhadas ao provedor, a menos que o provedor também defina essa propriedade. Como alternativa, o administrador também pode definir a opção `Nested Queries` do provedor para o provedor, a fim de fazer com que o SQL Server gere consultas aninhadas no provedor.

O provedor pode dar suporte a essas propriedades usando um conjunto de propriedades específico do SQL Server chamado `SQLPROPSET_OPTHINTS` e ter valores `PROPID` definidos. O conjunto de propriedades `SQLPROPSET_OPTHINTS` e as duas propriedades são definidos usando as seguintes constantes:

```
extern const GUID `SQLPROPSET_OPTHINTS` = { 0x2344480c, 0x33a7, 0x11d1, { 0x9b, 0x1a, 0x0, 0x60, 0x8, 0x26, 0x8b, 0x9e } };
enum SQLPROPERTIES {
SQLPROP_NESTEDQUERIES = 0x4,
SQLPROP_DYNAMICSQL = 0x5,
SQLPROP_GROUPBY = 0x6,
SQLPROP_DATELITERALS = 0x7,
SQLPROP_ANSILIKE = 0x8,
SQLPROP_INNERJOIN = 0x9,
SQLPROP_SUBQUERIES = 0x10
};
```

#### <a name="character-set-and-sort-order-implications"></a>Implicações da ordem de classificação e do conjunto de caracteres

O SQL Server dá suporte à especificação de uma ordenação para dados de caractere em um nível por coluna. A ordenação inclui o conjunto de caracteres e a especificação da ordem de classificação para dados de caractere não Unicode (colunas `char` e `varchar`). Para dados Unicode (colunas `nchar` e `nvarchar`), a ordenação especifica apenas a ordem de classificação.

O SQL Server delegará comparações de cadeia de caracteres ao provedor somente se o conjunto de caracteres (para dados não Unicode), a ordem de classificação e a semântica de comparação de cadeia de caracteres usados pelo servidor vinculado forem os mesmos usados pelo servidor local.

No caso de servidores vinculados do SQL Server, o SQL Server determina automaticamente a compatibilidade da ordenação. Para outros provedores, o administrador precisa indicar ao SQL Server a ordenação de dados de caractere de determinado servidor vinculado. No SQL Server, há suporte para uma nova opção de servidor vinculado chamada `Collation Name`. Se o administrador determinar que a semântica de ordenação adotada pelo servidor vinculado é a mesma que uma das ordenações padrão do SQL Server, ele poderá definir a opção `Collation Name` com esse nome de ordenação. A opção `Collation Name` pode ser definida usando o procedimento armazenado do sistema `sp_serveroption`. Essa opção só deverá ser definida se ambas as condições a seguir forem atendidas:

- A ordem de classificação remota e o conjunto de caracteres são os mesmos que a ordenação do SQL Server especificada.

- A semântica de comparação de cadeia de caracteres usada pelo provedor OLE DB segue as especificações do padrão SQL-92 ou, de maneira equivalente, a semântica de comparação do SQL Server.

Ainda há suporte para a opção Compatível com Ordenação no SQL Server 7.0, por motivos de compatibilidade com versões anteriores. Configurá-la como verdadeiro é equivalente a definir a opção Nome da Ordenação como a ordenação padrão do banco de dados mestre do SQL Server. Os novos aplicativos devem usar a opção Nome da Ordenação em vez da opção Compatível com Ordenação.

### <a name="indexed-access"></a>Acesso indexado

O SQL Server usa um índice exposto pelo provedor para avaliar determinados predicados da consulta distribuída. Esse cenário só é possível em provedores de índice e quando o usuário define a opção de provedor `Index as Access Path`. Estas são as principais etapas de alto nível executadas pelo SQL Server no provedor ao usar um índice para executar uma consulta:

1. Abre o conjunto de linhas de índice por meio de `IOpenRowset::OpenRowset` com os nomes completos da tabela e do índice. Os nomes completos de tabela e do índice são gerados conforme descrito anteriormente no cenário de consulta remota.

1. Abre o conjunto de linhas da tabela base por meio de `IOpenRowset::OpenRowset` com o nome completo da tabela.

1. Define intervalos no conjunto de linhas do índice com base no predicado de consulta por meio de `IRowsetIndex::SetRange`.

1. Examina as linhas no conjunto de linhas do índice por meio de `IRowset` no conjunto de linhas do índice.

1. Usa a coluna de indicadores das linhas de índice recuperadas para efetuar fetch de linhas correspondentes no conjunto de linhas da tabela base por meio de `IRowsetLocate::GetRowsByBookmark`.

As propriedades do conjunto de linhas `DBPROP_IRowsetLocate` e `DBPROP_BOOKMARKS` são necessárias no conjunto de linhas aberto na tabela base.

### <a name="pure-table-scans"></a>Verificações de tabela pura

O SQL Server examina toda a tabela remota do provedor e executa toda a avaliação de consulta localmente. O conjunto de linhas correspondente à tabela é aberto pela chamada a `IOpenRowset::OpenRowset`. O SQL Server constrói o nome da tabela fornecido para `OPENROWSET` com base nas partes do nome de objeto, catálogo e esquema da seguinte maneira:

1. Cada uma das partes do nome é colocada entre aspas com o caractere de aspas do provedor (`DBLITERAL_QUOTE`) e, em seguida, concatenada com o caractere `DBLITERAL_CATALOG_SEPARATOR` inserido entre eles.

1. Depois que o objeto de conjunto de linhas é aberto `IColumnsInfo`, o SQL Server usa a interface para verificar se os metadados de tempo de execução são os mesmos que os metadados de tempo de compilação para a tabela.

1. O SQL Server usa a interface `IRowset` para navegar pelas linhas da tabela e consumi-las. Use `IRowset::GetNextRows` para efetuar fetch de linhas, `IRowset::RestartPosition` para reposicionar o início do conjunto de linhas e `IRowset::ReleaseRows` para liberar linhas.

### <a name="update-and-delete-statements"></a>Instruções `UPDATE` e `DELETE`

As seguintes condições precisam ser atendidas para que uma tabela remota seja atualizada ou excluída de uma consulta distribuída do SQL Server:

- O provedor precisa dar suporte a indicadores no conjunto de linhas aberto por meio de `IOpenRowset` na tabela que está sendo atualizada ou excluída.

- O provedor precisa dar suporte às interfaces `IRowsetLocate` e `IRowsetChange` no conjunto de linhas aberto por meio de `IOpenRowset` na tabela que está sendo atualizada ou excluída.

- A interface `IRowsetChange` precisa dar suporte aos métodos UPDATE (`SetData`) e DELETE (`DeleteRows`).

- Se o provedor não der suporte a `ITransactionLocal`, as instruções `UPDATE` e `DELETE` serão permitidas somente se a opção `Non-transacted` for definida para esse provedor e se a instrução não estiver em uma transação de usuário.

- Se o provedor não der suporte a `ITransactionJoin`, uma instrução `UPDATE` ou `DELETE` será permitida somente se ela não estiver em uma transação de usuário.

As seguintes propriedades do conjunto de linhas são necessárias no conjunto de linhas aberto na tabela atualizada: `DBPROP_IRowsetLocate`, `DBPROP_IRowsetChange` e `DBPROP_BOOKMARKS`. A propriedade do conjunto de linhas `DBPROP_UPDATABILITY` é definida como `DBPROPVAL_UP_CHANGE` ou `DBPROPVAL_UP_DELETE`, dependendo se a operação executada é um `UPDATE` ou um `DELETE`, respectivamente.

As seguintes etapas de alto nível no provedor para processamento de uma operação `UPDATE` ou `DELETE` são executadas:

1. O SQL Server abre o conjunto de linhas da tabela base por meio da interface `IOpenRowset`. O SQL Server exige as propriedades mencionadas acima no conjunto de linhas.

1. O SQL Server determina o conjunto de linhas qualificadas a serem atualizadas ou excluídas.

1. O SQL Server usa os indicadores para posicionar as linhas qualificadas por meio da interface `IRowsetLocate`.

1. Use `IRowsetChange::SetData` para operações `UPDATE`ou `IRowsetChange::DeleteRows` para operações de exclusão para executar as alterações necessárias nas linhas qualificadas.

### <a name="insert-statement"></a>Instrução `INSERT`

As condições para dar suporte a instruções `INSERT` em uma tabela remota são menos rigorosas do que para as instruções `UPDATE` e `DELETE`:

- O provedor precisa dar suporte a `IRowsetChange::InsertRow` no conjunto de linhas aberto na tabela base que está sendo inserida.

- Se o provedor não der suporte a `ITransactionLocal`, as instruções `INSERT` serão permitidas somente se a opção `Non-transacted updates` for definida para esse servidor vinculado e se a instrução não estiver em uma transação de usuário.

- Se o provedor não der suporte a `ITransactionJoin`, as instruções `INSERT` serão permitidas somente se elas não estiverem em uma transação de usuário.

O SQL Server usa `IOpenRowset::OpenRowset` para abrir um conjunto de linhas na tabela base e chama `IRowsetChange::InsertRow` para inserir novas linhas no conjunto de linhas base.

### <a name="pass-through-queries"></a>Consultas passagem

Esse cenário é semelhante ao cenário na consulta remota, exceto pelo fato de que o texto do comando fornecido a `ICommand` é uma cadeia de caracteres de comando enviada pelo usuário e não é interpretada pelo SQL Server. O SQL Server usa `DBGUID_DEFAULT` como o identificador de dialeto quando chama `ICommandText::SetCommandText`. `DBGUID_DEFAULT` indica que o provedor deve usar seu dialeto padrão. Se esse texto de comando retornar mais de um conjunto de resultados, por exemplo, se o comando invocar um procedimento armazenado que retorna vários conjuntos de resultados, o SQL Server usará apenas o primeiro conjunto de resultados do comando.

Para obter uma lista de todas as interfaces OLE DB usadas pelo SQL Server, confira [Interfaces OLE DB consumidas pelo SQL Server](#appendixa).

### <a name="conclusion"></a>Conclusão

O Microsoft SQL Server oferece o conjunto mais robusto de ferramentas para acessar dados de fontes de dados heterogêneos. Ao compreender as interfaces OLE DB expostas pelo SQL Server, os desenvolvedores podem exercer um alto grau de controle e sofisticação em consultas distribuídas.

## <a name="appendixa"></a> Interfaces OLE DB consumidas pelo SQL Server

A tabela a seguir lista todas as interfaces OLE DB usadas pelo SQL Server. A coluna Obrigatório indica se a interface faz parte da funcionalidade OLE DB mínima necessária para o SQL Server ou se ela é opcional. Se determinada interface não estiver marcada como obrigatória, o SQL Server ainda poderá acessar o provedor, mas uma funcionalidade ou uma otimização específica do SQL Server não será possível no provedor.

No caso das interfaces opcionais, a coluna Cenários indica um ou mais dos seis cenários que usam a interface especificada. Por exemplo, a interface `IRowsetChange` em conjuntos de linhas da tabela base é uma interface opcional; essa interface é usada nas instruções `UPDATE` e DELETE e nos cenários da instrução `INSERT`. Se não houver suporte para essa interface, as instruções UPDATE, DELETE e `INSERT` não poderão ter suporte nesse provedor. Algumas das outras interfaces opcionais são marcadas como \"desempenho\" na coluna Cenários, indicando que a interface resulta em um melhor desempenho geral. Por exemplo, se não houver suporte para a interface `IDBSchemaRowset`, o SQL Server precisará abrir o conjunto de linhas duas vezes: uma vez para seus metadados e uma vez para a execução da consulta. Ao dar suporte a `IDBSchemaRowset`, o desempenho do SQL Server é aprimorado.

|Object|Interface|Obrigatório|Comentários|Cenários|
|:-----|:-----|:-----|:-----|:-----|
|Objeto de fonte de dados|`IDBInitialize`|Sim|Inicialize e configure o contexto de dados e segurança.| |
| |`IDBCreateSession`|Sim|Crie o objeto de sessão de BD.| |
| |`IDBProperties`|Sim|Obtenha informações sobre as funcionalidades do provedor, defina as propriedades de inicialização e a propriedade necessária: DBPROP_INIT_TIMEOUT.| |
| |`IDBInfo`|Não|Obtenha o literal de aspas, o catálogo, o nome, a parte, o separador, o caractere e assim por diante.|Consulta remota.|
|Objeto de sessão de BD|`IDBSchemaRowset`|Não|Obtenha metadados de tabela/coluna. Conjuntos de linhas necessários `TABLES`, `COLUMNS` e `PROVIDER_TYPES`; outros que são usados, se disponíveis: `INDEXES` e `TABLE_STATISTICS`.|Desempenho, acesso indexado.|
| |`IOpenRowset`|Sim|Abra um conjunto de linhas em uma tabela, um índice ou um histograma.| |
| |`IGetDataSource`|Sim|Use-a para retornar ao DSO de um objeto de sessão de BD.| |
| |`IDBCreateCommand`|Não|Use-a para criar um objeto de comando (consulta) para provedores que dão suporte à consulta.|Consulta remota, consulta passagem.|
| |`ITransactionLocal`|Não|Use-a para atualizações transacionadas.|Instruções `UPDATE`, `DELETE` e `INSERT`.|
| |`ITransactionJoin`|Não|Use-a para o suporte à transação distribuída.|Instruções `UPDATE`, `DELETE` e `INSERT` se estiverem em uma transação de usuário.|
|Objeto de conjunto de linhas|IRowset|Sim|Examine as linhas.| |
| |`IAccessor`|Sim|Faça uma associação a colunas em um conjunto de linhas.| |
| |`IColumnsInfo`|Sim|Obtenha informações sobre as colunas de um conjunto de linhas.| |
| |`IRowsetInfo`|Sim|Obtenha informações sobre as propriedades do conjunto de linhas.| |
| |`IRowsetLocate`|Não|Necessária para operações `UPDATE`/`DELETE` e para fazer pesquisas baseadas em índice; usada para pesquisar linhas por indicadores.|Acesso indexado, instruções `UPDATE` e `DELETE`.|
| |`IRowsetChange`|Não|Necessária para `INSERTS`/`UPDATES`/ `DELETES` em um conjunto de linhas. Os conjuntos de linhas nas tabelas base devem dar suporte a essa interface em instruções `INSERT`, `UPDATE` e `DELETE`.|Instruções `UPDATE`, `DELETE` e `INSERT`.|
| |`IConvertType`|Sim|Use-a para verificar se o conjunto de linhas dá suporte a conversões de tipo de dados específicos em suas colunas.| |
|Índice|`IRowset`|Sim|Examine as linhas.|Acesso indexado, desempenho.|
| |`IAccessor`|Sim|Faça uma associação a colunas em um conjunto de linhas.|Acesso indexado, desempenho.|
| |`IColumnsInfo`|Sim|Obtenha informações sobre as colunas de um conjunto de linhas.|Acesso indexado, desempenho.|
| |`IRowsetInfo`|Sim|Obtenha informações sobre as propriedades do conjunto de linhas.|Acesso indexado, desempenho.|
| |`IRowsetIndex`|Sim|Necessária somente para conjuntos de linhas em um índice; usada para a funcionalidade de indexação (definir intervalo, buscar).|Acesso indexado, desempenho.|
|Comando|`ICommand`|Sim| |Consulta remota, consulta passagem.|
| |`ICommandText`|Sim|Use-a para definir o texto da consulta.|Consulta remota, consulta passagem.|
| |`IColumnsInfo`|Sim|Use-a para obter metadados de coluna para os resultados da consulta.|Consulta remota, consulta passagem.|
| |`ICommandProperties`|Sim|Use-a para especificar as propriedades necessárias em conjuntos de linhas retornados pelo comando.|Consulta remota, consulta passagem.|
| |`ICommandWithParameters`|Não|Use-a para a execução de consulta parametrizada.|Consulta remota, desempenho.|
| |`ICommandPrepare`|Não|Use-a para preparar um comando para obter metadados (usados em consultas passagem, se disponíveis).|Consulta remota, desempenho.|
|Objeto de erro|`IErrorRecords`|Sim|Use-a para obter um ponteiro para uma interface `IErrorInfo` correspondente a um único registro de erro.| |
| |`IErrorInfo`|Sim|Use-a para obter um ponteiro para uma interface `IErrorInfo` correspondente a um único registro de erro.| |
|Qualquer objeto|`ISupportErrorInfo`|Não|Use-a para verificar se determinada interface dá suporte a objetos de erro.| |
|  |  |  |  |  |

>[!NOTE]
>O objeto `Index`, o objeto `Command` e o objeto `Error` não são obrigatórios. No entanto, se houver suporte para eles, as interfaces listadas serão obrigatórias, conforme especificado na coluna Obrigatório.

## <a name="appendixb"></a>Subconjunto SQL usado para gerar consultas remotas

O subconjunto SQL gerado pelo processador de consultas do SQL Server em um provedor de comando SQL depende do nível de sintaxe ao qual o provedor dá suporte, conforme indicado pela propriedade `DBPROP_SQLSUPPORT`.

Provedores de comando SQL que dão suporte ao nível de entrada SQL ou Núcleo ODBC

O SQL Server usa o seguinte subconjunto da linguagem SQL para consultas avaliadas por provedores de comandos SQL que dão suporte ao nível Entrada da SQL-92 ou Núcleo ODBC:

1. Instruções `SELECT` com as cláusulas `SELECT`, `FROM`, `WHERE`, `GROUP BY`, `UNION`, `UNION ALL`, `ORDER BY DESC`, `ASC` e `HAVING`.

1. `UNION` e `UNION ALL` são gerados somente em provedores que dão suporte ao nível Entrada da SQL-92, não naqueles que dão suporte ao Núcleo ODBC.

1. Cláusula `SELECT`:

   - Subconsultas escalares na lista `SELECT`.

   - Aliases de coluna sem a palavra-chave `AS`.

1. Cláusula `FROM`:

   - Palavras-chave de junção explícitas não são usadas; nomes de tabela separados por vírgula são usados para especificar junções internas e as junções externas não são especificadas em consultas remotas.

   - Consultas aninhadas do formato `FROM` (`<nested query>`) `<alias>`.

   - Aliases de tabela sem a palavra-chave AS.

1. A cláusula `WHERE` usa subconsultas com `NOT` `EXISTS`, `ANY` e `ALL`.

1. Expressões:

   - Funções de agregação usadas: `MIN([DISTINCT])`, `MAX([DISTINCT])`, `COUNT([DISTINCT])`, `SUM([DISTINCT])`, `AVG([DISTINCT])` e `COUNT(*)`.

   - Operadores de comparação: `<`, `=`, `<=`, `>`, `<>`, `>=`, `IS NULL` e `IS NOT NULL`.

   - Operadores boolianos: `AND`, `OR` e `NOT`.

 - Operadores aritméticos: `+`, `-`, `*` e `/`.

1. Constantes:

- Os literais numéricos e monetários são sempre colocados entre `( )`.

- Os literais de caracteres são colocados entre `' '`.

Provedores de comandos SQL que dão suporte ao nível SQL Mínimo

Nos provedores de comandos SQL que dão suporte ao nível SQL Mínimo, o SQL Server gera o SQL usando a gramática a seguir.

Essa gramática foi derivada com o uso da gramática de SQL Mínimo descrita no ODBC 3.0. Todas as diferenças dessa gramática são realçadas. Os itens mostrados em `*bold italics`* são aqueles adicionados à gramática de SQL Mínimo descrita no ODBC 3.0. Os itens mostrados como excluídos em verde são aqueles removidos dessa gramática.

*select-statement* ::=

`SELECT [ALL | DISTINCT] *select-list* FROM *table-reference-list*[WHERE *search-condition*] [order-by-clause]`

Cláusula `SELECT`

select-list ::= `*` | `select-sublist [, select-sublist]...`

select-sublist ::= expression * [`alias`]*

`*alias ::= user-defined-name`*

`FROM clause`

table-reference-list ::= table-reference

table-identifier ::= user-defined-name

table-name ::= table-identifier

table-reference ::= table-name

`WHERE clause`

search-condition ::= boolean-term \[OR search-condition\]

boolean-term ::= boolean-factor \[AND boolean-term\]

boolean-factor ::= \[NOT\] boolean-primary

boolean-primary ::= comparison-predicate \| ( search-condition )

comparison-predicate ::= expression comparison-operator expression

*\| `expression IS \[NOT\] NULL`*

comparison-operator ::= `< \| >` \| `<= \| >`= \| = \| `<>`

`ORDER BY clause`

order-by-clause ::= ORDER BY sort-specification \[, sort-specification\]\..

sort-specification ::= { \| column-name } \[ASC \| DESC\]

`Common syntactic elements`

expression ::= term \| expression {+\|--} term

term ::= factor \| term {\*\|/} factor

factor ::= \[+\|--\] primary

primary ::= column-name

Literal \|

\| (expressão)

column-name ::= \[table-name.\]column-identifier

literal ::= character-string-literal

*\| integer-literal*

*\| exact-numeric-literal*

character-string-literal ::= \'{character}...\'

(caractere é qualquer caractere no conjunto de caracteres do driver/da fonte de dados. Para incluir um único caractere de aspas literal (\') em um literal de cadeia de caracteres, use dois caracteres de aspas literais (\'\').)

`*integer-literal ::=* \[*+ \| -*\] *unsigned-integer`*

`*exact-numeric-literal::=* \[*+ \| -*\] *unsigned-integer* \[*period unsigned-integer*\]`

`*\| period unsigned-integer`*

base-table-name ::= base-table-identifier

base-table-identifier ::= user-defined-name

column-identifier ::= user-defined-name

user-defined-name ::= letter\[digit \| letter \| _\]\..

unsigned-integer ::= {digit}...

digit ::= 0 \| 1 \| 2 \| 3 \| 4 \| 5 \| 6 \| 7 \| 8 \| 9

period ::= . 

## <a name="appendixc"></a>Propriedades específicas do SQL Server

```
enum SQLPROPERTIES
       {
       SQLPROP_NOHPNEEDED = 0x1,
       SQLPROP_FREETHREADED = 0x2,
       SQLPROP_UMSENABLED = 0x3,
       SQLPROP_NESTEDQUERIES = 0x4,
       SQLPROP_DYNAMICSQL = 0x5,
       SQLPROP_GROUPBY = 0x6,
       SQLPROP_DATELITERALS = 0x7,
       SQLPROP_ANSILIKE = 0x8,
       SQLPROP_INNERJOIN = 0x9,
       SQLPROP_SUBQUERIES = 0x10, 
       SQLPROP_PARALLELSCAN = 0x11,
       SQLPROP_COLUMNCOLLATION = 0x12,
       SQLPROP_CARDINALITY = 0x13,
       SQLPROP_SIMPLEUPDATES = 0x14,
       SQLPROP_SQLLIKE = 0x15,
       SQLPROP_BITREMOTING = 0x16,
       SQLPROP_UNICODELITERALS = 0x17,
       SQLPROP_USELATESTCOLLATIONVERSION = 0x18
       };

```
