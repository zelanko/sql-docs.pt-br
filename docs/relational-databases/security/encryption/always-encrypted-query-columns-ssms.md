---
title: Consultar colunas usando o Always Encrypted com o SQL Server Management Studio | Microsoft Docs
description: Saiba como consultar colunas no modo Always Encrypted usando o SQL Server Management Studio. Recupere valores de texto cifrado ou simples armazenados em colunas criptografadas.
ms.custom: ''
ms.date: 10/31/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Always Encrypted, configure with SSMS
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f33d58a0fe9b61519c8946708dcd22c84dff90ba
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85627410"
---
# <a name="query-columns-using-always-encrypted-with-sql-server-management-studio"></a>Consultar colunas usando o Always Encrypted com o SQL Server Management Studio
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]

Este artigo descreve como consultar colunas criptografadas com o [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) usando o [SSMS (SQL Server Management Studio)](../../../ssms/download-sql-server-management-studio-ssms.md). Com o SSMS, você pode:
- Recuperar valores de texto cifrado armazenados em colunas criptografadas. 
- Recuperar valores de texto sem formatação armazenados em colunas criptografadas.   
- Envie valores de texto sem formatação para colunas criptografadas (por exemplo, em instruções `INSERT` ou `UPDATE` e como um parâmetro de pesquisa de cláusulas `WHERE` em instruções `SELECT`).

## <a name="retrieving-ciphertext-values-stored-in-encrypted-columns"></a>Recuperando valores de texto cifrado armazenados em colunas criptografadas    
A execução de consultas SELECT que recuperam o texto cifrado de dados armazenados em colunas criptografadas (sem descriptografar os dados) não exige que você tenha acesso às chaves mestras de coluna que protegem os dados. Para recuperar valores de uma coluna criptografada como texto cifrado no SSMS:

