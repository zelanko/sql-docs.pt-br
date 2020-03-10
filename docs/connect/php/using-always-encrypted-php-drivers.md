---
title: Usando o Always Encrypted com o PHP Drivers for SQL Server | Microsoft Docs
ms.date: 12/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: v-kaywon
ms.author: jroth
author: rothja
manager: v-mabarw
ms.openlocfilehash: 17bd2297a81ed8c4b9e62f80a8bffd7a4c87af34
ms.sourcegitcommit: ff1bd69a8335ad656b220e78acb37dbef86bc78a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2020
ms.locfileid: "78340528"
---
# <a name="using-always-encrypted-with-the-php-drivers-for-sql-server"></a>Usar o Always Encrypted com o PHP Drivers for SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

## <a name="applicable-to"></a>Aplicável a
 -   Microsoft Drivers 5.2 for PHP for SQL Server
 
## <a name="introduction"></a>Introdução

Este artigo fornece informações sobre como desenvolver aplicativos PHP usando o [Always Encrypted (mecanismo de banco de dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) e o [PHP Drivers para SQL Server](../../connect/php/Microsoft-php-driver-for-sql-server.md).

O Always Encrypted permite que os aplicativos cliente criptografem dados confidenciais e nunca revelem os dados nem as chaves de criptografia para o SQL Server ou o Banco de Dados SQL do Azure. Um driver habilitado para Always Encrypted, como o ODBC Driver for SQL Server, criptografa e descriptografa de modo transparente dados confidenciais no aplicativo cliente. O driver determina automaticamente quais parâmetros de consulta correspondem às colunas de banco de dados confidenciais (protegidas com o Always Encrypted) e criptografa os valores desses parâmetros antes de passar os dados para o SQL Server ou o Banco de Dados SQL do Azure. Da mesma forma, o driver descriptografa de modo transparente os dados recuperados das colunas de banco de dados criptografadas nos resultados da consulta. Para obter mais informações, veja [Always Encrypted (Mecanismo de Banco de Dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md). Os PHP Drivers for SQL Server utilizam o ODBC Driver for SQL Server para criptografar dados confidenciais.

## <a name="prerequisites"></a>Pré-requisitos

 -   Configure o Sempre Criptografado em seu banco de dados. Essa configuração envolve o provisionamento de chaves do Always Encrypted e a configuração de criptografia de colunas de banco de dados selecionadas. Se você ainda não tiver um banco de dados com o Sempre Criptografado configurado, siga as instruções em [Getting Started with Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted)(Introdução ao Sempre Criptografado). Em particular, seu banco de dados deve conter as definições de metadados para uma chave mestra de coluna (CMK), uma chave de criptografia de coluna (CEK) e uma tabela contendo uma ou mais colunas criptografadas usando esse CEK.
 -   Verifique se a versão 17 ou posterior do ODBC Driver for SQL Server está instalada no computador de desenvolvimento. Para saber mais, confira [ODBC Driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md).

## <a name="enabling-always-encrypted-in-a-php-application"></a>Habilitar o Always Encrypted em um Aplicativo do PHP

A maneira mais fácil para habilitar a criptografia de parâmetros direcionados às colunas criptografadas e a descriptografia dos resultados da consulta é definindo o valor da palavra-chave da cadeia de conexão `ColumnEncryption` como `Enabled`. Veja a seguir exemplos de como habilitar Always Encrypted nos drivers SQLSRV e PDO_SQLSRV:

SQLSRV:
```
$connectionInfo = array("Database"=>$databaseName, "UID"=>$uid, "PWD"=>$pwd, "ColumnEncryption"=>"Enabled");
$conn = sqlsrv_connect($server, $connectionInfo);
```

PDO_SQLSRV:
```
$connectionInfo = "Database = $databaseName; ColumnEncryption = Enabled;";
$conn = new PDO("sqlsrv:server = $server; $connectionInfo", $uid, $pwd);
```

Habilitar o Always Encrypted não é suficiente para o êxito da criptografia ou descriptografia. Do mesmo modo, é preciso ter certeza de que:
 -   O aplicativo tem as permissões de banco de dados VIEW ANY COLUMN MASTER KEY DEFINITION e VIEW ANY COLUMN ENCRYPTION KEY DEFINITION, necessárias para acessar os metadados sobre as chaves do Always Encrypted no banco de dados. Para saber mais, confira [Permissão de banco de dados](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions).
 -   O aplicativo pode acessar a CMK que protege as CEKs para as colunas criptografadas consultadas. Esse requisito é dependente do provedor do repositório de chaves que armazena o CMK. Para saber mais, confira [Como trabalhar com repositórios de chaves mestras de coluna](#working-with-column-master-key-stores).

## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>Recuperando e modificando dados em colunas criptografadas

Depois de habilitar o Always Encrypted em uma conexão, você pode usar APIs de SQLSRV padrão (confira [Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)) ou APIs do PDO_SQLSRV (confira [Referência da API do driver PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)) para recuperar ou modificar dados em colunas de banco de dados criptografadas. Supondo que seu aplicativo tem as permissões de banco de dados e pode acessar a chave mestra de coluna, o driver criptografa quaisquer parâmetros de consulta que se destinam a colunas criptografadas e descriptografa os dados recuperados de colunas criptografadas, comportando-se de forma transparente para o aplicativo, como se as colunas não fossem criptografadas.

Se o Always Encrypted não estiver habilitado, as consultas com parâmetros que se destinam a colunas criptografadas falharão. Os dados ainda podem ser recuperados de colunas criptografadas, desde que a consulta não tenha parâmetros que se destinem a colunas criptografadas. No entanto, o driver não tenta descriptografar nenhuma criptografia e o aplicativo recebe os dados binários criptografados (como matrizes de bytes).

A tabela abaixo resume o comportamento das consultas dependendo se Always Encrypted está habilitado ou não:

|Característica da consulta|O Always Encrypted está habilitado e o aplicativo pode acessar as chaves e os metadados da chave|O Sempre Criptografado está habilitado e o aplicativo não pode acessar as chaves nem os metadados da chave|O Sempre Criptografado está desabilitado|
|---|---|---|---|
|Parâmetros que se destinam a colunas criptografadas.|Os valores de parâmetro são criptografados de modo transparente.|Erro|Erro|
|Recuperando dados de colunas criptografadas, sem parâmetros que se destinam a colunas criptografadas.|Os resultados das colunas criptografadas são descriptografados de modo transparente. O aplicativo recebe valores de coluna de texto não criptografado. |Erro|Os resultados das colunas criptografadas não são descriptografados. O aplicativo recebe valores criptografados como matrizes de bytes.|
 
Os exemplos a seguir ilustram como recuperar e modificar dados em colunas criptografadas. Por exemplo, considere uma tabela com o seguinte esquema. As colunas SSN e BirthDate estão criptografadas.
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
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY])
 GO
```

### <a name="data-insertion-example"></a>Exemplo de inserção de dados

Os exemplos a seguir demonstram como usar os drivers SQLSRV e PDO_SQLSRV para inserir uma linha na tabela Pacientes. Observe os seguintes pontos:
 -   Não há nada específico de criptografia no código de exemplo. O driver detecta e criptografa automaticamente os valores dos parâmetros de SSN e BirthDate que se destinam a colunas criptografadas. Esse mecanismo torna a criptografia transparente para o aplicativo.
 -   Os valores inseridos nas colunas de banco de dados, incluindo as colunas criptografadas, são passados como parâmetros associados. Embora o uso de parâmetros seja opcional ao enviar valores para colunas não criptografadas (mesmo que seja altamente recomendável, pois ajuda a prevenir a injeção de SQL), ele é necessário para valores que se destinam a colunas criptografadas. Se os valores inseridos nas colunas SSN ou BirthDate foram passados como literais inseridos na instrução de consulta, a consulta falha, pois o driver não tenta criptografar ou processar os literais em consultas. Como resultado, o servidor os rejeitaria como incompatíveis com as colunas criptografadas.
 -   Ao inserir valores usando parâmetros de associação, um tipo SQL que é idêntico ao tipo de dados da coluna de destino ou cuja conversão para o tipo de dados da coluna de destino é compatível deve ser passado ao banco de dados. Esse requisito existe porque o Always Encrypted dá suporte a algumas conversões de tipo (para saber mais, confira [Always Encrypted (Mecanismo de Banco de Dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)). Os dois drivers PHP, SQLSRV e PDO_SQLSRV, têm um mecanismo para ajudar o usuário a determinar o tipo SQL do valor. Portanto, o usuário não precisa fornecer o tipo SQL explicitamente.
  -   Para o driver SQLSRV, o usuário tem duas opções:
   -   Confiar no driver PHP para determinar e definir o tipo SQL correto. Nesse caso, o usuário deve usar `sqlsrv_prepare` e `sqlsrv_execute` para executar uma consulta parametrizada.
   -   Definir o tipo SQL explicitamente.
  -   Para o driver PDO_SQLSRV, o usuário não tem a opção de definir explicitamente o tipo SQL de um parâmetro. Ao associar um parâmetro, o driver PDO_SQLSRV ajuda automaticamente o usuário a determinar o tipo SQL.
 -   Para os drivers determinarem o tipo SQL, algumas limitações se aplicam:
  -   Driver SQLSRV:
   -   Se o usuário quiser que o driver determine os tipos SQL para as colunas criptografadas, ele deverá usar `sqlsrv_prepare` e `sqlsrv_execute`.
   -   Se `sqlsrv_query` for preferencial, o usuário será responsável por especificar os tipos SQL para todos os parâmetros. O tipo SQL especificado deve incluir o comprimento da cadeia de caracteres para tipos de cadeia de caracteres e a escala e precisão para tipos decimais.
  -   Driver PDO_SQLSRV:
   -   Não há suporte para o atributo de instrução `PDO::SQLSRV_ATTR_DIRECT_QUERY` em uma consulta parametrizada.
   -   Não há suporte para o atributo de instrução `PDO::ATTR_EMULATE_PREPARES` em uma consulta parametrizada.
   
Driver SQLSRV e [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md):
```
// insertion into encrypted columns must use a parameterized query
$query = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?)";
$ssn = "795-73-9838";
$firstName = "Catherine";
$lastName = "Abel;
$birthDate = "1996-10-19";
$params = array($ssn, $firstName, $lastName, $birthDate);
// during sqlsrv_prepare, the driver determines the SQL types for each parameter and pass them to SQL server
$stmt = sqlsrv_prepare($conn, $query, $params);
sqlsrv_execute($stmt);
```

Driver SQLSRV e [sqlsrv_query](../../connect/php/sqlsrv-query.md):
```
// insertion into encrypted columns must use a parameterized query
$query = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?)";
$ssn = "795-73-9838";
$firstName = "Catherine";
$lastName = "Abel";
$birthDate = "1996-10-19";
// need to provide the SQL types for ALL parameters  
// note the SQL types (including the string length) have to be the same at the column definition
$params = array(array(&$ssn, null, null, SQLSRV_SQLTYPE_CHAR(11)),
                array(&$firstName, null, null, SQLSRV_SQLTYPE_NVARCHAR(50)),
                array(&$lastName, null, null, SQLSRV_SQLTYPE_NVARCHAR(50)),
                array(&$birthDate, null, null, SQLSRV_SQLTYPE_DATE));
