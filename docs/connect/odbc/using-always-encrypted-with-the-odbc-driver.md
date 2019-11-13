---
title: Como usar o recurso Always Encrypted com o ODBC Driver for SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 09/01/2018
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 02e306b8-9dde-4846-8d64-c528e2ffe479
ms.author: v-chojas
author: MightyPen
ms.openlocfilehash: bf15831517ebaa8646c1d6f3c080033c3a41405d
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594373"
---
# <a name="using-always-encrypted-with-the-odbc-driver-for-sql-server"></a>Como usar o recurso Always Encrypted com o ODBC Driver for SQL Server
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

### <a name="applicable-to"></a>Aplicável a

- ODBC Driver 13.1 for SQL Server
- ODBC Driver 17 for SQL Server

### <a name="introduction"></a>Introdução

Este artigo fornece informações sobre como desenvolver aplicativos ODBC usando o [Always Encrypted (Mecanismo de Banco de Dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) ou o [Always Encrypted com enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves.md) e [o driver ODBC para SQL Servidor](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md).

O Always Encrypted permite que os aplicativos cliente criptografem dados confidenciais e nunca revelem os dados nem as chaves de criptografia para o SQL Server ou o Banco de Dados SQL do Azure. Um driver habilitado para Always Encrypted, como o ODBC Driver for SQL Server, consegue fazer isso criptografando e descriptografando de modo transparente dados confidenciais no aplicativo cliente. O driver determina automaticamente quais parâmetros de consulta correspondem às colunas de banco de dados confidenciais (protegidas com o Always Encrypted) e criptografa os valores desses parâmetros antes de passar os dados para o SQL Server ou o Banco de Dados SQL do Azure. Da mesma forma, o driver descriptografa de modo transparente os dados recuperados das colunas de banco de dados criptografadas nos resultados da consulta. O Always Encrypted *com enclaves seguras* estende esse recurso para habilitar funcionalidades mais avançadas em dados confidenciais mantendo a confidencialidade desses dados.

Para obter mais informações, consulte [Always Encrypted (Mecanismo de Banco de Dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) e [Always Encrypted com enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves.md).

### <a name="prerequisites"></a>Prerequisites

Configure o Sempre Criptografado em seu banco de dados. Isso envolve o provisionamento de chaves do Sempre Criptografado e a configuração de criptografia de colunas de banco de dados selecionadas. Se você ainda não tiver um banco de dados com o Sempre Criptografado configurado, siga as instruções em [Getting Started with Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted)(Introdução ao Sempre Criptografado). Em particular, seu banco de dados deve conter as definições de metadados para uma chave mestra de coluna (CMK), uma chave de criptografia de coluna (CEK) e uma tabela contendo uma ou mais colunas criptografadas usando esse CEK.

### <a name="enabling-always-encrypted-in-an-odbc-application"></a>Habilitar o Always Encrypted para um aplicativo do ODBC

A maneira mais fácil de habilitar a criptografia de parâmetro e a descriptografia de colunas criptografadas do conjunto de resultados é definindo o valor da palavra-chave da cadeia de conexão `ColumnEncryption` como **Habilitado**. Veja a seguir o exemplo de uma cadeia de conexão que habilita Always Encrypted:

```
SQLWCHAR *connString = L"Driver={ODBC Driver 13 for SQL Server};Server={myServer};Trusted_Connection=yes;ColumnEncryption=Enabled;";
```

O Always Encrypted pode também ser habilitado na configuração de DSN, usando a mesma chave e valor (que serão substituídos pela configuração de cadeia de conexão, se presente) ou por meio de programação com o atributo de pré-conexão `SQL_COPT_SS_COLUMN_ENCRYPTION`. Defini-lo dessa maneira substitui o valor definido na cadeia de conexão ou DSN:

```
 SQLSetConnectAttr(hdbc, SQL_COPT_SS_COLUMN_ENCRYPTION, (SQLPOINTER)SQL_COLUMN_ENCRYPTION_ENABLE, 0);
```

Uma vez habilitado para a conexão, o comportamento do Always Encrypted pode ser ajustado para consultas individuais. Confira [Controle do impacto sobre o desempenho do Always Encrypted](#controlling-the-performance-impact-of-always-encrypted) abaixo para saber mais.

Observe que habilitar o Always Encrypted não é suficiente para o êxito da criptografia ou descriptografia. Do mesmo modo, é preciso ter certeza de que:

- O aplicativo tem as permissões de banco de dados *VIEW ANY COLUMN MASTER KEY DEFINITION* e *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* , necessárias para acessar os metadados sobre as chaves do Always Encrypted no banco de dados. Para saber mais, confira [Permissões de banco de dados](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions).

- O aplicativo pode acessar a CMK que protege as CEKs para as colunas criptografadas consultadas. Isso depende do provedor de repositório de chaves que armazena a CMK. Confira [Como trabalhar com repositórios de chaves mestras de coluna](#working-with-column-master-key-stores) para saber mais.

### <a name="enabling-always-encrypted-with-secure-enclaves"></a>Como habilitar o Always Encrypted com enclaves seguros

A partir da versão 17.4, o driver é compatível com Always Encrypted com enclaves seguros. Para habilitar o uso do enclave ao se conectar ao SQL Server 2019 ou posterior, defina o DSN `ColumnEncryption`, a cadeia de conexão ou o atributo de conexão com o nome do tipo enclave e o protocolo de atestado, e os dados de atestado associados, separados por uma vírgula. Na versão 17,4, somente o [segurança baseada em virtualização](https://www.microsoft.com/security/blog/2018/06/05/virtualization-based-security-vbs-memory-enclaves-data-protection-through-isolation/) tipo enclave e [serviço guardião de host](https://docs.microsoft.com/windows-server/security/set-up-hgs-for-always-encrypted-in-sql-server) protocolo de atestado, indicado por `VBS-HGS`, tem suporte; para usá-lo, especifique a URL do servidor de atestado, por exemplo:

```
Driver=ODBC Driver 17 for SQL Server;Server=yourserver.yourdomain;Trusted_Connection=Yes;ColumnEncryption=VBS-HGS,http://attestationserver.yourdomain/Attestation
```

Se o servidor e o serviço de atestado estiverem configurados corretamente, bem como CMKs e CEKs habilitados para enclave para as colunas desejadas, agora você poderá executar consultas que usam o enclave, como criptografia in-loco e computações avançadas, além do funcionalidade existente fornecida pelo Always Encrypted. Consulte [configurar Always Encrypted com enclaves seguros](../../relational-databases/security/encryption/configure-always-encrypted-enclaves.md) para obter mais informações.


### <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>Recuperando e modificando dados em colunas criptografadas

Depois de habilitar Always Encrypted em uma conexão, você pode usar APIs ODBC padrão. As APIs ODBC podem recuperar ou modificar dados em colunas de banco de dado criptografado. Os seguintes itens de documentação podem ajudar com isso:

- [Código de exemplo ODBC](cpp-code-example-app-connect-access-sql-db.md)
- [Referência do programador ODBC](../../odbc/reference/odbc-programmer-s-reference.md)

Seu aplicativo deve ter as permissões de banco de dados necessárias e deve ser capaz de acessar a chave mestra de coluna. Em seguida, o driver criptografa todos os parâmetros de consulta que se destinam a colunas criptografadas. O driver também descriptografa os dados recuperados de colunas criptografadas. O driver executa toda essa criptografia e descriptografia sem nenhuma assistência do seu código-fonte. Para o seu programa, é como se as colunas não estiverem criptografadas.

Se Always Encrypted não estiver habilitado, as consultas com parâmetros que se destinam a colunas criptografadas falharão. Os dados ainda podem ser recuperados de colunas criptografadas, desde que a consulta não tenha parâmetros que se destinem a colunas criptografadas. No entanto, o driver não tenta descriptografar nenhuma criptografia, e o aplicativo recebe os dados binários criptografados (como matrizes de bytes).

A tabela abaixo resume o comportamento das consultas, dependendo de se o Always Encrypted está habilitado ou não:

|Característica da consulta | O Sempre Criptografado está habilitado e o aplicativo pode acessar as chaves e os metadados da chave|O Sempre Criptografado está habilitado e o aplicativo não pode acessar as chaves nem os metadados da chave | O Sempre Criptografado está desabilitado|
|:---|:---|:---|:---|
| Parâmetros que se destinam a colunas criptografadas. | Os valores de parâmetro são criptografados de modo transparente. | Erro | Erro|
| Recuperando dados de colunas criptografadas, sem parâmetros que se destinam a colunas criptografadas.| Os resultados das colunas criptografadas são descriptografados de modo transparente. O aplicativo recebe valores de coluna de texto não criptografado. | Erro | Os resultados das colunas criptografadas não são descriptografados. O aplicativo recebe valores criptografados como matrizes de bytes.

Os exemplos a seguir ilustram como recuperar e modificar dados em colunas criptografadas. Por exemplo, considere uma tabela com o seguinte esquema. Observe que as colunas SSN e BirthDate estão criptografadas.

```
CREATE TABLE [dbo].[Patients](
 [PatientId] [int] IDENTITY(1,1),
 [SSN] [char](11) COLLATE Latin1_General_BIN2
 ENCRYPTED WITH (ENCRYPTION_TYPE = DETERMINISTIC,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = CEK1) NOT NULL,
 [FirstName] [nvarchar](50) NULL,
 [LastName] [nvarchar](50) NULL,
 [BirthDate] [date]
 ENCRYPTED WITH (ENCRYPTION_TYPE = RANDOMIZED,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = CEK1) NOT NULL
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY] )
 GO
```

#### <a name="data-insertion-example"></a>Exemplo de inserção de dados

Este exemplo insere uma linha na tabela Pacientes. Observe o seguinte:

- Não há nada específico de criptografia no código de exemplo. O driver detecta e criptografa automaticamente os valores dos parâmetros de SSN e data, que se destinam a colunas criptografadas. Isso torna a criptografia transparente para o aplicativo.

- Os valores inseridos nas colunas de banco de dados, incluindo as colunas criptografadas, são passados como parâmetros associados (consulte [Função SQLBindParameter](https://msdn.microsoft.com/library/ms710963(v=vs.85).aspx)). Embora o uso de parâmetros seja opcional ao enviar valores para colunas não criptografadas (mesmo que seja altamente recomendável, pois ajuda a prevenir a injeção de SQL), ele é necessário para valores que se destinam a colunas criptografadas. Se os valores inseridos nas colunas SSN ou BirthDate foram passados como literais inseridos na instrução de consulta, a consulta falha, pois o driver não tenta criptografar ou processar os literais em consultas. Como resultado, o servidor os rejeitaria como incompatíveis com as colunas criptografadas.

- O tipo SQL do parâmetro inserido na coluna SSN é definido como SQL_CHAR, que mapeia para o tipo de dados **char** do SQL Server (`rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 11, 0, (SQLPOINTER)SSN, 0, &cbSSN);`). Se o tipo do parâmetro foi definido como SQL_WCHAR, que é mapeado para **nchar**, a consulta falha, já que o Always Encrypted não oferece suporte a conversões de valores nchar criptografados em valores char criptografados no lado do servidor. Confira [Referência do programador de ODBC – Apêndice D: Tipos de dados](https://msdn.microsoft.com/library/ms713607.aspx) para saber mais sobre os mapeamentos de tipo de dados.

```
    SQL_DATE_STRUCT date;
    SQLLEN cbdate;   // size of date structure  

    SQLCHAR SSN[12];
    strcpy_s((char*)SSN, _countof(SSN), "795-73-9838");

    SQLWCHAR* firstName = L"Catherine";
    SQLWCHAR* lastName = L"Abel";
    SQLINTEGER cbSSN = SQL_NTS, cbFirstName = SQL_NTS, cbLastName = SQL_NTS;

    // Initialize the date structure  
    date.day = 10;
    date.month = 9;
    date.year = 1996;

    // Size of structures   
    cbdate = sizeof(SQL_DATE_STRUCT);

    SQLRETURN rc = 0;

    string queryText = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?) ";

    rc = SQLPrepare(hstmt, (SQLCHAR *)queryText.c_str(), SQL_NTS);

    //SSN
    rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 11, 0, (SQLPOINTER)SSN, 0, &cbSSN);
    //FirstName
    rc = SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_WCHAR, SQL_WCHAR, 50, 0, (SQLPOINTER)firstName, 0, &cbFirstName);
    //LastName
    rc = SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_WCHAR, SQL_WCHAR, 50, 0, (SQLPOINTER)lastName, 0, &cbLastName);
    //BirthDate
    rc = SQLBindParameter(hstmt, 4, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 10, 0, (SQLPOINTER)&date, 0, &cbdate);

    rc = SQLExecute(hstmt);
```

#### <a name="plaintext-data-retrieval-example"></a>Exemplo de recuperação de dados de texto não criptografado

O exemplo a seguir demonstra a filtragem de dados com base em valores criptografados e a recuperação de dados de texto sem formatação de colunas criptografadas. Observe o seguinte:

- O valor usado na cláusula WHERE a ser filtrado na coluna SSN precisa ser passado usando o SQLBindParameter para que o driver possa criptografá-lo de modo transparente antes de enviá-lo para o servidor.

- Todos os valores impressos pelo programa estarão em texto não criptografado, já que o driver descriptografará de modo transparente os dados recuperados das colunas SSN e BirthDate.

> [!NOTE]
> Observação: as consultas podem executar comparações de igualdade em colunas criptografadas somente se a criptografia for determinística. Para obter mais informações, confira [Seleção de criptografia determinística ou aleatória](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption).

```
SQLCHAR SSN[12];
strcpy_s((char*)SSN, _countof(SSN), "795-73-9838");

SQLWCHAR* firstName = L"Catherine";
SQLWCHAR* lastName = L"Abel";
SQLINTEGER cbSSN = SQL_NTS, cbFirstName = SQL_NTS, cbLastName = SQL_NTS;

SQLRETURN rc = 0;
string empty = "";
string queryText = "SELECT [SSN], [FirstName], [LastName], [BirthDate] " + empty +
    "FROM  [dbo].[Patients]" +
    "WHERE " +
    "[SSN] = ? ";

rc = SQLPrepare(hstmt, (SQLCHAR *)queryText.c_str(), SQL_NTS);

//SSN
rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 11, 0, (SQLPOINTER)SSN, 0, &cbSSN);

rc = SQLExecute(hstmt);
HandleDiagnosticRecord(hstmt, SQL_HANDLE_STMT, rc);

SQL_DATE_STRUCT dateVal;
SQLWCHAR firstNameVal[50];
SQLWCHAR lastNameVal[50];
SQLCHAR SSNVal[12];
SQLLEN cbdate;   // size of date structure  

int rowcount = 0;
while (SQL_SUCCEEDED(SQLFetch(hstmt)))
{
    rowcount++;
    SQLGetData(hstmt, 1, SQL_C_CHAR, &SSNVal, 11, &cbSSN);
    SQLGetData(hstmt, 2, SQL_C_WCHAR, &firstNameVal, 50, &cbFirstName);
    SQLGetData(hstmt, 3, SQL_C_WCHAR, &lastNameVal, 50, &cbLastName);
    SQLGetData(hstmt, 4, SQL_C_TYPE_DATE, &dateVal, 10, &cbdate);        
}
```

#### <a name="ciphertext-data-retrieval-example"></a>Exemplo de recuperação de dados de texto cifrado

Se o Always Encrypted não estiver habilitado, uma consulta ainda poderá recuperar dados de colunas criptografadas, desde que a consulta não tenha parâmetros que se destinam a colunas criptografadas.

O exemplo a seguir ilustra como recuperar dados binários criptografados de colunas criptografadas. Observe o seguinte:

- Como o Sempre Criptografado não está habilitado na cadeia de conexão, a consulta retornará valores criptografados de SSN e BirthDate como matrizes de bytes (o programa converte os valores em cadeias de caracteres).
- Uma consulta que recupera dados de colunas criptografadas com o Sempre Criptografado desabilitado pode ter parâmetros, desde que nenhum dos parâmetros se destinem a uma coluna criptografada. A consulta acima filtra por LastName, que não é criptografado no banco de dados. Se a consulta filtrar por SSN ou BirthDate, a consulta falhará.


```
SQLCHAR SSN[12];
strcpy_s((char*)SSN, _countof(SSN), "795-73-9838");

SQLWCHAR* firstName = L"Catherine";
SQLWCHAR* lastName = L"Abel";
SQLINTEGER cbSSN = SQL_NTS, cbFirstName = SQL_NTS, cbLastName = SQL_NTS;

SQLRETURN rc = 0;
string empty = "";
string queryText = "SELECT [SSN], [FirstName], [LastName], [BirthDate] " + empty +
    "FROM  [dbo].[Patients]" +
    "WHERE " +
    "[LastName] = ?";

rc = SQLPrepare(hstmt, (SQLCHAR *)queryText.c_str(), SQL_NTS);

//LastName
rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_WCHAR, SQL_WCHAR, 50, 0, (SQLPOINTER)lastName, 0, &cbLastName);

rc = SQLExecute(hstmt);
HandleDiagnosticRecord(hstmt, SQL_HANDLE_STMT, rc);

SQL_DATE_STRUCT dateVal;
SQLWCHAR firstNameVal[50];
SQLWCHAR lastNameVal[50];
SQLCHAR SSNVal[12];
SQLLEN cbdate;   // size of date structure  

int rowcount = 0;
while (SQL_SUCCEEDED(SQLFetch(hstmt)))
{
    rowcount++;
    SQLGetData(hstmt, 1, SQL_C_CHAR, &SSNVal, 11, &cbSSN);
    SQLGetData(hstmt, 2, SQL_C_WCHAR, &firstNameVal, 50, &cbFirstName);
    SQLGetData(hstmt, 3, SQL_C_WCHAR, &lastNameVal, 50, &cbLastName);
    SQLGetData(hstmt, 4, SQL_C_TYPE_DATE, &dateVal, 10, &cbdate);        
}
```

#### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>Evitando problemas comuns ao consultar colunas criptografadas

Esta seção descreve as categorias comuns de erros ao consultar colunas criptografadas de aplicativos ODBC e algumas diretrizes sobre como evitá-los.

##### <a name="unsupported-data-type-conversion-errors"></a>Erros de conversão de tipo de dados sem suporte

O Always Encrypted dá suporte a algumas conversões de tipos de dados criptografados. Confira [Always Encrypted (Mecanismo de Banco de Dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) para obter a lista detalhada de conversões de tipo compatíveis. Para evitar erros de conversão de tipo de dados, certifique-se de observar os seguintes pontos ao usar SQLBindParameter com parâmetros que se destinam a colunas criptografadas:

- O tipo SQL do parâmetro é exatamente o mesmo que o tipo da coluna de destino, ou a conversão de um tipo SQL para o tipo da coluna é suportada.

- A precisão e a escala dos parâmetros que se destinam a colunas dos tipos de dados `decimal` e `numeric` do SQL Server são iguais à precisão e à escala configuradas para a coluna de destino.

- A precisão dos parâmetros que se destinam às colunas dos tipos de dados `datetime2`, `datetimeoffset` ou `time` do SQL Server não é maior que a precisão da coluna de destino, em consultas que modificam a coluna de destino.  

##### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>Erros devido à passagem de texto sem formatação em vez de valores criptografados

Qualquer valor que se destina a uma coluna criptografada precisa ser criptografado antes de ser enviado ao servidor. Uma tentativa de inserir, modificar ou filtrar por um valor de texto não criptografado em uma coluna criptografada resultará em um erro. Para evitar esses erros, garanta que:

- O Always Encrypted esteja habilitado (no DSN, na cadeia de conexão, antes de conectar, definindo o atributo de conexão `SQL_COPT_SS_COLUMN_ENCRYPTION` para uma conexão específica, ou o atributo de instrução `SQL_SOPT_SS_COLUMN_ENCRYPTION` para uma instrução específica).

- Você use o SQLBindParameter para enviar dados que se destinam a colunas criptografadas. O exemplo abaixo mostra uma consulta que filtra incorretamente por uma/constante em uma coluna criptografada (SSN), em vez de passar o literal como um argumento para o SQLBindParameter.

```
string queryText = "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
```

### <a name="precautions-when-using-sqlsetpos-and-sqlmoreresults"></a>Precauções ao usar SQLSetPos e SQLMoreResults

#### <a name="sqlsetpos"></a>SQLSetPos

A API `SQLSetPos` permite que um aplicativo atualize linhas em um conjunto de resultados usando buffers que foram associados a SQLBindCol e nos quais a linha de dados foi obtida anteriormente. Devido ao comportamento de preenchimento assimétrico dos tipos de comprimento fixo criptografados, é possível que os dados dessas colunas sejam alterados inesperadamente durante a execução de atualizações em outras colunas na linha. Com o Always Encrypted, os valores de caracteres de comprimento fixo serão preenchidos se o valor for menor do que o tamanho do buffer.

Para atenuar esse comportamento, use o sinalizador `SQL_COLUMN_IGNORE` para ignorar colunas que não serão atualizadas como parte do `SQLBulkOperations` e ao usar `SQLSetPos` para atualizações baseadas em cursor.  Todas as colunas que não estão sendo modificadas diretamente pelo aplicativo devem ser ignoradas em relação ao desempenho e para evitar o truncamento de colunas limitadas a um buffer *menor* que o tamanho real (BD). Para saber mais, confira [Referência de função SQLSetPos](https://msdn.microsoft.com/library/ms713507(v=vs.85).aspx).

#### <a name="sqlmoreresults--sqldescribecol"></a>SQLMoreResults e SQLDescribeCol

Programas de aplicativo podem chamar [SQLDescribeCol](https://msdn.microsoft.com/library/ms716289(v=vs.85).aspx) para retornar metadados sobre colunas em instruções preparadas.  Quando o Always Encrypted estiver habilitado, chamar `SQLMoreResults` *antes* de chamar `SQLDescribeCol` faz com que [sp_describe_first_result_set](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) seja chamado, o que não retorna corretamente os metadados de texto não criptografado de colunas criptografadas. Para evitar esse problema, chame `SQLDescribeCol` em instruções preparadas *antes* de chamar `SQLMoreResults`.

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>Controle do impacto sobre o desempenho do Always Encrypted

Como o Always Encrypted é uma tecnologia de criptografia do lado do cliente, a maior parte da sobrecarga de desempenho é observada no lado do cliente, não no banco de dados. Além do custo das operações de criptografia e descriptografia, as outras fontes de sobrecarga de desempenho no lado do cliente são:

- Viagens de ida e volta adicionais ao banco de dados para recuperar metadados dos parâmetros de consulta.

- Chamadas a um repositório de chaves mestras de coluna para acessar uma chave mestra de coluna.

Esta seção descreve as otimizações de desempenho internas no ODBC Driver for SQL Server e como você pode controlar o impacto dos dois fatores acima sobre o desempenho.

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>Controle das viagens de ida e volta para recuperar metadados dos parâmetros de consulta

Se o Always Encrypted estiver habilitado para uma conexão, o driver por padrão chamará [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) para cada consulta parametrizada, passando a instrução de consulta (sem nenhum valor de parâmetro) para o SQL Server. Este procedimento armazenado analisa a instrução de consulta para descobrir se os parâmetros precisam ser criptografados e, se for o caso, retorna as informações relacionadas à criptografia para cada parâmetro para permitir ao driver criptografá-los. O comportamento acima garante um alto nível de transparência ao aplicativo cliente: o aplicativo (e o desenvolvedor do aplicativo) não precisa estar ciente de quais consultas acessam colunas criptografadas, desde que os valores que se destinam às colunas criptografadas sejam passados para o driver nos parâmetros.

### <a name="per-statement-always-encrypted-behavior"></a>Comportamento do Always Encrypted por instrução

Para controlar o impacto no desempenho da recuperação de metadados de criptografia para consultas parametrizadas, é possível alterar o comportamento do Always Encrypted para consultas individuais se ele tiver sido habilitado na conexão. Assim, você pode garantir que `sys.sp_describe_parameter_encryption` seja invocado apenas para consultas que você sabe que têm parâmetros que se destinam a colunas criptografadas. No entanto, observe que, ao fazer isso, você reduzirá a transparência da criptografia: se você criptografar colunas adicionais no seu banco de dados, poderá precisar alterar o código do aplicativo para alinhá-lo a alterações de esquema.

Para controlar o comportamento de Always Encrypted de uma instrução, chame SQLSetStmtAttr para definir o atributo de instrução `SQL_SOPT_SS_COLUMN_ENCRYPTION` como um dos seguintes valores:

|Valor|Descrição|
|-|-|
|`SQL_CE_DISABLED` (0)|O Always Encrypted está desabilitado para a instrução|
|`SQL_CE_RESULTSETONLY` (1)|Apenas descriptografia. Conjuntos de resultados e valores de retorno estão descriptografados, e parâmetros não estão criptografados|
|`SQL_CE_ENABLED` (3) | O Always Encrypted está habilitado e é usado para parâmetros e resultados|

Novos identificadores de instrução criados a partir de uma conexão com o Always Encrypted habilitado têm SQL_CE_ENABLED como padrão. Aqueles criados a partir de uma conexão com ele desabilitado têm SQL_CE_DISABLED como padrão (e não é possível habilitar o Always Encrypted neles).

Se a maioria das consultas de um aplicativo cliente acessa colunas criptografadas, é recomendável o seguinte:

- Defina a palavra-chave de cadeia de conexão `ColumnEncryption` como `Enabled`.

- Defina o atributo `SQL_SOPT_SS_COLUMN_ENCRYPTION` como `SQL_CE_DISABLED` em instruções que não acessam nenhuma coluna criptografada. Isso desabilita a chamada de `sys.sp_describe_parameter_encryption` e as tentativas de descriptografar todos os valores no conjunto de resultados.
    
- Defina o atributo `SQL_SOPT_SS_COLUMN_ENCRYPTION` como `SQL_CE_RESULTSETONLY` em instruções que não têm parâmetros que exigem criptografia, mas que recuperam dados de colunas criptografadas. Isso desabilita a chamada `sys.sp_describe_parameter_encryption` e a criptografia do parâmetro. Resultados contendo colunas criptografadas continuam sendo descriptografados.

## <a name="always-encrypted-security-settings"></a>Configurações de segurança do Always Encrypted

### <a name="force-column-encryption"></a>Forçar criptografia de coluna

Para impor a criptografia de um parâmetro, defina o campo descritor de parâmetro de implementação (IPD) `SQL_CA_SS_FORCE_ENCRYPT` por meio de uma chamada para a função SQLSetDescField. Um valor diferente de zero faz com que o driver retorne um erro quando nenhum metadado de criptografia retorna para o parâmetro associado.

```
SQLHDESC ipd;
SQLGetStmtAttr(hStmt, SQL_ATTR_IMP_PARAM_DESC, &ipd, 0, 0);
SQLSetDescField(ipd, paramNum, SQL_CA_SS_FORCE_ENCRYPT, (SQLPOINTER)TRUE, SQL_IS_SMALLINT);   
```

Se o SQL Server informar o driver de que o parâmetro não precisa ser criptografado, as consultas que usam tal parâmetro falharão. Isso fornece proteção adicional contra ataques à segurança que envolvem um SQL Server comprometido fornecer metadados de criptografia incorretos ao cliente, o que pode levar à divulgação de dados.

### <a name="column-encryption-key-caching"></a>Cache de chaves de criptografia de coluna

Para reduzir o número de chamadas a um repositório de chaves mestras de coluna para descriptografar chaves de criptografia de coluna, o driver armazena CEKs de texto não criptografado na memória. O cache da CEK é global para o driver e não está associado a nenhuma outra conexão. Depois de receber a ECEK dos metadados do banco de dados, o driver primeiro tenta encontrar a CEK de texto não criptografado correspondente ao valor da chave criptografada no cache. O driver chama o repositório de chaves que contém a CMK somente se ele não conseguir localizar a CEK de texto não criptografado correspondente no cache.

> [!NOTE]
> No ODBC Driver for SQL Server, as entradas no cache são removidas após um tempo limite de duas horas. Isso significa que, para determinada ECEK, o driver entra em contato com o repositório de chaves apenas uma vez durante o tempo de vida do aplicativo, ou a cada duas horas, o que for menor.

Começando com o ODBC Driver 17.1 for SQL Server, o tempo limite de cache da CEK pode ser ajustado usando o atributo de conexão `SQL_COPT_SS_CEKCACHETTL`, que especifica o número de segundos que uma CEK permanecerá no cache. Devido à natureza do cache global, esse atributo pode ser ajustado de qualquer indicador de conexão válido para o driver. Quando o cache de TTL é reduzido, CEKs existentes que excederiam o TTL novo também são removidos. Se for 0, nenhuma CEK é armazenada em cache.

### <a name="trusted-key-paths"></a>Caminhos de chave confiáveis

A partir do ODBC Driver 17.1 for SQL Server, o atributo de conexão `SQL_COPT_SS_TRUSTEDCMKPATHS` permite que um aplicativo exija que as operações de Always Encrypted usem somente uma lista especificada de CMKs, identificadas por seus caminhos da chave. Por padrão, esse atributo é NULL, o que significa que o driver aceita qualquer caminho de chave. Para usar esse recurso, defina `SQL_COPT_SS_TRUSTEDCMKPATHS` para apontar para uma cadeia de caracteres longa terminada em nulo, que lista os caminhos da chave permitidos. A memória apontada por esse atributo deve permanecer válida durante as operações de criptografia ou descriptografia usando o identificador de conexão em que ela está definida. O driver, então, verificará se o caminho da CMK conforme especificado pelos metadados do servidor não diferencia maiúsculas de minúsculas nesta lista. Se o caminho da CMK não estiver na lista, a operação falhará. O aplicativo pode alterar o conteúdo da memória para o qual esse atributo aponta, a fim de alterar sua lista de CMKs confiáveis, sem definir o atributo novamente.

## <a name="working-with-column-master-key-stores"></a>Trabalhando com repositórios de chaves mestras de coluna

Para criptografar ou descriptografar dados, o driver precisa obter uma CEK que é configurada para a coluna de destino. As CEKs são armazenadas em formato criptografado (ECEKs) nos metadados do banco de dados. Cada CEK tem uma CMK correspondente que foi usada para criptografá-la. Os [metadados de banco de dados](../../t-sql/statements/create-column-master-key-transact-sql.md) não armazenam a CMK em si. Eles contêm apenas o nome do repositório de chaves e as informações que o repositório de chaves pode usar para localizar a CMK.

Para obter o valor de texto não criptografado de uma ECEK, o driver primeiro obtém os metadados sobre a CEK e sua CMK correspondente e, em seguida, usa essas informações para entrar em contato com o repositório de chaves que contém a CMK e solicitar para descriptografar a ECEK. O driver se comunica com um repositório de chaves usando um provedor de repositório de chaves.

### <a name="built-in-keystore-providers"></a>Provedores de repositório de chaves internos

O ODBC Driver for SQL Server tem os seguintes provedores de repositório de chaves internos:

| Nome | Descrição | Nome do provedor (metadados) |Disponibilidade|
|:---|:---|:---|:---|
|Cofre de Chave do Azure |Armazena CMKs em um Azure Key Vault | `AZURE_KEY_VAULT` |Windows, macOS, Linux|
|Repositório de Certificados do Windows|Armazena CMKs localmente no repositório de chaves do Windows| `MSSQL_CERTIFICATE_STORE`|Windows|

- Você (ou seu DBA) precisa verificar se o nome do provedor, configurado nos metadados da chave mestra de coluna, está correto e se o caminho da chave mestra de coluna está em conformidade com o formato do caminho da chave para o provedor determinado. É recomendável configurar as chaves usando ferramentas como o SQL Server Management Studio, que gera automaticamente os nomes de provedor válidos e os caminhos de chaves ao emitir a instrução [CREATE COLUMN MASTER KEY (Transact-SQL)](../../t-sql/statements/create-column-master-key-transact-sql.md) .

- Você precisa garantir que seu aplicativo possa acessar a chave no repositório de chaves. Isso pode envolver a concessão de acesso para o aplicativo à chave e/ou ao repositório de chaves, dependendo do repositório de chaves, ou a execução de outras etapas de configuração específicas do repositório de chaves. Por exemplo, para acessar um Azure Key Vault, você precisa fornecer as credenciais corretas para o repositório de chaves.

### <a name="using-the-azure-key-vault-provider"></a>Uso do provedor do Azure Key Vault

O AKV (Azure Key Vault) é uma opção conveniente para armazenar e gerenciar chaves mestras de coluna do Always Encrypted (especialmente se seus aplicativos estiverem hospedados no Azure). O ODBC Driver for SQL Server no Linux, macOS e Windows inclui um provedor de repositório de chaves mestras de coluna interno para o Azure Key Vault. Confira [Azure Key Vault: passo a passo](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/), [Introdução ao Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-get-started/) e [Criação de chaves mestras de coluna no Azure Key Vault](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_2) para saber mais sobre como configurar um Azure Key Vault para Always Encrypted.

> [!NOTE]
> O driver ODBC não oferece suporte a Serviços de Federação do Active Directory (AD FS) para autenticação AKV. Se você estiver usando Azure Active Directory autenticação para AKV e sua configuração de Active Directory incluir serviços federados, a autenticação poderá falhar.
> No Linux e macOS, para a versão de driver 17.2 e posterior, `libcurl` é necessário para usar esse provedor, mas não é uma dependência explícita, pois outras operações com o driver não precisam dele. Se você encontrar um erro em relação ao `libcurl`, verifique se ele está instalado.

O driver oferece suporte à autenticação no Azure Key Vault usando os seguintes tipos de credenciais:

- Nome de usuário/senha: com esse método, as credenciais são o nome de um usuário do Azure Active Directory e sua senha.

- ID do cliente/segredo: com esse método, as credenciais são uma ID do cliente do aplicativo e um segredo do aplicativo.

Para permitir que o driver use CMKs armazenadas no AKV para criptografia de coluna, use as seguintes palavras-chave somente de cadeia de conexão:

|Tipo de Credencial| `KeyStoreAuthentication` |`KeyStorePrincipalId`| `KeyStoreSecret` |
|-|-|-|-|
|Nome de usuário/senha| `KeyVaultPassword`|Nome UPN|Senha|
|ID do cliente/segredo| `KeyVaultClientSecret`|ID do Cliente|Segredo|

#### <a name="example-connection-strings"></a>Exemplo de cadeias de conexão

As cadeias de conexão a seguir mostram como autenticar no Azure Key Vault com os dois tipos de credenciais:

**ClientID/Segredo**:

```
DRIVER=ODBC Driver 13 for SQL Server;SERVER=myServer;Trusted_Connection=Yes;DATABASE=myDB;ColumnEncryption=Enabled;KeyStoreAuthentication=KeyVaultClientSecret;KeyStorePrincipalId=<clientId>;KeyStoreSecret=<secret>
```

**Nome de usuário/senha**:

```
DRIVER=ODBC Driver 13 for SQL Server;SERVER=myServer;Trusted_Connection=Yes;DATABASE=myDB;ColumnEncryption=Enabled;KeyStoreAuthentication=KeyVaultPassword;KeyStorePrincipalId=<username>;KeyStoreSecret=<password>
```

Nenhuma outra alteração de aplicativo de ODBC é necessária para usar o AKV para armazenamento de CMK.

### <a name="using-the-windows-certificate-store-provider"></a>Uso do Provedor do Repositório de Certificados do Windows

O ODBC Driver for SQL Server no Windows inclui um provedor de repositório de chaves mestras de coluna interno para o Repositório de Certificados do Windows chamado `MSSQL_CERTIFICATE_STORE`. (Esse provedor não está disponível no macOS ou no Linux.) Com esse provedor, a CMK é armazenada localmente no computador cliente e nenhuma configuração adicional pelo aplicativo é necessária para usá-la com o driver. No entanto, o aplicativo deve ter acesso ao certificado e sua chave privada no repositório. Veja [Criar e armazenar chaves mestras de coluna (Always Encrypted)](https://docs.microsoft.com/sql/relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted).

### <a name="using-custom-keystore-providers"></a>Uso de provedores de repositórios de chaves personalizados

O ODBC Driver for SQL Server também oferece suporte a provedores de repositório de chaves personalizado de terceiros usando a interface CEKeystoreProvider. Isso permite que um aplicativo carregue, faça consultas e configure provedores de repositório de chaves para que possam ser usados pelo driver para acessar colunas criptografadas. Os aplicativos podem ainda interagir diretamente com um provedor de repositório de chaves para criptografar CEKs para armazenamento no SQL Server e executar tarefas além de acessar colunas criptografadas com o ODBC. Para saber mais, confira [Provedores de repositório de chaves personalizados](../../connect/odbc/custom-keystore-providers.md).

Dois atributos de conexão são usados para interagir com provedores de armazenamento de chaves personalizados. São eles:

- `SQL_COPT_SS_CEKEYSTOREPROVIDER`

- `SQL_COPT_SS_CEKEYSTOREDATA`

O primeiro é usado para carregar e enumerar os provedores de repositório de chaves carregados, enquanto o segundo permite a comunicação entre provedor e aplicativo. Esses atributos de conexão podem ser usados a qualquer momento, antes ou depois de estabelecer uma conexão, desde que a interação entre provedor e aplicativo não envolva a comunicação com o SQL Server. No entanto, uma vez que o driver não foi carregado ainda, configurar e obter esses atributos antes de conectar fará com que eles sejam processados pelo Gerenciador de Driver, e podem não produzir os resultados esperados.

#### <a name="loading-a-keystore-provider"></a>Carregar um provedor de repositório de chaves

Definir o atributo de conexão `SQL_COPT_SS_CEKEYSTOREPROVIDER` possibilita que um aplicativo cliente carregue uma biblioteca de provedor, tornando disponíveis para uso os provedores de repositório de chaves contidos nela.

```
SQLRETURN SQLSetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER StringLength);
```

| Argumento | Descrição |
|:---|:---|
|`ConnectionHandle`|[Entrada] Identificador de conexão. Deve ser um identificador de conexão válido, mas provedores carregados por meio de um identificador de conexão são acessíveis de qualquer outro no mesmo processo.|
|`Attribute`|[Entrada] Atributo a ser definido: a constante `SQL_COPT_SS_CEKEYSTOREPROVIDER`.|
|`ValuePtr`|[Entrada] Ponteiro para uma cadeia de caracteres terminada em nulo que especifica o nome do arquivo da biblioteca do provedor. Para SQLSetConnectAttrA, é uma cadeia de caracteres ANSI (multibyte). Para SQLSetConnectAttrW, é uma cadeia de caracteres Unicode (wchar_t).|
|`StringLength`|[Entrada] O comprimento da cadeia de caracteres ValuePtr, ou SQL_NTS.|

O driver tenta carregar a biblioteca identificada pelo parâmetro ValuePtr usando o mecanismo de carregamento de biblioteca dinâmica definido pela plataforma (`dlopen()` no Linux e macOS, `LoadLibrary()` no Windows), e adiciona quaisquer provedores definidos à lista de provedores conhecidos para o driver. Podem ocorrer os seguintes erros:

| Erro | Descrição |
|:--|:--|
|`CE203`|Não foi possível carregar a biblioteca dinâmica.|
|`CE203`|O símbolo exportado de "CEKeyStoreProvider" não foi encontrado na biblioteca.|
|`CE203`|Um ou mais provedores da biblioteca já estão carregados.|

`SQLSetConnectAttr` retorna o erro ou valores de êxito comuns, e informações adicionais estão disponíveis para quaisquer erros que ocorreram por meio do mecanismo de diagnóstico padrão de ODBC.

> [!NOTE]
> O programador do aplicativo deve garantir que quaisquer provedores personalizados sejam carregados antes de qualquer consulta que exija o envio deles por uma conexão. Não fazer isso resultará no erro:

| Erro | Descrição |
|:--|:--|
|`CE200`|Provedor do repositório de chaves %1 não encontrado. Verifique se a biblioteca do provedor do repositório de chaves adequada foi carregada.|

> [!NOTE]
> Os implementadores do provedor do repositório de chaves devem evitar usar `MSSQL` no nome de seus provedores personalizados. Esse termo é reservado exclusivamente para uso da Microsoft e pode causar conflitos com futuros provedores internos. Usar esse termo no nome de um provedor personalizado pode gerar um aviso do ODBC.

#### <a name="getting-the-list-of-loaded-providers"></a>Obter a lista de provedores carregados

Obter este atributo de conexão permite que um aplicativo cliente determine os provedores de repositório de chaves atualmente carregados no driver (incluindo os internos). Isso só pode ser executado após a conexão.

```
SQLRETURN SQLGetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER BufferLength, SQLINTEGER * StringLengthPtr);
```

| Argumento | Descrição |
|:---|:---|
|`ConnectionHandle`|[Entrada] Identificador de conexão. Deve ser um identificador de conexão válido, mas provedores carregados por meio de um identificador de conexão são acessíveis de qualquer outro no mesmo processo.|
|`Attribute`|[Entrada] Atributo a ser recuperado: a constante `SQL_COPT_SS_CEKEYSTOREPROVIDER`.|
|`ValuePtr`|[Saída] Um ponteiro para a memória no qual se deve retornar o nome do próximo provedor carregado.|
|`BufferLength`|[Entrada] O comprimento do buffer ValuePtr.|
|`StringLengthPtr`|[Saída] Um ponteiro para um buffer no qual se deve retornar o número total de bytes (exceto o caractere de terminação nula) disponível para retornar em \*ValuePtr. Se ValuePtr for um ponteiro nulo, nenhum comprimento retorna. Se o valor do atributo é uma cadeia de caracteres e o número de bytes disponível para retornar é maior que BufferLength menos o comprimento do caractere de terminação nula, os dados em \*ValuePtr são truncados para BufferLength menos o comprimento do caractere de terminação nula; em seguida, os dados são terminados em nulo pelo driver.|

Para permitir recuperar a lista inteira, todas as operações Get retornam o nome do provedor atual e incrementam um contador interno para o próximo. Depois que esse contador atinge o final da lista, uma cadeia de caracteres vazia ("") retorna, e o contador é redefinido. Operações Get sucessivas continuam, então, novamente desde o início da lista.

### <a name="communicating-with-keystore-providers"></a>Comunicação com provedores de repositório de chaves

O atributo de conexão `SQL_COPT_SS_CEKEYSTOREDATA` permite que um aplicativo cliente se comunique com provedores do repositório de chaves carregados para configurar outros parâmetros, material de criação de chaves, etc. A comunicação entre um aplicativo cliente e um provedor segue um protocolo simples de solicitação e resposta, com base em solicitações Get e Set, utilizando esse atributo de conexão. A comunicação é iniciada somente pelo aplicativo cliente.

> [!NOTE]
> Devido à natureza das chamadas de ODBC às quais CEKeyStoreProvider responde (SQLGet/SetConnectAttr), a interface do ODBC oferece suporte somente à configuração de dados com a resolução do contexto de conexão.

O aplicativo comunica-se com provedores de repositório de chaves por meio do driver e através da estrutura de CEKeystoreData:

```
typedef struct CEKeystoreData {
wchar_t *name;
unsigned int dataSize;
char data[];
} CEKEYSTOREDATA;
```

| Argumento | Descrição |
|:---|:---|
|`name`|[Entrada] Após Set, o nome do provedor para o qual os dados são enviados. Ignorado após Get. Cadeia de caracteres largos terminada em nulo.|
|`dataSize`|[Entrada] O tamanho da matriz de dados seguindo a estrutura.|
|`data`|[Entrada/saída] Após Set, os dados a serem enviados para o provedor. Podem ser dados arbitrários. O driver não faz nenhuma tentativa de interpretá-los. Após Get, o buffer para receber os dados lidos do provedor.|

#### <a name="writing-data-to-a-provider"></a>Gravar dados em um provedor

Uma chamada `SQLSetConnectAttr` usando o atributo `SQL_COPT_SS_CEKEYSTOREDATA` grava um "pacote" de dados em um provedor de repositório de chaves especificado.
```
SQLRETURN SQLSetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER StringLength);
```

| Argumento | Descrição |
|:---|:---|
|`ConnectionHandle`| [Entrada] Identificador de conexão. Deve ser um identificador de conexão válido, mas provedores carregados por meio de um identificador de conexão são acessíveis de qualquer outro no mesmo processo.|
|`Attribute`|[Entrada] Atributo a ser definido: a constante `SQL_COPT_SS_CEKEYSTOREDATA`.|
|`ValuePtr`|[Entrada] Ponteiro para uma estrutura CEKeystoreData. O campo de nome da estrutura identifica o provedor para o qual os dados são destinados.|
|`StringLength`|[Entrada] Constante SQL_IS_POINTER|

É possível obter informações de erro mais detalhadas com [SQLGetDiacRec](https://msdn.microsoft.com/library/ms710921(v=vs.85).aspx).

> [!NOTE]
> O provedor pode usar o identificador de conexão para associar os dados gravados a uma conexão específica, se desejado. Isso é útil para implementar a configuração por conexão. Ele também pode ignorar o contexto de conexão e tratar os dados de forma idêntica, independentemente da conexão usada para enviar os dados. Confira [Associação de contexto](../../connect/odbc/custom-keystore-providers.md#context-association) para saber mais.

#### <a name="reading-data-from-a-provider"></a>Ler dados de um provedor

Uma chamada para `SQLGetConnectAttr` usando o atributo `SQL_COPT_SS_CEKEYSTOREDATA` lê um "pacote" de dados do provedor *em que foi gravado por último*. Se não houver nenhum, ocorre um erro de sequência de função. Recomendamos que os implementadores do provedor de repositório de chaves ofereçam suporte a "gravações fictícias" de 0 bytes como uma maneira de selecionar o provedor para operações de leitura sem causar outros efeitos colaterais.

```
SQLRETURN SQLGetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER BufferLength, SQLINTEGER * StringLengthPtr);
```

| Argumento | Descrição |
|:---|:---|
|`ConnectionHandle`|[Entrada] Identificador de conexão. Deve ser um identificador de conexão válido, mas provedores carregados por meio de um identificador de conexão são acessíveis de qualquer outro no mesmo processo.|
|`Attribute`|[Entrada] Atributo a ser recuperado: a constante `SQL_COPT_SS_CEKEYSTOREDATA`.|
|`ValuePtr`|[Saída] Um ponteiro para uma estrutura CEKeystoreData na qual é colocada a leitura do provedor de dados.|
|`BufferLength`|[Entrada] Constante SQL_IS_POINTER|
|`StringLengthPtr`|[Saída] Um ponteiro para um buffer no qual retornar BufferLength. Se *ValuePtr for um ponteiro nulo, nenhum comprimento será retornado.|

O chamador deve garantir que um buffer de comprimento suficiente seguindo a estrutura CEKEYSTOREDATA está alocado para o provedor fazer gravações. Após o retorno, seu campo dataSize é atualizado com o comprimento real dos dados lidos do provedor. É possível obter informações de erro mais detalhadas com [SQLGetDiacRec](https://msdn.microsoft.com/library/ms710921(v=vs.85).aspx).

Essa interface não exige requisitos adicionais sobre o formato dos dados transferidos entre um aplicativo e um provedor de repositório de chaves. Cada provedor pode definir seu próprio formato de dados/protocolo, dependendo das suas necessidades.

Para obter um exemplo de implementação de seu próprio provedor de repositório de chaves, confira [Provedores de repositório de chaves personalizados](../../connect/odbc/custom-keystore-providers.md)

## <a name="limitations-of-the-odbc-driver-when-using-always-encrypted"></a>Limitações do driver ODBC ao usar o Always Encrypted

### <a name="asynchronous-operations"></a>Operações assíncronas
Embora o driver ODBC permita o uso de [operações assíncronas](../../relational-databases/native-client/odbc/creating-a-driver-application-asynchronous-mode-and-sqlcancel.md) com o Always Encrypted, há um impacto no desempenho das operações quando o Always Encrypted está habilitado. A chamada para `sys.sp_describe_parameter_encryption` para determinar os metadados de criptografia para a instrução está bloqueando e fará com que o driver aguarde o servidor retornar os metadados antes de retornar `SQL_STILL_EXECUTING`.

### <a name="retrieve-data-in-parts-with-sqlgetdata"></a>Recuperar dados em partes com SQLGetData
Não é possível recuperar caracteres criptografados e colunas binárias em partes com o SQLGetData, antes de implantar o ODBC Driver 17 for SQL Server. É possível fazer apenas uma chamada para o SQLGetData com um buffer de comprimento adequado para incluir os dados da coluna inteira.

### <a name="send-data-in-parts-with-sqlputdata"></a>Enviar dados em partes com SQLPutData
Antes do ODBC Driver 17.3 for SQL Server, não é possível enviar dados de inserção ou comparação em partes com o SQLPutData. É possível fazer apenas uma chamada para o SQLPutData com um buffer contendo os dados completos. Para inserir dados longos em colunas criptografadas, use a API de Cópia em Massa, com um arquivo de dados de entrada, conforme descrito na seção a seguir.

### <a name="encrypted-money-and-smallmoney"></a>Money e smallmoney criptografados
Não é possível direcionar as colunas **money** criptografado ou **smallmoney** por parâmetros, porque não há tipos de dados ODBC específicos que mapeiem para esses tipos, gerando erros de Conflito de tipo de operando.

## <a name="bulk-copy-of-encrypted-columns"></a>Cópia em massa de colunas criptografadas

O uso das [funções de Cópia em Massa do SQL](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md) e do utilitário **bcp** tem suporte com o Always Encrypted, após a implantação do ODBC Driver 17 for SQL Server. O texto não criptografado (criptografado na inserção e descriptografado na recuperação) e o texto cifrado (transmitido textualmente) podem ser inseridos e recuperados por meio das APIs de cópia em massa (bcp_&#42;) e o utilitário **bcp**.

- Para recuperar texto cifrado no formulário varbinary(max) (por exemplo, para carregamento em massa em um banco de dados diferente), conecte-se sem a opção `ColumnEncryption` (ou defina-a como `Disabled`) e execute uma operação BCP OUT.

- Para inserir e recuperar texto não criptografado e permitir que o driver execute criptografia e descriptografia de modo transparente conforme necessário, basta definir `ColumnEncryption` como `Enabled`. Caso contrário, a funcionalidade da API BCP permanece inalterada.

- Para inserir texto cifrado no formulário varbinary(max) (por exemplo, como recuperado acima), defina a opção `BCPMODIFYENCRYPTED` como TRUE e execute uma operação BCP IN. Para descriptografar os dados resultantes, verifique se a CEK da coluna do destino é a mesma da qual o texto cifrado foi originalmente obtido.

Ao usar o utilitário **bcp**: para controlar a configuração `ColumnEncryption`, use a opção -D e especifique um DSN que contenha o valor desejado. Para inserir texto cifrado, verifique se a configuração `ALLOW_ENCRYPTED_VALUE_MODIFICATIONS` do usuário está habilitada.

A tabela a seguir fornece um resumo das ações ao operar em uma coluna criptografada:

|`ColumnEncryption`|Direção BCP|Descrição|
|----------------|-------------|-----------|
|`Disabled`|OUT (para o cliente)|Recupera o texto cifrado. O tipo de dados observado é **varbinary(max)**.|
|`Enabled`|OUT (para o cliente)|Recupera texto não criptografado. O driver descriptografará os dados da coluna.|
|`Disabled`|IN (para servidor)|Insere o texto cifrado. Destina-se a mover os dados criptografados discretamente sem a necessidade de serem descriptografados. A operação falhará se a opção `ALLOW_ENCRYPTED_VALUE_MODIFICATIONS` não estiver definida no usuário ou se BCPMODIFYENCRYPTED não estiver definido no identificador de conexão. Veja a seguir para obter mais informações.|
|`Enabled`|IN (para servidor)|Insere texto não criptografado. O driver descriptografará os dados da coluna.|

### <a name="the-bcpmodifyencrypted-option"></a>A opção BCPMODIFYENCRYPTED

Para evitar dados corrompidos, o servidor normalmente não permite inserir texto cifrado diretamente em uma coluna criptografada e, portanto, tentar fazer isso gera uma falha. No entanto, para carregamento em massa de dados criptografados usando a API BCP, definir a opção `BCPMODIFYENCRYPTED` [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) como TRUE permite que o texto cifrado seja inserido diretamente e reduz o risco de corromper os dados criptografados pela configuração da opção `ALLOW_ENCRYPTED_VALUE_MODIFICATIONS` na conta de usuário. No entanto, as chaves devem corresponder aos dados, e recomenda-se realizar algumas verificações de somente leitura dos dados inseridos após a inserção em massa e antes de um futuro uso.

Veja [Migrar dados confidenciais protegidos por Always Encrypted](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md) para obter mais informações.

## <a name="always-encrypted-api-summary"></a>Resumo da API do Always Encrypted

### <a name="connection-string-keywords"></a>Palavras-chave de cadeia de conexão

|Nome|Descrição|  
|----------|-----------------|  
|`ColumnEncryption`|Os valores aceitos são `Enabled`/`Disabled`.<br>`Enabled` -- habilita ou desabilita a funcionalidade Always Encrypted para a conexão.<br>`Disabled` -- desabilita a funcionalidade Always Encrypted para a conexão.<br>*o tipo*, *de dados*--(versão 17,4 e posterior) habilita Always Encrypted com o Secure enclave and atestado Protocol *Type*e dados de atestado associados *data*. <br><br>O padrão é `Disabled`.|
|`KeyStoreAuthentication` | Valores válidos: `KeyVaultPassword`, `KeyVaultClientSecret` |
|`KeyStorePrincipalId` | Quando `KeyStoreAuthentication` = `KeyVaultPassword`, defina este valor como um nome UPN válido do Azure Active Directory. <br>Quando `KeyStoreAuthetication` = `KeyVaultClientSecret`, defina este valor como uma ID de cliente válida do Azure Active Directory. |
|`KeyStoreSecret` | Quando `KeyStoreAuthentication` = `KeyVaultPassword`, defina este valor como a senha para o nome de usuário correspondente. <br>Quando `KeyStoreAuthentication` = `KeyVaultClientSecret`, defina este valor como o segredo do aplicativo associado a uma ID do cliente do aplicativo válida do Azure Active Directory. |


### <a name="connection-attributes"></a>Atributos de conexão

|Nome|Tipo|Descrição|  
|----------|-------|----------|  
|`SQL_COPT_SS_COLUMN_ENCRYPTION`|Antes de conectar-se|`SQL_COLUMN_ENCRYPTION_DISABLE` (0): desabilitar o Always Encrypted <br>`SQL_COLUMN_ENCRYPTION_ENABLE` (1): habilitar o Always Encrypted<br> Ponteiro para *tipo*,*dados* cadeia de caracteres--(versão 17,4 e posterior) habilitar com Secure enclave|
|`SQL_COPT_SS_CEKEYSTOREPROVIDER`|Após conectar-se|[Set] Tentativa de carregar CEKeystoreProvider<br>[Get] Retorna um nome de CEKeystoreProvider|
|`SQL_COPT_SS_CEKEYSTOREDATA`|Após conectar-se|[Set] Gravar dados em CEKeystoreProvider<br>[Set] Ler dados de CEKeystoreProvider|
|`SQL_COPT_SS_CEKCACHETTL`|Após conectar-se|[Set] Definir o TTL do cache da CEK<br>[Get] Obter o TTL do cache da CEK atual|
|`SQL_COPT_SS_TRUSTEDCMKPATHS`|Após conectar-se|[Set] Definir o ponteiro de caminhos de CMK confiável<br>[Get] Obter o ponteiro de caminhos de CMK confiável atual|

### <a name="statement-attributes"></a>Atributos de instrução

|Nome|Descrição|  
|----------|-----------------|  
|`SQL_SOPT_SS_COLUMN_ENCRYPTION`|`SQL_CE_DISABLED` (0): o Always Encrypted é desabilitado para a instrução <br>`SQL_CE_RESULTSETONLY` (1): apenas descriptografia. Conjuntos de resultados e valores de retorno estão descriptografados, e parâmetros não estão criptografados <br>`SQL_CE_ENABLED` (3): o Always Encrypted está habilitado e é usado para parâmetros e resultados|

### <a name="descriptor-fields"></a>Campos de descritor

|Campo IPD|Tamanho/tipo|Valor Padrão|Descrição|
|-|-|-|-|  
|`SQL_CA_SS_FORCE_ENCRYPT` (1236)|WORD (2 bytes)|0|Quando 0 (padrão): a decisão de criptografar esse parâmetro é determinada pela disponibilidade de metadados de criptografia.<br><br>Quando for diferente de zero: se os metadados de criptografia estão disponíveis para esse parâmetro, eles são criptografados. Caso contrário, a solicitação falha com erro [CE300] [Microsoft][ODBC Driver 13 for SQL Server]A criptografia obrigatória foi especificada para um parâmetro, mas nenhum metadado de criptografia foi fornecido pelo servidor.|

### <a name="bcp_control-options"></a>Opções bcp_control

|Nome da opção|Valor Padrão|Descrição|
|-|-|-|
|`BCPMODIFYENCRYPTED` (21)|FALSE|Quando TRUE, permite que valores varbinary(max) sejam inseridos em uma coluna criptografada. Quando FALSE, evita a inserção, a menos que o tipo e os metadados de criptografia corretos sejam fornecidos.|

## <a name="see-also"></a>Consulte Também

- [Always Encrypted (mecanismo de banco de dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted com enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves.md)
- [Blog do Always Encrypted](https://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)
