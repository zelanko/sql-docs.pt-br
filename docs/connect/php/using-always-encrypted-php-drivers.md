---
title: Use sempre criptografado com os Drivers PHP para SQL Server | Microsoft Docs
ms.date: 01/08/2018
ms.prod: sql
ms.prod_service: connectivity
ms.suite: sql
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
manager: mbarwin
ms.openlocfilehash: 6f5035dc42b130afe7da8c27a1c6036e79e2fa0a
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35309905"
---
# <a name="using-always-encrypted-with-the-php-drivers-for-sql-server"></a>Use sempre criptografado com os Drivers PHP para SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

## <a name="applicable-to"></a>Aplicável a
 -   Drivers 5.2 da Microsoft para PHP para SQL Server
 
## <a name="introduction"></a>Introdução

Este artigo fornece informações sobre como desenvolver aplicativos PHP usando [sempre criptografados (mecanismo de banco de dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) e [Drivers de PHP para SQL Server](../../connect/php/Microsoft-php-driver-for-sql-server.md).

O Always Encrypted permite que os aplicativos cliente criptografem dados confidenciais e nunca revelem os dados nem as chaves de criptografia para o SQL Server ou o Banco de Dados SQL do Azure. Um sempre criptografado habilitado driver, como o Driver ODBC para SQL Server, transparentemente criptografa e descriptografa os dados confidenciais no aplicativo cliente. O driver determina automaticamente quais parâmetros de consulta correspondem às colunas de banco de dados confidenciais (protegidas com o Always Encrypted) e criptografa os valores desses parâmetros antes de passar os dados para o SQL Server ou o Banco de Dados SQL do Azure. Da mesma forma, o driver descriptografa de modo transparente os dados recuperados das colunas de banco de dados criptografadas nos resultados da consulta. Para obter mais informações, veja [Always Encrypted (Mecanismo de Banco de Dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md). Os Drivers de PHP para SQL Server usam o Driver ODBC para SQL Server criptografar dados confidenciais.

## <a name="prerequisites"></a>Prerequisites

 -   Configure o Sempre Criptografado em seu banco de dados. Essa configuração envolve o provisionamento de chaves do sempre criptografado e configurar a criptografia para colunas de banco de dados selecionado. Se você ainda não tiver um banco de dados com o Sempre Criptografado configurado, siga as instruções em [Getting Started with Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted)(Introdução ao Sempre Criptografado). Em particular, o banco de dados deve conter as definições de metadados para uma chave mestra de coluna (CMK), uma chave de criptografia de coluna (CEK) e uma tabela contendo uma ou mais colunas criptografadas usando essa CEK.
 -   Verifique se o que driver ODBC para SQL Server versão 17 ou superior está instalado no computador de desenvolvimento. Para obter detalhes, consulte [o Driver ODBC para SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md).

## <a name="enabling-always-encrypted-in-a-php-application"></a>Habilitando sempre criptografado em um aplicativo PHP

É a maneira mais fácil de habilitar a criptografia de parâmetros que se destinam as colunas criptografadas e a descriptografia dos resultados da consulta definindo o valor da `ColumnEncryption` palavra-chave de cadeia de caracteres de conexão para `Enabled`. A seguir estão exemplos de como habilitar o sempre criptografado nos drivers SQLSRV e PDO_SQLSRV:

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

Habilitando sempre criptografado não é suficiente para a criptografia ou descriptografia tenha êxito; Você também precisa garantir que:
 -   O aplicativo tem as permissões de banco de dados VIEW ANY COLUMN MASTER KEY DEFINITION e VIEW ANY COLUMN ENCRYPTION KEY DEFINITION, necessárias para acessar os metadados sobre chaves Always Encrypted no banco de dados. Para obter detalhes, consulte [permissão de banco de dados](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions).
 -   O aplicativo pode acessar a CMK que protege os CEKs para as colunas criptografadas consultadas. Esse requisito é depende do provedor de repositório de chaves que armazena a CMK. Para obter mais informações, consulte [trabalhando com repositórios de chaves mestras de coluna](#working-with-column-master-key-stores).

## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>Recuperando e modificando dados em colunas criptografadas

Depois de habilitar o sempre criptografado em uma conexão, você pode usar as APIs do SQLSRV padrão (consulte [referência da API do JDBC Driver](../../connect/php/sqlsrv-driver-api-reference.md)) ou APIs PDO_SQLSRV (consulte [referência de API do Driver PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)) para recuperar ou modificar dados em colunas de banco de dados criptografado. Supondo que seu aplicativo tem as permissões de banco de dados necessários e pode acessar a chave mestra de coluna, o driver criptografa quaisquer parâmetros de consulta que se destinam a colunas criptografadas e descriptografar os dados recuperados de colunas criptografadas, se comportar de forma transparente para o aplicativos como se as colunas não foram criptografadas.

Se o sempre criptografado não estiver habilitado, as consultas com parâmetros que se destinam a colunas criptografadas falhar. Dados ainda podem ser recuperados de colunas criptografadas, desde que a consulta não tem parâmetros destinam a colunas criptografadas. No entanto, o driver não tentará qualquer descriptografia e o aplicativo recebe os dados binários criptografados (como matrizes de bytes).

A tabela a seguir resume o comportamento das consultas, dependendo se sempre criptografado está habilitado ou não:

| Característica de consulta | Sempre criptografado está habilitado e o aplicativo pode acessar as chaves e os metadados de chave | Sempre criptografado está habilitado e o aplicativo não pode acessar as chaves ou os metadados de chave | Sempre criptografado está desabilitado | | Parâmetros que se destinam a colunas criptografadas. | Valores de parâmetro são criptografados de forma transparente. | Erro | Erro | | Recuperando dados de colunas criptografadas, sem parâmetros que se destinam a colunas criptografadas. | Resultados de colunas criptografadas são descriptografados de maneira transparente. O aplicativo recebe valores de coluna de texto sem formatação. | Erro | Resultados de colunas criptografadas não são descriptografados. O aplicativo recebe valores criptografados como matrizes de bytes. |
 
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
 -   Os valores inseridos em colunas de banco de dados, incluindo as colunas criptografadas, são passados como parâmetros associados. Embora o uso de parâmetros é opcional ao enviar valores para colunas não criptografadas (embora é altamente recomendado, pois ajuda a prevenir a injeção de SQL), é necessário para valores que se destinam a colunas criptografadas. Se os valores inseridos nas colunas SSN ou BirthDate fossem passados como literais inseridos na instrução de consulta, a consulta falhará porque o driver não tentará criptografar ou processar literais em consultas. Como resultado, o servidor os rejeitaria como incompatíveis com as colunas criptografadas.
 -   Ao inserir valores usando os parâmetros de ligação, um tipo SQL que é idêntico ao tipo de dados da coluna de destino ou cuja conversão para o tipo de dados da coluna de destino é suportado deve ser passado para o banco de dados. Esse requisito é porque sempre criptografado dá suporte a algumas conversões de tipo (para obter detalhes, consulte [sempre criptografados (mecanismo de banco de dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)). Os dois drivers PHP, SQLSRV e PDO_SQLSRV, cada um tem um mecanismo para ajudar o usuário a determinar o tipo do valor de SQL. Portanto, o usuário não precisa fornecer o tipo SQL explicitamente.
  -   Para o driver SQLSRV, o usuário tem duas opções:
   -   Contar com o driver do PHP para determinar e definir o tipo correto do SQL. Nesse caso, o usuário deve usar `sqlsrv_prepare` e `sqlsrv_execute` para executar uma consulta parametrizada.
   -   Defina explicitamente o tipo de SQL.
  -   Para o driver PDO_SQLSRV, o usuário não tem a opção de definir explicitamente o tipo SQL de um parâmetro. O driver PDO_SQLSRV automaticamente ajuda o usuário a determinar o tipo SQL ao associar um parâmetro.
 -   Para os drivers determinar o tipo SQL, algumas limitações se aplicam:
  -   SQLSRV Driver:
   -   Se o usuário deseja o driver para determinar os tipos SQL para as colunas criptografadas, o usuário deve usar `sqlsrv_prepare` e `sqlsrv_execute`.
   -   Se `sqlsrv_query` é preferencial, o usuário é responsável por especificar os tipos de SQL para todos os parâmetros. O tipo SQL especificado deve incluir o comprimento da cadeia de caracteres para tipos de cadeia de caracteres e a escala e precisão para tipos decimais.
  -   PDO_SQLSRV Driver:
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

Driver PDO_SQLSRV e [PDO](../../connect/php/pdo-prepare.md):
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

Os exemplos a seguir demonstram a filtragem de dados com base em valores criptografados e recuperar dados de texto sem formatação de colunas criptografadas usando os drivers SQLSRV e PDO_SQLSRV. Observe os seguintes pontos:
 -   O valor usado na cláusula WHERE para filtrar a coluna SSN precisa ser passado com parâmetro de associação, para que o driver transparentemente pode criptografá-lo antes de enviá-la para o servidor.
 -   Ao executar uma consulta com parâmetros associados, os drivers PHP determina automaticamente o tipo SQL para o usuário, a menos que o usuário especifica explicitamente o tipo SQL usando o driver SQLSRV.
 -   Todos os valores impressos pelo programa são em texto não criptografado, pois o driver de modo transparente descriptografa os dados recuperados das colunas SSN e BirthDate.
 
Observação: Consultas podem executar comparações de igualdade em colunas criptografadas somente se a criptografia é determinística. Para obter mais informações, consulte [criptografia selecionando determinística ou aleatória](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption).

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
 -   Como sempre criptografado não é habilitado na cadeia de conexão, a consulta retorna os valores criptografados de SSN e BirthDate como matrizes de bytes (o programa converte os valores em cadeias de caracteres).
 -   Uma consulta que recupera dados de colunas criptografadas com o Sempre Criptografado desabilitado pode ter parâmetros, desde que nenhum dos parâmetros se destinem a uma coluna criptografada. Os seguintes filtros de consulta por LastName, que não são criptografados no banco de dados. Se a consulta filtrar por SSN ou BirthDate, a consulta falhará.
 
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

Esta seção descreve as categorias de erros comuns ao consultar colunas criptografadas de aplicativos PHP e algumas diretrizes sobre como evitá-los.

#### <a name="unsupported-data-type-conversion-errors"></a>Erros de conversão de tipo de dados sem suporte

O Always Encrypted dá suporte a algumas conversões de tipos de dados criptografados. Consulte [sempre criptografados (mecanismo de banco de dados)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) para a lista detalhada de conversões de tipo com suporte. Faça o seguinte para evitar erros de conversão de tipo de dados:
 -   Ao usar o driver SQLSRV com `sqlsrv_prepare` e `sqlsrv_execute` o tipo SQL, juntamente com o tamanho da coluna e o número de casas decimais do parâmetro é determinado automaticamente.
 -   Ao usar o driver PDO_SQLSRV para executar uma consulta, o tipo SQL com o tamanho da coluna e o número de casas decimais do parâmetro é determinado automaticamente
 -   Ao usar o driver SQLSRV com `sqlsrv_query` para executar uma consulta:
  -   O tipo SQL do parâmetro é exatamente o mesmo que o tipo da coluna de destino ou a conversão do tipo SQL para o tipo da coluna é suportada.
  -   A precisão e escala dos parâmetros de direcionamento colunas do `decimal` e `numeric` tipos de dados do SQL Server é o mesmo, assim como a precisão e escala configuram para a coluna de destino.
  -   A precisão de parâmetros que se destinam a colunas de `datetime2`, `datetimeoffset`, ou `time` tipos de dados do SQL Server não é maior do que a precisão da coluna de destino, em consultas que modificam a coluna de destino.
 -   Não use os atributos de instrução PDO_SQLSRV `PDO::SQLSRV_ATTR_DIRECT_QUERY` ou `PDO::ATTR_EMULATE_PREPARES` em uma consulta parametrizada
 
#### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>Erros devido à passagem de texto sem formatação em vez de valores criptografados

Qualquer valor que tem como alvo uma coluna criptografada precisa ser criptografado antes de serem enviados ao servidor. Uma tentativa de inserir, modificar ou filtrar por um valor de texto sem formatação em uma coluna criptografada resulta em um erro. Para evitar esses erros, verifique se:
 -   Sempre criptografado está habilitado (na cadeia de conexão, defina o `ColumnEncryption` palavra-chave `Enabled`).
 -   Use o parâmetro de associação para enviar dados visando colunas criptografadas. O exemplo a seguir mostra uma consulta que filtra incorretamente por uma literal ou uma constante em uma coluna criptografada (SSN):
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
```

## <a name="controlling-performance-impact-of-always-encrypted"></a>Controlando o impacto no desempenho do Sempre Criptografado

Como sempre criptografado é uma tecnologia de criptografia do lado do cliente, a maioria da sobrecarga de desempenho é observada no lado do cliente, não no banco de dados. Além do custo de operações de criptografia e descriptografia, as outras fontes de desempenho sobrecarga no lado do cliente são:
 -   Viagens adicionais ao banco de dados para recuperar metadados para parâmetros de consulta.
 -   Chamadas a um repositório de chaves mestras de coluna para acessar uma chave mestra de coluna.
 
### <a name="round-trips-to-retrieve-metadata-for-query-parameters"></a>Ida e volta para recuperar metadados para parâmetros de consulta

Se o sempre criptografado está habilitado para uma conexão, o Driver ODBC, por padrão, chamará [sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) para cada consulta parametrizada, passando a instrução de consulta (sem nenhum valor de parâmetro) para SQL Server . Esse procedimento armazenado analisa a instrução de consulta para descobrir se os parâmetros precisam ser criptografados e nesse caso, retorna as informações relacionadas à criptografia para cada parâmetro para permitir que o driver para criptografá-los.

Como os drivers PHP permitem que o usuário associar um parâmetro em uma instrução preparada sem fornecer o SQL, digite, ao associar um parâmetro em uma conexão sempre criptografado habilitado, os Drivers de PHP chamar [SQLDescribeParam](../../odbc/reference/syntax/sqldescribeparam-function.md) sobre o Para obter o tipo SQL, o tamanho da coluna e os dígitos decimais. Os metadados são usados para chamar [SQLBindParameter]( ../../odbc/reference/syntax/sqlbindparameter-function.md). Esses extra `SQLDescribeParam` chamadas não exigem viagem extra ao banco de dados como o Driver ODBC já tenha armazenado as informações no lado do cliente quando `sys.sp_describe_parameter_encryption` foi chamado.

Os comportamentos anteriores garantir um alto nível de transparência para o aplicativo cliente (e o desenvolvedor do aplicativo) não precisa estar ciente de quais consultas acessam colunas criptografadas, desde que os valores que se destinam a colunas criptografadas sejam passados para o driver no parâmetros.

Ao contrário do Driver ODBC para SQL Server, habilitando o sempre criptografado no nível de instrução/consulta-ainda não é suportado nos drivers do PHP. 

### <a name="column-encryption-key-caching"></a>Cache de chave de criptografia de coluna

Para reduzir o número de chamadas para um repositório de chaves mestras de coluna para descriptografar as chaves de criptografia de coluna (CEK), o driver armazena em cache o CEKs texto não criptografado na memória. Depois de receber a CEK criptografada (ECEK) de metadados do banco de dados, o driver ODBC primeiro tenta localizar o texto sem formatação CEK correspondente ao valor de chave criptografado no cache. O driver chama o repositório de chaves que contém a CMK apenas se não é possível localizar o texto não criptografado correspondente CEK no cache.

Observação: No Driver ODBC para SQL Server, as entradas no cache são removidas após um tempo limite de duas horas. Esse comportamento significa que, para um determinado ECEK, o driver contata o repositório de chaves apenas uma vez durante o tempo de vida do aplicativo ou a cada duas horas, o que for menor.

## <a name="working-with-column-master-key-stores"></a>Trabalhando com repositórios de chaves mestras de coluna

Para criptografar ou descriptografar dados, o driver precisa obter uma CEK que está configurada para a coluna de destino. CEKs são armazenadas em formato criptografado (ECEKs) nos metadados do banco de dados. Cada CEK tem uma CMK correspondente que foi usada para criptografá-lo. O [metadados de banco de dados](../../t-sql/statements/create-column-master-key-transact-sql.md) não armazena a CMK; ele contém apenas o nome do repositório de chaves e informações que o repositório de chaves pode usar para localizar a CMK.

Para obter o valor de texto sem formatação de um ECEK, o driver primeiro obtém os metadados sobre a CEK e seu CMK correspondente, e, em seguida, usa essas informações para entrar em contato com o repositório de chaves que contém a CMK e solicitações para descriptografar o ECEK. O driver se comunica com um repositório de chaves usando um provedor de repositório de chaves.

Para o Microsoft Driver 5.2.0 para PHP para SQL Server, há suporte para apenas Windows provedor de repositório de certificado. Ainda não há suporte para os dois outros Keystore provedores com suporte pelo Driver ODBC (Cofre de chaves do Azure e provedor de armazenamento de chaves personalizado).

### <a name="using-the-windows-certificate-store-provider"></a>Usando o provedor de repositório de certificados do Windows

O Driver ODBC para SQL Server no Windows inclui um provedor de repositório de chaves mestras de coluna interna para o repositório de certificados do Windows, chamado `MSSQL_CERTIFICATE_STORE`. (Este provedor não está disponível no macOS ou Linux). Com esse provedor, CMK é armazenado localmente no computador cliente e nenhuma configuração adicional pelo aplicativo é necessária para uso com o driver. No entanto, o aplicativo deve ter acesso ao certificado e sua chave privada no repositório. Para obter mais informações, consulte [Create and Store Column Master Keys (Always Encrypted)](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)Criar e armazenar chaves mestras de coluna (Always Encrypted).

## <a name="limitations-of-the-php-drivers-when-using-always-encrypted"></a>Limitações dos drivers de PHP ao usar sempre criptografado

SQLSRV e PDO_SQLSRV:
 -   Suporte a Linux/MacOS
  -   Linux/MacOS não oferecem suporte a provedor de repositório de certificados do Windows e é o único provedor de armazenamento de chaves com suporte atualmente pelos drivers de PHP
 -   Forçar criptografia de parâmetros
 -   Habilitando sempre criptografado no nível de instrução 
 
SQLSRV:
 -   Usando `sqlsrv_query` para o parâmetro de associação sem especificar o tipo de SQL
 -   Usando `sqlsrv_prepare` para parâmetros de associação em um lote de instruções SQL  
 
PDO_SQLSRV:
 -   `PDO::SQLSRV_ATTR_DIRECT_QUERY` atributo de declaração especificado em uma consulta parametrizada
 -   `PDO::ATTR_EMULATE_PREPARE` atributo de declaração especificado em uma consulta parametrizada
 -   parâmetros de associação em um lote de instruções SQL
 
Os drivers PHP também herdam as limitações impostas pelo Driver ODBC para SQL Server e o banco de dados. Consulte [limitações do driver ODBC ao usar sempre criptografado](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) e [sempre criptografados detalhes do recurso](../../relational-databases/security/encryption/always-encrypted-database-engine.md#feature-details).  
  
## <a name="see-also"></a>Consulte também  
[Guia de programação para o driver SQL de PHP](../../connect/php/programming-guide-for-php-sql-driver.md)
[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
[Referência de API do Driver PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