sqlsrv_query($conn, $query, $params);
```

Driver PDO_SQLSRV e [PDO::prepare](../../connect/php/pdo-prepare.md):
```
// insertion into encrypted columns must use a parameterized query
$query = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?)";
$ssn = "795-73-9838";
$firstName = "Catherine";
$lastName = "Able";
$birthDate = "1996-10-19";
// during PDO::prepare, the driver determines the SQL types for each parameter and pass them to SQL server
$stmt = $conn->prepare($query);
$stmt->bindParam(1, $ssn);
$stmt->bindParam(2, $firstName);
$stmt->bindParam(3, $lastName);
$stmt->bindParam(4, $birthDate);
$stmt->execute();
```

### <a name="plaintext-data-retrieval-example"></a>Exemplo de recuperação de dados de texto não criptografado

Os exemplos a seguir demonstram a filtragem de dados com base em valores criptografados e a recuperação de dados de texto não criptografado de colunas criptografadas usando os drivers SQLSRV e PDO_SQLSRV. Observe os seguintes pontos:
 -   O valor usado na cláusula WHERE a ser filtrado na coluna SSN precisa ser passado como um parâmetro using bind para que o driver possa criptografá-lo de modo transparente antes de enviá-lo ao servidor.
 -   Ao executar uma consulta com parâmetros associados, os drivers PHP determinam automaticamente o tipo SQL para o usuário, a menos que o usuário especifique explicitamente o tipo SQL ao usar o driver SQLSRV.
 -   Todos os valores impressos pelo programa estão em texto não criptografado, já que o driver descriptografa de modo transparente os dados recuperados das colunas SSN e BirthDate.
 
Observação: Consultas podem executar comparações de igualdade em colunas criptografadas somente se a criptografia for determinística. Para obter mais informações, confira [Seleção de criptografia determinística ou aleatória](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption).

SQLSRV:
```
// since SSN is an encrypted column, need to pass the value in the WHERE clause through bind parameter
$query = "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN] = ?";
$ssn = "795-73-9838";
$stmt = sqlsrv_prepare($conn, $query, array(&$ssn));
// during sqlsrv_execute, the driver encrypts the ssn value and passes it to the database
sqlsrv_execute($stmt);
// fetch like usual
$row = sqlsrv_fetch_array($stmt);
```

PDO_SQLSRV:
```
// since SSN is an encrypted column, need to pass the value in the WHERE clause through bind parameter
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN] = ?";
$ssn = "795-73-9838";
$stmt = $conn->prepare($query);
$stmt->bindParam(1, $ssn);
// during PDOStatement::execute, the driver encrypts the ssn value and passes it to the database
$stmt->execute();
// fetch like usual
$row = $stmt->fetch();
```

### <a name="ciphertext-data-retrieval-example"></a>Exemplo de recuperação de dados de texto cifrado

Se o Always Encrypted não estiver habilitado, uma consulta ainda poderá recuperar dados de colunas criptografadas, desde que a consulta não tenha parâmetros que se destinam a colunas criptografadas.

Os exemplos a seguir ilustram como recuperar dados binários criptografados de colunas criptografadas usando os drivers SQLSRV e PDO_SQLSRV. Observe os seguintes pontos:
 -   Como o Always Encrypted não está habilitado na cadeia de conexão, a consulta retorna valores criptografados de SSN e BirthDate como matrizes de bytes (o programa converte os valores em cadeias de caracteres).
 -   Uma consulta que recupera dados de colunas criptografadas com o Sempre Criptografado desabilitado pode ter parâmetros, desde que nenhum dos parâmetros se destinem a uma coluna criptografada. A consulta a seguir filtra por LastName, que não é criptografado no banco de dados. Se a consulta filtrar por SSN ou BirthDate, a consulta falhará.
 
SQLSRV:
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [LastName] = ?";
$lastName = "Abel";
$stmt = sqlsrv_prepare($conn, $query, array(&$lastName));
sqlsrv_execute($stmt);
$row = sqlsrv_fetch_array($stmt);
```

