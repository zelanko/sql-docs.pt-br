---
description: Consultar colunas usando o Always Encrypted com o Azure Data Studio
title: Consultar colunas usando o Always Encrypted com o Azure Data Studio | Microsoft Docs
ms.custom: ''
ms.date: 5/19/2020
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3c1f91effdea8225df62e3782e43ff5e863d827c
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91866700"
---
# <a name="query-columns-using-always-encrypted-with-azure-data-studio"></a>Consultar colunas usando o Always Encrypted com o Azure Data Studio
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]

Este artigo descreve como consultar colunas criptografadas com o [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) usando o [Azure Data Studio](../../../azure-data-studio/what-is.md). Com o Azure Data Studio, você pode:
- Recuperar valores de texto cifrado armazenados em colunas criptografadas. 
- Recuperar valores de texto sem formatação armazenados em colunas criptografadas.  
- Envie valores de texto sem formatação para colunas criptografadas (por exemplo, em instruções `INSERT` ou `UPDATE` e como um parâmetro de pesquisa de cláusulas `WHERE` em instruções `SELECT`). 

## <a name="retrieving-ciphertext-values-stored-in-encrypted-columns"></a>Recuperando valores de texto cifrado armazenados em colunas criptografadas    
Esta seção descreve como recuperar dados armazenados em colunas criptografadas como texto cifrado.

