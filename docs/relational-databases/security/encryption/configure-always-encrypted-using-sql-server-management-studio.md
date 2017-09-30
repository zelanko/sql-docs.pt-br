---
title: Configurar o Always Encrypted usando o SQL Server Management Studio | Microsoft Docs
ms.custom: 
ms.date: 11/30/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.SWB.COLUMNMASTERKEY.PAGE.F1
- SQL13.SWB.COLUMNENCRYPTIONKEY.PAGE.F1
- SQL13.SWB.COLUMNMASTERKEY.ROTATION.F1
helpviewer_keywords:
- Always Encrypted, configure with SSMS
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 097ce7fb331df64de9b293a6af9e05e7d95f1b37
ms.contentlocale: pt-br
ms.lasthandoff: 09/27/2017

---
# <a name="configure-always-encrypted-using-sql-server-management-studio"></a>Configurar o Always Encrypted usando o SQL Server Management Studio
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Este artigo descreve as tarefas para configurar o Always Encrypted e gerenciar bancos de dados que usam o Always Encrypted como [SSMS (SQL Server Management Studio)](../../../ssms/download-sql-server-management-studio-ssms.md).

Quando você usa o SSMS para configurar o Always Encrypted, o SSMS lida com dados sensíveis e chaves do Always Encrypted, por isso, as chaves e os dados aparecem em texto não criptografado dentro do processo do SSMS. Portanto, é importante que você execute o SSMS em um computador seguro. Se seu banco de dados estiver hospedado no SQL Server, certifique-se de que o SSMS seja executado em um computador diferente do computador que hospeda a instância do SQL Server. Como o objetivo principal do Always Encrypted é garantir que os dados confidenciais criptografados estejam seguros mesmo se o sistema do banco de dados for comprometido, a execução de um script do PowerShell que processa chaves ou dados confidenciais no computador do SQL Server pode reduzir ou anular os benefícios do recurso. Para obter recomendações adicionais, consulte [Security Considerations for Key Management](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md#SecurityForKeyManagement)(Considerações de segurança para o Gerenciamento de Chaves).

O SSMS não dá suporte à separação de funções entre aquelas que gerenciam o banco de dados (DBAs) e aquelas que gerenciam os segredos de criptografia e têm acesso aos dados de texto não criptografado (Administradores de Segurança e/ou Administradores de Aplicativos). Se sua organização impõe a separação de funções, você deve usar o PowerShell para configurar o Always Encrypted. Para obter informações adicionais, consulte [Overview of Key Management for Always Encrypted](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md) (Visão geral do gerenciamento de chaves do Sempre Criptografado) e [Configurar o Always Encrypted usando o PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md).

## <a name="configuring-always-encrypted-using-the-always-encrypted-wizard"></a>Configurando o Always Encrypted usando o Assistente do Always Encrypted

O [Assistente do Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-wizard.md) é uma ferramenta poderosa que permite que você defina a configuração de criptografia desejada para as colunas do banco de dados selecionadas. Dependendo da configuração atual do Always Encrypted e da configuração do destino desejado, o assistente pode criptografar uma coluna, descriptografá-la (remover a criptografia) ou criptografá-la novamente (por exemplo, usando uma nova chave de criptografia de coluna ou um tipo de criptografia que é diferente do tipo atual, configurado para a coluna). É possível configurar várias colunas em uma única execução do assistente.

Se você não tiver fornecido nenhuma chave para o Always Encrypted, o assistente as gerará automaticamente para você. Você precisa apenas escolher um repositório para sua chave mestra de coluna: Repositório de Certificados do Windows ou Cofre de Chaves do Azure. O assistente gerará automaticamente nomes para as chaves e seus objetos de metadados no banco de dados. Se você precisar de mais controle de como as chaves são provisionadas (e mais opções para um repositório de chaves que contém uma chave mestra de coluna), você pode usar as caixas de diálogo **Nova Chave Mestra da Coluna** e **Nova Chave de Criptografia da Coluna** (descritas abaixo) para provisionar chaves antes de iniciar o assistente. No Assistente do Always Encrypted, você pode escolher a chave de criptografia de coluna existente.

Para obter detalhes sobre como usar o assistente, consulte  [Assistente do Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-wizard.md).

## <a name="querying-encrypted-columns"></a>Consultando colunas criptografadas

Esta seção descreve como:   
-   Recuperar valores de texto cifrado armazenados em colunas criptografadas.   
-   Recuperar valores de texto sem formatação armazenados em colunas criptografadas.   
-   Envie valores de texto sem formatação para colunas criptografadas (por exemplo, em instruções `INSERT` ou `UPDATE` e como um parâmetro de pesquisa de cláusulas `WHERE` em instruções `SELECT` ).   

### <a name="retrieving-ciphertext-values-stored-in-encrypted-columns"></a>Recuperando valores de texto cifrado armazenados em colunas criptografadas    

Para recuperar valores de uma coluna criptografada como texto cifrado (sem descriptografar os valores):
1.  Certifique-se de que Always Encrypted esteja desabilitado para a conexão de banco de dados da janela do Editor de Consultas na qual você está executando sua consulta `SELECT` . Veja [Habilitando e desabilitando Always Encrypted para uma conexão de banco de dados](#en-dis) abaixo.      
2.  Execute uma consulta `SELECT` . Os dados recuperados de colunas criptografadas serão retornados como valores binários (criptografados).   

*Exemplo*   
Supondo que `SSN` seja uma coluna criptografada na tabela `Patients` , a consulta mostrada abaixo recuperará valores binários de texto codificado, se Always Encrypted estiver desabilitado para a conexão de banco de dados.   

![always-encrypted-ciphertext](../../../relational-databases/security/encryption/media/always-encrypted-ciphertext.png)
 
### <a name="retrieving-plaintext-values-stored-in-encrypted-columns"></a>Recuperar valores de texto sem formatação armazenados em colunas criptografadas    

Para recuperar valores de uma coluna criptografada como texto sem formatação (para descriptografar os valores):   
1.  Certifique-se de que o Always Encrypted esteja habilitado para a conexão de banco de dados da janela do Editor de Consultas, na qual você está executando sua consulta `SELECT` . Isso instruirá o .NET Framework Data Provider para SQL Server (usado pelo SSMS) a descriptografar os dados recuperados de colunas criptografadas. Veja [Habilitando e desabilitando Always Encrypted para uma conexão de banco de dados](#en-dis) abaixo.
2.  Verifique se você pode acessar todas as chaves mestras de coluna configuradas para colunas criptografadas. Por exemplo, se a chave mestra de coluna for um certificado, você precisará se certificar de que o certificado seja implantado no computador em que o SSMS está sendo executado. Ou, se a chave mestra de coluna for uma chave armazenada no Cofre de Chaves do Azure, você precisará se certificar de que tem permissões para acessar a chave (além disso, talvez você tenha de entrar no Azure).
3.  Execute uma consulta `SELECT` . Os dados recuperados de colunas criptografadas serão retornados como texto sem formatação, como valores dos tipos de dados original.   

*Exemplo*   
Supondo que SSN seja uma coluna `char(11)` criptografada na tabela `Patients` , a consulta, mostrada abaixo, retornará valores de texto sem formatação, se o Always Encrypted estiver habilitado para a conexão de banco de dados e se você tiver acesso à chave mestra de coluna configurada para a coluna `SSN` .   

![always-encrypted-plaintext](../../../relational-databases/security/encryption/media/always-encrypted-plaintext.png)
 
### <a name="sending-plaintext-values-targeting-encrypted-columns"></a>Enviar valores de texto sem formatação destinados a colunas criptografadas       

Para executar uma consulta que envia um valor destinado a uma coluna criptografada, por exemplo, uma consulta que insere, atualiza ou filtra por um valor armazenado em uma coluna criptografada:   
1.  Certifique-se de que o Always Encrypted esteja habilitado para a conexão de banco de dados da janela do Editor de Consultas, na qual você está executando sua consulta `SELECT` . Isso instruirá o .NET Framework Data Provider para SQL Server (usado pelo SSMS) a criptografar as variáveis Transact-SQL com parâmetros (veja abaixo) destinadas a colunas criptografadas. Veja [Habilitando e desabilitando Always Encrypted para uma conexão de banco de dados](#en-dis) abaixo.   
2.  Verifique se você pode acessar todas as chaves mestras de coluna configuradas para colunas criptografadas. Por exemplo, se a chave mestra de coluna for um certificado, você precisará se certificar de que o certificado seja implantado no computador em que o SSMS está sendo executado. Ou, se a chave mestra de coluna for uma chave armazenada no Cofre de Chaves do Azure, você precisará se certificar de que tem permissões para acessar a chave (além disso, talvez você tenha de entrar no Azure).   
3.  Certifique-se de que a Parametrização de Always Encrypted esteja habilitada para a janela do Editor de Consultas. (Requer pelo menos o SSMS versão 17.0) Declare uma variável Transact-SQL e inicie-a com um valor que você deseja enviar (inserir, atualizar ou filtrar por) para o banco de dados. Confira [Parametrização de Always Encrypted](#param) abaixo para obter detalhes.   
    >   [!NOTE]
    >   Como o Always Encrypted oferece suporte a um subconjunto limitado de conversões de tipo, em muitos casos, é necessário que o tipo de dados de uma variável Transact-SQL seja o mesmo que o tipo da coluna de banco de dados de destino, ao qual ele se destina.   
4.  Execute a consulta enviando o valor da variável Transact-SQL para o banco de dados. O SSMS converterá a variável em um parâmetro de consulta e ele criptografará seu valor antes de enviá-la para o banco de dados.   

*Exemplo*   
Supondo que `SSN` seja uma coluna `char(11)` criptografada na tabela `Patients` , o script abaixo tentará localizar uma linha que contenha `'795-73-9838'` na coluna SSN e retornará o valor da coluna `LastName` , desde que o Always Encrypted esteja habilitado para a conexão de banco de dados, a Parametrização de Always Encrypted esteja habilitada para a janela do Editor de Consultas e você tenha acesso à chave mestra de coluna configurada para a coluna `SSN` .   

![always-encrypted-patients](../../../relational-databases/security/encryption/media/always-encrypted-patients.png)
 
### <a name="en-dis"></a> Habilitando e desabilitando Always Encrypted para uma conexão de banco de dados   

Habilitar o Always Encrypted para uma conexão de banco de dados instrui o .NET Framework Data Provider para SQL Server, usado pelo SQL Server Management Studio, a tentar de forma transparente:   
-   Descriptografar todos os valores que são recuperados de colunas criptografadas e retornados nos resultados da consulta.   
-   Criptografar os valores das variáveis Transact-SQL com parâmetros que se destinam a colunas de banco de dados criptografadas.   
Para habilitar o Always Encrypted para uma conexão de banco de dados, especifique `Column Encryption Setting=Enabled` na guia **Propriedades Adicionais** da caixa de diálogo **Conectar ao Servidor** .    
Para desabilitar o Always Encrypted para uma conexão de banco de dados, especifique `Column Encryption Setting=Disabled` ou simplesmente remova a definição de **Configuração de Criptografia de Coluna** da guia **Propriedades Adicionais** da caixa de diálogo **Conectar ao Servidor** (seu valor padrão é **Desabilitado**).   

>  [!TIP] 
>  Para habilitar ou desabilitar Always Encrypted em uma janela do Editor de Consultas existente:   
>  1.   Clique com o botão direito do mouse em qualquer lugar na janela do Editor de Consultas.
>  2.   Selecione **Conexão** > **Alterar Conexão...**, 
>  3.   Clique em **Opções** >>,
>  4.   Selecione a guia **Propriedades Adicionais** e digite `Column Encryption Setting=Enabled` (para habilitar o comportamento de Always Encrypted) ou remover a configuração (para desabilitar o comportamento de Always Encrypted).   
>  5.   Clique em **Conectar**.   
   
### <a name="param"></a>Parametrização de Always Encrypted   
 
A Parametrização de Always Encrypted é um recurso do SQL Server Management Studio que converte automaticamente as variáveis Transact-SQL em parâmetros de consulta (instâncias da [Classe SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx)). (Requer pelo menos o SSMS versão 17.0) Isso permite que o .NET Framework Data Provider para SQL Server subjacente detecte dados destinados a colunas criptografadas e criptografe esses dados antes de enviá-los para o banco de dados. 
  
Sem parametrização, o .NET Framework Data Provider passa cada instrução, que você cria no Editor de Consultas, como uma consulta sem parâmetros. Se a consulta contiver literais ou variáveis Transact-SQL destinados a colunas criptografadas, o .NET Framework Data Provider para SQL Server não será capaz de detectá-los e criptografá-los, antes de enviar a consulta ao banco de dados. Como resultado, a consulta falhará devido à incompatibilidade de tipo (entre a variável Transact-SQL literal de texto sem formatação e a coluna criptografada). Por exemplo, a consulta a seguir falhará sem parametrização, supondo que a coluna `SSN` seja criptografada.   

```tsql
DECLARE @SSN NCHAR(11) = '795-73-9838'
SELECT * FROM [dbo].[Patients]
WHERE [SSN] = @SSN
```

#### <a name="enablingdisabling-parameterization-for-always-encrypted"></a>Habilitando/desabilitando a Parametrização de Always Encrypted   


A Parametrização de Always Encrypted é desabilitada por padrão.    

Para habilitar/desabilitar a Parametrização de Always Encrypted na janela atual do Editor de Consultas:   
1.  Selecione **Consulta** no menu principal.   
2.  Selecione **Opções de Consulta…**.   
3.  Navegue para **Execução** > **Avançado**.   
4.  Selecione ou desmarque **Habilitar Parametrização de Always Encrypted**.   
5.  Clique em **OK**.   

Para habilitar/desabilitar a Parametrização de Always Encrypted nas janelas futuras do Editor de Consultas:   
1.  Selecione **Ferramentas** no menu principal.   
2.  Selecione **Opções...**.   
3.  Navegue para **Execução da Consulta** > **SQL Server** > **Avançado**.   
4.  Selecione ou desmarque **Habilitar Parametrização de Always Encrypted**.   
5.  Clique em **OK**.   

Se você executar uma consulta em uma janela do Editor de Consultas que usa uma conexão de banco de dados com o Always Encrypted habilitado, mas a parametrização não estiver habilitada para a janela do Editor de Consultas, você deverá habilitá-la.   
>   [!NOTE]   
>   A Parametrização de Always Encrypted funciona apenas nas janelas do Editor de Consultas que usam conexões de banco de dados com Always Encrypted habilitado (consulte [Habilitando e desabilitando Always Encrypted para um banco de dados](#en-dis)). Nenhuma variável Transact-SQL será parametrizada se a janela do Editor de Consultas usar uma conexão de banco de dados sem o Always Encrypted habilitado.   

#### <a name="how-parameterization-for-always-encrypted-works"></a>Funcionamento da Parametrização do Always Encrypted   

Se a Parametrização de Always Encrypted e o comportamento do Always Encrypted na conexão de banco de dados estiverem habilitados em uma janela do Editor de Consultas, o SQL Server Management Studio sempre tentará parametrizar as variáveis Transact-SQL que atendem às seguintes condições de pré-requisito:    
- São declaradas e inicializadas na mesma instrução (inicialização embutida). Variáveis declaradas usando instruções `SET` separadas não serão parametrizadas.   
- São inicializadas usando um único literal. Variáveis inicializadas usando expressões, inclusive operadores ou funções, não serão parametrizadas.      

A seguir estão exemplos de variáveis, que o SQL Server Management Studio irá parametrizar.   
```tsql
DECLARE @SSN char(11) = '795-73-9838';
   
DECLARE @BirthDate date = '19990104';
DECLARE @Salary money = $30000;
```

E, aqui estão alguns exemplos de variáveis que o SQL Server Management Studio não tentará parametrizar:   
```tsql
DECLARE @Name nvarchar(50); --Initialization seperate from declaration
SET @Name = 'Abel';
   
DECLARE @StartDate date = GETDATE(); -- a function used instead of a literal
   
DECLARE @NewSalary money = @Salary * 1.1; -- an expression used instead of a literal
```
 
Para uma parametrização tentada ser bem-sucedida:   
- O tipo do literal usado para a inicialização da variável a ser parametrizada, deve corresponder ao tipo na declaração da variável.   
- Se o tipo declarado da variável for um tipo de data ou hora, a variável deverá ser inicializada usando uma cadeia de caracteres que usa um dos seguintes formatos ISO 8601 compatíveis.   

Estes são exemplos de declarações de variáveis Transact-SQL que resultarão em erros de parametrização:   
```tsql
DECLARE @BirthDate date = '01/04/1999' -- unsupported date format   
   
DECLARE @Number int = 1.1 -- the type of the literal does not match the type of the variable   
```
O SQL Server Management Studio usa o Intellisense para informar quais variáveis podem ser parametrizadas com êxito e quais tentativas de parametrização falham (e por quê).   

Uma declaração de uma variável que pode ser parametrizada com êxito é marcada com um sublinhado de aviso no Editor de Consultas. Caso passe o mouse sobre uma instrução de declaração que foi marcada com um sublinhado de aviso, você verá os resultados do processo de parametrização, incluindo os valores das propriedades de chave do objeto [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) resultante (a variável é mapeada para): [SqlDbType](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.sqldbtype.aspx), [Tamanho](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.size.aspx), [Precisão](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.precision.aspx), [Escala](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.scale.aspx), [SqlValue](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.sqlvalue.aspx). Você também pode ver a lista completa de todas as variáveis que foram parametrizadas com êxito na guia **Aviso** do modo de exibição **Lista de Erros** . Para abrir o modo de exibição **Lista de Erros** , selecione **Exibição** no menu principal e escolha **Lista de Erros**.    

Se o SQL Server Management Studio tentou parametrizar uma variável, mas a parametrização falhou, a declaração da variável será marcada com um sublinhado de erro. Caso passe o mouse sobre a instrução de declaração que foi marcada com um sublinhado de erro, você obterá resultados sobre o erro. Você também pode ver a lista completa de erros de parametrização de todas as variáveis na guia **Erro** do modo de exibição **Lista de Erros** . Para abrir o modo de exibição **Lista de Erros** , selecione **Exibição** no menu principal e escolha **Lista de Erros**.   

A captura de tela abaixo mostra um exemplo de seis declarações de variável. O SQL Server Management Studio parametrizou com êxito as primeiras três variáveis. As últimas três variáveis não atenderam às condições de pré-requisito de parametrização e, portanto, o SQL Server Management Studio não tentou parametrizá-las (suas declarações não são marcadas de forma alguma).   

![always-encrypted-parameter-warnings](../../../relational-databases/security/encryption/media/always-encrypted-parameter-warnings.png)
 
Outro exemplo abaixo mostra duas variáveis que atendem às condições de pré-requisito de parametrização, mas a tentativa de parametrização falhou porque as variáveis foram inicializadas incorretamente.    
 
![always-encrypted-error](../../../relational-databases/security/encryption/media/always-encrypted-error.png)
 
>   [!NOTE]
>   Como o Always Encrypted oferece suporte a um subconjunto limitado de conversões de tipo, em muitos casos, é necessário que o tipo de dados de uma variável Transact-SQL seja o mesmo que o tipo da coluna de banco de dados de destino, ao qual ele se destina. Por exemplo, supondo que o tipo da coluna `SSN` na tabela `Patients` seja `char(11)`, a consulta abaixo falhará, já que o tipo da variável `@SSN` , que é `nchar(11)`, não coincide com o tipo da coluna.   

```tsql
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

>   [!NOTE]
>   Sem parametrização, a consulta inteira, incluindo as conversões de tipo, é processada dentro do SQL Server/Banco de Dados SQL do Azure. Com a parametrização habilitada, algumas conversões de tipo são realizadas pelo .NET Framework no SQL Server Management Studio. Devido às diferenças entre o sistema de tipos do .NET Framework e o sistema de tipos do SQL Server (por exemplo, diferente precisão de alguns tipos, como float), uma consulta executada com parametrização habilitada pode produzir resultados diferentes da consulta executada sem parametrização habilitada. 

#### <a name="permissions"></a>Permissões      

Para executar as consultas em colunas criptografadas, incluindo consultas que recuperam dados em texto cifrado, são necessárias as permissões `VIEW ANY COLUMN MASTER KEY DEFINITION` e `VIEW ANY COLUMN ENCRYPTION KEY DEFINITION` no banco de dados.   
Além das permissões acima, para descriptografar qualquer resultado de consulta ou criptografar os parâmetros de consulta (produzidos por parametrização de variáveis Transact-SQL), você também precisa acessar a chave mestra de coluna protegendo as colunas de destino:   
- **Repositório de Certificados – computador local** Você deve ter acesso `Read` ao certificado que é usado como chave mestra da coluna, ou ser o administrador do computador.   
- **Cofre de Chaves do Azure** Você precisa de `get`, `unwrapKey`e verificar as permissões no cofre que contém a chave mestra da coluna.   
- **Provedor do Repositório de Chaves (CNG)** A permissão e as credenciais necessárias que podem ser solicitadas ao usar um repositório de chaves ou uma chave, dependendo do repositório e da configuração do KSP.   
- **Provedor de Serviços de Criptografia (CAPI)** A permissão e as credenciais necessárias que podem ser solicitadas ao usar um repositório de chaves ou uma chave, dependendo do repositório e da configuração do CSP.   

Para obter mais informações, consulte [Create and Store Column Master Keys (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)Criar e armazenar chaves mestras de coluna (Always Encrypted).


<a name="provisioncmk"></a>
## <a name="provisioning-column-master-keys-new-column-master-key"></a>Provisionando chaves mestras da coluna (Nova Chave Mestra da Coluna)

A caixa de diálogo **Nova Chave Mestra da Coluna** permite que você gere uma chave mestra da coluna ou escolha uma chave existente em um repositório de chaves e crie metadados de chave mestra da coluna para a chave criada ou selecionada no banco de dados.

1.  Usando o **Pesquisador de Objetos**, navegue até a pasta **Segurança > Chaves Always Encrypted** em seu banco de dados.
2.  Clique com o botão direito do mouse na pasta **Chaves Mestras de Coluna** e selecione **Nova Chave Mestra de Coluna...**. 
3.  Na caixa de diálogo **Nova Chave Mestra de Coluna** , digite o nome do objeto de metadados de chave mestra de coluna.
4.  Selecione um repositório de chaves:
    - **Repositório de Certificados – Usuário atual** : indica o local do repositório do certificado do usuário atual no Repositório de Certificados do Windows, que é seu repositório pessoal. 
    - **Repositório de Certificados – Computador local** : indica o local do repositório de certificados do computador local no Repositório de Certificados do Windows. 
    - **Cofre de Chaves do Azure** : você precisará entrar no Azure (clique em **Entrar**). Após entrar, você poderá escolher uma das suas assinaturas do Azure e um cofre de chaves.
    - **Provedor do Repositório de Chaves (CNG)** : indica um repositório de chaves que é acessível por meio do KSP (provedor do repositório de chaves) que implementa a API CNG (Cryptography Next Generation). Normalmente, esse tipo de repositório é um HSM (módulo de segurança de hardware). Depois de selecionar essa opção, você precisará escolher um KSP. **Provedor de Armazenamento de Chaves do Software Microsoft** é selecionado por padrão. Se você desejar usar uma chave mestra de coluna armazenada em um HSM, selecione um KSP para seu dispositivo (deve ser instalado e configurado no computador antes de abrir a caixa de diálogo).
    -   **Provedor de Serviços de Criptografia (CAPI)** : um repositório de chaves que é acessível por meio de um CSP (provedor de serviços de criptografia) que implementa a CAPI (Cryptography API). Normalmente, esse tipo de repositório é um HSM (módulo de segurança de hardware). Depois de selecionar essa opção, você precisará escolher um CSP.  Se você desejar usar uma chave mestra de coluna armazenada em um HSM, selecione um CSP para seu dispositivo (deve ser instalado e configurado no computador antes de abrir a caixa de diálogo).
    
    >   [!NOTE]
    >   Como a CAPI é uma API preterida, a opção Provedor de Serviços de Criptografia (CAPI) é desabilitada por padrão. Você pode habilitar criando o valor CAPI Provider Enabled DWORD na chave **[HKEY_CURRENT_USER\Software\Microsoft\Microsoft SQL Server\sql13\Tools\Client\Always Encrypted]** no Registro do Windows e definindo-o como 1. Você deve usar o CNG em vez de CAPI, a menos que seu repositório de chaves não dê suporte ao CNG.
   
    Para obter mais informações sobre os repositórios de chaves acima, consulte [Create and Store Column Master Keys (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)Criar e armazenar chaves mestras de coluna (Always Encrypted).

5.  Selecione uma chave existente no seu repositório de chaves ou clique no botão **Gerar Chave** ou **Gerar Certificado** para criar uma chave no repositório de chaves. 
6.  Clique em **OK** e a nova chave aparecerá na lista. 

O SQL Server Management Studio criará metadados para a chave mestra da coluna no banco de dados. A caixa de diálogo consegue isso gerando e emitindo uma instrução [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) .


<a name="provisioncek"></a> 
## <a name="provisioning-column-encryption-keys-new-column-encryption-key"></a>Provisionamento de chaves de criptografia da coluna (Nova Chave de Criptografia da Coluna)

A caixa de diálogo **Nova Chave de Criptografia de Coluna** permite gerar uma nova chave de criptografia de coluna, criptografá-la com uma chave mestra da coluna e criar metadados de chave de criptografia de coluna no banco de dados.

1.  Usando o **Pesquisador de Objetos**, navegue até a pasta **Segurança/Chaves Always Encrypted** em seu banco de dados.
2.  Clique com o botão direito do mouse na pasta **Chaves de Criptografia de Coluna** e selecione **Nova Chave de Criptografia da Coluna...**. 
3.  Na caixa de diálogo **Nova Chave de Criptografia da Coluna** , digite o nome do objeto de metadados de chave de criptografia da coluna.
4.  Selecione um objeto de metadados que representa a chave mestra da coluna no banco de dados.
5.  Clique em **OK**. 


O SQL Server Management Studio gerará uma nova chave de criptografia da coluna e, em seguida, recuperará os metadados para a chave mestra da coluna selecionada do banco de dados. O SQL Server Management Studio, em seguida, usará os metadados de chave mestra da coluna para entrar em contato com o repositório de chaves que contém a chave mestra da coluna e criptografará a chave de criptografia da coluna. Por fim, os metadados da nova chave de criptografia da coluna serão criados no banco de dados. A caixa de diálogo consegue isso gerando e emitindo uma instrução [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md) .

### <a name="permissions"></a>Permissões

Você precisa das permissões de banco de dados *ALTER ANY ENCRYPTION MASTER KEY* e *VIEW ANY COLUMN MASTER KEY DEFINITION* no banco de dados para a caixa de diálogo criar os metadados da chave de criptografia da coluna e para acessar os metadados de chave mestra da coluna.
Para acessar um repositório de chaves e usar a chave mestra da coluna, você pode precisar de permissões no repositório de chaves e/ou na chave:
- **Repositório de Certificados – Computador local** : você deve ter acesso de leitura ao certificado que é usado como uma chave mestra da coluna ou ser o administrador do computador.
- **Cofre de Chaves do Azure** : você precisa das permissões *get*, *unwrapKey*, *wrapKey*, *sign*e *verify*  no cofre que contém a chave mestra da coluna.
- **Provedor do Repositório de Chaves (CNG)** : as permissões e credenciais necessárias que podem ser solicitadas ao usar um repositório de chaves ou uma chave, dependendo do repositório e da configuração do KSP.
- **Provedor de Serviços de Criptografia (CAPI)** : a permissão e as credenciais necessárias podem ser solicitadas ao usar um repositório de chaves ou uma chave, dependendo do repositório e da configuração do CSP.

Para obter mais informações, consulte [Create and Store Column Master Keys (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)Criar e armazenar chaves mestras de coluna (Always Encrypted).

<a name="rotatecmk"></a>
## <a name="rotating-column-master-keys"></a>Rotação de chaves mestras de coluna

A rotação de uma chave mestra de coluna é um processo de substituição de uma chave mestra de coluna existente por uma nova chave mestra de coluna. Pode ser necessário girar uma chave se ela tiver sido comprometida ou para manter a conformidade com políticas e regulamentos da sua organização que exigem que chaves criptográficas sejam giradas com regularidade. A rotação de chave mestra de coluna envolve a descriptografia de chaves de criptografia de coluna que são protegidas com a chave mestra de coluna atual, criptografando-as novamente usando a nova chave mestra de coluna e atualizando os metadados da chave. Para obter mais informações, consulte [Overview of Key Management for Always Encrypted](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)(Visão geral do gerenciamento de chaves do Sempre Criptografado).

**Etapa 1: Provisionar uma nova chave mestra de coluna**

Provisione uma nova chave mestra de coluna seguindo as etapas na seção Provisionando chaves mestras da coluna acima.

**Etapa 2: Criptografar chaves de criptografia de coluna com a nova chave mestra de coluna**

Normalmente, uma chave mestra de coluna protege uma ou mais chaves de criptografia de coluna. Cada chave de criptografia de coluna tem um valor criptografado armazenado no banco de dados, que é o produto da criptografia da chave de criptografia de coluna com a chave mestra de coluna.
Nesta etapa, criptografe cada uma das chaves de criptografia de coluna que são protegidas com a chave mestra de coluna que você está girando, com a nova chave mestra de coluna, e armazene o novo valor criptografado no banco de dados. Como resultado, cada chave de criptografia de coluna afetada pela rotação terá dois valores criptografados: um valor criptografado com a chave mestra de coluna existente e um novo valor criptografado com a nova chave mestra de coluna.

1.  Usando o **Pesquisador de Objetos**, navegue até a pasta **Segurança &gt; Chaves Always Encrypted &gt; Chaves Mestras de Coluna** e localize a chave mestra de coluna que você está girando.
2.  Clique com o botão direito do mouse na chave mestra de coluna e selecione **Girar**.
3.  Na caixa de diálogo **Rotação de Chave Mestra de Coluna** , selecione o nome de sua nova chave mestra de coluna, criada na Etapa 1, no campo **Destino** .
4.  Examine a lista de chaves de criptografia de coluna, protegidas pelas chaves mestras de coluna existente. Essas chaves serão afetadas pela rotação.
5.  Clique em **OK**.

O SQL Server Management Studio obterá os metadados das chaves de criptografia de coluna que são protegidos pela chave mestra de coluna antiga e os metadados das chaves mestras de coluna antiga e nova. Em seguida, o SSMS usará os metadados de chave mestra de coluna para acessar o repositório de chaves que contém a chave mestra de coluna antiga e descriptografará as chaves de criptografia de coluna. Subsequentemente, o SSMS acessará o repositório de chaves que mantém a nova chave mestra de coluna para gerar um novo conjunto de valores criptografados das chaves de criptografia de coluna e, em seguida, adicionará os novos valores aos metadados (gerando e emitindo instruções [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md) ).

> [!NOTE]
> Certifique-se de que cada uma das chaves de criptografia de coluna, criptografadas com a chave mestra de coluna antiga, não esteja criptografada com nenhuma outra chave mestra de coluna. Em outras palavras, cada chave de criptografia de coluna afetada pela rotação, deve ter exatamente um valor criptografado no banco de dados. Se qualquer chave de criptografia de coluna afetada tiver mais de um valor criptografado, será necessário remover o valor antes de prosseguir com a rotação (consulte a *Etapa 4* sobre como remover um valor criptografado de uma chave de criptografia de coluna).

**Etapa 3: Configurar seus aplicativos com a nova chave mestra de coluna**

Nesta etapa, você precisa se certificar de que todos os aplicativos cliente que consultam colunas de banco de dados protegidas pela chave mestra de coluna que você está girando possam acessar a nova chave mestra de coluna (isto é, colunas de banco de dados criptografadas com uma chave de criptografia de coluna que está criptografada com a chave mestra de coluna, que está sendo girada). Esta etapa depende do tipo de repositório de chaves em que sua nova chave mestra de coluna está. Por exemplo:
- Se a nova chave mestra de coluna for um certificado armazenado no Repositório de Certificados do Windows, você precisará implantar o certificado no mesmo local do repositório de certificados (*Usuário Atual* ou *Computador local*) que o local especificado no caminho da chave de sua chave mestra de coluna no banco de dados. O aplicativo precisa ser capaz de acessar o certificado:
    - Se o certificado for armazenado no local do repositório de certificados do *Usuário Atual* , o certificado precisará ser importado no repositório do Usuário Atual da identidade (usuário) do Windows do aplicativo.
    - Se o certificado for armazenado no local do repositório de certificados do *Computador local* , a identidade do Windows do aplicativo deverá ter permissão para acessar o certificado.
- Se a nova chave mestra de coluna for armazenada no Cofre de Chaves do Microsoft Azure, o aplicativo deverá ser implementado para que possa se autenticar no Azure e tenha permissão para acessar a chave.

Para obter detalhes, consulte [Create and Store Column Master Keys (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)Criar e armazenar chaves mestras de coluna (Always Encrypted).

> [!NOTE]
> Neste ponto da rotação, a chave mestra de coluna antiga e a nova chave mestra de coluna são válidas e podem ser usadas para acessar os dados.

**Etapa 4: Limpar os valores de chave de criptografia de coluna criptografadas com a chave mestra de coluna antiga**

Depois de configurar todos os seus aplicativos para usar a nova chave mestra de coluna, remova do banco de dados os valores das chaves de criptografia de coluna que são criptografados com a chave mestra de coluna *antiga* . A remoção de valores antigos garantirá a preparação para a próxima rotação (lembre-se, cada chave de criptografia de coluna, protegida com uma chave mestra de coluna que será girada, deve ter exatamente um valor criptografado).

Outro motivo para limpar o valor antigo, antes de arquivar ou remover a chave mestra de coluna antiga, está relacionado ao desempenho: ao consultar uma coluna criptografada, talvez um driver de cliente com Always Encrypted habilitado tente descriptografar dois valores: o valor antigo e o novo. O driver não sabe qual das duas chaves mestras de coluna é válida no ambiente do aplicativo, portanto ele recuperará os dois valores criptografados do servidor. Se a descriptografia de um dos valores falhar, por estar protegido com a chave mestra de coluna que não está disponível (por exemplo, a chave mestra de coluna antiga que foi removida do armazenamento), o driver tentará descriptografar outro valor usando a nova chave mestra de coluna.

> [!WARNING]
> Se você remover um valor de uma chave de criptografia de coluna antes de sua chave mestra de coluna correspondente ter sido disponibilizada para um aplicativo, o aplicativo não poderá mais descriptografar a coluna do banco de dados.

1.  Usando o **Pesquisador de Objetos**, navegue até a pasta **Segurança > Chaves Always Encrypted** e localize a chave mestra de coluna existente que deseja substituir.
2.  Clique com o botão direito do mouse em sua chave mestra de coluna existente e selecione **Limpar**.
3.  Examine a lista de valores de chave de criptografia da coluna a serem removidos.
4.  Clique em **OK**.

O SQL Server Management Studio emitirá instruções [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md) para remover os valores criptografados das chaves de criptografia de coluna que estão criptografados com a chave mestra de coluna antiga.

**Etapa 5: Excluir metadados para a chave mestra de coluna antigo**

Se você optar por remover a definição da chave mestra de coluna antiga do banco de dados, use as etapas abaixo. 
1.  Usando o **Pesquisador de Objetos**, navegue até a pasta **Segurança &gt; Chaves Always Encrypted &gt; Chaves Mestras de Coluna** e localize a chave mestra de coluna antiga a ser removida do banco de dados.
2.  Clique com o botão direito do mouse na chave mestra de coluna antiga e selecione **Excluir**. (Isso gerará e emitirá uma instrução [DROP COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/drop-column-master-key-transact-sql.md) para remover os metadados da chave mestra de coluna.)
3.  Clique em **OK**.

> [!NOTE]
> É altamente recomendável não excluir a chave mestra de coluna antiga permanentemente após a rotação. Em vez disso, você deve manter a chave mestra de coluna antiga em seu repositório de chaves atual ou arquivá-la em outro local seguro. Se você restaurar seu banco de dados de um arquivo de backup para um ponto anterior à configuração da nova chave mestra de coluna, precisará da chave antiga para acessar os dados.

### <a name="permissions"></a>Permissões

Girar uma chave mestra de coluna requer as seguintes permissões de banco de dados:

- **ALTER ANY COLUMN MASTER KEY** : necessária para criar os metadados para a nova chave mestra de coluna e excluir os metadados da chave mestra de coluna antiga.
- **ALTER ANY COLUMN ENCRYPTION KEY** : necessária para modificar metadados de chave de criptografia de coluna (adicionar novos valores criptografados).
- **VIEW ANY COLUMN MASTER KEY DEFINITION** : necessária para acessar e ler os metadados das chaves mestras de coluna.
- **VIEW ANY COLUMN ENCRYPTION KEY DEFINITION** : necessária para acessar e ler os metadados das chaves de criptografia de coluna. 

Você também precisa ser capaz de acessar a chave mestra de coluna antiga e a nova chave mestra de coluna em seus repositórios de chaves. Para acessar um repositório de chaves e usar uma chave mestra da coluna, você pode precisar de permissões no repositório de chaves e/ou na chave:
- **Repositório de Certificados – Computador local** : você deve ter acesso de leitura ao certificado que é usado como chave mestra da coluna ou ser o administrador do computador.
- **Cofre de Chaves do Azure** : você precisa das permissões *create*, *get*, *unwrapKey*, *wrapKey*, *sign*e *verify* no cofre que contém as chaves mestras da coluna.
- **Provedor do Repositório de Chaves (CNG)** : as permissões e credenciais necessárias que podem ser solicitadas ao usar um repositório de chaves ou uma chave, dependendo do repositório e da configuração do KSP.
- **Provedor de Serviços de Criptografia (CAPI)** : a permissão e as credenciais necessárias podem ser solicitadas ao usar um repositório de chaves ou uma chave, dependendo do repositório e da configuração do CSP.

Para obter mais informações, consulte [Create and Store Column Master Keys (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)Criar e armazenar chaves mestras de coluna (Always Encrypted).

<a name="rotatecek"></a> 
## <a name="rotating-column-encryption-keys"></a>Girando chaves de criptografia de coluna

Girar uma chave de criptografia da coluna envolve descriptografar os dados em todas as colunas que estão criptografados com a chave a ser girada e criptografá-los novamente usando a nova chave de criptografia de coluna.

>[!NOTE]
> Girar uma chave de criptografia de coluna pode demorar muito tempo se as tabelas que contêm as colunas criptografadas com a chave que está sendo girada forem grandes. Enquanto os dados estão sendo criptografados novamente, os aplicativos não podem realizar gravações nas tabelas afetadas. Portanto, sua organização precisa planejar uma rotação de chave de criptografia de coluna com muito cuidado.
Para girar uma chave de criptografia de coluna, use o Assistente do Always Encrypted.

1.  Abra o assistente para o banco de dados: clique com o botão direito do mouse, aponte para **Tarefas**e clique em **Criptografar Colunas**.
2.  Examine a página **Introdução** e, em seguida, clique em **Avançar**.
3.  Na página **Seleção de Coluna** , expanda as tabelas e localize todas as colunas que deseja substituir que atualmente estão criptografadas com a chave de criptografia de coluna.
4.  Para cada coluna criptografada com a chave de criptografia de coluna antiga, defina a **Chave de Criptografia** para uma nova chave gerada automaticamente. **Observação:** como alternativa, você pode criar uma nova chave de criptografia de coluna antes de executar o assistente. Consulte a seção *Provisionamento de chaves de criptografia da coluna* acima.
5.  Na página **Configuração da Chave Mestra** , selecione um local para armazenar a nova chave e uma fonte de chave mestra e clique em **Avançar**. **Observação:** se você estiver usando uma chave de criptografia de coluna existente (não uma gerada automaticamente), não há nenhuma ação a ser executada nesta página.
6.  Na **página Validação**, escolha se deseja executar o script imediatamente ou criar um script do PowerShell e, em seguida, clique em **Avançar**.
7.  Na página **Resumo** , examine as opções que você selecionou, clique em **Concluir** e feche o assistente após a conclusão.
8.  Usando o **Pesquisador de Objetos**, navegue até a pasta **Segurança/Chaves Always Encrypted/Chaves de Criptografia de Coluna** e localize a chave de criptografia de coluna antiga a ser removida do banco de dados. Clique com o botão direito do mouse na chave e selecione **Excluir**.

### <a name="permissions"></a>Permissões

A rotação de uma chave de criptografia de coluna requer as seguintes permissões de banco de dados: **ALTER ANY COLUMN MASTER KEY** : necessária se você usar uma nova chave de criptografia de coluna gerada automaticamente (uma nova chave mestra de coluna e seus novos metadados também serão gerados).
**ALTER ANY COLUMN ENCRYPTION KEY** : necessária para adicionar metadados para a nova chave de criptografia de coluna.
**VIEW ANY COLUMN MASTER KEY DEFINITION** : necessária para acessar e ler os metadados das chaves mestras de coluna.
**VIEW ANY COLUMN ENCRYPTION KEY DEFINITION** : necessária para acessar e ler os metadados das chaves de criptografia de coluna.

Você também precisa ser capaz de acessar as chaves mestras de coluna das chaves de criptografia de coluna nova e antiga. Para acessar um repositório de chaves e usar uma chave mestra da coluna, você pode precisar de permissões no repositório de chaves e/ou na chave:
- **Repositório de Certificados – Computador local** : você deve ter acesso de leitura para o certificado que é usado como chave mestra da coluna ou ser o administrador do computador.
- **Cofre de Chaves do Azure** : você precisa das permissões get, unwrapKey e verify no cofre que contém a chave mestra da coluna.
- **Provedor do Repositório de Chaves (CNG)** : as permissões e credenciais necessárias que podem ser solicitadas ao usar um repositório de chaves ou uma chave, dependendo do repositório e da configuração do KSP.
- **Provedor de Serviços de Criptografia (CAPI)** : a permissão e as credenciais necessárias podem ser solicitadas ao usar um repositório de chaves ou uma chave, dependendo do repositório e da configuração do CSP.

Para obter mais informações, consulte [Create and Store Column Master Keys (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)Criar e armazenar chaves mestras de coluna (Always Encrypted).

## <a name="performing-dac-upgrade-operations-when-database-or-dacpac-uses-always-encrypted"></a>Executando operações de atualização de DAC quando o banco de dados ou o DACPAC usa o Always Encrypted

As[operações de DAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_3) têm suporte em arquivos DACPAC e bancos de dados com esquemas contendo colunas criptografadas. Considerações especiais são aplicadas à operação de atualização de DAC. Consulte [Atualizar um aplicativo da camada de dados](../../../relational-databases/data-tier-applications/upgrade-a-data-tier-application.md) sobre como executar uma operação de atualização de DAC em várias ferramentas, incluindo o SSMS. 

Quando você atualiza um banco de dados usando um DACPAC e o DACPAC ou o banco de dados de destino tem colunas criptografadas, a operação de atualização disparará uma operação de criptografia de dados se todas as seguintes condições forem atendidas:
- O banco de dados contém uma coluna com dados.
- A mesma coluna existe no DACPAC.
- A configuração de criptografia da coluna no banco de dados é diferente da configuração da coluna correspondente no DACPAC. Consulte a tabela a seguir para obter detalhes.

| Condição|Ação|
|:---|:---|
|A coluna está criptografada no DACPAC e não está criptografada no banco de dados.| Os dados na coluna serão criptografados.|
|A coluna não está criptografada no DACPAC e está criptografada no banco de dados.| Os dados na coluna serão descriptografados (a criptografia será removida da coluna).|
| A coluna está criptografada no DACPAC e no banco de dados, mas a coluna no DACPAC usa um tipo de criptografia diferente e/ou uma chave de criptografia de coluna diferente da coluna correspondente no banco de dados.|Os dados na coluna serão descriptografados e criptografados novamente para corresponder à configuração de criptografia no DACPAC.|

> [!NOTE]
> Se a chave mestra de coluna configurada para a coluna no banco de dados ou no DACPAC estiver armazenada em um Cofre de Chaves do Azure, você será solicitado a entrar no Azure (caso ainda não tenha entrado).

### <a name="permissions"></a>Permissões

Para executar uma operação de atualização de DAC se o Always Encrypted estiver configurado no DACPAC ou no banco de dados de destino, talvez seja necessário ter algumas ou todas as permissões abaixo, dependendo das diferenças entre o esquema no DACPAC e o esquema do banco de dados de destino.

*ALTER ANY COLUMN MASTER KEY*, *ALTER ANY COLUMN ENCRYPTION KEY*, *VIEW ANY COLUMN MASTER KEY DEFINITION*, *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION*

Se a operação de atualização disparar uma operação de criptografia de dados, você também precisará ser capaz de acessar as chaves mestras de coluna configuradas para as colunas afetadas:
- **Repositório de Certificados – Computador local** : você deve ter acesso de leitura ao certificado que é usado como chave mestra da coluna ou ser o administrador do computador.
- **Cofre de Chaves do Azure** : você precisa das permissões *create*, *get*, *unwrapKey*, *wrapKey*, *sign*e *verify* no cofre que contém as chaves mestras da coluna.
- **Provedor do Repositório de Chaves (CNG)** : as permissões e credenciais necessárias que podem ser solicitadas ao usar um repositório de chaves ou uma chave, dependendo do repositório e da configuração do KSP.
- **Provedor de Serviços de Criptografia (CAPI)** : a permissão e as credenciais necessárias podem ser solicitadas ao usar um repositório de chaves ou uma chave, dependendo do repositório e da configuração do CSP.

Para obter mais informações, consulte [Create and Store Column Master Keys (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)Criar e armazenar chaves mestras de coluna (Always Encrypted).

## <a name="migrating-databases-with-encrypted-columns-using-bacpac"></a>Migrando bancos de dados com colunas criptografadas usando BACPAC

Quando você exporta um banco de dados, todos os dados armazenados em colunas criptografadas são recuperados e colocados no [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) resultante (em formato criptografado). O BACPAC resultante também contém os metadados de chaves Always Encrypted.

Quando você importa o BACPAC em um banco de dados, os dados criptografados dele são carregados no banco de dados e os metadados de chave Always Encrypted são recriados.

Se você tiver um aplicativo que está configurado para modificar ou recuperar os dados criptografados armazenados no banco de dados de origem (aquele exportado), não será necessário fazer nada especial para permitir que o aplicativo consulte os dados criptografados no banco de dados de destino, uma vez que as chaves nos dois bancos de dados são iguais.


### <a name="permissions"></a>Permissões

Você precisa de *ALTER ANY COLUMN MASTER KEY* e *ALTER ANY COLUMN ENCRYPTION KEY* no banco de dados de origem. Você precisa de *ALTER ANY COLUMN MASTER KEY*, *ALTER ANY COLUMN ENCRYPTION KEY*, *VIEW ANY COLUMN MASTER KEY DEFINITION*e *VIEW ANY COLUMN ENCRYPTION* no banco de dados de destino.

## <a name="migrating-databases-with-encrypted-columns-using-sql-server-import-and-export-wizard"></a>Migrando bancos de dados com colunas criptografadas usando o Assistente de Importação e Exportação do SQL Server

Em comparação com o uso de arquivos BACPAC, o [Assistente de Importação e Exportação do SQL Server](~/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md) proporciona mais controle sobre como os dados armazenados nas colunas criptografadas são manipulados durante a migração de dados.

- Se sua fonte de dados for um banco de dados usando o Always Encrypted, você poderá configurar a conexão da fonte de dados para que os dados armazenados nas colunas criptografadas sejam descriptografadas durante a operação de exportação ou permaneçam criptografadas.
- Se o destino de dados for um banco de dados usando o Always Encrypted, você poderá configurar sua conexão de destino de dados para que os dados visando colunas criptografadas sejam criptografados.

Para habilitar a descriptografia (para a fonte de dados) ou criptografia (para o destino de dados), você precisa configurar a conexão de origem/destino de dados para usar o [Provedor de dados .NET Framework para SqlServer](https://msdn.microsoft.com/library/system.data.sqlclient.aspx) e definir as palavras-chave da cadeia de conexão Column Encryption Setting como *Enabled*.

A tabela a seguir lista os cenários de migração possíveis e como eles se relacionam com o Always Encrypted juntamente com a configuração da fonte de dados e do destino de dados para cada conexão.

| Cenário|Configuração da conexão da fonte| Configuração da conexão do destino
|:---|:---|:---
|Criptografar dados na migração (os dados são armazenados em texto não criptografado na fonte de dados e são migrados para colunas criptografadas no destino de dados).| Provedor de dados/driver: *qualquer um*<br><br>Column Encryption Setting = Disabled<br><br>(se o Provedor de dados .NET Framework para SqlServer e o .NET Framework 4.6 ou posterior forem usados.) | Provedor de dados/driver: *Provedor de dados .NET Framework para SqlServer* (.NET Framework 4.6 ou posterior obrigatório)<br><br>Column Encryption Setting = Enabled
| Descriptografar os dados na migração (os dados são armazenados em colunas criptografadas na fonte de dados e são migrados em texto não criptografado para o destino de dados. Se o destino de dados for um banco de dados, as colunas de destino não serão criptografadas).<br><br>**Observação:** as tabelas de destino com colunas criptografadas devem existir antes da migração.|Provedor de dados/driver: *Provedor de dados .NET Framework para SqlServer* (.NET Framework 4.6 ou posterior obrigatório)<br><br>Column Encryption Setting=Enabled|Provedor de dados/driver: *qualquer um*<br><br>Column Encryption Setting = Disabled<br><br>(se o Provedor de dados .NET Framework para SqlServer e o .NET Framework 4.6 ou posterior forem usados.)
|Criptografar novamente os dados na migração (os dados são armazenados em colunas criptografadas na fonte de dados e são migrados em texto não criptografado para o destino de dados para as colunas que usam tipos de criptografia diferentes das chaves de criptografia da coluna).<br><br>**Observação:** as tabelas de destino com colunas criptografadas devem existir antes da migração.| Provedor de dados/driver: *Provedor de dados .NET Framework para SqlServer* (.NET Framework 4.6 ou posterior obrigatório)<br><br>Column Encryption Setting=Enabled|Provedor de dados/driver: *Provedor de dados .NET Framework para SqlServer* (.NET Framework 4.6 ou posterior obrigatório)<br><br>Column Encryption Setting=Enabled
|Mover os dados criptografados sem descriptografá-los.<br><br>**Observação:** as tabelas de destino com colunas criptografadas devem existir antes da migração.| Provedor de dados/driver: *qualquer um*<br>Column Encryption Setting = Disabled<br><br>(se o Provedor de dados .NET Framework para SqlServer e o .NET Framework 4.6 ou posterior forem usados.)| Provedor de dados/driver: *qualquer um*<br>Column Encryption Setting = Disabled<br><br>(se o Provedor de dados .NET Framework para SqlServer e o .NET Framework 4.6 ou posterior forem usados.)<br><br>O usuário deve ter ALLOW_ENCRYPTED_VALUE_MODIFICATIONS definido como ON.<br><br>Para obter detalhes, consulte [Migrar dados confidenciais protegidos pelo Always Encrypted](../../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md).


### <a name="permissions"></a>Permissões

Para **criptografar** ou **descriptografar** os dados armazenados na fonte de dados, você precisará das permissões *VIEW ANY COLUMN MASTER KEY DEFINITION* e *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* no banco de dados de origem.

Você também precisa acessar as chaves mestras de coluna, configuradas para as colunas, armazenando os dados que estão sendo criptografados ou descriptografados:
- **Repositório de Certificados – Computador local** : você deve ter acesso de leitura para o certificado que é usado como chave mestra da coluna ou ser o administrador do computador.
- **Cofre de Chaves do Azure** : você precisa das permissões get, unwrapKey, wrapKey, sign e verify no cofre que contém a chave mestra da coluna.
- **Provedor do Repositório de Chaves (CNG)** : a permissão e as credenciais necessárias que podem ser solicitadas ao usar um repositório de chaves ou uma chave, dependendo do repositório e da configuração do KSP.
- **Provedor de Serviços de Criptografia (CAPI)** : a permissão e as credenciais necessárias que podem ser solicitadas ao usar um repositório de chaves ou uma chave, dependendo do repositório e da configuração do CSP.
Para obter mais informações, consulte [Create and Store Column Master Keys (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)Criar e armazenar chaves mestras de coluna (Always Encrypted).

## <a name="see-also"></a>Consulte também
- [Always Encrypted (mecanismo de banco de dados)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Assistente do Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-wizard.md)
- [Visão geral do gerenciamento de chaves do Always Encrypted](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [Criar e armazenar chaves mestras de coluna (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)
- [Always Encrypted (desenvolvimento de cliente)](../../../relational-databases/security/encryption/always-encrypted-client-development.md)
- [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)
- [DROP COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/drop-column-master-key-transact-sql.md)
- [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md)
- [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md)
- [DROP COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/drop-column-encryption-key-transact-sql.md) 
- [sys.column_master_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
- [sys.column_encryption_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)
- [Configurar Always Encrypted usando o PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)