PDO_SQLSRV:
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [LastName] = ?";
$lastName = "Abel";
$stmt = $conn->prepare($query);
$stmt->bindParam(1, $lastName);
$stmt->execute();
$row = $stmt->fetch();
```

### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>Evitando problemas comuns ao consultar colunas criptografadas

Esta seção descreve as categorias comuns de erros ao consultar colunas criptografadas de aplicativos PHP e algumas diretrizes para como evitá-los.

#### <a name="unsupported-data-type-conversion-errors"></a>Erros de conversão de tipo de dados sem suporte

O Always Encrypted dá suporte a algumas conversões de tipos de dados criptografados. Confira [Always Encrypted (Mecanismo de Banco de Dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) para obter a lista detalhada de conversões de tipo compatíveis. Faça o seguinte para evitar erros de conversão de tipo de dados:
 -   Ao usar o driver SQLSRV com `sqlsrv_prepare` e `sqlsrv_execute`, o tipo SQL é determinado automaticamente junto com o tamanho da coluna e o número de dígitos decimais do parâmetro.
 -   Ao usar o driver PDO_SQLSRV para executar uma consulta, o tipo SQL com o tamanho da coluna e o número de dígitos decimais do parâmetro também é determinado automaticamente
 -   Ao usar o driver SQLSRV com `sqlsrv_query` para executar uma consulta:
  -   O tipo SQL do parâmetro é exatamente o mesmo que o tipo da coluna de destino, ou a conversão de um tipo SQL para o tipo da coluna é suportada.
  -   A precisão e a escala dos parâmetros que se destinam às colunas dos tipos de dados `decimal` e `numeric` do SQL Server são iguais à precisão e à escala configuradas para a coluna de destino.
  -   A precisão dos parâmetros que se destinam às colunas dos tipos de dados `datetime2`, `datetimeoffset` ou `time` do SQL Server não é maior que a precisão da coluna de destino, em consultas que modificam a coluna de destino.
 -   Não use atributos de instrução `PDO::SQLSRV_ATTR_DIRECT_QUERY` ou `PDO::ATTR_EMULATE_PREPARES` do PDO_SQLSRV em uma consulta parametrizada
 
#### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>Erros devido à passagem de texto sem formatação em vez de valores criptografados

Qualquer valor que se destina a uma coluna criptografada precisa ser criptografado antes de ser enviado ao servidor. Uma tentativa de inserir, modificar ou filtrar por um valor de texto não criptografado em uma coluna criptografada resulta em um erro. Para evitar esses erros, garanta que:
 -   O Always Encrypted esteja habilitado (na cadeia de conexão, defina a palavra-chave `ColumnEncryption` como `Enabled`).
 -   Use o parâmetro de associação para enviar dados que se destinam a colunas criptografadas. O exemplo a seguir mostra uma consulta filtrada incorretamente por um literal/constante em uma coluna criptografada (SSN):
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
```

