---
title: Como usar o recurso Always Encrypted com o ODBC Driver for SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 10/01/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 02e306b8-9dde-4846-8d64-c528e2ffe479
caps.latest.revision: 3
ms.author: v-chojas
manager: craigg
author: MightyPen
ms.openlocfilehash: b32be273b26a163263798c3b6a5312432cc54eb6
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38980678"
---
# <a name="using-always-encrypted-with-the-odbc-driver-for-sql-server"></a>Como usar o recurso Always Encrypted com o ODBC Driver for SQL Server
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

### <a name="applicable-to"></a>Aplicável a

- Driver ODBC 13.1 para SQL Server
- ODBC Driver 17 for SQL Server

### <a name="introduction"></a>Introdução

Este artigo fornece informações sobre como desenvolver aplicativos de ODBC usando [Always Encrypted (mecanismo de banco de dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) e o [ODBC Driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md).

O Always Encrypted permite que os aplicativos cliente criptografem dados confidenciais e nunca revelem os dados nem as chaves de criptografia para o SQL Server ou o Banco de Dados SQL do Azure. Um driver habilitado para Always Encrypted, como o ODBC Driver for SQL Server, consegue fazer isso criptografando e descriptografando de modo transparente dados confidenciais no aplicativo cliente. O driver determina automaticamente quais parâmetros de consulta correspondem às colunas de banco de dados confidenciais (protegidas com o Always Encrypted) e criptografa os valores desses parâmetros antes de passar os dados para o SQL Server ou o Banco de Dados SQL do Azure. Da mesma forma, o driver descriptografa de modo transparente os dados recuperados das colunas de banco de dados criptografadas nos resultados da consulta. Para obter mais informações, veja [Always Encrypted (Mecanismo de Banco de Dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md).

### <a name="prerequisites"></a>Prerequisites

Configure o Sempre Criptografado em seu banco de dados. Isso envolve o provisionamento de chaves do Sempre Criptografado e a configuração de criptografia de colunas de banco de dados selecionadas. Se você ainda não tiver um banco de dados com o Sempre Criptografado configurado, siga as instruções em [Getting Started with Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted)(Introdução ao Sempre Criptografado). Em particular, o banco de dados deve conter as definições de metadados para uma chave mestra de coluna (CMK), uma chave de criptografia de coluna (CEK) e uma tabela contendo uma ou mais colunas criptografadas usando esse CEK.

### <a name="enabling-always-encrypted-in-an-odbc-application"></a>Habilitando o Always Encrypted em um aplicativo ODBC

A maneira mais fácil para habilitar o parâmetro criptografia e descriptografia de coluna criptografada de conjunto de resultados está definindo o valor de `ColumnEncryption` palavra-chave de cadeia de caracteres de conexão para **Enabled**. Veja a seguir o exemplo de uma cadeia de conexão que habilita Always Encrypted:

```
SQLWCHAR *connString = L"Driver={ODBC Driver 13 for SQL Server};Server={myServer};Trusted_Connection=yes;ColumnEncryption=Enabled;";
```

Sempre criptografado pode também ser habilitado na configuração de DSN, usando a mesma chave e valor (que será substituído pela configuração de cadeia de caracteres de conexão, se presente) ou por meio de programação com o `SQL_COPT_SS_COLUMN_ENCRYPTION` atributo da conexão. Defini-lo dessa maneira substitui o valor definido na cadeia de caracteres de conexão ou DSN:

```
 SQLSetConnectAttr(hdbc, SQL_COPT_SS_COLUMN_ENCRYPTION, (SQLPOINTER)SQL_COLUMN_ENCRYPTION_ENABLE, 0);
```

Uma vez habilitada para a conexão, o comportamento do Always Encrypted pode ser ajustado para consultas individuais. Ver [controlando o desempenho do impacto do Always Encrypted](#controlling-the-performance-impact-of-always-encrypted) abaixo para obter mais informações.

Observe que habilitar o sempre criptografado não é suficiente para a criptografia ou descriptografia seja bem-sucedida; Você também precisará ter certeza de que:

- O aplicativo tem as permissões de banco de dados *VIEW ANY COLUMN MASTER KEY DEFINITION* e *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* , necessárias para acessar os metadados sobre as chaves do Always Encrypted no banco de dados. Para obter detalhes, consulte [permissões de banco de dados](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions).

- O aplicativo pode acessar a CMK que protege os CEKs para as colunas criptografadas consultadas. Isso é dependente do provedor de repositório de chaves que armazena a CMK. Ver [trabalhando com repositórios de chaves mestras de coluna](#working-with-column-master-key-stores) para obter mais informações.

### <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>Recuperando e modificando dados em colunas criptografadas

Depois de habilitar o Always Encrypted em uma conexão, você pode usar APIs de ODBC padrão (consulte [código de exemplo do ODBC](https://code.msdn.microsoft.com/windowsapps/ODBC-sample-191624ae/sourcecode?fileId=51137&pathId=1980325953) ou [referência do programador de ODBC](https://msdn.microsoft.com/library/ms714177(v=vs.85).aspx)) para recuperar ou modificar dados em colunas de banco de dados criptografado. Supondo que seu aplicativo tem as permissões de banco de dados e pode acessar a chave mestra de coluna, o driver criptografará quaisquer parâmetros de consulta que se destinam a colunas criptografadas e descriptografar os dados recuperados de colunas criptografadas, comportando-se de forma transparente para o aplicativo como se as colunas não foram criptografadas.

Se Always Encrypted não estiver habilitado, as consultas com parâmetros que se destinam a colunas criptografadas falharão. Os dados ainda podem ser recuperados de colunas criptografadas, desde que a consulta não tenha parâmetros que se destinem a colunas criptografadas. No entanto, o driver não tentará qualquer descriptografia e o aplicativo receberá os dados binários criptografados (como matrizes de bytes).

A tabela abaixo resume o comportamento das consultas, dependendo de se o Always Encrypted está habilitado ou não:

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

- Os valores inseridos nas colunas de banco de dados, incluindo as colunas criptografadas, são passados como parâmetros associados (veja [função SQLBindParameter](https://msdn.microsoft.com/library/ms710963(v=vs.85).aspx)). Embora o uso de parâmetros seja opcional ao enviar valores para colunas não criptografadas (mesmo que seja altamente recomendável, pois ajuda a prevenir a injeção de SQL), ele é necessário para valores que se destinam a colunas criptografadas. Se os valores inseridos nas colunas SSN ou BirthDate fossem passados como literais inseridos na instrução de consulta, a consulta falharia, pois o driver não tentará criptografar ou processar os literais em consultas. Como resultado, o servidor os rejeitaria como incompatíveis com as colunas criptografadas.

- O tipo SQL do parâmetro inserido na coluna SSN é definido como SQL_CHAR, que mapeia para o **char** tipo de dados do SQL Server (`rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 11, 0, (SQLPOINTER)SSN, 0, &cbSSN);`). Se o tipo do parâmetro foi definido como SQL_WCHAR, que mapeia para **nchar**, a consulta falharia, como Always Encrypted não suporta conversões de lado do servidor de valores nchar criptografados em valores criptografados char. Ver [referência do programador de ODBC – tipos de dados do apêndice d:](https://msdn.microsoft.com/library/ms713607.aspx) para obter informações sobre os mapeamentos de tipo de dados.

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

- O valor usado na cláusula WHERE para filtrar na coluna SSN precisa ser passado com SQLBindParameter, para que o driver de modo transparente pode criptografá-lo antes de enviá-la para o servidor.

- Todos os valores impressos pelo programa será em texto não criptografado, já que o driver descriptografará de modo transparente os dados recuperados das colunas SSN e BirthDate.

> [!NOTE]
> As consultas podem executar comparações de igualdade em colunas criptografadas somente se a criptografia é determinística. Para obter mais informações, confira [Seleção de criptografia determinística ou aleatória](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption).

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

O Always Encrypted dá suporte a algumas conversões de tipos de dados criptografados. Confira [Always Encrypted (Mecanismo de Banco de Dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) para obter a lista detalhada de conversões de tipo compatíveis. Para evitar erros de conversão de tipo de dados, certifique-se de que você observa os seguintes pontos ao usar SQLBindParameter com parâmetros que se destinam a colunas criptografadas:

- O tipo SQL do parâmetro seja exatamente o mesmo que o tipo da coluna de destino ou a conversão de um tipo SQL para o tipo da coluna é suportada.

- A precisão e a escala dos parâmetros que se destinam a colunas dos tipos de dados `decimal` e `numeric` do SQL Server são iguais à precisão e à escala configuradas para a coluna de destino.

- A precisão dos parâmetros que se destinam às colunas dos tipos de dados `datetime2`, `datetimeoffset` ou `time` do SQL Server não é maior que a precisão da coluna de destino, em consultas que modificam a coluna de destino.  

##### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>Erros devido à passagem de texto sem formatação em vez de valores criptografados

Qualquer valor que tem como alvo uma coluna criptografada precisa ser criptografado antes de serem enviados ao servidor. Uma tentativa de inserir, modificar ou filtrar por um valor de texto não criptografado em uma coluna criptografada resultará em um erro. Para evitar esses erros, garanta que:

- Always Encrypted está habilitado (no DSN, a cadeia de caracteres de conexão, conectando antes, definindo o `SQL_COPT_SS_COLUMN_ENCRYPTION` atributo de conexão para uma conexão específica, ou o `SQL_SOPT_SS_COLUMN_ENCRYPTION` atributo da instrução para uma instrução específica).

- Você use o SQLBindParameter para enviar dados que se destinam a colunas criptografadas. O exemplo abaixo mostra uma consulta que filtra incorretamente por uma/constante em uma coluna criptografada (SSN), em vez de passar o literal como um argumento para o SQLBindParameter.

```
string queryText = "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
```

### <a name="precautions-when-using-sqlsetpos-and-sqlmoreresults"></a>Precauções ao usar SQLSetPos e SQLMoreResults

#### <a name="sqlsetpos"></a>SQLSetPos

O `SQLSetPos` API permite que um aplicativo atualizar linhas em um conjunto de resultados usando buffers que foram associados com SQLBindCol e em qual linha dados foi obtidos anteriormente. Devido ao comportamento de preenchimento assimétrica dos tipos de comprimento fixo criptografados, é possível inesperadamente alteram os dados dessas colunas durante a execução de atualizações em outras colunas na linha. Valores de caracteres de comprimento fixo com AE, serão preenchidos se o valor for menor do que o tamanho do buffer.

Para atenuar esse comportamento, use o `SQL_COLUMN_IGNORE` sinalizador para ignorar colunas que não serão atualizadas como parte da `SQLBulkOperations` e ao usar `SQLSetPos` para cursor com base em atualizações.  Todas as colunas que não estão sendo modificadas diretamente pelo aplicativo devem ser ignoradas, tanto para desempenho e para evitar o truncamento de colunas que são associados a um buffer *menores* além do tamanho real (DB). Para obter mais informações, consulte [referência de função SQLSetPos](https://msdn.microsoft.com/library/ms713507(v=vs.85).aspx).

#### <a name="sqlmoreresults--sqldescribecol"></a>SQLMoreResults & SQLDescribeCol

Programas de aplicativo podem chamar [SQLDescribeCol](https://msdn.microsoft.com/library/ms716289(v=vs.85).aspx) para retornar metadados sobre colunas em instruções preparadas.  Quando o Always Encrypted estiver habilitado, chamando `SQLMoreResults` *antes de* chamando `SQLDescribeCol` faz com que o [sp_describe_first_result_set](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) para ser chamado, que não retorna corretamente o texto não criptografado metadados de colunas criptografadas. Para evitar esse problema, chame `SQLDescribeCol` em instruções preparadas *antes de* chamando `SQLMoreResults`.

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>Controle do impacto sobre o desempenho do Always Encrypted

Como o Always Encrypted é uma tecnologia de criptografia do lado do cliente, a maior parte da sobrecarga de desempenho é observada no lado do cliente, não no banco de dados. Além do custo das operações de criptografia e descriptografia, as outras fontes de sobrecarga de desempenho no lado do cliente são:

- Viagens de ida e volta adicionais ao banco de dados para recuperar metadados dos parâmetros de consulta.

- Chamadas a um repositório de chaves mestras de coluna para acessar uma chave mestra de coluna.

Esta seção descreve as otimizações de desempenho internas no ODBC Driver for SQL Server e como você pode controlar o impacto dos dois fatores acima sobre o desempenho.

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>Controle das viagens de ida e volta para recuperar metadados dos parâmetros de consulta

Se o Always Encrypted estiver habilitado para uma conexão, o driver por padrão chamará [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) para cada consulta parametrizada, passando a instrução de consulta (sem nenhum valor de parâmetro) para o SQL Server. Esse procedimento armazenado analisa a instrução de consulta para descobrir se os parâmetros precisam ser criptografados e nesse caso, retorna as informações relacionadas à criptografia para cada parâmetro para permitir que o driver criptografá-los. O comportamento acima garante um alto nível de transparência para o aplicativo cliente: O aplicativo (e o desenvolvedor do aplicativo) não precisam estar ciente de quais consultas acessam colunas criptografadas, desde que os valores que se destinam a colunas criptografadas são passados para o driver nos parâmetros.

### <a name="per-statement-always-encrypted-behavior"></a>Por instrução Always Encrypted comportamento

Para controlar o impacto no desempenho de recuperação de metadados de criptografia para consultas parametrizadas, você pode alterar o comportamento de Always Encrypted para consultas individuais, se ele tiver sido habilitado na conexão. Dessa forma, você pode garantir que `sys.sp_describe_parameter_encryption` é invocado apenas para consultas que você sabe que têm parâmetros que se destinam a colunas criptografadas. No entanto, observe que, ao fazer isso, você reduzirá a transparência da criptografia: se você criptografar colunas adicionais no seu banco de dados, poderá precisar alterar o código do aplicativo para alinhá-lo a alterações de esquema.

Para controlar o comportamento de Always Encrypted de uma instrução, chame SQLSetStmtAttr para definir o `SQL_SOPT_SS_COLUMN_ENCRYPTION` atributo da instrução para um dos seguintes valores:

|Valor|Descrição|
|-|-|
|`SQL_CE_DISABLED` (0)|Sempre criptografado está desabilitado para a instrução|
|`SQL_CE_RESULTSETONLY` (1)|Descriptografia. Conjuntos de resultados e valores de retorno são descriptografados e parâmetros que não estão criptografados|
|`SQL_CE_ENABLED` (3) | Always Encrypted está habilitado e usado para parâmetros e resultados|

Novos identificadores de instrução criados a partir de uma conexão com o Always Encrypted habilitado SQL_CE_ENABLED como padrão. Aqueles criados de uma conexão com ele desabilitado padrão para SQL_CE_DISABLED (e não é possível habilitar o Always Encrypted neles.)

Se a maioria das consultas de um aplicativo cliente acessar colunas criptografadas, é recomendável o seguinte:

- Defina a palavra-chave de cadeia de conexão `ColumnEncryption` como `Enabled`.

- Defina as `SQL_SOPT_SS_COLUMN_ENCRYPTION` atributo `SQL_CE_DISABLED` em instruções que não acessam nenhuma coluna criptografada. Isso desabilitará a ambos os chamada `sys.sp_describe_parameter_encryption` , bem como tenta descriptografar todos os valores no resultado definido.
    
- Defina as `SQL_SOPT_SS_COLUMN_ENCRYPTION` atributo `SQL_CE_RESULTSETONLY` em instruções que não têm parâmetros que exijam criptografia, mas que recuperam dados de colunas criptografadas. Isso desabilitará a chamada `sys.sp_describe_parameter_encryption` e criptografia do parâmetro. Resultados contendo colunas criptografadas continuarão a ser descriptografado.

## <a name="always-encrypted-security-settings"></a>Always Encrypted as configurações de segurança

### <a name="force-column-encryption"></a>Forçar criptografia de coluna

Para impor a criptografia de um parâmetro, defina o `SQL_CA_SS_FORCE_ENCRYPT` campo do descritor de parâmetro de implementação (IPD) por meio de uma chamada para a função SQLSetDescField. Um valor diferente de zero faz com que o driver retornará um erro quando nenhum metadado de criptografia é retornado para o parâmetro associado.

```
SQLHDESC ipd;
SQLGetStmtAttr(hStmt, SQL_ATTR_IMP_PARAM_DESC, &ipd, 0, 0);
SQLSetDescField(ipd, paramNum, SQL_CA_SS_FORCE_ENCRYPT, (SQLPOINTER)TRUE, SQL_IS_SMALLINT);   
```

Se o SQL Server informar o driver de que o parâmetro não precisa ser criptografado, as consultas que usam tal parâmetro falharão. Isso fornece proteção adicional contra ataques à segurança que envolvem um SQL Server comprometido fornecer metadados de criptografia incorretos ao cliente, o que pode levar à divulgação de dados.

### <a name="column-encryption-key-caching"></a>Cache de chaves de criptografia de coluna

Para reduzir o número de chamadas para um repositório de chave mestra de coluna para descriptografar as chaves de criptografia de coluna, o driver armazena em cache o CEKs texto não criptografado na memória. O cache CEK é global para o driver e não está associado com qualquer uma conexão. Depois de receber o ECEK dos metadados do banco de dados, o driver primeiro tenta encontrar a CEK texto sem formatação correspondente ao valor de chave criptografado no cache. O driver chama o repositório de chaves que contém a CMK somente se ele não é possível localizar o CEK de texto sem formatação correspondente no cache.

> [!NOTE]
> No Driver ODBC para SQL Server, as entradas no cache são removidas após um tempo limite de duas horas. Isso significa que, para um determinado ECEK, o driver entra em contato com o repositório de chaves apenas uma vez durante o tempo de vida do aplicativo ou a cada duas horas, o que for menor.

Começando com o 17.1 do Driver ODBC para SQL Server, o tempo de limite de cache CEK pode ser ajustado usando o `SQL_COPT_SS_CEKCACHETTL` atributo de conexão, que especifica o número de segundos que uma CEK permanecerão no cache. Devido à natureza do cache global, esse atributo pode ser ajustado de qualquer identificador de conexão válida para o driver. Quando o cache de TTL é reduzida, CEKs existentes que excederia o TTL novos também são removidos. Se for 0, nenhuma CEKs são armazenados em cache.

### <a name="trusted-key-paths"></a>Caminhos de chave confiáveis

Começando com o 17.1 do Driver ODBC para SQL Server, o `SQL_COPT_SS_TRUSTEDCMKPATHS` atributo de conexão permite que um aplicativo para exigir que as operações de Always Encrypted só usam uma lista especificada de CMKs, identificados por seus caminhos de chave. Por padrão, esse atributo é NULL, o que significa que o driver aceita qualquer caminho da chave. Para usar esse recurso, defina `SQL_COPT_SS_TRUSTEDCMKPATHS` para apontar para uma cadeia de caracteres largos delimitada por nulo, terminada em nulo que lista o caminho de chave permitido (s). A memória apontada por esse atributo deve permanecer válida durante as operações de criptografia ou descriptografia usando o identificador de conexão em que ele está definido---no qual o driver verificará se o caminho CMK conforme especificado pelos metadados do servidor case-insensitively está neste lista. Se o caminho da CMK não estiver na lista, a operação falhará. O aplicativo pode alterar o conteúdo da memória, que esse atributo aponta, para alterar sua lista de CMKs confiáveis, sem definir o atributo novamente.

## <a name="working-with-column-master-key-stores"></a>Trabalhando com repositórios de chaves mestras de coluna

Para criptografar ou descriptografar dados, o driver precisa obter uma CEK que está configurada para a coluna de destino. CEKs são armazenados em formato criptografado (ECEKs) nos metadados do banco de dados. Cada CEK tem uma CMK correspondente que foi usada para criptografá-lo. O [metadados de banco de dados](../../t-sql/statements/create-column-master-key-transact-sql.md) não armazena a CMK em si; ele contém apenas o nome do repositório de chaves e as informações que o repositório de chaves pode usar para localizar a CMK.

Para obter o valor de texto sem formatação de um ECEK, o driver primeiro obtém os metadados sobre a CEK e seu CMK correspondente e, em seguida, ele usa essas informações, entre em contato com o repositório de chaves que contém a CMK e solicitá-lo para descriptografar o ECEK. O driver se comunica com um repositório de chaves usando um provedor de repositório de chaves.

### <a name="built-in-keystore-providers"></a>Provedores de repositório de chaves interno

O Driver ODBC para SQL Server vem com os seguintes provedores de repositório de chaves interno:

| Nome | Descrição | Nome do provedor (metadados) |Disponibilidade|
|:---|:---|:---|:---|
|Cofre de Chave do Azure |Repositórios de CMKs em um cofre de chaves do Azure | `AZURE_KEY_VAULT` |Windows, macOS, Linux|
|Repositório de Certificados do Windows|Armazena CMKs localmente no repositório de chaves do Windows| `MSSQL_CERTIFICATE_STORE`|Windows|

- Você (ou seu DBA) precisa verificar se o nome do provedor, configurado nos metadados da chave mestra de coluna, está correto e se o caminho da chave mestra de coluna está em conformidade com o formato do caminho da chave para o provedor determinado. É recomendável configurar as chaves usando ferramentas como o SQL Server Management Studio, que gera automaticamente os nomes de provedor válidos e os caminhos de chaves ao emitir a instrução [CREATE COLUMN MASTER KEY (Transact-SQL)](../../t-sql/statements/create-column-master-key-transact-sql.md) .

- Você precisa garantir que seu aplicativo possa acessar a chave no repositório de chaves. Isso pode envolver a concessão de acesso para o aplicativo à chave e/ou ao repositório de chaves, dependendo do repositório de chaves, ou a execução de outras etapas de configuração específicas do repositório de chaves. Por exemplo, para acessar um Azure Key Vault, você precisa fornecer as credenciais corretas para o repositório de chaves.

### <a name="using-the-azure-key-vault-provider"></a>Uso do provedor do Azure Key Vault

O Cofre de Chaves do Azure é uma opção conveniente para armazenar e gerenciar chaves mestras de coluna do Always Encrypted (especialmente se seus aplicativos estiverem hospedados no Azure). O Driver ODBC para SQL Server no Linux, macOS e Windows inclui um provedor de repositório de chaves mestras de coluna interna para o Azure Key Vault. Ver [Azure Key Vault - passo a passo](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/), [Introdução ao Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-get-started/), e [Criando chaves mestras de coluna no Azure Key Vault](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_2) para obter mais informações sobre como configurar uma chave do Azure Cofre para Always Encrypted.

> [!NOTE]
> No Linux e macOS, para a versão de driver 17.2 e posterior, `libcurl` é necessária para usar esse provedor, mas não é uma dependência explícita, pois outras operações com o driver não exigem. Se você encontrar um erro em relação ao `libcurl`, verifique se ele está instalado.

O driver dá suporte à autenticação no Azure Key Vault usando os seguintes tipos de credencial:

- Nome de usuário/senha – com esse método, as credenciais são o nome de um usuário do Active Directory do Azure e sua senha.

- ID/segredo do cliente – com esse método, as credenciais são uma ID de cliente do aplicativo e um segredo do aplicativo.

Para permitir que o driver usar CMKs armazenadas no AKV para criptografia de coluna, use as seguintes palavras chave conexão-apenas cadeias de caracteres:

|Tipo de Credencial| `KeyStoreAuthentication` |`KeyStorePrincipalId`| `KeyStoreSecret` |
|-|-|-|-|
|Nome de usuário/senha| `KeyVaultPassword`|Nome UPN|Senha|
|ID/segredo do cliente| `KeyVaultClientSecret`|ID do Cliente|Segredo|

#### <a name="example-connection-strings"></a>Exemplo de cadeias de conexão

As cadeias de conexão a seguir mostram como autenticar no Azure Key Vault com os dois tipos de credencial:

**ClientID/segredo**:

```
DRIVER=ODBC Driver 13 for SQL Server;SERVER=myServer;Trusted_Connection=Yes;DATABASE=myDB;ColumnEncryption=Enabled;KeyStoreAuthentication=KeyVaultClientSecret;KeyStorePrincipalId=<clientId>;KeyStoreSecret=<secret>
```

**Nome de usuário/senha**

```
DRIVER=ODBC Driver 13 for SQL Server;SERVER=myServer;Trusted_Connection=Yes;DATABASE=myDB;ColumnEncryption=Enabled;KeyStoreAuthentication=KeyVaultPassword;KeyStorePrincipalId=<username>;KeyStoreSecret=<password>
```

Nenhuma outra alteração de aplicativo de ODBC devem usar o AKV para armazenamento CMK.

### <a name="using-the-windows-certificate-store-provider"></a>Usando o provedor do Windows Store de certificado

O Driver ODBC para SQL Server no Windows inclui um provedor de repositório de chaves mestras de coluna interna para a Store de certificado do Windows, chamado `MSSQL_CERTIFICATE_STORE`. (Esse provedor não está disponível no macOS ou Linux.) Com esse provedor, a CMK é armazenada localmente no computador cliente e nenhuma configuração adicional pelo aplicativo é necessária usá-lo com o driver. No entanto, o aplicativo deve ter acesso ao certificado e sua chave privada no repositório. Veja [Criar e armazenar chaves mestras de coluna (Always Encrypted)](https://docs.microsoft.com/sql/relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted).

### <a name="using-custom-keystore-providers"></a>Uso de provedores de repositórios de chaves personalizados

O Driver ODBC para SQL Server também oferece suporte a provedores de armazenamento de chaves personalizado de terceiros usando a interface CEKeystoreProvider. Isso permite que um aplicativo carrega, consulta e configurar provedores de repositório de chaves para que pode ser usados pelo driver para acessar colunas criptografadas. Aplicativos podem interagir diretamente com um provedor de repositório de chaves para criptografar CEKs para armazenamento no SQL Server e executar tarefas além de acessar colunas criptografadas com o ODBC; Para obter mais informações, consulte [provedores de repositório de chaves personalizado](../../connect/odbc/custom-keystore-providers.md).

Dois atributos de conexão são usados para interagir com provedores de armazenamento de chaves personalizado. São eles:

- `SQL_COPT_SS_CEKEYSTOREPROVIDER`

- `SQL_COPT_SS_CEKEYSTOREDATA`

O primeiro é usado para carregar e enumerar os provedores de repositório de chaves carregado, enquanto a última opção permite a comunicação de provedor de aplicativo. Esses atributos de conexão podem ser usados a qualquer momento, antes ou depois de estabelecer uma conexão, desde que a interação do provedor de aplicativo não envolvem a comunicação com o SQL Server. No entanto, porque o driver ainda não foi carregado, configuração e como esses atributos antes de conectar-se fará com que eles sejam processados pelo Gerenciador de Driver e podem não produzir os resultados esperados.

#### <a name="loading-a-keystore-provider"></a>Carregar um provedor de repositório de chaves

Definindo o `SQL_COPT_SS_CEKEYSTOREPROVIDER` atributo de conexão permite que um aplicativo cliente para carregar uma biblioteca de provedor, tornando disponíveis para uso de provedores de repositório de chaves contidos nos mesmos.

```
SQLRETURN SQLSetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER StringLength);
```
| Argumento | Descrição |
|:---|:---|
|`ConnectionHandle`|[Entrada] Identificador de Conexão. Deve ser um identificador de conexão válida, mas provedores carregados por meio do identificador de uma conexão são acessíveis de qualquer outro no mesmo processo.|
|`Attribute`|[Entrada] Atributo a ser definido: o `SQL_COPT_SS_CEKEYSTOREPROVIDER` constante.|
|`ValuePtr`|[Entrada] Ponteiro para uma cadeia de caracteres terminada em nulo que especifica o nome do arquivo da biblioteca do provedor. Para SQLSetConnectAttrA, essa é uma cadeia de caracteres ANSI (multibyte). Para SQLSetConnectAttrW, isso é uma cadeia de caracteres Unicode (wchar_t).|
|`StringLength`|[Entrada] O comprimento da cadeia de caracteres ValuePtr ou SQL_NTS.|

O driver tenta carregar a biblioteca identificada pelo parâmetro ValuePtr usando a biblioteca dinâmica plataforma definida pelo mecanismo de carregamento (`dlopen()` no Linux e macOS, `LoadLibrary()` no Windows), e adiciona quaisquer provedores definidos à lista de provedores conhecidos para o driver. Os seguintes erros podem ocorrer:

| Erro | Descrição |
|:--|:--|
|`CE203`|Não foi possível carregar a biblioteca dinâmica.|
|`CE203`|O símbolo de "CEKeyStoreProvider" exportado não foi encontrado na biblioteca.|
|`CE203`|Um ou mais provedores na biblioteca já estão carregados.|

`SQLSetConnectAttr` Retorna o erro usual ou valores de êxito e informações adicionais está disponível para quaisquer erros que ocorreram por meio do mecanismo de diagnóstico de ODBC padrão.

> [!NOTE]
> O programador de aplicativos deve garantir que quaisquer provedores personalizados são carregados antes de qualquer consulta exigir que eles é enviada por qualquer conexão. Não fazer isso resultará no erro:

| Erro | Descrição |
|:--|:--|
|`CE200`|Provedor de keystore %1 não encontrado. Certifique-se de que a biblioteca do provedor de repositório de chaves apropriados foram carregada.|

> [!NOTE]
> Implementações do provedor de repositório de chaves devem evitar o uso de `MSSQL` no nome de seus provedores personalizados. Esse termo é reservado exclusivamente para uso da Microsoft e pode causar conflitos com os provedores internos futuras. Uso esse termo no nome de um provedor personalizado pode resultar em um aviso de ODBC.

#### <a name="getting-the-list-of-loaded-providers"></a>Obtendo a lista de provedores carregados

Introdução a este atributo de conexão permite que um aplicativo cliente para determinar os provedores de repositório de chaves atualmente carregados no driver (incluindo aquelas embutidas). Isso só pode ser executado após a conexão.

```
SQLRETURN SQLGetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER BufferLength, SQLINTEGER * StringLengthPtr);
```
| Argumento | Descrição |
|:---|:---|
|`ConnectionHandle`|[Entrada] Identificador de Conexão. Deve ser um identificador de conexão válida, mas provedores carregados por meio do identificador de uma conexão são acessíveis de qualquer outro no mesmo processo.|
|`Attribute`|[Entrada] Atributo a ser recuperado: o `SQL_COPT_SS_CEKEYSTOREPROVIDER` constante.|
|`ValuePtr`|[Saída] Um ponteiro de memória no qual retornar o próximo nome de provedor carregado.|
|`BufferLength`|[Entrada] O comprimento do buffer ValuePtr.|
|`StringLengthPtr`|[Saída] Um ponteiro para um buffer no qual retornar o número total de bytes (exceto o caractere nulo de terminação) disponíveis para retornar em \*ValuePtr. Se ValuePtr for um ponteiro nulo, nenhum comprimento será retornado. Se o valor do atributo é uma cadeia de caracteres e o número de bytes disponíveis para retornar é maior que BufferLength menos o comprimento do encerramento nulo de caractere, os dados em \*ValuePtr é truncado para BufferLength menos o comprimento das caractere de terminação NULL e é terminada em nulo pelo driver.|

Para permitir ao recuperar a lista inteira, todas as operações Get retorna o nome do provedor atual e incrementa um contador interno para o próximo. Depois que esse contador atinge o final da lista, uma cadeia de caracteres vazia ("") é retornado, e o contador é redefinido; operações sucessivas de Get, em seguida, continuar novamente desde o início da lista.

### <a name="communicating-with-keystore-providers"></a>Comunicando-se com provedores de repositório de chaves

O `SQL_COPT_SS_CEKEYSTOREDATA` atributo de conexão permite que um aplicativo cliente para se comunicar com provedores de repositório de chaves carregado para configurar parâmetros adicionais, como material de chaveamento etc. A comunicação entre um aplicativo cliente e um provedor segue um protocolo simples de solicitação-resposta, com base em Get e Set solicitações utilizando esse atributo de conexão. Comunicação é iniciada somente pelo aplicativo cliente.

> [!NOTE]
> Devido à natureza de ODBC chama responder do CEKeyStoreProvider (SQLGet SetConnectAttr), o ODBC interface oferece suporte somente à configuração de dados com a resolução do contexto de conexão.

O aplicativo se comunica com provedores de repositório de chaves por meio do driver por meio da estrutura de CEKeystoreData:

```
typedef struct CEKeystoreData {
wchar_t *name;
unsigned int dataSize;
char data[];
} CEKEYSTOREDATA;
```
| Argumento | Descrição |
|:---|:---|
|`name`|[Entrada] Em conjunto, o nome do provedor para que os dados são enviados. Ignorado após Get. Cadeia de caracteres terminada em nulo, o caractere largo.|
|`dataSize`|[Entrada] O tamanho da matriz de dados, a estrutura a seguir.|
|`data`|[Entrada/saída] Em conjunto, os dados a serem enviados para o provedor. Isso pode ser dados arbitrários; o driver não fará nenhuma tentativa para interpretá-lo. Após Get, o buffer para receber os dados lidos do provedor.|

#### <a name="writing-data-to-a-provider"></a>Gravação de um provedor de dados

Um `SQLSetConnectAttr` chamar usando o `SQL_COPT_SS_CEKEYSTOREDATA` atributo grava um "pacote" de dados para o provedor de keystore especificado.
```
SQLRETURN SQLSetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER StringLength);
```
| Argumento | Descrição |
|:---|:---|
|`ConnectionHandle`| [Entrada] Identificador de Conexão. Deve ser um identificador de conexão válida, mas provedores carregados por meio do identificador de uma conexão são acessíveis de qualquer outro no mesmo processo.|
|`Attribute`|[Entrada] Atributo a ser definido: o `SQL_COPT_SS_CEKEYSTOREDATA` constante.|
|`ValuePtr`|[Entrada] Ponteiro para uma estrutura CEKeystoreData. O campo nome da estrutura identifica o provedor para o qual os dados se destina.|
|`StringLength`|[Entrada] Constante SQL_IS_POINTER|

Informações de erro detalhadas adicionais podem ser obtidas por meio [SQLGetDiacRec](https://msdn.microsoft.com/library/ms710921(v=vs.85).aspx).

> [!NOTE]
> O provedor pode usar o identificador de conexão para associar os dados gravados para uma conexão específica, se desejado. Isso é útil para implementar a configuração por conexão. Ele também pode ignorar o contexto de conexão e tratar os dados de forma idêntica, independentemente da conexão usada para enviar os dados. Ver [associação de contexto](../../connect/odbc/custom-keystore-providers.md#context-association) para obter mais informações.

#### <a name="reading-data-from-a-provider"></a>Leitura de um provedor de dados

Uma chamada para `SQLGetConnectAttr` usando o `SQL_COPT_SS_CEKEYSTOREDATA` atributo lê um "pacote" de dados do *o last-gravados-to* provedor. Se não houver nenhum, ocorre um erro de sequência de função. Os implementadores de provedor de repositório de chaves são incentivados a dar suporte a "fictício" gravações de 0 bytes como uma maneira de selecionar o provedor para operações de leitura sem causar outros efeitos colaterais se faz sentido fazê-lo.

```
SQLRETURN SQLGetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER BufferLength, SQLINTEGER * StringLengthPtr);
```
| Argumento | Descrição |
|:---|:---|
|`ConnectionHandle`|[Entrada] Identificador de Conexão. Deve ser um identificador de conexão válida, mas provedores carregados por meio do identificador de uma conexão são acessíveis de qualquer outro no mesmo processo.|
|`Attribute`|[Entrada] Atributo a ser recuperado: o `SQL_COPT_SS_CEKEYSTOREDATA` constante.|
|`ValuePtr`|[Saída] Um ponteiro para uma estrutura CEKeystoreData na qual a leitura do provedor de dados são colocados.|
|`BufferLength`|[Entrada] Constante SQL_IS_POINTER|
|`StringLengthPtr`|[Saída] Um ponteiro para um buffer no qual retornar BufferLength. Se * ValuePtr for um ponteiro nulo, nenhum comprimento será retornado.|

O chamador deve garantir que um buffer de tamanho suficiente seguindo a estrutura CEKEYSTOREDATA está alocado para o provedor gravar no. Após o retorno, seu campo dataSize é atualizado com o comprimento real dos dados lidos do provedor. Informações de erro detalhadas adicionais podem ser obtidas por meio [SQLGetDiacRec](https://msdn.microsoft.com/library/ms710921(v=vs.85).aspx).

Essa interface não coloca nenhum requisito adicional sobre o formato dos dados transferidos entre um aplicativo e um provedor de repositório de chaves. Cada provedor pode definir seu próprio formato de dados do protocolo, dependendo das suas necessidades.

Para obter um exemplo de implementação de seu próprio provedor de repositório de chaves, consulte [provedores de repositório de chaves personalizado](../../connect/odbc/custom-keystore-providers.md)

## <a name="limitations-of-the-odbc-driver-when-using-always-encrypted"></a>Limitações do driver ODBC ao usar o Always Encrypted

### <a name="asynchronous-operations"></a>Operações assíncronas
Embora o driver ODBC permitirá o uso de [operações assíncronas](../../relational-databases/native-client/odbc/creating-a-driver-application-asynchronous-mode-and-sqlcancel.md) com Always Encrypted, há um impacto no desempenho nas operações de quando o Always Encrypted está habilitado. A chamada para `sys.sp_describe_parameter_encryption` para determinar os metadados de criptografia para a instrução está bloqueando e fará com que o driver aguardar o servidor retorne os metadados antes de retornar `SQL_STILL_EXECUTING`.

### <a name="retrieve-data-in-parts-with-sqlgetdata"></a>Recuperar dados em partes com SQLGetData
Não é possível recuperar caracteres criptografados e colunas binárias em partes com o SQLGetData, antes de implantar o ODBC Driver 17 for SQL Server. É possível fazer apenas uma chamada para o SQLGetData com um buffer de comprimento adequado para incluir os dados da coluna inteira.

### <a name="send-data-in-parts-with-sqlputdata"></a>Enviar dados em partes com SQLPutData
Não é possível enviar dados de inserção ou comparação em partes com o SQLPutData. É possível fazer apenas uma chamada para o SQLPutData com um buffer contendo os dados completos. Para inserir dados longos em colunas criptografadas, use a API de Cópia em Massa, com um arquivo de dados de entrada, conforme descrito na seção a seguir.

### <a name="encrypted-money-and-smallmoney"></a>Money e smallmoney criptografados
Não é possível direcionar as colunas **money** criptografado ou **smallmoney** por parâmetros, porque não há tipos de dados ODBC específicos que mapeiem para esses tipos, gerando erros de Conflito de tipo de operando.

## <a name="bulk-copy-of-encrypted-columns"></a>Cópia em massa de colunas criptografadas

O uso das [funções de Cópia em Massa do SQL](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md) e do utilitário **bcp** tem suporte com o Always Encrypted, após a implantação do ODBC Driver 17 for SQL Server. Tanto o texto não criptografado (criptografado na inserção e descriptografado na recuperação) como o texto cifrado (textual transferido) podem ser inseridos e recuperados usando as APIs de cópia em massa (bcp_*) e o utilitário **bcp**.

- Para recuperar texto cifrado no formulário varbinary(max) (por exemplo, para carregamento em massa em um banco de dados diferente), conecte-se sem a opção `ColumnEncryption` (ou defina-a como `Disabled`) e execute uma operação BCP OUT.

- Para inserir e recuperar texto não criptografado e permitir que o driver execute criptografia e descriptografia de modo transparente conforme necessário, basta definir `ColumnEncryption` como `Enabled`. Caso contrário, a funcionalidade da API BCP permanece inalterada.

- Para inserir texto cifrado no formulário varbinary(max) (por exemplo, como recuperado acima), defina a opção `BCPMODIFYENCRYPTED` como TRUE e execute uma operação BCP IN. Para descriptografar os dados resultantes, verifique se a CEK da coluna do destino é a mesma da qual o texto cifrado foi originalmente obtido.

Ao usar o **bcp** utilitário: para controlar o `ColumnEncryption` configuração, use a opção -D e especifique um DSN que contém o valor desejado. Para inserir texto cifrado, verifique se o `ALLOW_ENCRYPTED_VALUE_MODIFICATIONS` configuração do usuário está habilitada.

A tabela a seguir fornece um resumo das ações ao operar em uma coluna criptografada:

|`ColumnEncryption`|Direção BCP|Descrição|
|----------------|-------------|-----------|
|`Disabled`|SAÍDA (para o cliente)|Recupera o texto cifrado. É o tipo de dados observado **varbinary (max)**.|
|`Enabled`|SAÍDA (para o cliente)|Recupera o texto sem formatação. O driver descriptografará os dados da coluna.|
|`Disabled`|IN (para servidor)|Insere o texto cifrado. Isso destina-se de forma opaca mover os dados criptografados sem a necessidade de ele ser descriptografadas. A operação falhará se o `ALLOW_ENCRYPTED_VALUE_MODIFICATIONS` opção não estiver definida no usuário ou BCPMODIFYENCRYPTED não está definido no identificador de conexão. Veja a seguir para obter mais informações.|
|`Enabled`|IN (para servidor)|Insere o texto sem formatação. O driver criptografará os dados da coluna.|

### <a name="the-bcpmodifyencrypted-option"></a>A opção BCPMODIFYENCRYPTED

Para evitar dados corrompidos, o servidor normalmente não permite inserir texto cifrado diretamente em uma coluna criptografada, e, portanto, tentar fazer isso falhará; No entanto, para carregamento em massa de dados criptografados usando a API BCP, definindo o `BCPMODIFYENCRYPTED` [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) opção como TRUE permitirá que o texto cifrado a serem inseridos diretamente e reduz o risco de corromper os dados criptografados pela configuração do `ALLOW_ENCRYPTED_VALUE_MODIFICATIONS` opção da conta de usuário. No entanto, as chaves devem corresponder aos dados e é uma boa ideia realizar algumas verificações de somente leitura dos dados inseridos após a inserção em massa e antes do uso adicional.

Veja [Migrar dados confidenciais protegidos por Always Encrypted](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md) para obter mais informações.

## <a name="always-encrypted-api-summary"></a>Resumo da API Always Encrypted

### <a name="connection-string-keywords"></a>Palavras-chave de cadeia de conexão

|Nome|Descrição|  
|----------|-----------------|  
|`ColumnEncryption`|Os valores aceitos são `Enabled` / `Disabled`.<br>`Enabled` -- habilita ou desabilita a funcionalidade Always Encrypted para a conexão.<br>`Disabled` – desabilitar a funcionalidade Always Encrypted para a conexão. <br><br>O padrão é `Disabled`.|  
|`KeyStoreAuthentication` | Valores válidos: `KeyVaultPassword`, `KeyVaultClientSecret` |
|`KeyStorePrincipalId` | Quando `KeyStoreAuthentication`  =  `KeyVaultPassword`, defina esse valor como um nome válido de entidade de usuário do Active Directory do Azure. <br>Quando `KeyStoreAuthetication`  =  `KeyVaultClientSecret` definir esse valor como um válido do Azure Active Directory aplicativo ID do cliente |
|`KeyStoreSecret` | Quando `KeyStoreAuthentication`  =  `KeyVaultPassword` definir esse valor como a senha para o nome de usuário correspondente. <br>Quando `KeyStoreAuthentication`  =  `KeyVaultClientSecret` definir esse valor como o segredo do aplicativo associado com um válido do Azure Active Directory aplicativo ID do cliente|

### <a name="connection-attributes"></a>Atributos de conexão

|Nome|Tipo|Descrição|  
|----------|-------|----------|  
|`SQL_COPT_SS_COLUMN_ENCRYPTION`|Pré-conectar-se|`SQL_COLUMN_ENCRYPTION_DISABLE` (0) – desabilitar Always Encrypted <br>`SQL_COLUMN_ENCRYPTION_ENABLE` (1)-- habilitar o Always Encrypted|
|`SQL_COPT_SS_CEKEYSTOREPROVIDER`|Após conectar-se|[Definido] Tentativa de carregar CEKeystoreProvider<br>[Introdução] Retorna um nome de CEKeystoreProvider|
|`SQL_COPT_SS_CEKEYSTOREDATA`|Após conectar-se|[Definido] Gravar dados CEKeystoreProvider<br>[Introdução] Ler dados de CEKeystoreProvider|
|`SQL_COPT_SS_CEKCACHETTL`|Após conectar-se|[Definido] Definir o cache CEK TTL<br>[Introdução] Obter o cache CEK TTL atual|
|`SQL_COPT_SS_TRUSTEDCMKPATHS`|Após conectar-se|[Definido] Definir o ponteiro de caminhos CMK confiável<br>[Introdução] Obter o ponteiro de caminhos CMK confiável atual|

### <a name="statement-attributes"></a>Atributos de instrução

|Nome|Descrição|  
|----------|-----------------|  
|`SQL_SOPT_SS_COLUMN_ENCRYPTION`|`SQL_CE_DISABLED` (0) – always Encrypted está desabilitada para a instrução <br>`SQL_CE_RESULTSETONLY` (1)-- apenas para descriptografia. Conjuntos de resultados e valores de retorno são descriptografados e parâmetros que não estão criptografados <br>`SQL_CE_ENABLED` (3) – always Encrypted está habilitado e usado para parâmetros e resultados|

### <a name="descriptor-fields"></a>Campos de descritor

|Campo IPD|Tamanho/tipo|Valor Padrão|Descrição|
|-|-|-|-|  
|`SQL_CA_SS_FORCE_ENCRYPT` (1236)|WORD (2 bytes)|0|Quando 0 (padrão): a decisão de criptografar esse parâmetro é determinado pela disponibilidade de metadados de criptografia.<br><br>Quando for diferente de zero: se os metadados de criptografia estão disponíveis para esse parâmetro, ele é criptografado. Caso contrário, a solicitação falha com erro [CE300] criptografia obrigatória do [Microsoft] [ODBC Driver 13 para SQL Server] foi especificada para um parâmetro, mas nenhum metadado de criptografia foi fornecido pelo servidor.|

### <a name="bcpcontrol-options"></a>Opções de bcp_control

|Nome da opção|Valor Padrão|Descrição|
|-|-|-|
|`BCPMODIFYENCRYPTED` (21)|FALSE|Quando for verdadeiro, permite que valores varbinary (max) a ser inserido em uma coluna criptografada. Quando for falso, evita a inserção, a menos que corrigir metadados de tipo e a criptografia é fornecido.|

## <a name="see-also"></a>Consulte Também

- [Always Encrypted (mecanismo de banco de dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Blog do Always Encrypted](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