1. Verifique se você consegue acessar os metadados sobre as chaves que protegem as colunas nas quais você está executando a consulta. Embora não precise conseguir acessar as chaves mestras de coluna reais, você precisa ter permissões no nível de banco de dados para exibir os objetos de metadados da chave mestra de coluna e da chave de criptografia de coluna no banco de dados. Para obter detalhes, confira [Permissões para consultar colunas criptografadas](#permissions-for-querying-encrypted-columns) abaixo.
1. Verifique se você desabilitou o Always Encrypted para a conexão de banco de dados na janela do Editor de Consultas, na qual você executará uma consulta `SELECT` recuperando valores de texto cifrado. Confira [Como habilitar e desabilitar o Always Encrypted para uma conexão de banco de dados](#en-dis) abaixo.     
1. Execute a consulta `SELECT`. Os dados recuperados de colunas criptografadas serão retornados como valores binários (criptografados).   

### <a name="example"></a>Exemplo
Supondo que `SSN` seja uma coluna criptografada na tabela `Patients` , a consulta mostrada abaixo recuperará valores binários de texto codificado, se Always Encrypted estiver desabilitado para a conexão de banco de dados.   

![always-encrypted-ciphertext](../../../relational-databases/security/encryption/media/always-encrypted-ciphertext.png)
 
## <a name="retrieving-plaintext-values-stored-in-encrypted-columns"></a>Recuperar valores de texto sem formatação armazenados em colunas criptografadas    
Para recuperar valores de uma coluna criptografada como texto sem formatação (para descriptografar os valores):   
1. Verifique se você consegue acessar as chaves mestras de coluna e os metadados sobre as chaves que protegem as colunas nas quais você está executando a consulta. Para obter detalhes, confira [Permissões para consultar colunas criptografadas](#permissions-for-querying-encrypted-columns) abaixo.
1.  Verifique se você habilitou o Always Encrypted para a conexão de banco de dados na janela do Editor de Consultas, na qual você executará uma consulta `SELECT` recuperando e descriptografando os dados. Isso instruirá o provedor de Dados .NET Framework para SQL Server (usado pelo SSMS) a descriptografar as colunas criptografadas no conjunto de resultados da consulta. Confira [Como habilitar e desabilitar o Always Encrypted para uma conexão de banco de dados](#en-dis) abaixo.
1.  Execute a consulta `SELECT`. Os dados recuperados de colunas criptografadas serão retornados como valores de texto não criptografado dos tipos de dados originais.
 
### <a name="example"></a>Exemplo
Supondo que SSN seja uma coluna `char(11)` criptografada na tabela `Patients` , a consulta, mostrada abaixo, retornará valores de texto sem formatação, se o Always Encrypted estiver habilitado para a conexão de banco de dados e se você tiver acesso à chave mestra de coluna configurada para a coluna `SSN` .   

![always-encrypted-plaintext](../../../relational-databases/security/encryption/media/always-encrypted-plaintext.png)
 
## <a name="sending-plaintext-values-targeting-encrypted-columns"></a>Enviar valores de texto sem formatação destinados a colunas criptografadas       
Para executar uma consulta que envia um valor destinado a uma coluna criptografada, por exemplo, uma consulta que insere, atualiza ou filtra por um valor armazenado em uma coluna criptografada:

1. Verifique se você consegue acessar as chaves mestras de coluna e os metadados das chaves que protegem as colunas nas quais a consulta é executada. Para obter mais informações, confira [Permissões para consultar colunas criptografadas](#permissions-for-querying-encrypted-columns) abaixo.
1.  Verifique se você habilitou o Always Encrypted para a conexão de banco de dados na janela do Editor de Consultas, na qual você executará uma consulta `SELECT` recuperando e descriptografando os dados. Isso instruirá o provedor de Dados .NET Framework para SQL Server (usado pelo SSMS) a descriptografar as colunas criptografadas no conjunto de resultados da consulta. Confira [Como habilitar e desabilitar o Always Encrypted para uma conexão de banco de dados](#en-dis) abaixo.
1. Certifique-se de que a Parametrização de Always Encrypted esteja habilitada para a janela do Editor de Consultas. (Requer pelo menos o SSMS versão 17.0) Declare uma variável Transact-SQL e inicie-a com um valor que você deseja enviar (inserir, atualizar ou filtrar por) para o banco de dados. Confira [Parametrização de Always Encrypted](#param) abaixo para obter detalhes.

1. Execute a consulta enviando o valor da variável Transact-SQL para o banco de dados. O SSMS converterá a variável em um parâmetro de consulta e ele criptografará seu valor antes de enviá-la para o banco de dados.   

### <a name="example"></a>Exemplo
Supondo que `SSN` seja uma coluna `char(11)` criptografada na tabela `Patients` , o script abaixo tentará localizar uma linha que contenha `'795-73-9838'` na coluna SSN e retornará o valor da coluna `LastName` , desde que o Always Encrypted esteja habilitado para a conexão de banco de dados, a Parametrização de Always Encrypted esteja habilitada para a janela do Editor de Consultas e você tenha acesso à chave mestra de coluna configurada para a coluna `SSN` .   

![always-encrypted-patients](../../../relational-databases/security/encryption/media/always-encrypted-patients.png)

## <a name="permissions-for-querying-encrypted-columns"></a>Permissões para consultar colunas criptografadas

Para executar as consultas em colunas criptografadas, incluindo consultas que recuperam dados em texto cifrado, são necessárias as permissões `VIEW ANY COLUMN MASTER KEY DEFINITION` e `VIEW ANY COLUMN ENCRYPTION KEY DEFINITION` no banco de dados.

Além das permissões acima, para descriptografar qualquer resultado de consulta ou criptografar os parâmetros de consulta (produzidos por parametrização de variáveis Transact-SQL), você também precisa acessar a chave mestra de coluna protegendo as colunas de destino:

- **Repositório de Certificados – Computador local** Você precisa ter o acesso `Read` ao certificado que é usado como a chave mestra da coluna ou ser o administrador do computador.   
- **Azure Key Vault** Você precisará das permissões `get`, `unwrapKey` e `verify` no cofre que contém a chave mestra de coluna.
- **Provedor do Repositório de Chaves (KSP)** – a permissão e as credenciais necessárias que poderão ser solicitadas quando você usar um repositório de chaves ou uma chave, dependendo do repositório e da configuração do KSP.   
- **Provedor de Serviços de Criptografia (CSP)** : a permissão e as credenciais necessárias que poderão ser solicitadas quando você usar um repositório de chaves ou uma chave, dependendo do repositório e da configuração do CSP.

Para obter mais informações, consulte [Create and Store Column Master Keys (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)Criar e armazenar chaves mestras de coluna (Always Encrypted).

## <a name="enabling-and-disabling-always-encrypted-for-a-database-connection"></a><a name="en-dis"></a> Habilitando e desabilitando Always Encrypted para uma conexão de banco de dados   
Ao se conectar a um banco de dados no SSMS, habilite ou desabilite o Always Encrypted para a conexão de banco de dados. Por padrão, o Always Encrypted está desabilitado. 

Habilitar o Always Encrypted para uma conexão de banco de dados instrui o .NET Framework Data Provider para SQL Server, usado pelo SQL Server Management Studio, a tentar de forma transparente:   
-   Descriptografar todos os valores que são recuperados de colunas criptografadas e retornados nos resultados da consulta.   
-   Criptografar os valores das variáveis Transact-SQL com parâmetros que se destinam a colunas de banco de dados criptografadas.   

Se você não habilitar o Always Encrypted para uma conexão, o provedor de dados .NET Framework para SQL Server usado pelo SSMS não tentará criptografar os parâmetros de consulta nem descriptografar os resultados.

Habilite ou desabilite o Always Encrypted ao criar uma conexão ou alterar uma conexão existente usando a caixa de diálogo **Conectar ao Servidor**. 

Para habilitar (desabilitar) o Always Encrypted:
1. Abra a caixa de diálogo **Conectar ao Servidor** (confira [Conectar-se a uma Instância do SQL Server](../../../ssms/tutorials/connect-query-sql-server.md#connect-to-a-sql-server-instance) para obter detalhes).
1. Clique em **Opções >>** .
1. Se você estiver usando o SSMS 18 ou mais recente:
    1. Selecione a guia **Always Encrypted**.
    1. Para habilitar o Always Encrypted, selecione **Habilitar o Always Encrypted (criptografia de coluna)** . Para desabilitar o Always Encrypted, verifique se a opção **Habilitar o Always Encrypted (criptografia de coluna)** não está selecionada.
    1. Se você estiver usando o [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)] e a Instância do SQL Server estiver configurada com um enclave seguro, especifique uma URL de atestado de enclave. Se a Instância do SQL Server não usar um enclave seguro, deixe a caixa de texto **URL de Atestado de Enclave** em branco. Para obter mais informações, consulte [Always Encrypted com enclaves seguros](always-encrypted-enclaves.md).
1. Se você estiver usando o SSMS 17 ou mais antigo:
    1. Selecione a guia **Propriedades Adicionais**.
    1. Para habilitar o Always Encrypted, digite `Column Encryption Setting = Enabled`. Para desabilitar o Always Encrypted, especifique `Column Encryption Setting = Disabled` ou remova a **Configuração de Criptografia de Coluna** na guia **Propriedades Adicionais** (o valor padrão é **Desabilitado**).   
 1. Clique em **Conectar**.

> [!TIP]
> Para habilitar ou desabilitar Always Encrypted em uma janela do Editor de Consultas existente:   
> 1.    Clique com o botão direito do mouse em qualquer lugar na janela do Editor de Consultas.
> 2.    Selecione **Conexão** > **Alterar Conexão...** . Isso abrirá a caixa de diálogo **Conectar ao Servidor** para a conexão atual na janela do Editor de Consultas. 
> 2.    Habilite ou desabilite o Always Encrypted seguindo as etapas acima e clique em **Conectar**.  
   
## <a name="parameterization-for-always-encrypted"></a><a name="param"></a>Parametrização de Always Encrypted   
 
A Parametrização de Always Encrypted é um recurso do SQL Server Management Studio que converte automaticamente as variáveis Transact-SQL em parâmetros de consulta (instâncias da [Classe SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx)). (Requer pelo menos o SSMS versão 17.0) Isso permite que o .NET Framework Data Provider para SQL Server subjacente detecte dados destinados a colunas criptografadas e criptografe esses dados antes de enviá-los para o banco de dados. 
  
Sem parametrização, o .NET Framework Data Provider passa cada instrução, que você cria no Editor de Consultas, como uma consulta sem parâmetros. Se a consulta contiver literais ou variáveis Transact-SQL destinados a colunas criptografadas, o Provedor de Dados do .NET Framework para SQL Server não conseguirá detectá-los e criptografá-los antes de enviar a consulta ao banco de dados. Como resultado, a consulta falhará devido à incompatibilidade de tipo (entre a variável Transact-SQL literal de texto sem formatação e a coluna criptografada). Por exemplo, a consulta a seguir falhará sem parametrização, supondo que a coluna `SSN` seja criptografada.   

```sql
DECLARE @SSN NCHAR(11) = '795-73-9838'
SELECT * FROM [dbo].[Patients]
WHERE [SSN] = @SSN
```

### <a name="enabling-and-disabling-parameterization-for-always-encrypted"></a>Como habilitar e desabilitar a Parametrização do Always Encrypted

A Parametrização de Always Encrypted é desabilitada por padrão.

Para habilitar/desabilitar a Parametrização de Always Encrypted na janela atual do Editor de Consultas:

1. Selecione **Consulta** no menu principal.
2. Selecione **Opções de Consulta...** .
3. Navegue para **Execução** > **Avançado**.
4. Selecione ou desmarque **Habilitar Parametrização de Always Encrypted**.
5. Clique em **OK**.

Para habilitar/desabilitar a Parametrização de Always Encrypted nas janelas futuras do Editor de Consultas:

1. Selecione **Ferramentas** no menu principal.
2. Selecione **Opções...** .
3. Navegue para **Execução da Consulta** > **SQL Server** > **Avançado**.
4. Selecione ou desmarque **Habilitar Parametrização de Always Encrypted**.
5. Clique em **OK**.

Se você executar uma consulta em uma janela do Editor de Consultas que usa uma conexão de banco de dados com o Always Encrypted habilitado, mas a parametrização não estiver habilitada para a janela do Editor de Consultas, você receberá uma solicitação para habilitá-la.

> [!NOTE]
> A Parametrização do Always Encrypted funciona apenas nas janelas do Editor de Consultas que usam conexões de banco de dados com o Always Encrypted habilitado (confira [Como habilitar e desabilitar a Parametrização do Always Encrypted](#enabling-and-disabling-parameterization-for-always-encrypted)). Nenhuma variável Transact-SQL será parametrizada se a janela do Editor de Consultas usar uma conexão de banco de dados sem o Always Encrypted habilitado.

### <a name="how-parameterization-for-always-encrypted-works"></a>Funcionamento da Parametrização do Always Encrypted

Se a Parametrização de Always Encrypted e o comportamento do Always Encrypted na conexão de banco de dados estiverem habilitados em uma janela do Editor de Consultas, o SQL Server Management Studio sempre tentará parametrizar as variáveis Transact-SQL que atendem às seguintes condições de pré-requisito:

- São declaradas e inicializadas na mesma instrução (inicialização embutida). As variáveis declaradas usando instruções `SET` separadas não serão parametrizadas.
- São inicializadas usando um único literal. As variáveis inicializadas usando expressões, inclusive operadores ou funções, não serão parametrizadas.

Veja abaixo exemplos de variáveis que serão parametrizadas pelo SQL Server Management Studio.

```sql
DECLARE @SSN char(11) = '795-73-9838';
   
DECLARE @BirthDate date = '19990104';
DECLARE @Salary money = $30000;
```

E aqui estão alguns exemplos de variáveis que o SQL Server Management Studio não tentará parametrizar:

```sql
DECLARE @Name nvarchar(50); --Initialization separate from declaration
SET @Name = 'Abel';

DECLARE @StartDate date = GETDATE(); -- a function used instead of a literal

DECLARE @NewSalary money = @Salary * 1.1; -- an expression used instead of a literal
```
 
Para uma parametrização tentada ser bem-sucedida:   
- O tipo do literal usado para a inicialização da variável a ser parametrizada, deve corresponder ao tipo na declaração da variável.   
- Se o tipo declarado da variável for um tipo de data ou hora, a variável deverá ser inicializada usando uma cadeia de caracteres que usa um dos [formatos em conformidade com ISO 8601](https://docs.microsoft.com/sql/t-sql/functions/cast-and-convert-transact-sql#date-and-time-styles) a seguir.    

Estes são exemplos de declarações de variáveis Transact-SQL que resultarão em erros de parametrização:   
```sql
DECLARE @BirthDate date = '01/04/1999' -- unsupported date format   
   
DECLARE @Number int = 1.1 -- the type of the literal does not match the type of the variable   
```
O SQL Server Management Studio usa o Intellisense para informar quais variáveis podem ser parametrizadas com êxito e quais tentativas de parametrização falham (e por quê).   

Uma declaração de uma variável que pode ser parametrizada com êxito é marcada com um sublinhado de aviso no Editor de Consultas. Caso passe o mouse sobre uma instrução de declaração que foi marcada com um sublinhado de aviso, você verá os resultados do processo de parametrização, incluindo os valores das propriedades de chave do objeto [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) resultante (a variável é mapeada para): [SqlDbType](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.sqldbtype.aspx), [Size](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.size.aspx), [Precision](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.precision.aspx), [Scale](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.scale.aspx), [SqlValue](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.sqlvalue.aspx). Você também pode ver a lista completa de todas as variáveis que foram parametrizadas com êxito na guia **Aviso** do modo de exibição **Lista de Erros** . Para abrir o modo de exibição **Lista de Erros** , selecione **Exibição** no menu principal e escolha **Lista de Erros**.    

Se o SQL Server Management Studio tentou parametrizar uma variável, mas a parametrização falhou, a declaração da variável será marcada com um sublinhado de erro. Caso passe o mouse sobre a instrução de declaração que foi marcada com um sublinhado de erro, você obterá resultados sobre o erro. Você também pode ver a lista completa de erros de parametrização de todas as variáveis na guia **Erro** do modo de exibição **Lista de Erros** . Para abrir o modo de exibição **Lista de Erros** , selecione **Exibição** no menu principal e escolha **Lista de Erros**.   

A captura de tela abaixo mostra um exemplo de seis declarações de variável. O SQL Server Management Studio parametrizou com êxito as primeiras três variáveis. As últimas três variáveis não atenderam às condições de pré-requisito de parametrização e, portanto, o SQL Server Management Studio não tentou parametrizá-las (suas declarações não são marcadas de forma alguma).

![always-encrypted-parameter-warnings](../../../relational-databases/security/encryption/media/always-encrypted-parameter-warnings.png)
 
Outro exemplo abaixo mostra duas variáveis que atendem às condições de pré-requisito de parametrização, mas a tentativa de parametrização falhou porque as variáveis foram inicializadas incorretamente.    
 
![always-encrypted-error](../../../relational-databases/security/encryption/media/always-encrypted-error.png)
 
> [!NOTE]
> Como o Always Encrypted oferece suporte a um subconjunto limitado de conversões de tipo, em muitos casos, é necessário que o tipo de dados de uma variável Transact-SQL seja o mesmo que o tipo da coluna de banco de dados de destino, ao qual ele se destina. Por exemplo, supondo que o tipo da coluna `SSN` na tabela `Patients` seja `char(11)`, a consulta abaixo falhará, já que o tipo da variável `@SSN` , que é `nchar(11)`, não coincide com o tipo da coluna.   

```sql
DECLARE @SSN nchar(11) = '795-73-9838'
SELECT * FROM [dbo].[Patients]
WHERE [SSN] = @SSN;
```

    Msg 402, Level 16, State 2, Line 5   
    The data types char(11) encrypted with (encryption_type = 'DETERMINISTIC', 
    encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'CEK_Auto1', 
    column_encryption_key_database_name = 'Clinic') collation_name = 'Latin1_General_BIN2' 
    and nchar(11) encrypted with (encryption_type = 'DETERMINISTIC', 
    encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'CEK_Auto1', 
    column_encryption_key_database_name = 'Clinic') are incompatible in the equal to operator. 

> [!NOTE]
> Sem parametrização, a consulta inteira, incluindo as conversões de tipo, é processada dentro do SQL Server/Banco de Dados SQL do Azure. Com a parametrização habilitada, algumas conversões de tipo são realizadas pelo .NET Framework no SQL Server Management Studio. Devido às diferenças entre o sistema de tipos do .NET Framework e o sistema de tipos do SQL Server (por exemplo, diferente precisão de alguns tipos, como float), uma consulta executada com parametrização habilitada pode produzir resultados diferentes da consulta executada sem parametrização habilitada. 

## <a name="next-steps"></a>Próximas etapas
- [Desenvolver aplicativos usando o Always Encrypted](always-encrypted-client-development.md)


## <a name="see-also"></a>Consulte Também
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