## <a name="controlling-performance-impact-of-always-encrypted"></a>Controlando o impacto no desempenho do Sempre Criptografado

Como o Always Encrypted é uma tecnologia de criptografia do lado do cliente, a maior parte da sobrecarga de desempenho é observada no lado do cliente, não no banco de dados. Além do custo das operações de criptografia e descriptografia, as outras fontes de sobrecarga de desempenho no lado do cliente são:
 -   Viagens de ida e volta adicionais ao banco de dados para recuperar metadados dos parâmetros de consulta.
 -   Chamadas a um repositório de chaves mestras de coluna para acessar uma chave mestra de coluna.
 
### <a name="round-trips-to-retrieve-metadata-for-query-parameters"></a>Viagens de ida e volta para recuperar metadados dos parâmetros de consulta

Se o Always Encrypted estiver habilitado para uma conexão, por padrão, o ODBC Driver chamará [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) para cada consulta parametrizada, passando a instrução de consulta (sem nenhum valor de parâmetro) para o SQL Server. Este procedimento armazenado analisa a instrução de consulta para descobrir se os parâmetros precisam ser criptografados e, se for o caso, retorna as informações relacionadas à criptografia para cada parâmetro para permitir ao driver criptografá-los.

Como os drivers PHP permitem que o usuário associe um parâmetro em uma instrução preparada sem fornecer o tipo SQL, ao associar um parâmetro em uma conexão habilitada Always Encrypted, os drivers PHP chamam o [SQLDescribeParam](../../odbc/reference/syntax/sqldescribeparam-function.md) no parâmetro para obter o tipo SQL, o tamanho da coluna e os dígitos decimais. Os metadados são usados para chamar o [SQLBindParameter]( ../../odbc/reference/syntax/sqlbindparameter-function.md). Essas chamadas extras de `SQLDescribeParam` não exigem viagens adicionais de ida e volta ao banco de dados, pois o driver ODBC já armazenou as informações no lado do cliente quando `sys.sp_describe_parameter_encryption` foi chamado.

