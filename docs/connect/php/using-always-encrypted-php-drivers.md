---
title: Usando o Always Encrypted com o PHP Drivers for SQL Server | Microsoft Docs
ms.date: 01/08/2018
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
manager: mbarwin
ms.openlocfilehash: 531286af24740e37e125708a4b874b6aba27c3dc
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52403421"
---
# <a name="using-always-encrypted-with-the-php-drivers-for-sql-server"></a>Usando o Always Encrypted com o PHP Drivers for SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

## <a name="applicable-to"></a>Aplicável a
 -   Microsoft Drivers 5.2 for PHP for SQL Server
 
## <a name="introduction"></a>Introdução

Este artigo fornece informações sobre como desenvolver aplicativos PHP usando [Always Encrypted (mecanismo de banco de dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) e o [Drivers de PHP para SQL Server](../../connect/php/Microsoft-php-driver-for-sql-server.md).

O Always Encrypted permite que os aplicativos cliente criptografem dados confidenciais e nunca revelem os dados nem as chaves de criptografia para o SQL Server ou o Banco de Dados SQL do Azure. Um driver habilitado para Always Encrypted, como o ODBC Driver for SQL Server, criptografa e descriptografa de modo transparente dados confidenciais no aplicativo cliente. O driver determina automaticamente quais parâmetros de consulta correspondem às colunas de banco de dados confidenciais (protegidas com o Always Encrypted) e criptografa os valores desses parâmetros antes de passar os dados para o SQL Server ou o Banco de Dados SQL do Azure. Da mesma forma, o driver descriptografa de modo transparente os dados recuperados das colunas de banco de dados criptografadas nos resultados da consulta. Para obter mais informações, veja [Always Encrypted (Mecanismo de Banco de Dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md). Os Drivers de PHP para SQL Server utilizam o ODBC Driver for SQL Server criptografar dados confidenciais.

## <a name="prerequisites"></a>Prerequisites

 -   Configure o Sempre Criptografado em seu banco de dados. Essa configuração envolve o provisionamento de chaves do Always Encrypted e a configuração de criptografia de colunas de banco de dados selecionadas. Se você ainda não tiver um banco de dados com o Sempre Criptografado configurado, siga as instruções em [Getting Started with Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted)(Introdução ao Sempre Criptografado). Em particular, o banco de dados deve conter as definições de metadados para uma chave mestra de coluna (CMK), uma chave de criptografia de coluna (CEK) e uma tabela contendo uma ou mais colunas criptografadas usando esse CEK.
 -   Verifique se o que driver ODBC para SQL Server versão 17 ou posterior está instalado no computador de desenvolvimento. Para obter detalhes, consulte [ODBC Driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md).

## <a name="enabling-always-encrypted-in-a-php-application"></a>Habilitando o Always Encrypted em um aplicativo PHP

A maneira mais fácil para habilitar a criptografia de parâmetros direcionados às colunas criptografadas e a descriptografia dos resultados da consulta é definindo o valor da palavra-chave da cadeia de conexão `ColumnEncryption` como `Enabled`. A seguir estão exemplos de habilitar o Always Encrypted em que os drivers SQLSRV e PDO_SQLSRV:

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

Habilitar o sempre criptografado não é suficiente para a criptografia ou descriptografia seja bem-sucedida; Você também precisará ter certeza de que:
 -   O aplicativo tem as permissões de banco de dados VIEW ANY COLUMN MASTER KEY DEFINITION e VIEW ANY COLUMN ENCRYPTION KEY DEFINITION, necessárias para acessar os metadados sobre as chaves do Always Encrypted no banco de dados. Para obter detalhes, consulte [permissão de banco de dados](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions).
 -   O aplicativo pode acessar a CMK que protege os CEKs para as colunas criptografadas consultadas. Esse requisito depende do provedor de repositório de chaves que armazena a CMK. Para obter mais informações, consulte [trabalhando com repositórios de chaves mestras de coluna](#working-with-column-master-key-stores).

## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>Recuperando e modificando dados em colunas criptografadas

Depois de habilitar o Always Encrypted em uma conexão, você pode usar APIs do SQLSRV padrão (consulte [referência da API do Driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)) ou as APIs de PDO_SQLSRV (consulte [referência de API do Driver PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)) para recuperar ou modificar dados nas colunas de banco de dados criptografado. Supondo que seu aplicativo tem as permissões de banco de dados necessários e pode acessar a chave mestra de coluna, o driver criptografa todos os parâmetros que se destinam a colunas criptografadas e descriptografar os dados recuperados de colunas criptografadas, comportando-se de forma transparente para o aplicativo como se as colunas não foram criptografadas.

Se o Always Encrypted não estiver habilitado, as consultas com parâmetros que se destinam a colunas criptografadas falharão. Os dados ainda podem ser recuperados de colunas criptografadas, desde que a consulta não tenha parâmetros que se destinem a colunas criptografadas. No entanto, o driver não tentará qualquer descriptografia e o aplicativo recebe os dados binários criptografados (como matrizes de bytes).

A tabela abaixo resume o comportamento das consultas dependendo se Always Encrypted está habilitado ou não:

|Característica da consulta|O Sempre Criptografado está habilitado e o aplicativo pode acessar as chaves e os metadados da chave|O Sempre Criptografado está habilitado e o aplicativo não pode acessar as chaves nem os metadados da chave|O Sempre Criptografado está desabilitado|
|---|---|---|---|
|Parâmetros que se destinam a colunas criptografadas.|Os valores de parâmetro são criptografados de modo transparente.|Erro|Erro|
|Recuperando dados de colunas criptografadas, sem parâmetros que se destinam a colunas criptografadas.|Os resultados das colunas criptografadas são descriptografados de modo transparente. O aplicativo recebe valores de coluna de texto sem formatação. |Erro|Os resultados das colunas criptografadas não são descriptografados. O aplicativo recebe valores criptografados como matrizes de bytes.|
 
Os exemplos a seguir ilustram como recuperar e modificar dados em colunas criptografadas. Os exemplos assumem uma tabela com o esquema a seguir. As colunas SSN e BirthDate estão criptografadas.
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

Os exemplos a seguir demonstram como usar os drivers SQLSRV e PDO_SQLSRV para inserir uma linha na tabela pacientes. Observe os seguintes pontos:
 -   Não há nada específico de criptografia no código de exemplo. O driver detecta automaticamente e criptografa os valores dos parâmetros de SSN e BirthDate, que se destinam a colunas criptografadas. Esse mecanismo torna a criptografia transparente para o aplicativo.
 -   Os valores inseridos nas colunas de banco de dados, incluindo as colunas criptografadas, são passados como parâmetros associados. Embora o uso de parâmetros seja opcional ao enviar valores para colunas não criptografadas (mesmo que seja altamente recomendável, pois ajuda a prevenir a injeção de SQL), ele é necessário para valores que se destinam a colunas criptografadas. Se os valores inseridos nas colunas SSN ou BirthDate fossem passados como literais inseridos na instrução de consulta, a consulta falharia, pois o driver não tentará criptografar ou processar os literais em consultas. Como resultado, o servidor os rejeitaria como incompatíveis com as colunas criptografadas.
 -   Ao inserir valores usando os parâmetros de ligação, um tipo SQL que é idêntico ao tipo de dados da coluna de destino ou cuja conversão para o tipo de dados da coluna de destino é suportado deve ser passado para o banco de dados. Esse requisito existe porque o Always Encrypted dá suporte a algumas conversões de tipo (para obter detalhes, consulte [Always Encrypted (mecanismo de banco de dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)). Os dois drivers PHP, SQLSRV e PDO_SQLSRV, cada um tem um mecanismo para ajudar o usuário a determinar o tipo do valor de SQL. Portanto, o usuário não precisa fornecer o tipo SQL explicitamente.
  -   Para o driver SQLSRV, o usuário tem duas opções:
   -   Contar com o driver do PHP para determinar e definir o tipo correto do SQL. Nesse caso, o usuário deve usar `sqlsrv_prepare` e `sqlsrv_execute` para executar uma consulta parametrizada.
   -   Defina explicitamente o tipo de SQL.
  -   Para o driver PDO_SQLSRV, o usuário não tem a opção de definir explicitamente o tipo SQL de um parâmetro. O driver PDO_SQLSRV automaticamente ajuda o usuário a determinar o tipo SQL ao associar um parâmetro.
 -   Para os drivers determinar o tipo SQL, algumas limitações se aplicam:
  -   Driver SQLSRV:
   -   Se o usuário deseja o driver para determinar os tipos SQL para as colunas criptografadas, o usuário deve usar `sqlsrv_prepare` e `sqlsrv_execute`.
   -   Se `sqlsrv_query` é preferencial, o usuário é responsável por especificar os tipos de SQL para todos os parâmetros. O tipo SQL especificado deve incluir o comprimento da cadeia de caracteres para tipos de cadeia de caracteres e a escala e precisão dos tipos de decimais.
  -   Driver PDO_SQLSRV:
   -   O atributo de instrução `PDO::SQLSRV_ATTR_DIRECT_QUERY` não tem suporte em uma consulta parametrizada.
   -   O atributo de instrução `PDO::ATTR_EMULATE_PREPARES` não tem suporte em uma consulta parametrizada.
   
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

Driver PDO_SQLSRV e [PDO:: Prepare](../../connect/php/pdo-prepare.md):
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

### <a name="plaintext-data-retrieval-example"></a>Exemplo de recuperação de dados de texto sem formatação

Os exemplos a seguir demonstram a filtragem de dados com base em valores criptografados e recuperando dados de texto sem formatação de colunas criptografadas usando os drivers SQLSRV e PDO_SQLSRV. Observe os seguintes pontos:
 -   O valor usado na cláusula WHERE a ser filtrado na coluna SSN precisa ser passado como um parâmetro using bind para que o driver possa criptografá-lo de modo transparente antes de enviá-lo ao servidor.
 -   Ao executar uma consulta com parâmetros associados, os drivers PHP determina automaticamente o tipo SQL para o usuário, a menos que o usuário especifica explicitamente o tipo SQL usando o driver SQLSRV.
 -   Todos os valores impressos pelo programa estarão em texto não criptografado, já que o driver descriptografará de modo transparente os dados recuperados das colunas SSN e BirthDate.
 
Observação: Consultas só podem executar comparações de igualdade em colunas criptografadas se a criptografia é determinística. Para obter mais informações, confira [Seleção de criptografia determinística ou aleatória](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption).

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
 -   Ao usar o driver SQLSRV com `sqlsrv_prepare` e `sqlsrv_execute` o tipo SQL, juntamente com o tamanho da coluna e o número de casas decimais do parâmetro é determinado automaticamente.
 -   Ao usar o driver PDO_SQLSRV para executar uma consulta, o tipo SQL com o tamanho da coluna e o número de casas decimais do parâmetro é determinado automaticamente
 -   Ao usar o driver SQLSRV com `sqlsrv_query` para executar uma consulta:
  -   O tipo SQL do parâmetro seja exatamente o mesmo que o tipo da coluna de destino ou a conversão de um tipo SQL para o tipo da coluna é suportada.
  -   A precisão e a escala dos parâmetros que se destinam às colunas dos tipos de dados `decimal` e `numeric` do SQL Server são iguais à precisão e à escala configuradas para a coluna de destino.
  -   A precisão dos parâmetros que se destinam às colunas dos tipos de dados `datetime2`, `datetimeoffset` ou `time` do SQL Server não é maior que a precisão da coluna de destino, em consultas que modificam a coluna de destino.
 -   Não use atributos de instrução PDO_SQLSRV `PDO::SQLSRV_ATTR_DIRECT_QUERY` ou `PDO::ATTR_EMULATE_PREPARES` em uma consulta parametrizada
 
#### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>Erros devido à passagem de texto sem formatação em vez de valores criptografados

Qualquer valor que tem como alvo uma coluna criptografada precisa ser criptografado antes de serem enviados ao servidor. Uma tentativa de inserir, modificar ou filtrar por um valor de texto não criptografado em uma coluna criptografada resulta em um erro. Para evitar esses erros, garanta que:
 -   Always Encrypted está habilitado (na cadeia de conexão, defina as `ColumnEncryption` palavra-chave para `Enabled`).
 -   Use o parâmetro de associação para enviar dados que se destinam a colunas criptografadas. O exemplo a seguir mostra uma consulta que filtra incorretamente por uma literal ou uma constante em uma coluna criptografada (SSN):
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
```

## <a name="controlling-performance-impact-of-always-encrypted"></a>Controlando o impacto no desempenho do Sempre Criptografado

Como o Always Encrypted é uma tecnologia de criptografia do lado do cliente, a maior parte da sobrecarga de desempenho é observada no lado do cliente, não no banco de dados. Além do custo das operações de criptografia e descriptografia, as outras fontes de sobrecarga de desempenho no lado do cliente são:
 -   Viagens de ida e volta adicionais ao banco de dados para recuperar metadados dos parâmetros de consulta.
 -   Chamadas a um repositório de chaves mestras de coluna para acessar uma chave mestra de coluna.
 
### <a name="round-trips-to-retrieve-metadata-for-query-parameters"></a>Viagens de ida e volta para recuperar metadados dos parâmetros de consulta

Se o Always Encrypted estiver habilitado para uma conexão, por padrão, o ODBC Driver chamará [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) para cada consulta parametrizada, passando a instrução de consulta (sem nenhum valor de parâmetro) para o SQL Server. Esse procedimento armazenado analisa a instrução de consulta para descobrir se os parâmetros precisam ser criptografados e nesse caso, retorna as informações relacionadas à criptografia para cada parâmetro para permitir que o driver criptografá-los.

Como os drivers PHP permite que o usuário associar um parâmetro em uma instrução preparada, sem fornecer a SQL tipo, ao associar um parâmetro em uma conexão de Always Encrypted habilitado, os Drivers de PHP chamar [SQLDescribeParam](../../odbc/reference/syntax/sqldescribeparam-function.md) sobre o parâmetro para obter o tipo SQL, o tamanho da coluna e os dígitos decimais. Os metadados, em seguida, é usado para chamar [SQLBindParameter]( ../../odbc/reference/syntax/sqlbindparameter-function.md). Esses extras `SQLDescribeParam` chamadas não exigem extras viagens de ida e volta ao banco de dados como o Driver ODBC já tenha armazenado as informações no lado do cliente quando `sys.sp_describe_parameter_encryption` foi chamado.

Os comportamentos anteriores garantir um alto nível de transparência para o aplicativo cliente (e o desenvolvedor do aplicativo) não precisa estar ciente de quais consultas acessam colunas criptografadas, desde que os valores que se destinam a colunas criptografadas são passados para o driver no parâmetros.

Ao contrário do Driver ODBC para SQL Server, habilitando o Always Encrypted no nível de instrução/consulta-ainda não é suportado nos drivers PHP. 

### <a name="column-encryption-key-caching"></a>Cache de chaves de criptografia de coluna

Para reduzir o número de chamadas para um repositório de chave mestra de coluna para descriptografar as chaves de criptografia de coluna (CEK), o driver armazena em cache o CEKs texto não criptografado na memória. Depois de receber a CEK criptografado (ECEK) dos metadados do banco de dados, o driver ODBC primeiro tenta encontrar a CEK texto sem formatação correspondente ao valor de chave criptografado no cache. O driver chama o repositório de chaves que contém a CMK somente se ele não é possível localizar o CEK de texto sem formatação correspondente no cache.

Observação: No Driver ODBC para SQL Server, as entradas no cache são removidas após um tempo limite de duas horas. Esse comportamento significa que, para um determinado ECEK, o driver entra em contato com o repositório de chaves apenas uma vez durante o tempo de vida do aplicativo ou a cada duas horas, o que for menor.

## <a name="working-with-column-master-key-stores"></a>Trabalhando com repositórios de chaves mestras de coluna

Para criptografar ou descriptografar dados, o driver precisa obter uma CEK que está configurada para a coluna de destino. CEKs são armazenados em formato criptografado (ECEKs) nos metadados do banco de dados. Cada CEK tem uma CMK correspondente que foi usada para criptografá-lo. O [metadados de banco de dados](../../t-sql/statements/create-column-master-key-transact-sql.md) não armazena a CMK em si; ele contém apenas o nome do repositório de chaves e informações que o repositório de chaves pode usar para localizar a CMK.

Para obter o valor de texto sem formatação de um ECEK, o driver primeiro obtém os metadados sobre a CEK e seu CMK correspondente e, em seguida, ele usa essas informações, entre em contato com o repositório de chaves que contém a CMK e solicitá-lo para descriptografar o ECEK. O driver se comunica com um repositório de chaves usando um provedor de repositório de chaves.

Para o Microsoft Driver 5.3.0 para PHP para SQL Server, somente o Windows Certificate Store Provider e o Azure Key Vault têm suporte. Ainda não há suporte para o provedor de repositório de chaves que têm suporte no Driver ODBC (provedor de repositório de chaves personalizado).

### <a name="using-the-windows-certificate-store-provider"></a>Uso do Provedor do Repositório de Certificados do Windows

O Driver ODBC para SQL Server no Windows inclui um provedor de repositório de chaves mestras de coluna interna para a Store de certificado do Windows, chamado `MSSQL_CERTIFICATE_STORE`. (Esse provedor não está disponível no macOS ou Linux.) Com esse provedor, a CMK é armazenada localmente no computador cliente e nenhuma configuração adicional pelo aplicativo é necessária usá-lo com o driver. No entanto, o aplicativo deve ter acesso ao certificado e sua chave privada no repositório. Para obter mais informações, consulte [Create and Store Column Master Keys (Always Encrypted)](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)Criar e armazenar chaves mestras de coluna (Always Encrypted).

### <a name="using-azure-key-vault"></a>Usando o Azure Key Vault

O Azure Key Vault oferece uma maneira de armazenar as chaves de criptografia, senhas e outros segredos usando o Azure e pode ser usado para armazenar as chaves para Always Encrypted. O Driver ODBC para SQL Server (versão 17 e superior) inclui um provedor de repositório de chave interna do mestre para o Azure Key Vault. As seguintes opções de conexão lidar com a configuração do Azure Key Vault: `KeyStoreAuthentication`, `KeyStorePrincipalId`, e `KeyStoreSecret`. 
 -   `KeyStoreAuthentication` pode levar a um dos dois valores de cadeia de caracteres possíveis: `KeyVaultPassword` e `KeyVaultClientSecret`. Esses valores controlam quais tipos de credenciais de autenticação são usados com as outras duas palavras-chave.
 -   `KeyStorePrincipalId` usa uma cadeia de caracteres que representa um identificador para a conta de busca acessar o Cofre de chaves do Azure. 
     -   Se `KeyStoreAuthentication` é definido como `KeyVaultPassword`, em seguida, `KeyStorePrincipalId` deve ser o nome de um usuário do Active Directory do Azure.
     -   Se `KeyStoreAuthentication` é definido como `KeyVaultClientSecret`, em seguida, `KeyStorePrincipalId` deve ser uma ID de cliente do aplicativo.
 -   `KeyStoreSecret` usa uma cadeia de caracteres que representa um segredo de credencial. 
     -   Se `KeyStoreAuthentication` é definido como `KeyVaultPassword`, em seguida, `KeyStoreSecret` deve ser a senha do usuário. 
     -   Se `KeyStoreAuthentication` é definido como `KeyVaultClientSecret`, em seguida, `KeyStoreSecret` deve ser o segredo do aplicativo associado com a ID do aplicativo cliente.

Todas as três opções devem estar presentes na cadeia de conexão para usar o Azure Key Vault. Além disso, `ColumnEncryption` deve ser definida como `Enabled`. Se `ColumnEncryption` é definido como `Disabled` , mas as opções de Cofre de chaves do Azure estão presentes, o script continuará sem erros, mas nenhuma criptografia será executada.

Os exemplos a seguir mostram como se conectar ao SQL Server usando o Azure Key Vault.

SQLSRV:

Usando uma conta do Azure Active Directory:
```
$connectionInfo = array("Database"=>$databaseName, "UID"=>$uid, "PWD"=>$pwd, "ColumnEncryption"=>"Enabled", "KeyStoreAuthentication"=>"KeyVaultPassword", "KeyStorePrincipalId"=>$AADUsername, "KeyStoreAuthentication"=>$AADPassword);
$conn = sqlsrv_connect($server, $connectionInfo);
```
Usando uma ID de cliente de aplicativo do Azure e o segredo:
```
$connectionInfo = array("Database"=>$databaseName, "UID"=>$uid, "PWD"=>$pwd, "ColumnEncryption"=>"Enabled", "KeyStoreAuthentication"=>"KeyVaultClientSecret", "KeyStorePrincipalId"=>$applicationClientID, "KeyStoreAuthentication"=>$applicationClientSecret);
$conn = sqlsrv_connect($server, $connectionInfo);
```

PDO_SQLSRV: Usando uma conta do Azure Active Directory:
```
$connectionInfo = "Database = $databaseName; ColumnEncryption = Enabled; KeyStoreAuthentication = KeyVaultPassword; KeyStorePrincipalId = $AADUsername; KeyStoreAuthentication = $AADPassword;";
$conn = new PDO("sqlsrv:server = $server; $connectionInfo", $uid, $pwd);
```
Usando uma ID de cliente de aplicativo do Azure e o segredo:
```
$connectionInfo = "Database = $databaseName; ColumnEncryption = Enabled; KeyStoreAuthentication = KeyVaultClientSecret; KeyStorePrincipalId = $applicationClientID; KeyStoreAuthentication = $applicationClientSecret;";
$conn = new PDO("sqlsrv:server = $server; $connectionInfo", $uid, $pwd);
```

## <a name="limitations-of-the-php-drivers-when-using-always-encrypted"></a>Limitações dos drivers de PHP ao usar o Always Encrypted

SQLSRV e PDO_SQLSRV:
 -   Linux/macOS não dão suporte a Windows Certificate Store Provider
 -   Forçando a criptografia de parâmetro
 -   Habilitando o Always Encrypted no nível de instrução 
 -   Ao usar as localidades de recurso e não-UTF8 Always Encrypted no Linux e macOS (por exemplo, "en_US. ISO-8859-1 "), inserindo dados nulos ou uma cadeia de caracteres vazia em uma coluna char criptografados pode não funcionar, a menos que uma página de código 1252 foi instalado no seu sistema
 
SQLSRV:
 -   Usando `sqlsrv_query` para o parâmetro de associação sem especificar o tipo de SQL
 -   Usando `sqlsrv_prepare` para parâmetros de associação em um lote de instruções SQL  
 
PDO_SQLSRV:
 -   `PDO::SQLSRV_ATTR_DIRECT_QUERY` atributo de instrução especificado em uma consulta parametrizada
 -   `PDO::ATTR_EMULATE_PREPARE` atributo de instrução especificado em uma consulta parametrizada
 -   parâmetros de associação em um lote de instruções SQL
 
Os drivers PHP também herdam as limitações impostas pelo Driver ODBC para SQL Server e o banco de dados. Ver [limitações do driver ODBC ao usar o Always Encrypted](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) e [sempre criptografados detalhes do recurso](../../relational-databases/security/encryption/always-encrypted-database-engine.md#feature-details).  
  
## <a name="see-also"></a>Consulte Também  
[Guia de programação para o driver SQL de PHP](../../connect/php/programming-guide-for-php-sql-driver.md)
[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
[Referência da API do Driver PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
