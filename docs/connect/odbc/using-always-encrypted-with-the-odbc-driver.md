---
title: Use sempre criptografado com o ODBC Driver 13.1 para SQL Server | Microsoft Docs
ms.custom: 
ms.date: 07/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 02e306b8-9dde-4846-8d64-c528e2ffe479
caps.latest.revision: 3
ms.author: v-chojas
manager: jhubbard
author: MightyPen
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: d28b647de71c5064dfbe0d49f399119f6a9ac283
ms.contentlocale: pt-br
ms.lasthandoff: 09/27/2017

---
# <a name="using-always-encrypted-with-the-odbc-driver-131-for-sql-server"></a>Use sempre criptografado com o ODBC Driver 13.1 para SQL Server
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

Este artigo fornece informações sobre como desenvolver aplicativos de ODBC usando [sempre criptografados (mecanismo de banco de dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) e [ODBC Driver 13.1 para SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md).

O Always Encrypted permite que os aplicativos cliente criptografem dados confidenciais e nunca revelem os dados nem as chaves de criptografia para o SQL Server ou o Banco de Dados SQL do Azure. Um sempre criptografado habilitado driver, como o ODBC Driver 13.1 para SQL Server, consegue isso criptografando e descriptografando dados confidenciais no aplicativo cliente de forma transparente. O driver determina automaticamente quais parâmetros de consulta correspondem às colunas de banco de dados confidenciais (protegidas com o Always Encrypted) e criptografa os valores desses parâmetros antes de passar os dados para o SQL Server ou o Banco de Dados SQL do Azure. Da mesma forma, o driver descriptografa de modo transparente os dados recuperados das colunas de banco de dados criptografadas nos resultados da consulta. Para obter mais informações, veja [Always Encrypted (Mecanismo de Banco de Dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md).

### <a name="prerequisites"></a>Pré-requisitos

Configure o Sempre Criptografado em seu banco de dados. Isso envolve o provisionamento de chaves do Sempre Criptografado e a configuração de criptografia de colunas de banco de dados selecionadas. Se você ainda não tiver um banco de dados com o Sempre Criptografado configurado, siga as instruções em [Getting Started with Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted)(Introdução ao Sempre Criptografado). Em particular, o banco de dados deve conter as definições de metadados para uma chave mestra de coluna (CMK), uma chave de criptografia de coluna (CEK) e uma tabela contendo uma ou mais colunas criptografadas usando essa CEK.

### <a name="enabling-always-encrypted-in-an-odbc-application"></a>Habilitando sempre criptografado em um aplicativo ODBC

A maneira mais fácil para habilitar o parâmetro criptografia e descriptografia de coluna resultset criptografado está definindo o valor da `ColumnEncryption` palavra-chave de cadeia de caracteres de conexão para **habilitado**. Este é um exemplo de uma cadeia de caracteres de conexão que habilita o sempre criptografado:

```
SQLWCHAR *connString = L"Driver={ODBC Driver 13 for SQL Server};Server={myServer};Trusted_Connection=yes;ColumnEncryption=Enabled;";
```

Sempre criptografado pode também ser habilitado na configuração de DSN, usando a mesma chave e valor (que será substituído pela configuração de cadeia de caracteres de conexão, se presente) ou por meio de programação com o `SQL_COPT_SS_COLUMN_ENCRYPTION` atributo da conexão. Definir o valor dessa maneira substitui o valor definido na cadeia de caracteres de conexão ou DSN:

```
 SQLSetConnectAttr(hdbc, SQL_COPT_SS_COLUMN_ENCRYPTION, (SQLPOINTER)SQL_COLUMN_ENCRYPTION_ENABLE, 0);
```

Uma vez habilitada para a conexão, o comportamento do sempre criptografado pode ser ajustado para consultas individuais. Consulte [controlando o desempenho do impacto do sempre criptografado](#controlling-the-performance-impact-of-always-encrypted) abaixo para obter mais informações.

Observe que não é suficiente para a criptografia ou descriptografia tenha êxito; habilitando sempre criptografado Você também precisa garantir que:

- O aplicativo tem as permissões de banco de dados *VIEW ANY COLUMN MASTER KEY DEFINITION* e *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* , necessárias para acessar os metadados sobre as chaves do Always Encrypted no banco de dados. Para obter detalhes, consulte [permissões de banco de dados](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions).

- O aplicativo pode acessar a CMK que protege os CEKs para as colunas criptografadas consultadas. Isso é depende do provedor de armazenamento de chaves que armazena a CMK. Consulte [trabalhando com repositórios de chaves mestras de coluna](#working-with-column-master-key-stores) para obter mais informações.

### <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>Recuperando e modificando dados em colunas criptografadas

Depois de habilitar o sempre criptografado em uma conexão, você pode usar APIs ODBC padrão (consulte [código de exemplo do ODBC](https://code.msdn.microsoft.com/windowsapps/ODBC-sample-191624ae/sourcecode?fileId=51137&pathId=1980325953) ou [referência do programador de ODBC](https://msdn.microsoft.com/library/ms714177(v=vs.85).aspx)) para recuperar ou modificar dados em colunas de banco de dados criptografado. Supondo que seu aplicativo tenha as permissões de banco de dados e pode acessar a chave mestra de coluna, o driver criptografará quaisquer parâmetros de consulta que se destinam a colunas criptografadas e descriptografar os dados recuperados de colunas criptografadas, se comportar de forma transparente para o aplicativos como se as colunas não foram criptografadas.

Se o sempre criptografado não estiver habilitado, consultas com parâmetros que se destinam a colunas criptografadas falharão. Dados ainda podem ser recuperados de colunas criptografadas, desde que a consulta não tem parâmetros destinam a colunas criptografadas. No entanto, o driver não tentará qualquer descriptografia e o aplicativo receberá os dados binários criptografados (como matrizes de bytes).

A tabela a seguir resume o comportamento das consultas, dependendo se sempre criptografado está habilitado ou não:

|Característica da consulta | O Sempre Criptografado está habilitado e o aplicativo pode acessar as chaves e os metadados da chave|O Sempre Criptografado está habilitado e o aplicativo não pode acessar as chaves nem os metadados da chave | O Sempre Criptografado está desabilitado|
|:---|:---|:---|:---|
| Parâmetros que se destinam a colunas criptografadas. | Os valores de parâmetro são criptografados de modo transparente. | Erro | Erro|
| Recuperando dados de colunas criptografadas, sem parâmetros que se destinam a colunas criptografadas.| Os resultados das colunas criptografadas são descriptografados de modo transparente. O aplicativo recebe valores de coluna de texto sem formatação. | Erro | Os resultados das colunas criptografadas não são descriptografados. O aplicativo recebe valores criptografados como matrizes de bytes.

Os exemplos a seguir ilustram como recuperar e modificar dados em colunas criptografadas. Os exemplos assumem uma tabela com o esquema a seguir. Observe que as colunas SSN e BirthDate estão criptografadas.

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

- Não há nada específico de criptografia no código de exemplo. O driver detecta automaticamente e criptografa os valores dos parâmetros de SSN e data, que se destinam a colunas criptografadas. Isso torna a criptografia transparente para o aplicativo.

- Os valores inseridos em colunas de banco de dados, incluindo as colunas criptografadas, são passados como parâmetros associados (consulte [função SQLBindParameter](https://msdn.microsoft.com/library/ms710963(v=vs.85).aspx)). Embora o uso de parâmetros é opcional ao enviar valores para colunas não criptografadas (embora é altamente recomendado, pois ajuda a prevenir a injeção de SQL), é necessário para valores que se destinam a colunas criptografadas. Se os valores inseridos nas colunas SSN ou BirthDate fossem passados como literais inseridos na instrução de consulta, a consulta falhará porque o driver não tentará criptografar ou processar literais em consultas. Como resultado, o servidor os rejeitaria como incompatíveis com as colunas criptografadas.

- O tipo SQL do parâmetro inserido na coluna SSN é definido como SQL_CHAR, que mapeia para o **char** tipo de dados do SQL Server (`rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 11, 0, (SQLPOINTER)SSN, 0, &cbSSN);`). Se o tipo do parâmetro foi definido como SQL_WCHAR, que é mapeada para **nchar**, a consulta falhará, pois sempre criptografado não oferece suporte conversões do lado do servidor de valores nchar criptografados em valores criptografados char. Consulte [referência do programador de ODBC - tipos de dados do apêndice d:](https://msdn.microsoft.com/library/ms713607.aspx) para obter informações sobre os mapeamentos de tipo de dados.

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

#### <a name="plaintext-data-retrieval-example"></a>Exemplo de recuperação de dados de texto sem formatação

O exemplo a seguir demonstra a filtragem de dados com base em valores criptografados e a recuperação de dados de texto sem formatação de colunas criptografadas. Observe o seguinte:

- O valor usado na cláusula WHERE para filtrar a coluna SSN precisa ser passado com SQLBindParameter, para que o driver transparentemente pode criptografá-lo antes de enviá-la para o servidor.

- Todos os valores impressos pelo programa será em texto não criptografado, pois o driver descriptografará de modo transparente os dados recuperados das colunas SSN e BirthDate.

> [!NOTE]
> Consultas podem executar comparações de igualdade em colunas criptografadas, somente se a criptografia é determinística. Para obter mais informações, consulte [criptografia selecionando determinística ou aleatória](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption).

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

Esta seção descreve as categorias de erros comuns ao consultar colunas criptografadas de aplicativos de ODBC e algumas diretrizes sobre como evitá-los.

##### <a name="unsupported-data-type-conversion-errors"></a>Erros de conversão de tipo de dados sem suporte

O Always Encrypted dá suporte a algumas conversões de tipos de dados criptografados. Consulte [sempre criptografados (mecanismo de banco de dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) para a lista detalhada de conversões de tipo com suporte. Para evitar erros de conversão de tipo de dados, certifique-se de que você observar os seguintes pontos ao usar SQLBindParameter com parâmetros que se destinam a colunas criptografadas:

- O tipo SQL do parâmetro é exatamente o mesmo que o tipo da coluna de destino ou a conversão do tipo SQL para o tipo da coluna é suportada.

- A precisão e escala de parâmetros que se destinam a colunas do `decimal` e `numeric` tipos de dados do SQL Server é o mesmo que a precisão e escala configuradas para a coluna de destino.

- A precisão de parâmetros que se destinam a colunas de `datetime2`, `datetimeoffset`, ou `time` tipos de dados do SQL Server não é maior do que a precisão da coluna de destino, em consultas que modificam a coluna de destino.  

##### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>Erros devido à passagem de texto sem formatação em vez de valores criptografados

Qualquer valor que tem como alvo uma coluna criptografada precisa ser criptografado antes de serem enviados ao servidor. Uma tentativa de inserir, modificar ou filtrar por um valor de texto sem formatação em uma coluna criptografada resultará em erro. Para evitar esses erros, verifique se:

- Sempre criptografado está habilitado (no DSN, a cadeia de caracteres de conexão, conectando antes, definindo o `SQL_COPT_SS_COLUMN_ENCRYPTION` atributo de conexão para uma conexão específica, ou o `SQL_SOPT_SS_COLUMN_ENCRYPTION` atributo da instrução para uma instrução específica).

- Você pode usar SQLBindParameter para enviar dados visando colunas criptografadas. O exemplo a seguir mostra uma consulta que filtra incorretamente por uma literal ou uma constante em uma coluna criptografada (SSN), em vez de passar o literal como um argumento para SQLBindParameter.

```
string queryText = "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
```

### <a name="precautions-when-using-sqlsetpos-and-sqlmoreresults"></a>Precauções ao usar SQLSetPos e SQLMoreResults

#### <a name="sqlsetpos"></a>SQLSetPos

O `SQLSetPos` API permite que um aplicativo atualizar linhas em um conjunto de resultados usando buffers que foram associadas SQLBindCol e em qual linha de dados foi obtidos anteriormente. Devido ao comportamento de preenchimento assimétrica dos tipos de comprimento fixo criptografados, é possível inesperadamente alterar os dados dessas colunas ao executar atualizações em outras colunas na linha. Valores de caracteres de comprimento fixo com AE, serão preenchidos se o valor for menor do que o tamanho do buffer.

Para atenuar esse comportamento, use o `SQL_COLUMN_IGNORE` sinalizador para ignorar colunas que não serão atualizadas como parte do `SQLBulkOperations` e ao usar `SQLSetPos` de cursor com base em atualizações.  Todas as colunas que não estão sendo modificadas diretamente pelo aplicativo devem ser ignoradas, tanto para desempenho e evitar o truncamento de colunas que estão associadas a um buffer *menor* além do tamanho real (DB). Para obter mais informações, consulte [referência de função SQLSetPos](https://msdn.microsoft.com/library/ms713507(v=vs.85).aspx).

#### <a name="sqlmoreresults--sqldescribecol"></a>SQLMoreResults & SQLDescribeCol

Os aplicativos podem chamar [SQLDescribeCol](https://msdn.microsoft.com/library/ms716289(v=vs.85).aspx) para retornar metadados sobre colunas em instruções preparadas.  Quando sempre criptografado está habilitado, chamando `SQLMoreResults` *antes de* chamando `SQLDescribeCol` faz com que [sp_describe_first_result_set](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) para ser chamado, que não retorna corretamente o texto não criptografado metadados de colunas criptografadas. Para evitar esse problema, chame `SQLDescribeCol` em instruções preparadas *antes de* chamando `SQLMoreResults`.

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>Controlando o impacto no desempenho do sempre criptografado

Como sempre criptografado é uma tecnologia de criptografia do lado do cliente, a maioria da sobrecarga de desempenho é observada no lado do cliente, não no banco de dados. Além do custo de operações de criptografia e descriptografia, as outras fontes de desempenho sobrecarga no lado do cliente são:

- Viagens de ida e volta adicionais ao banco de dados para recuperar metadados dos parâmetros de consulta.

- Chamadas a um repositório de chaves mestras de coluna para acessar uma chave mestra de coluna.

Esta seção descreve as otimizações de desempenho internas no ODBC Driver 13.1 para SQL Server e como você pode controlar o impacto de dois fatores acima no desempenho.

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>Controle de ida e volta para recuperar metadados para parâmetros de consulta

Se o sempre criptografado está habilitado para uma conexão, o ODBC Driver 13.1 para SQL Server, por padrão, chame [sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) para cada consulta parametrizada, passando a instrução de consulta (sem nenhum parâmetro os valores) para o SQL Server. Esse procedimento armazenado analisa a instrução de consulta para descobrir se os parâmetros precisam ser criptografados e nesse caso, retorna as informações relacionadas à criptografia para cada parâmetro para permitir que o driver para criptografá-los. O comportamento acima garante um alto nível de transparência para o aplicativo cliente: O aplicativo (e o desenvolvedor do aplicativo) não precisam estar ciente de quais consultas acessam colunas criptografadas, desde que os valores que se destinam a colunas criptografadas sejam passados para o driver em parâmetros.

### <a name="per-statement-always-encrypted-behavior"></a>Por instrução sempre criptografado comportamento

Para controlar o impacto no desempenho de recuperação de metadados de criptografia para consultas parametrizadas, você pode alterar o comportamento do sempre criptografado para consultas individuais se ele tiver sido habilitado na conexão. Dessa forma, você pode garantir que `sys.sp_describe_parameter_encryption` é invocado apenas para consultas que você sabe que têm parâmetros que se destinam a colunas criptografadas. No entanto, observe que ao fazer isso, você reduzirá a transparência da criptografia: se você criptografar colunas adicionais no banco de dados, talvez seja necessário alterar o código do seu aplicativo para alinhá-lo com as alterações de esquema.

Para controlar o comportamento do sempre criptografado de uma instrução, chame SQLSetStmtAttr para definir o `SQL_SOPT_SS_COLUMN_ENCRYPTION` atributo da instrução para um dos seguintes valores:

|Valor|Description|
|-|-|
|`SQL_CE_DISABLED` (0)|Sempre criptografado está desabilitado para a instrução|
|`SQL_CE_RESULTSETONLY` (1)|Descriptografia. Conjuntos de resultados e valores de retorno são descriptografados e parâmetros não são criptografados.|
|`SQL_CE_ENABLED` (3) | Sempre criptografado está habilitado e usado para parâmetros e resultados|

Novos identificadores de instrução criados a partir de uma conexão com o sempre criptografado habilitado SQL_CE_ENABLED como padrão. Criado de uma conexão com ele desabilitado padrão para SQL_CE_DISABLED (e não é possível habilitar o sempre criptografado neles.)

Se a maioria das consultas de um aplicativo cliente acessa colunas criptografadas, é recomendável o seguinte:

- Definir o `ColumnEncryption` palavra-chave de cadeia de caracteres de conexão para `Enabled`.

- Definir o `SQL_SOPT_SS_COLUMN_ENCRYPTION` atributo `SQL_CE_DISABLED` em instruções que não acessam colunas criptografadas. Isso desabilitará os dois chamada `sys.sp_describe_parameter_encryption` , bem como tenta descriptografar todos os valores no resultado definido.
    
- Definir o `SQL_SOPT_SS_COLUMN_ENCRYPTION` atributo `SQL_CE_RESULTSETONLY` em instruções que não têm qualquer parâmetro que exija criptografia, mas recuperam dados de colunas criptografadas. Isso desabilitará a chamada `sys.sp_describe_parameter_encryption` e criptografia de parâmetros. Resultados contendo colunas criptografadas continuará a ser descriptografado.

## <a name="always-encrypted-security-settings"></a>Sempre criptografado configurações de segurança

### <a name="force-column-encryption"></a>Forçar criptografia de coluna

Para impor a criptografia de um parâmetro, defina o `SQL_CA_SS_FORCE_ENCRYPT` campo do descritor de parâmetro de implementação (IPD) por meio de uma chamada para a função SQLSetDescField. Um valor diferente de zero faz com que o driver retornará um erro quando não há metadados de criptografia é retornado para o parâmetro associado.

```
SQLHDESC ipd;
SQLGetStmtAttr(hStmt, SQL_ATTR_IMP_PARAM_DESC, &ipd, 0, 0);
SQLSetDescField(ipd, paramNum, SQL_CA_SS_FORCE_ENCRYPT, (SQLPOINTER)TRUE, SQL_IS_SMALLINT);   
```

Se o SQL Server informar o driver que o parâmetro não precisam ser criptografados, consultas que usam esse parâmetro falhará. Isso fornece proteção adicional contra ataques de segurança que envolvem um SQL Server comprometido fornecendo metadados de criptografia incorretos ao cliente, o que pode levar à divulgação de dados.

### <a name="column-encryption-key-caching"></a>Cache de chave de criptografia de coluna

Para reduzir o número de chamadas para um repositório de chaves mestras de coluna para descriptografar as chaves de criptografia de coluna, o driver armazena em cache o CEKs texto não criptografado na memória. Depois de receber o ECEK dos metadados do banco de dados, o driver primeiro tenta localizar o texto sem formatação CEK correspondente ao valor de chave criptografado no cache. O driver chama o repositório de chaves que contém a CMK apenas se não é possível localizar o texto não criptografado correspondente CEK no cache.

> [!NOTE]
> Em ODBC Driver 13.1 para SQL Server, as entradas no cache são removidas após um tempo limite de duas horas. Isso significa que, para um determinado ECEK, o driver contata o repositório de chaves apenas uma vez durante o tempo de vida do aplicativo ou a cada duas horas, o que for menor.

## <a name="working-with-column-master-key-stores"></a>Trabalhando com repositórios de chaves mestras de coluna

Para criptografar ou descriptografar dados, o driver precisa obter uma CEK que está configurada para a coluna de destino. CEKs são armazenadas em formato criptografado (ECEKs) nos metadados do banco de dados. Cada CEK tem uma CMK correspondente que foi usada para criptografá-lo. O [metadados de banco de dados](../../t-sql/statements/create-column-master-key-transact-sql.md) não armazena a CMK; ele contém apenas o nome do repositório de chaves e informações de que o armazenamento de chaves pode usar para localizar a CMK.

Para obter o valor de texto sem formatação de um ECEK, o driver primeiro obtém os metadados sobre a CEK e seu CMK correspondente, e, em seguida, usa essas informações para entrar em contato com o armazenamento de chaves que contém a CMK e solicitações para descriptografar o ECEK. O driver se comunica com um armazenamento de chaves usando um provedor de armazenamento de chaves.

### <a name="built-in-keystore-providers"></a>Provedores de repositório de chave

O ODBC Driver 13.1 para SQL Server é fornecido com os seguintes provedores de repositório de chave:

| Nome | Description | Nome do provedor (metadados) |Disponibilidade|
|:---|:---|:---|:---|
|Cofre de Chave do Azure |Armazenamento de CMKs em um cofre de chaves do Azure | `AZURE_KEY_VAULT` |Windows, macOS, Linux|
|Repositório de certificados do Windows|Armazena CMKs localmente no armazenamento de chaves do Windows| `MSSQL_CERTIFICATE_STORE`|Windows|

- Você (ou seu DBA) precisa certificar-se de que o nome do provedor, configurado nos metadados de chave mestra de coluna, está correto e o caminho da chave mestra de coluna está em conformidade com o formato do caminho da chave para o provedor especificado. É recomendável configurar as chaves usando ferramentas como o SQL Server Management Studio, que gera automaticamente os nomes de provedor válidos e os caminhos de chaves ao emitir a instrução [CREATE COLUMN MASTER KEY (Transact-SQL)](../../t-sql/statements/create-column-master-key-transact-sql.md) .

- Você precisa garantir que seu aplicativo pode acessar a chave no armazenamento de chaves. Isso pode envolver a concessão de acesso ao seu aplicativo para a chave e/ou o armazenamento de chaves, dependendo do repositório de chaves, ou executar outras etapas de configuração de armazenamento de chaves específico. Por exemplo, para acessar o Cofre de chaves do Azure, você precisa fornecer as credenciais corretas para o armazenamento de chaves.

### <a name="using-the-azure-key-vault-provider"></a>Usando o provedor do Cofre de chaves do Azure

O Cofre de Chaves do Azure é uma opção conveniente para armazenar e gerenciar chaves mestras de coluna do Always Encrypted (especialmente se seus aplicativos estiverem hospedados no Azure). O ODBC Driver 13.1 para SQL Server no Windows, Linux e macOS inclui um provedor de armazenamento de chave mestra de coluna interna para o Cofre de chaves do Azure. Consulte [Cofre de chaves do Azure – passo](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/), [guia de Introdução ao Cofre de chaves](https://azure.microsoft.com/documentation/articles/key-vault-get-started/), e [Criando chaves mestras de coluna no cofre de chaves do Azure](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_2) para obter mais informações sobre como configurar uma chave do Azure Cofre para sempre criptografado.

O driver dá suporte à autenticação no cofre de chaves do Azure usando os seguintes tipos de credencial:

- Nome de usuário/senha – com esse método, as credenciais são o nome de um usuário do Active Directory do Azure e sua senha.

- ID de cliente/segredo – com esse método, as credenciais são uma ID de cliente do aplicativo e um segredo do aplicativo.

Para permitir que o driver usar CMKs armazenados em AKV para criptografia de coluna, use as seguintes conexão-cadeia de caracteres somente palavras-chave:

|Tipo de Credencial| `KeyStoreAuthentication` |`KeyStorePrincipalId`| `KeyStoreSecret` |
|-|-|-|-|
|Nome de usuário e senha| `KeyVaultPassword`|Nome Principal do usuário|Senha|
|ID/segredo do cliente| `KeyVaultClientSecret`|ID do Cliente|Segredo|

#### <a name="example-connection-strings"></a>Exemplos de cadeias de Conexão

As cadeias de conexão a seguir mostram como autenticar para o Cofre de chaves do Azure com os dois tipos de credencial:

**ClientID/segredo**:

```
DRIVER=ODBC Driver 13 for SQL Server;SERVER=myServer;Trusted_Connection=Yes;DATABASE=myDB;ColumnEncryption=Enabled;KeyStoreAuthentication=KeyVaultClientSecret;KeyStorePrincipalId=<clientId>;KeyStoreSecret=<secret>
```

**Nome de usuário e senha**

```
DRIVER=ODBC Driver 13 for SQL Server;SERVER=myServer;Trusted_Connection=Yes;DATABASE=myDB;ColumnEncryption=Enabled;KeyStoreAuthentication=KeyVaultPassword;KeyStorePrincipalId=<username>;KeyStoreSecret=<password>
```

Nenhuma outra alteração de aplicativo de ODBC é necessários para usar AKV para armazenamento CMK.

### <a name="using-the-windows-certificate-store-provider"></a>Usando o provedor de repositório de certificados do Windows

O ODBC Driver 13.1 para SQL Server no Windows inclui um provedor de repositório de chaves mestras de coluna interna para o repositório de certificados do Windows, chamado `MSSQL_CERTIFICATE_STORE`. (Este provedor não está disponível no macOS ou Linux). Com esse provedor, CMK é armazenado localmente no computador cliente e nenhuma configuração adicional pelo aplicativo é necessária para uso com o driver. No entanto, o aplicativo deve ter acesso ao certificado e sua chave privada no repositório. Consulte [criar e chaves mestras de repositório de coluna (Always Encrypted)](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted) para obter mais informações.

### <a name="using-custom-keystore-providers"></a>Usando provedores de armazenamento de chaves personalizado

O ODBC Driver 13.1 para SQL Server também oferece suporte a provedores de armazenamento de chaves personalizado de terceiros usando a interface CEKeystoreProvider. Isso permite que um aplicativo carrega, consulta e configurar provedores de armazenamento de chaves para que pode ser usados pelo driver para acessar colunas criptografadas. Aplicativos podem interagir diretamente com um provedor de armazenamento de chaves para criptografam CEKs para armazenamento no SQL Server e executar tarefas além de acessar colunas criptografadas com ODBC; Para obter mais informações, consulte [provedores de armazenamento de chaves personalizado](../../connect/odbc/custom-keystore-providers.md).

Dois atributos de conexão são usados para interagir com provedores de armazenamento de chaves personalizado. São eles:

- `SQL_COPT_SS_CEKEYSTOREPROVIDER`

- `SQL_COPT_SS_CEKEYSTOREDATA`

O primeiro é usado para carregar e enumerar os provedores de carregados do armazenamento de chaves, enquanto o último permite a comunicação de provedor do aplicativo. Esses atributos de conexão podem ser usados a qualquer momento antes ou depois de estabelecer uma conexão, pois a interação do provedor de aplicativo não envolvem a comunicação com o SQL Server. No entanto, porque o driver ainda não foi carregado, configuração e Obtendo esses atributos antes de se conectar fará com que eles sejam processados pelo Gerenciador de Driver e não podem produzir os resultados esperados.

#### <a name="loading-a-keystore-provider"></a>Carregar um provedor de armazenamento de chaves

Definindo o `SQL_COPT_SS_CEKEYSTOREPROVIDER` atributo de conexão permite que um aplicativo cliente para carregar uma biblioteca do provedor, disponibilizando para usar os provedores de armazenamento de chaves nele contidos.

```
SQLRETURN SQLSetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER StringLength);
```
| Argumento | Description |
|:---|:---|
|`ConnectionHandle`|[Entrada] Identificador de Conexão. Deve ser um identificador de conexão válido, mas provedores carregados por meio do identificador de uma conexão são acessíveis de qualquer outro no mesmo processo.|
|`Attribute`|[Entrada] Atributo a ser definido: o `SQL_COPT_SS_CEKEYSTOREPROVIDER` constante.|
|`ValuePtr`|[Entrada] Ponteiro para uma cadeia de caracteres terminada em nulo especificando o nome do arquivo da biblioteca do provedor. Para SQLSetConnectAttrA, esta é uma cadeia de caracteres ANSI (multibyte). Para SQLSetConnectAttrW, esta é uma cadeia de caracteres Unicode (wchar_t).|
|`StringLength`|[Entrada] O comprimento da cadeia de caracteres ValuePtr ou SQL_NTS.|

O driver tentará carregar a biblioteca identificada pelo parâmetro ValuePtr usando a biblioteca dinâmica definidas por plataforma mecanismo (`dlopen()` em Linux e macOS, `LoadLibrary()` no Windows), e adiciona quaisquer provedores definidos à lista de provedores conhecidos para o driver. Os seguintes erros podem ocorrer:

| Erro | Description |
|:--|:--|
|`CE203`|Não foi possível carregar a biblioteca dinâmica.|
|`CE203`|O símbolo "CEKeyStoreProvider" exportado não foi encontrado na biblioteca.|
|`CE203`|Um ou mais provedores na biblioteca já estão carregados.|

`SQLSetConnectAttr`Retorna o erro comum ou valores de êxito e informações adicionais está disponível para quaisquer erros que ocorreram por meio do mecanismo de diagnóstico de ODBC padrão.

> [!NOTE]
> O programador de aplicativo deve garantir que quaisquer provedores personalizados são carregados antes de qualquer consulta exigir que eles é enviada através de qualquer conexão. Falha ao fazer isso resulta no erro:

| Erro | Description |
|:--|:--|
|`CE200`|Provedor de keystore %1 não encontrado. Certifique-se de que a biblioteca do provedor de keystore apropriado foi carregada.|

> [!NOTE]
> Implementações do provedor de armazenamento de chaves devem evitar o uso de `MSSQL` no nome de seus provedores personalizados. Esse termo é reservado exclusivamente para uso da Microsoft e pode causar conflitos com futuras provedores internos. Usar este termo no nome de um provedor personalizado pode resultar em um aviso de ODBC.

#### <a name="getting-the-list-of-loaded-providers"></a>Obter a lista de provedores carregados

Obter esse atributo de conexão permite que um aplicativo cliente para determinar os provedores de armazenamento de chaves atualmente carregados no driver (incluindo aqueles criados). Isso só pode ser executado depois de se conectar.

```
SQLRETURN SQLGetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER BufferLength, SQLINTEGER * StringLengthPtr);
```
| Argumento | Description |
|:---|:---|
|`ConnectionHandle`|[Entrada] Identificador de Conexão. Deve ser um identificador de conexão válido, mas provedores carregados por meio do identificador de uma conexão são acessíveis de qualquer outro no mesmo processo.|
|`Attribute`|[Entrada] Atributo recuperar: o `SQL_COPT_SS_CEKEYSTOREPROVIDER` constante.|
|`ValuePtr`|[Saída] Um ponteiro de memória no qual retornar o próximo nome de provedor carregado.|
|`BufferLength`|[Entrada] O comprimento do buffer ValuePtr.|
|`StringLengthPtr`|[Saída] Um ponteiro para um buffer no qual retornar o número total de bytes (excluindo o caractere null de terminação) disponíveis para retornar em \*ValuePtr. Se ValuePtr for um ponteiro nulo, nenhum comprimento será retornado. Se o valor do atributo é uma cadeia de caracteres e o número de bytes disponíveis para retornar é maior do que BufferLength menos o comprimento do encerramento nulo de caractere, os dados em \*ValuePtr é truncado para BufferLength menos o comprimento das caractere NULL de terminação e é terminada em nulo pelo driver.|

Para permitir a recuperar a lista inteira, todas as operações Get retorna o nome do provedor atual e incrementa um contador interno para o próximo. Quando esse contador atinge o final da lista, uma cadeia de caracteres vazia ("") for retornado, e o contador é redefinido; operações Get sucessivas, continue novamente desde o início da lista.

### <a name="communicating-with-keystore-providers"></a>Comunicação com provedores de armazenamento de chaves

O `SQL_COPT_SS_CEKEYSTOREDATA` atributo de conexão permite que um aplicativo cliente para se comunicar com provedores de keystore carregado para configurar parâmetros adicionais, a criação de material, etc. A comunicação entre um aplicativo cliente e um provedor segue um protocolo de solicitação-resposta simples, com base em Get e Set solicitações usando o atributo de conexão. A comunicação é iniciada somente pelo aplicativo cliente.

> [!NOTE]
> Devido à natureza do ODBC chama responder do CEKeyStoreProvider (SQLGet SetConnectAttr), a ODBC interface oferece suporte somente a definição de dados na resolução do contexto de conexão.

O aplicativo se comunica com os provedores de armazenamento de chaves por meio do driver por meio da estrutura de CEKeystoreData:

```
typedef struct CEKeystoreData {
wchar_t *name;
unsigned int dataSize;
char data[];
} CEKEYSTOREDATA;
```
| Argumento | Description |
|:---|:---|
|`name`|[Entrada] Em conjunto, o nome do provedor para que os dados são enviados. Ignorado ao Get. Cadeia de caracteres terminada em nulo, o caractere largo.|
|`dataSize`|[Entrada] O tamanho da matriz de dados, a estrutura a seguir.|
|`data`|[Entrada/saída] Em conjunto, os dados sejam enviados para o provedor. Podem ser dados arbitrários; o driver não faz nenhuma tentativa para interpretá-lo. Após Get, o buffer para receber os dados de leitura do provedor.|

#### <a name="writing-data-to-a-provider"></a>Gravação de um provedor de dados

Um `SQLSetConnectAttr` chamar usando o `SQL_COPT_SS_CEKEYSTOREDATA` atributo grava um "pacote" de dados para o provedor de keystore especificado.
```
SQLRETURN SQLSetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER StringLength);
```
| Argumento | Description |
|:---|:---|
|`ConnectionHandle`| [Entrada] Identificador de Conexão. Deve ser um identificador de conexão válido, mas provedores carregados por meio do identificador de uma conexão são acessíveis de qualquer outro no mesmo processo.|
|`Attribute`|[Entrada] Atributo a ser definido: o `SQL_COPT_SS_CEKEYSTOREDATA` constante.|
|`ValuePtr`|[Entrada] Ponteiro para uma estrutura CEKeystoreData. O campo nome da estrutura de identifica o provedor para o qual os dados se destina.|
|`StringLength`|[Entrada] Constante SQL_IS_POINTER|

Informações de erro detalhadas adicionais podem ser obtidas por meio de [SQLGetDiacRec](https://msdn.microsoft.com/library/ms710921(v=vs.85).aspx).

> [!NOTE]
> O provedor pode usar o identificador de conexão para associar os dados gravados para uma conexão específica, se ele assim desejar. Isso é útil para implementar a configuração por conexão. Ele também pode ignorar o contexto de conexão e tratar os dados de forma idêntica, independentemente da conexão usada para enviar os dados. Consulte [contexto de associação](../../connect/odbc/custom-keystore-providers.md#context-association) para obter mais informações.

#### <a name="reading-data-from-a-provider"></a>Lendo dados de um provedor

Uma chamada para `SQLGetConnectAttr` usando o `SQL_COPT_SS_CEKEYSTOREDATA` atributo lê um "pacote" de dados de *o último gravado-para* provedor. Se não houver nenhum, ocorre um erro de sequência de função. Os implementadores de provedor de armazenamento de chaves são incentivados a dar suporte a "fictício grava" de 0 bytes como uma maneira de selecionar o provedor para operações de leitura sem causar outros efeitos colaterais se faz sentido fazer isso.

```
SQLRETURN SQLGetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER BufferLength, SQLINTEGER * StringLengthPtr);
```
| Argumento | Description |
|:---|:---|
|`ConnectionHandle`|[Entrada] Identificador de Conexão. Deve ser um identificador de conexão válido, mas provedores carregados por meio do identificador de uma conexão são acessíveis de qualquer outro no mesmo processo.|
|`Attribute`|[Entrada] Atributo recuperar: o `SQL_COPT_SS_CEKEYSTOREDATA` constante.|
|`ValuePtr`|[Saída] Um ponteiro para uma estrutura CEKeystoreData em que a leitura do provedor de dados são colocados.|
|`BufferLength`|[Entrada] Constante SQL_IS_POINTER|
|`StringLengthPtr`|[Saída] Um ponteiro para um buffer no qual retornar BufferLength. Se * ValuePtr é um ponteiro nulo, nenhum comprimento é retornado.|

O chamador deve garantir que um buffer de tamanho suficiente seguindo a estrutura CEKEYSTOREDATA está alocado para o provedor gravar no. No retorno, o campo dataSize é atualizado com o comprimento real da leitura do provedor de dados. Informações de erro detalhadas adicionais podem ser obtidas por meio de [SQLGetDiacRec](https://msdn.microsoft.com/library/ms710921(v=vs.85).aspx).

Essa interface coloca sem requisitos adicionais sobre o formato de dados transferidos entre um aplicativo e um provedor de armazenamento de chaves. Cada provedor pode definir seu próprio formato de data/protocolo, dependendo de suas necessidades.

Para obter um exemplo de como implementar seu próprio provedor de armazenamento de chaves, consulte [provedores de armazenamento de chaves personalizado](../../connect/odbc/custom-keystore-providers.md)

## <a name="limitations-of-the-odbc-driver-when-using-always-encrypted"></a>Limitações do driver ODBC ao usar sempre criptografado

### <a name="bulk-copy-function-usage"></a>Uso de funções de cópia em massa
Usar o [funções de cópia em massa SQL](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md) não tem suporte ao usar o driver ODBC com o sempre criptografado. Nenhuma criptografia/descriptografia transparente ocorrerá em colunas criptografadas que são usadas com as funções de cópia em massa de SQL.

### <a name="asynchronous-operations"></a>Operações assíncronas
Enquanto o driver ODBC permitirá o uso de [operações assíncronas](../../relational-databases/native-client/odbc/creating-a-driver-application-asynchronous-mode-and-sqlcancel.md) com sempre criptografado, há um impacto de desempenho nas operações de quando sempre criptografado está habilitado. A chamada para `sys.sp_describe_parameter_encryption` para determinar os metadados de criptografia para a instrução está bloqueando e fará com que o driver de espera para o servidor retornar os metadados antes de retornar `SQL_STILL_EXECUTING`.

## <a name="always-encrypted-api-summary"></a>Resumo de APIs de sempre criptografado

### <a name="connection-string-keywords"></a>Palavras-chave de cadeia de conexão

|Nome|Description|  
|----------|-----------------|  
|`ColumnEncryption`|Os valores aceitos são `Enabled` / `Disabled`.<br>`Enabled`-Habilita a funcionalidade sempre criptografado para a conexão.<br>`Disabled`-desabilitar a funcionalidade sempre criptografado para a conexão. <br><br>O padrão é `Disabled`.|  
|`KeyStoreAuthentication` | Valores válidos: `KeyVaultPassword`,`KeyVaultClientSecret` |
|`KeyStorePrincipalId` | Quando `KeyStoreAuthentication`  =  `KeyVaultPassword`, defina esse valor como um nome de entidade de usuário do Active Directory do Azure válido. <br>Quando `KeyStoreAuthetication`  =  `KeyVaultClientSecret` definir esse valor como um Azure Active Directory aplicativo ID de cliente válida |
|`KeyStoreSecret` | Quando `KeyStoreAuthentication`  =  `KeyVaultPassword` definir esse valor como a senha para o nome de usuário correspondente. <br>Quando `KeyStoreAuthentication`  =  `KeyVaultClientSecret` definir esse valor como o segredo do aplicativo associado a um Azure Active Directory aplicativo ID de cliente válida|

### <a name="connection-attributes"></a>Atributos de conexão

|Nome|Tipo|Description|  
|----------|-------|----------|  
|`SQL_COPT_SS_COLUMN_ENCRYPTION`|Pré-conexão|`SQL_COLUMN_ENCRYPTION_DISABLE`(0) – desabilitar sempre criptografado <br>`SQL_COLUMN_ENCRYPTION_ENABLE`(1)-- habilitar sempre criptografado|
|`SQL_COPT_SS_CEKEYSTOREPROVIDER`|Após conectar-se|[Set] Tentativa de carregar CEKeystoreProvider<br>[Get] Retorna um nome de CEKeystoreProvider|
|`SQL_COPT_SS_CEKEYSTOREDATA`|Após conectar-se|[Set] Gravação de dados CEKeystoreProvider<br>[Get] Ler dados de CEKeystoreProvider|

### <a name="statement-attributes"></a>Atributos de instrução

|Nome|Description|  
|----------|-----------------|  
|`SQL_SOPT_SS_COLUMN_ENCRYPTION`|`SQL_CE_DISABLED`(0) — sempre criptografado está desabilitado para a instrução <br>`SQL_CE_RESULTSETONLY`(1)-- apenas para descriptografia. Conjuntos de resultados e valores de retorno são descriptografados e parâmetros não são criptografados. <br>`SQL_CE_ENABLED`(3) – sempre criptografado está habilitado e usado para parâmetros e resultados|

### <a name="descriptor-fields"></a>Campos de descritor

|Campo IPD|Tipo de tamanho /|Valor padrão|Description|
|-|-|-|-|  
|`SQL_CA_SS_FORCE_ENCRYPT` (1236)|WORD (2 bytes)|0|Quando 0 (padrão): decisão para criptografar esse parâmetro é determinado pela disponibilidade de metadados de criptografia.<br><br>Quando for diferente de zero: se os metadados de criptografia estão disponíveis para esse parâmetro, ele é criptografado. Caso contrário, a solicitação falhará com erro [CE300] criptografia obrigatória [Microsoft] [ODBC Driver 13 para SQL Server] foi especificada para um parâmetro, mas não há metadados de criptografia foi fornecido pelo servidor.|

## <a name="see-also"></a>Consulte também

- [Always Encrypted (mecanismo de banco de dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Blog do Always Encrypted](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)