Os comportamentos anteriores garantem um alto nível de transparência ao aplicativo cliente (e o desenvolvedor do aplicativo) não precisa estar ciente de quais consultas acessam colunas criptografadas, desde que os valores que se destinam às colunas criptografadas sejam passados para o driver nos parâmetros.

Ao contrário do driver ODBC para SQL Server, ainda não há suporte nos drivers PHP para habilitação de Always Encrypted no nível da instrução/consulta. 

### <a name="column-encryption-key-caching"></a>Cache de chaves de criptografia de coluna

Para reduzir o número de chamadas a um repositório de chaves mestras de coluna para descriptografar chaves de criptografia de coluna (CEK), o driver armazena CEKs de texto não criptografado na memória. Depois de receber a CEK criptografada (ECEK) dos metadados do banco de dados, o driver do ODBC primeiro tenta encontrar a CEK de texto não criptografado correspondente ao valor da chave criptografada no cache. O driver chama o repositório de chaves que contém a CMK somente se ele não conseguir localizar a CEK de texto não criptografado correspondente no cache.

Observação: No ODBC Driver for SQL Server, as entradas no cache são removidas após um tempo limite de duas horas. Esse comportamento significa que, para determinada ECEK, o driver entra em contato com o repositório de chaves apenas uma vez durante o tempo de vida do aplicativo, ou a cada duas horas, o que for menor.