### <a name="steps"></a>Etapas
1. Verifique se você desabilitou o Always Encrypted para a conexão de banco de dados na janela de consultas, na qual você executará uma consulta `SELECT` recuperando valores de texto cifrado. Confira [Como habilitar e desabilitar o Always Encrypted para uma conexão de banco de dados](#enabling-and-disabling-always-encrypted-for-a-database-connection) abaixo.     
1. Execute a consulta `SELECT`. Os dados recuperados de colunas criptografadas serão retornados como valores binários (criptografados).   

### <a name="example"></a>Exemplo
Supondo que `SSN` seja uma coluna criptografada na tabela `Patients` , a consulta mostrada abaixo recuperará valores binários de texto codificado, se Always Encrypted estiver desabilitado para a conexão de banco de dados.   

![always-encrypted-ads-query-ciphertext](../../../relational-databases/security/encryption/media/always-encrypted-ads-query-ciphertext.png)
 
## <a name="retrieving-plaintext-values-stored-in-encrypted-columns"></a>Recuperar valores de texto sem formatação armazenados em colunas criptografadas    
Esta seção descreve como recuperar dados armazenados em colunas criptografadas como texto cifrado.

### <a name="prerequisites"></a>Pré-requisitos
- Azure Data Studio versão 17.1 ou posterior.
- Você precisa ter acesso às chaves mestras de coluna e aos metadados sobre as chaves que protegem as colunas nas quais você está executando a consulta. Para obter detalhes, confira [Permissões para consultar colunas criptografadas](#permissions-for-querying-encrypted-columns) abaixo.
- As chaves mestras de coluna precisam ser armazenadas no Azure Key Vault ou no Repositório de Certificados do Windows. Azure Data Studio não é compatível com outros repositórios de chaves.

### <a name="steps"></a>Etapas
1.  Verifique se você habilitou o Always Encrypted para a conexão de banco de dados na janela de consultas, na qual você executará uma consulta `SELECT` recuperando e descriptografando os dados. Isso instruirá o [Provedor de Dados Microsoft .NET para SQL Server](../../../connect/ado-net/sql/sqlclient-support-always-encrypted.md) (usado pelo Azure Data Studio) a descriptografar as colunas criptografadas no conjunto de resultados da consulta. Confira [Como habilitar e desabilitar o Always Encrypted para uma conexão de banco de dados](#enabling-and-disabling-always-encrypted-for-a-database-connection) abaixo.
1.  Execute a consulta `SELECT`. Os dados recuperados de colunas criptografadas serão retornados como valores de texto não criptografado dos tipos de dados originais.
 
### <a name="example"></a>Exemplo
Supondo que SSN seja uma coluna criptografada na tabela `Patients`, a consulta mostrada abaixo retornará valores de texto sem formatação, se o Always Encrypted estiver habilitado para a conexão de banco de dados e se você tiver acesso à chave mestra de coluna configurada para a coluna `SSN`.   

![always-encrypted-ads-query-plaintext](../../../relational-databases/security/encryption/media/always-encrypted-ads-query-plaintext.png)
 
## <a name="sending-plaintext-values-targeting-encrypted-columns"></a>Enviar valores de texto sem formatação destinados a colunas criptografadas       
Esta seção descreve como executar uma consulta que envia valores direcionados a uma coluna criptografada. Por exemplo, uma consulta que insere, atualiza ou filtra por um valor armazenado em uma coluna criptografada:

### <a name="prerequisites"></a>Pré-requisitos
- Azure Data Studio versão 18.1 ou posterior.
- Você precisa ter acesso às chaves mestras de coluna e aos metadados sobre as chaves que protegem as colunas nas quais você está executando a consulta. Para obter detalhes, confira [Permissões para consultar colunas criptografadas](#permissions-for-querying-encrypted-columns) abaixo.
- As chaves mestras de coluna precisam ser armazenadas no Azure Key Vault ou no Repositório de Certificados do Windows. Azure Data Studio não é compatível com outros repositórios de chaves.

### <a name="steps"></a>Etapas
1. Verifique se você habilitou o Always Encrypted para a conexão de banco de dados na janela de consultas, na qual você executará uma consulta `SELECT` recuperando e descriptografando os dados. Isso instruirá o [Provedor de Dados Microsoft .NET para SQL Server](../../../connect/ado-net/sql/sqlclient-support-always-encrypted.md) (usado pelo Azure Data Studio) a criptografar os parâmetros de consulta destinados a colunas criptografadas e a descriptografar os resultados recuperados de colunas criptografadas. Confira [Como habilitar e desabilitar o Always Encrypted para uma conexão de banco de dados](#enabling-and-disabling-always-encrypted-for-a-database-connection) abaixo. 
1. Habilitar a Parametrização de Always Encrypted para a janela de consultas. Confira [Parametrização de Always Encrypted](#parameterization-for-always-encrypted) abaixo para obter detalhes.
1. Declare uma variável Transact-SQL e inicialize-a com um valor que deseja enviar (inserir, atualizar ou filtrar por) para o banco de dados. 
1. Execute a consulta enviando o valor da variável Transact-SQL para o banco de dados. O Azure Data Studio converterá a variável em um parâmetro de consulta e criptografará seu valor antes de enviá-la ao banco de dados.   

### <a name="example"></a>Exemplo
Supondo que `SSN` seja uma coluna `char(11)` criptografada na tabela `Patients`, o script abaixo tentará localizar uma linha contendo `'795-73-9838'` na coluna SSN. Os resultados serão retornados se Always Encrypted estiver habilitado para a conexão de banco de dados, a parametrização para Always Encrypted será habilitada para a janela de consultas e você terá acesso à chave mestra de coluna configurada para a coluna `SSN`.   

![always-encrypted-ads-query-parameters](../../../relational-databases/security/encryption/media/always-encrypted-ads-query-parameters.png)

## <a name="permissions-for-querying-encrypted-columns"></a>Permissões para consultar colunas criptografadas

Para executar as consultas em colunas criptografadas, incluindo consultas que recuperam dados em texto cifrado, você precisará das permissões **VIEW ANY COLUMN MASTER KEY DEFINITION** e **VIEW ANY COLUMN ENCRYPTION KEY DEFINITION** no banco de dados.

Além das permissões acima, para descriptografar qualquer resultado de consulta ou criptografar os parâmetros de consulta (produzidos por parametrização de variáveis Transact-SQL), você também precisa acessar a chave mestra de coluna protegendo as colunas de destino:

- **Repositório de certificados – Computador local:** você precisa ter acesso de **Leitura** ao certificado que é usado como uma chave mestra de coluna ou ser o administrador do computador.   
- **Azure Key Vault:** você precisará das permissões **get**, **unwrapKey** e **verify** sobre o cofre de chaves que contém a chave mestra de coluna.

Para obter mais informações, consulte [Create and Store Column Master Keys (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)Criar e armazenar chaves mestras de coluna (Always Encrypted).

## <a name="enabling-and-disabling-always-encrypted-for-a-database-connection"></a>Habilitando e desabilitando o Always Encrypted para uma conexão de banco de dados   
Ao se conectar com um banco de dados no Azure Data Studio, você pode habilitar ou desabilitar o Always Encrypted para a conexão de banco de dados. Por padrão, o Always Encrypted está desabilitado. 

Habilitar o Always Encrypted para uma conexão de banco de dados instrui o [Provedor de Dados Microsoft .NET para SQL Server](../../../connect/ado-net/sql/sqlclient-support-always-encrypted.md), usado pelo Azure Data Studio, a tentar de maneira transparente:   
-   descriptografar todos os valores recuperados de colunas criptografadas e retornados nos resultados da consulta.   
-   Criptografar os valores das variáveis Transact-SQL com parâmetros que se destinam a colunas de banco de dados criptografadas.   

Se você não habilitar o Always Encrypted para uma conexão, o Provedor de Dados Microsoft .NET para SQL Server não tentará criptografar os parâmetros de consulta nem descriptografar os resultados.

Você pode habilitar ou desabilitar o Always Encrypted ao se conectar a um banco de dados. Para obter informações gerais sobre como se conectar a um banco de dados, confira:
- [Início Rápido: Conectar e consultar o SQL Server usando o Azure Data Studio](../../../azure-data-studio/quickstart-sql-server.md)
- [Início Rápido: use o Azure Data Studio para se conectar e consultar e o Banco de Dados SQL do Azure](../../../azure-data-studio/quickstart-sql-database.md)

Para habilitar (desabilitar) o Always Encrypted:
1. Na caixa de diálogo **Conexão**, clique em **Avançado...** .
2. Para habilitar o Always Encrypted para a conexão, defina o campo **Always Encrypted** como **Habilitado**. Para desabilitar o Always Encrypted, deixe o valor do campo **Always Encrypted** em branco ou defina-o como **Desabilitado**.
3. Se você estiver usando o [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)] e a Instância do SQL Server estiver configurada com um enclave seguro, você poderá especificar um protocolo de enclave e uma URL de atestado de enclave. Se a Instância do SQL Server não usar um enclave seguro, verifique se você deixou os campos **Protocolo de Atestado** e **URL de Atestado de Enclave** em branco. Para obter mais informações, consulte [Always Encrypted com enclaves seguros](always-encrypted-enclaves.md).
4. Clique em **OK** para fechar as **Propriedades avançadas**.

![always-encrypted-ads-parameterization](../../../relational-databases/security/encryption/media/always-encrypted-ads-connect.gif)

> [!TIP]
> Para alternar entre a habilitação e a desabilitação do Always Encrypted para uma janela de consultas existente, clique em **Desconectar** e em **Conectar** e conclua as etapas acima para se reconectar ao banco de dados com os valores desejados do campo **Always Encrypted**. 

> [!NOTE] 
> O botão **Alterar conexão** em uma janela de consultas atualmente não é compatível com a alternância entre habilitar e desabilitar o Always Encrypted.

## <a name="parameterization-for-always-encrypted"></a>Parametrização do Always Encrypted

A Parametrização do Always Encrypted é um recurso do Azure Data Studio 18.1 e posterior que converte automaticamente as variáveis Transact-SQL em parâmetros de consulta (instâncias da [Classe SqlParameter](/dotnet/api/microsoft.data.sqlclient.sqlparameter)). Isso permite que o [Provedor de Dados Microsoft .NET para SQL Server](../../../connect/ado-net/sql/sqlclient-support-always-encrypted.md) subjacente detecte dados destinados a colunas criptografadas e criptografe esses dados antes de enviá-los para o banco de dados.
  
Sem a parametrização, o Provedor de Dados Microsoft .NET para SQL Server passa cada instrução que você cria na janela de consultas como uma consulta sem parâmetros. Se a consulta contiver literais ou variáveis Transact-SQL destinados a colunas criptografadas, o Provedor de Dados do .NET Framework para SQL Server não conseguirá detectá-los e criptografá-los antes de enviar a consulta ao banco de dados. Como resultado, a consulta falhará devido à incompatibilidade de tipo (entre a variável Transact-SQL literal de texto sem formatação e a coluna criptografada). Por exemplo, a consulta a seguir falhará sem parametrização, supondo que a coluna `SSN` seja criptografada.   

```sql
DECLARE @SSN CHAR(11) = '795-73-9838'
SELECT * FROM [dbo].[Patients]
WHERE [SSN] = @SSN
```

### <a name="enabling-and-disabling-parameterization-for-always-encrypted"></a>Como habilitar e desabilitar a Parametrização do Always Encrypted

A Parametrização de Always Encrypted é desabilitada por padrão.

Para habilitar/desabilitar a Parametrização do Always Encrypted:

1. Selecione **Arquivo** > **Preferências** > **Configurações** (**Código** > **Preferências** > **Configurações** no Mac).
2. Navegue até **Dados** > **Microsoft SQL Server**.
3. Selecione ou desmarque **Habilitar Parametrização de Always Encrypted**.
4. Feche a janela **Configurações**.

![always-encrypted-ads-parameterization](../../../relational-databases/security/encryption/media/always-encrypted-ads-parameterization.gif)

> [!NOTE]
> A Parametrização do Always Encrypted funciona apenas em uma consulta que usa conexões de banco de dados com o Always Encrypted habilitado (confira [Habilitando e desabilitando o Always Encrypted para uma conexão de banco de dados](#enabling-and-disabling-always-encrypted-for-a-database-connection)). Nenhuma variável Transact-SQL será parametrizada se a janela de consultas usar uma conexão de banco de dados sem o Always Encrypted habilitado.

### <a name="how-parameterization-for-always-encrypted-works"></a>Funcionamento da Parametrização do Always Encrypted

Se a Parametrização do Always Encrypted e o Always Encrypted estiverem habilitados para uma janela de consultas, o Azure Data Studio tentará parametrizar as variáveis Transact-SQL que atendem às seguintes condições de pré-requisito:

- São declaradas e inicializadas na mesma instrução (inicialização embutida). As variáveis declaradas usando instruções `SET` separadas não serão parametrizadas.
- São inicializadas usando um único literal. As variáveis inicializadas usando expressões, inclusive operadores ou funções, não serão parametrizadas.

Veja abaixo exemplos de variáveis que serão parametrizadas pelo Azure Data Studio.

```sql
DECLARE @SSN char(11) = '795-73-9838';
   
DECLARE @BirthDate date = '19990104';
DECLARE @Salary money = $30000;
```

E aqui estão alguns exemplos de variáveis que o Azure Data Studio não tentará parametrizar:

```sql
DECLARE @Name nvarchar(50); --Initialization separate from declaration
SET @Name = 'Abel';

DECLARE @StartDate date = GETDATE(); -- a function used instead of a literal

DECLARE @NewSalary money = @Salary * 1.1; -- an expression used instead of a literal
```
 
Para uma parametrização tentada ser bem-sucedida:   
- O tipo do literal usado para a inicialização da variável a ser parametrizada deve corresponder ao tipo na declaração da variável.   
- Se o tipo declarado da variável for um tipo de data ou hora, a variável deverá ser inicializada usando uma cadeia de caracteres que usa um dos seguintes formatos ISO 8601 compatíveis.   

Estes são exemplos de declarações de variáveis Transact-SQL que resultarão em erros de parametrização:

```sql
DECLARE @BirthDate date = '01/04/1999' -- unsupported date format   
   
DECLARE @Number int = 1.1 -- the type of the literal does not match the type of the variable   
```

O Azure Data Studio usa o IntelliSense para informar quais variáveis podem ser parametrizadas com sucesso e quais tentativas de parametrização falham (e por quê).   

Uma declaração de uma variável que pode ser parametrizada com sucesso é marcada com um sublinhado na mensagem de informações na janela de consultas. Caso passe o mouse sobre uma instrução de declaração que foi marcada com um sublinhado na mensagem de informações, você verá a mensagem contendo os resultados do processo de parametrização, incluindo os valores das propriedades de chave do objeto [SqlParameter Class](/dotnet/api/microsoft.data.sqlclient.sqlparameter) resultante (a variável é mapeada para: [SqlDbType](/dotnet/api/microsoft.data.sqlclient.sqlparameter.dbtype), [Size](/dotnet/api/microsoft.data.sqlclient.sqlparameter.size), [Precision](/dotnet/api/microsoft.data.sqlclient.sqlparameter.precision), [Scale](/dotnet/api/microsoft.data.sqlclient.sqlparameter.scale), [SqlValue](/dotnet/api/microsoft.data.sqlclient.sqlparameter.sqlvalue)). Você também pode ver a lista completa de todas as variáveis que foram parametrizadas com sucesso na exibição de **Problemas**. Para abrir a exibição de **Problemas**, selecione **Exibir** > **Problemas**.    



Se o Azure Data Studio tentou parametrizar uma variável, mas a parametrização falhou, a declaração da variável será marcada com um sublinhado de erro. Caso passe o mouse sobre a instrução de declaração que foi marcada com um sublinhado de erro, você obterá resultados sobre o erro. Você também poderá ver a lista completa de erros de parametrização para todas as variáveis na exibição de **Problemas**.

 
> [!NOTE]
> Como o Always Encrypted é compatível com um subconjunto limitado de conversões de tipo, em muitos casos, é necessário que o tipo de dados de uma variável Transact-SQL seja o mesmo que o tipo da coluna do banco de dados de destino a que ela se destina. Por exemplo, supondo que o tipo da coluna `SSN` na tabela `Patients` seja `char(11)`, a consulta abaixo falhará, pois o tipo da variável `@SSN`, que é `nchar(11)`, não corresponde ao tipo da coluna.   

```sql
DECLARE @SSN nchar(11) = '795-73-9838'
SELECT * FROM [dbo].[Patients]
WHERE [SSN] = @SSN;
```

```output
Msg 402, Level 16, State 2, Line 5   
The data types char(11) encrypted with (encryption_type = 'DETERMINISTIC', 
encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'CEK_Auto1', 
column_encryption_key_database_name = 'Clinic') collation_name = 'Latin1_General_BIN2' 
and nchar(11) encrypted with (encryption_type = 'DETERMINISTIC', 
encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'CEK_Auto1', 
column_encryption_key_database_name = 'Clinic') are incompatible in the equal to operator.
```

> [!NOTE]
> Sem parametrização, a consulta inteira, incluindo as conversões de tipo, será processada dentro do SQL Server/Banco de Dados SQL do Azure. Com a parametrização habilitada, algumas conversões de tipo são executadas pelo Provedor de Dados Microsoft .NET para SQL Server, dentro do Azure Data Studio. Devido às diferenças entre o sistema de tipos do Microsoft .NET e o sistema de tipos do SQL Server (por exemplo, diferente precisão de alguns tipos, como o float), uma consulta executada com a parametrização habilitada poderá produzir resultados diferentes da consulta executada sem a parametrização habilitada. 

## <a name="next-steps"></a>Próximas etapas
- [Desenvolver aplicativos usando o Always Encrypted](always-encrypted-client-development.md)


## <a name="see-also"></a>Consulte Também
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)