## <a name="working-with-column-master-key-stores"></a>Trabalhando com repositórios de chaves mestras de coluna

Para criptografar ou descriptografar dados, o driver precisa obter uma CEK que é configurada para a coluna de destino. As CEKs são armazenadas em formato criptografado (ECEKs) nos metadados do banco de dados. Cada CEK tem uma CMK correspondente que foi usada para criptografá-la. Os [metadados de banco de dados](../../t-sql/statements/create-column-master-key-transact-sql.md) não armazenam a CMK em si. Eles contêm apenas o nome do repositório de chaves e as informações que o repositório de chaves pode usar para localizar a CMK.

Para obter o valor de texto não criptografado de uma ECEK, o driver primeiro obtém os metadados sobre a CEK e sua CMK correspondente e, em seguida, usa essas informações para entrar em contato com o repositório de chaves que contém a CMK e solicitar para descriptografar a ECEK. O driver se comunica com um repositório de chaves usando um provedor de repositório de chaves.

No Microsoft Driver 5.3.0 para PHP para SQL Server, existe suporte somente para o Provedor de Repositório de Certificados do Windows e o Azure Key Vault. Ainda não há suporte para o outro Provedor de Repositório de Chaves com suporte do driver ODBC (Provedor de Repositório de Chaves Personalizado).

### <a name="using-the-windows-certificate-store-provider"></a>Uso do Provedor do Repositório de Certificados do Windows

O ODBC Driver for SQL Server no Windows inclui um provedor de repositório de chaves mestras de coluna interno para o Repositório de Certificados do Windows chamado `MSSQL_CERTIFICATE_STORE`. (Esse provedor não está disponível no macOS ou no Linux.) Com esse provedor, a CMK é armazenada localmente no computador cliente e nenhuma configuração adicional pelo aplicativo é necessária para usá-la com o driver. No entanto, o aplicativo deve ter acesso ao certificado e sua chave privada no repositório. Para obter mais informações, consulte [Create and Store Column Master Keys (Always Encrypted)](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)Criar e armazenar chaves mestras de coluna (Always Encrypted).

### <a name="using-azure-key-vault"></a>Como usar o Azure Key Vault

O Azure Key Vault oferece uma maneira de armazenar chaves de criptografia, senhas e outros dados confidenciais usando o Azure e pode ser usado para armazenar chaves para Always Encrypted. O ODBC Driver for SQL Server (versão 17 e posteriores) inclui um provedor de repositório de chaves mestras interno para o Azure Key Vault. As seguintes opções de conexão usam a configuração do Azure Key Vault: `KeyStoreAuthentication`, `KeyStorePrincipalId` e `KeyStoreSecret`. 
 -   `KeyStoreAuthentication` pode usar um dos dois valores de cadeia de caracteres possíveis: `KeyVaultPassword` e `KeyVaultClientSecret`. Esses valores controlam quais tipo de credenciais de autenticação são usadas com as outras duas palavras-chave.
 -   `KeyStorePrincipalId` usa uma cadeia de caracteres que representa um identificador da conta que quer acessar o Azure Key Vault. 
     -   Se `KeyStoreAuthentication` for definido como `KeyVaultPassword`, `KeyStorePrincipalId` deverá ser o nome de um usuário do Azure ActiveDirectory.
     -   Se `KeyStoreAuthentication` for definido como `KeyVaultClientSecret`, `KeyStorePrincipalId` deverá ser uma ID de cliente de aplicativo.
 -   `KeyStoreSecret` usa uma cadeia de caracteres que representa um segredo de credencial. 
     -   Se `KeyStoreAuthentication` for definido como `KeyVaultPassword`, `KeyStoreSecret` deverá ser a senha do usuário. 
     -   Se `KeyStoreAuthentication` for definido como `KeyVaultClientSecret`, `KeyStoreSecret` deverá ser o segredo do aplicativo associado à ID do cliente do aplicativo.

Todas as três opções devem estar presentes na cadeia de conexão para usar o Azure Key Vault. Além disso, `ColumnEncryption` deve ser definido como `Enabled`. Se `ColumnEncryption` for definido como `Disabled`, mas as opções do Azure Key Vault estiverem presentes, o script continuará sem erros, mas não será executada criptografia.

Os exemplos a seguir mostram como se conectar ao SQL Server usando o Azure Key Vault.

SQLSRV:

Usar uma conta do Azure Active Directory:
```
$connectionInfo = array("Database"=>$databaseName, "UID"=>$uid, "PWD"=>$pwd, "ColumnEncryption"=>"Enabled", "KeyStoreAuthentication"=>"KeyVaultPassword", "KeyStorePrincipalId"=>$AADUsername, "KeyStoreSecret"=>$AADPassword);
$conn = sqlsrv_connect($server, $connectionInfo);
```
Usar uma ID e um segredo do cliente do aplicativo Azure:
```
$connectionInfo = array("Database"=>$databaseName, "UID"=>$uid, "PWD"=>$pwd, "ColumnEncryption"=>"Enabled", "KeyStoreAuthentication"=>"KeyVaultClientSecret", "KeyStorePrincipalId"=>$applicationClientID, "KeyStoreSecret"=>$applicationClientSecret);
$conn = sqlsrv_connect($server, $connectionInfo);
```

PDO_SQLSRV: Usar uma conta do Azure Active Directory:
```
$connectionInfo = "Database = $databaseName; ColumnEncryption = Enabled; KeyStoreAuthentication = KeyVaultPassword; KeyStorePrincipalId = $AADUsername; KeyStoreSecret = $AADPassword;";
$conn = new PDO("sqlsrv:server = $server; $connectionInfo", $uid, $pwd);
```
Usar uma ID e um segredo do cliente do aplicativo Azure:
```
$connectionInfo = "Database = $databaseName; ColumnEncryption = Enabled; KeyStoreAuthentication = KeyVaultClientSecret; KeyStorePrincipalId = $applicationClientID; KeyStoreSecret = $applicationClientSecret;";
$conn = new PDO("sqlsrv:server = $server; $connectionInfo", $uid, $pwd);
```

## <a name="limitations-of-the-php-drivers-when-using-always-encrypted"></a>Limitações de drivers PHP ao usar o Always Encrypted

SQLSRV e PDO_SQLSRV:
 -   O Linux/macOS não dá suporte ao Provedor de Repositório de Certificados do Windows
 -   Forçando a criptografia de parâmetro
 -   Habilitar o Always Encrypted no nível da instrução 
 -   Ao usar o recurso Always Encrypted e localidades não UTF8 no Linux e no macOS (como "en_US.ISO-8859-1"), a inserção de dados nulos ou uma cadeia de caracteres vazia na coluna de caracteres criptografados (n) pode não funcionar, a menos que a página de código 1252 esteja instalada em seu sistema
 
Somente no SQLSRV:
 -   Usar `sqlsrv_query` como parâmetro de associação sem especificar o tipo SQL
 -   Usar `sqlsrv_prepare` como parâmetros de associação em um lote de instruções SQL  
 
Somente no PDO_SQLSRV:
 -   O atributo de instrução `PDO::SQLSRV_ATTR_DIRECT_QUERY` especificado em uma consulta parametrizada
 -   O atributo de instrução `PDO::ATTR_EMULATE_PREPARE` especificado em uma consulta parametrizada
 -   parâmetros de associação em um lote de instruções SQL
 
Os drivers PHP também herdam as limitações impostas pelo banco de dados e pelo ODBC Driver for SQL Server. Confira [Limitações do Driver ODBC ao usar Always Encrypted](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) e [Detalhes do recurso Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md#feature-details).  
  
## <a name="see-also"></a>Consulte Também  
[Guia de programação para o driver SQL de PHP](../../connect/php/programming-guide-for-php-sql-driver.md)

[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  

[Referência da API do Driver PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
