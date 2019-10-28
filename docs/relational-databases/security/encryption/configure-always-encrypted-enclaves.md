---
title: Configurar o Always Encrypted com enclaves seguros | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 27f78de54735559365f771aaee3669b8f08856c7
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72902995"
---
# <a name="configure-always-encrypted-with-secure-enclaves"></a>Configurar o Always Encrypted com enclaves seguros

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O [Always Encrypted com enclaves seguros](always-encrypted-enclaves.md) estende o recurso [Always Encrypted](always-encrypted-database-engine.md) existente para habilitar funcionalidades mais avançadas em dados confidenciais mantendo a confidencialidade desses dados.

Para configurar o Always Encrypted com enclaves seguros, use o seguinte fluxo de trabalho:

1. Configurar o atestado do HGS (Serviço Guardião de Host).
2. Instale o [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] no computador com SQL Server.
3. Instalar as ferramentas no computador cliente/de desenvolvimento.
4. Configurar o tipo de enclave em sua instância do SQL Server.
5. Provisionar chaves habilitadas para enclave.
6. Criptografar colunas que contêm dados confidenciais.

> [!NOTE]
> Para obter um tutorial passo a passo sobre como configurar um ambiente de teste e experimentar a funcionalidade do Always Encrypted com enclaves seguras no SSMS, confira [Tutorial: Introdução ao Always Encrypted com enclaves seguros usando o SSMS](../tutorial-getting-started-with-always-encrypted-enclaves.md).

## <a name="configure-your-environment"></a>Configurar seu ambiente

Para usar enclaves seguros com o Always Encrypted, seu ambiente precisa do Windows Server 2019 Preview, do SSMS (SQL Server Management Studio) 18.0, do .NET Framework e de vários outros componentes. As seções a seguir fornecem detalhes e links para obter os componentes necessários.

### <a name="sql-server-computer-requirements"></a>Requisitos do computador com SQL Server

O computador que executa o SQL Server precisa do sistema operacional e da versão do SQL Server a seguir:

*SQL Server*:

- [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] ou posterior

*Windows*:

- Windows 10 Enterprise, versão 1809
- Windows Server DataCenter (Canal Semestral), versão 1809
- Windows Server 2019 DataCenter

> [!IMPORTANT]
> O computador com SQL Server deve ser configurado como um host protegido, atestado pelo HGS. O atestado do TPM é o método de atestado de enclave recomendado para ambientes de produção e requer que o SQL Server seja executado em um computador físico, não em uma máquina virtual. Máquinas virtuais são adequadas apenas para ambientes de pré-produção.

### <a name="hgs-computer-requirements"></a>Requisitos do computador de HGS

Apenas um computador de HGS é suficiente durante o teste e a criação de protótipos. Para produção, é recomendável usar um cluster de failover do Windows com três computadores.

O HGS (Serviço Guardião de Host) do Windows precisa ser instalado em computadores de HGS separados, e não no mesmo computador que o SQL Server. Para obter detalhes sobre os requisitos e a configuração do computador de HGS, confira [Configurando o Serviço Guardião de Host para Always Encrypted no SQL Server](https://docs.microsoft.com/windows-server/security/set-up-hgs-for-always-encrypted-in-sql-server).


### <a name="determine-your-attestation-service-url"></a>Determinar a URL do serviço de atestado

Para determinar a URL do serviço de atestado, você precisa configurar suas ferramentas e aplicativos:

1. Entre como administrador no computador com SQL Server.
2. Execute o PowerShell como administrador.
3. Execute [Get-HGSClientConfiguration](https://docs.microsoft.com/powershell/module/hgsclient/get-hgsclientconfiguration).
4. Tome nota e salve a propriedade AttestationServerURL. Ela deve ser semelhante a: `https://x.x.x.x/Attestation`.

### <a name="install-tools"></a>Instalar ferramentas

Instale as ferramentas a seguir no computador cliente/de desenvolvimento:

1. [.NET Framework 4.7.2](https://www.microsoft.com/net/download/dotnet-framework-runtime).
2. [SSMS 18.0 ou posterior](../../../ssms/download-sql-server-management-studio-ssms.md).
3. [Módulo do SQL Server PowerShell](../../../powershell/download-sql-server-ps-module.md) versão 21.1 ou posterior.
4. [Visual Studio (2017 ou posterior recomendado)](https://visualstudio.microsoft.com/downloads/).
5. [Pacote do Desenvolvedor para .NET Framework 4.7.2](https://www.microsoft.com/net/download/visual-studio-sdks).
6. [Pacote NuGet Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider](https://www.nuget.org/packages/Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider), versão 2.2.0 ou posterior.
7. [Pacote NuGet Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders](https://www.nuget.org/packages?q=Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders).

Use os pacotes do NuGet em projetos do Visual Studio para desenvolver aplicativos usando o Always Encrypted com enclaves seguros. O primeiro pacote é necessário somente se você armazena chaves mestras de coluna no Azure Key Vault. Para obter detalhes, consulte [Desenvolver aplicativos](#develop-applications-issuing-rich-queries-in-visual-studio).

### <a name="configure-a-secure-enclave"></a>Configurar um enclave seguro

Abra o computador cliente/de desenvolvimento:

1. Abra o SSMS e conecte-se à sua instância do SQL Server como um administrador do AD (Active Directory).
2. Para confirmar se o Always Encrypted com enclaves seguros tem suporte em sua instância, execute a seguinte consulta:

   ```sql
   SELECT [name], [value], [value_in_use] FROM sys.configurations
   WHERE [name] = 'column encryption enclave type';
   ```

    A consulta deve retornar uma linha semelhante à seguinte:  

    | NAME                           | value | value_in_use |
    | ------------------------------ | ----- | -------------|
    | column encryption enclave type | 0     | 0            |

3. Configure o tipo do enclave seguro como enclaves de VBS.

   ```sql
   EXEC sys.sp_configure 'column encryption enclave type', 1;
   RECONFIGURE;
   ```

4. Reinicie a instância do SQL Server para que as alterações anteriores entrem em vigor. Para reiniciar a instância no SSMS, clique nela com o botão direito do mouse no Pesquisador de Objetos e selecionando Reiniciar. Após a instância ser reiniciada, conecte-se a ela novamente.

5. Confirme que o enclave seguro está carregado executando a consulta a seguir:

   ```sql
   SELECT [name], [value], [value_in_use] FROM sys.configurations
   WHERE [name] = 'column encryption enclave type';
   ```   

    A consulta deve retornar uma linha semelhante à seguinte:  

    | NAME                           | value | value_in_use |
    | ------------------------------ | ----- | -------------- |
    | column encryption enclave type | 1     | 1              |

6. Para habilitar cálculos avançados em colunas criptografadas, execute a consulta a seguir:

   ```sql
   DBCC traceon(127,-1);
   ```

    > [!NOTE]
    > Cálculos avançados são desabilitados por padrão no [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)]. Eles precisam ser habilitados usando a instrução acima após cada reinicialização de sua instância do SQL Server.

## <a name="provision-enclave-enabled-keys"></a>Provisionar chaves habilitadas para enclave

A introdução de chaves habilitadas para enclave não altera fundamentalmente os [fluxos de trabalho de provisionamento e de gerenciamento de chaves para o Always Encrypted](overview-of-key-management-for-always-encrypted.md). A única alteração está no fluxo de trabalho de provisionamento da chave mestra de coluna. Agora você pode marcar a chave como habilitada para enclave por padrão, mas as chaves mestras da coluna não estão habilitadas para enclave. Quando você configura a nova chave mestra da coluna como habilitada para enclave (com o SSMS ou o PowerShell), ocorre o seguinte:

- A propriedade `ENCLAVE_COMPUTATIONS` nos metadados da chave mestra da coluna no banco de dados é definida.
- Os valores de propriedade da chave mestra da coluna, incluindo a configuração `ENCLAVE_COMPUTATIONS`, são assinados digitalmente. A ferramenta adiciona a assinatura, que é produzida usando a chave mestra da coluna real, aos metadados. A assinatura evita a violação mal-intencionada da configuração `ENCLAVE_COMPUTATIONS`. Os drivers do cliente SQL verificam as assinaturas antes de permitir o uso do enclave. Isso proporciona aos administradores da segurança o controle de quais dados da coluna podem ser calculados dentro de enclave.

A propriedade `ENCLAVE_COMPUTATIONS` de uma chave mestra de coluna é imutável. Não é possível alterá-la depois que a chave é provisionada. No entanto, é possível substituir a chave mestra da coluna por uma nova chave para a propriedade `ENCLAVE_COMPUTATIONS` com um valor diferente da chave original. Para substituir a chave mestra da coluna, [gire a chave mestra da coluna](#make-columns-enclave-enabled-by-rotating-their-column-master-key). Para saber mais sobre a propriedade `ENCLAVE_COMPUTATIONS`, confira [CRIAR A CHAVE MESTRA DA COLUNA](../../../t-sql/statements/create-column-master-key-transact-sql.md).

Para provisionar uma chave de criptografia de coluna habilitada para enclave, você precisará garantir que a chave mestra da coluna que criptografa a chave de criptografia da coluna esteja habilitada para enclave.

Atualmente, as seguintes limitações se aplicam às chaves de enclave de provisionamento:

- Chaves mestras de coluna habilitadas para enclave precisam ser armazenadas no [Repositório de Certificados do Windows](/windows/desktop/seccrypto/managing-certificates-with-certificate-stores) ou no [Azure Key Vault](/azure/key-vault/key-vault-whatis/). Atualmente, não há suporte para armazenar chaves mestras de coluna habilitadas para enclave em outros tipos de repositórios de chaves, como módulos de segurança de hardware ou repositórios de chave personalizados.

### <a name="provision-enclave-enabled-keys-using-sql-server-management-studio-ssms"></a>Provisionar chaves habilitadas para enclave usando o SSMS (SQL Server Management Studio)

As etapas a seguir criam chaves habilitadas para enclave (é necessário o SSMS 18.0 ou posterior):

1. Conecte-se a seu banco de dados usando o SSMS.
2. No **Pesquisador de Objetos**, expanda o banco de dados e navegue até **Segurança** > **Chaves Always Encrypted**.
3. Provisione uma nova chave mestra da coluna habilitada para enclave:

    1. Clique com o botão direito do mouse em **Chaves Always Encrypted** e selecione **Nova chave mestra da coluna...** .
    2. Selecione o nome de sua chave mestra da coluna.
    3. Certifique-se de selecionar **Repositório de certificados do Windows (usuário atual ou computador local)** ou **Azure Key Vault**.
    4. Selecione **Permitir computações de enclave**.
    5. Se tiver selecionado o Azure Key Vault, entre no Azure e selecione seu cofre de chaves. Para obter mais informações sobre como criar um cofre de chaves para Always Encrypted, veja [Gerenciar cofres de chaves do portal do Azure](https://blogs.technet.microsoft.com/kv/2016/09/12/manage-your-key-vaults-from-new-azure-portal/).
    6. Selecione a chave se ela já existir ou siga as instruções no formulário para criar uma nova chave.
    7. Clique em **OK**.

        ![Permitir computações de enclave](./media/always-encrypted-enclaves/allow-enclave-computations.png)

4. Crie uma nova chave de criptografia de coluna habilitada para enclave:

    1. Clique com o botão direito do mouse em **Chaves Always Encrypted** e selecione **Nova chave de criptografia da coluna**.
    2. Insira um nome para a nova chave de criptografia da coluna.
    3. No menu suspenso **Chave mestra da coluna**, selecione a chave mestra da coluna criada nas etapas anteriores.
    4. Clique em **OK**.

### <a name="provision-enclave-enabled-keys-using-powershell"></a>Provisionar chaves habilitadas para enclave usando o PowerShell

As seções a seguir fornecem exemplos de scripts do PowerShell para o provisionamento de chaves habilitadas para enclave. As etapas que são específicas (novas) do Always Encrypted com enclaves seguros estão realçadas. Para obter mais informações (não específicas do Always Encrypted com enclaves seguros) sobre o provisionamento de chaves usando o PowerShell, consulte [Configurar chaves do Always Encrypted usando o PowerShell](configure-always-encrypted-keys-using-powershell.md).

#### <a name="provisioning-enclave-enabled-keys---windows-certificate-store"></a>Provisionamento de chaves habilitadas para enclave – Repositório de Certificados do Windows

No computador do cliente/de desenvolvimento, abra o ISE do Windows PowerShell e execute o seguinte script.

É importante observar o uso do parâmetro `-AllowEnclaveComputations` no cmdlet [**New-SqlCertificateStoreColumnMasterKeySettings**](https://docs.microsoft.com/powershell/module/sqlserver/new-sqlcertificatestorecolumnmasterkeysettings).

```powershell
# Create a column master key in Windows Certificate Store.
$cert = New-SelfSignedCertificate -Subject "\<Subject Name\>" -CertStoreLocation Cert:CurrentUser\\My -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage DataEncipherment -KeySpec KeyExchange

# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database. Provide the server/db name. Modify the connection string, if needed.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Data Source = " + $serverName + "; Initial Catalog = " + $databaseName + "; Integrated Security = true"
$database = Get-SqlDatabase -ConnectionString $connStr

# Create a SqlColumnMasterKeySettings object for your column master key
# using the -AllowEnclaveComputations parameter.
$cmkSettings = New-SqlCertificateStoreColumnMasterKeySettings -CertificateStoreLocation "CurrentUser" -Thumbprint $cert.Thumbprint -AllowEnclaveComputations

# Create column master key metadata in the database.
$cmkName = "<column master key name in the database>"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database.
$cekName = "<column encryption key name in the database>"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName
```

#### <a name="provisioning-enclave-enabled-keys---azure-key-vault"></a>Provisionamento de chaves habilitadas para enclave – Azure Key Vault

No computador do cliente/de desenvolvimento, abra o ISE do Windows PowerShell e execute o seguinte script.

**Etapa 1: Provisionar uma chave mestra da coluna no Azure Key Vault**

Isso também pode ser feito usando o portal do Azure. Para obter detalhes, consulte [Gerenciar os cofres de chaves do portal do Azure](https://blogs.technet.microsoft.com/kv/2016/09/12/manage-your-key-vaults-from-new-azure-portal/).


```powershell
Import-Module Az
Connect-AzAccount

# User values
$SubscriptionId = "<Azure SubscriptionId>"
$resourceGroup = "<resource group name>"
$azureLocation = "<datacenter location>"
$akvName = "<key vault name>"
$akvKeyName = "<key name>"

# Set the context to the specified subscription.
$azureCtx = Set-AzContext -SubscriptionId $SubscriptionId

# Create a new resource group - skip, if your desired group already exists.
New-AzResourceGroup -Name $resourceGroup -Location $azureLocation

# Create a new key vault - skip if your vault already exists.
New-AzKeyVault -VaultName $akvName -ResourceGroupName $resourceGroup -Location $azureLocation

# Grant yourself permissions needed to create and use the column master key.
Set-AzKeyVaultAccessPolicy -VaultName $akvName -ResourceGroupName $resourceGroup -PermissionsToKeys get, create, list, update, wrapKey,unwrapKey, sign, verify -UserPrincipalName $azureCtx.Account

# Create a column master key in Azure Key Vault.
$akvKey = Add-AzureKeyVaultKey -VaultName $akvName -Name $akvKeyName -Destination "Software"
```

**Etapa 2: Criar metadados da chave mestra da coluna no banco de dados, criar uma chave de criptografia da coluna e criar metadados da chave de criptografia da coluna no banco de dados**


```powershell
# Import the SqlServer module.
Import-Module "SqlServer" -Version

# Connect to your database. Provide the server and db name. If needed, modify the connection string.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Data Source = " + $serverName + "; Initial Catalog = " + $databaseName + "; Integrated Security = true"
$database = Get-SqlDatabase -ConnectionString $connStr

# Authenticate to Azure before calling New-SqlAzureKeyVaultColumnMasterKeySettings,
# because -AllowEnclaveComputations causes a call to Azure Key Vault
# to generate the signature of the column master key.
Add-SqlAzureAuthenticationContext -Interactive

# Create a SqlColumnMasterKeySettings object for your column master key.
$cmkSettings = New-SqlAzureKeyVaultColumnMasterKeySettings -KeyURL $akvKey.ID -AllowEnclaveComputations

# Create column master key metadata in the database.
$cmkName = "<column master key name in the database>"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database.
$cekName = "<column encryption key name in the database>"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName
```

## <a name="identify-enclave-enabled-keys-and-columns"></a>Identificar colunas e chaves habilitadas para enclave

Para listar as chaves mestras de coluna configuradas em seu banco de dados, confira a exibição de catálogo [column_master_keys](../../system-catalog-views/sys-column-master-keys-transact-sql.md) (por exemplo, no SSMS). A nova coluna **allow_enclave_computations** indica se a chave mestra da coluna está habilitada para enclave.

```sql
SELECT name, allow_enclave_computations
FROM sys.column_master_keys;
```

Quando uma chave de criptografia de coluna é criptografada com chaves de criptografia de coluna habilitada para enclave, ela está habilitada para enclave. Para retornar chaves de criptografia de coluna habilitada para enclave, a consulta a seguir une [sys.column_master_keys](../../system-catalog-views/sys-column-master-keys-transact-sql.md), [sys.column_encryption_key_values](../../system-catalog-views/sys-column-encryption-key-values-transact-sql.md) e [sys.column_encryption_keys](../../system-catalog-views/sys-column-encryption-keys-transact-sql.md).

```sql
SELECT cek.name AS [cek_name]
, cmk.name AS [cmk_name]
, cmk.allow_enclave_computations
FROM sys.column_master_keys cmk
JOIN sys.column_encryption_key_values cekv
   ON cmk.column_master_key_id = cekv.column_master_key_id
JOIN sys.column_encryption_keys cek
   ON cekv.column_encryption_key_id = cek.column_encryption_key_id;
```

Colunas criptografadas com chaves habilitadas para enclave estão habilitadas para enclave. Para determinar quais colunas estão habilitadas para enclave, use a consulta a seguir:

```sql
SELECT c.name AS column_name
, cek.name AS cek_name
, cmk.name AS [cmk_name]
, cmk.allow_enclave_computations
from sys.columns c
JOIN sys.column_encryption_keys cek 
ON c.column_encryption_key_id = cek.column_encryption_key_id 
JOIN sys.column_encryption_key_values cekv 
ON cekv.column_encryption_key_id = cek.column_encryption_key_id 
JOIN sys.column_master_keys cmk 
ON cmk.column_master_key_id = cekv.column_master_key_id;
```

## <a name="manage-collations"></a>Gerenciar ordenações

Always Encrypted restringe ordenações. Não são permitidas ordenações não BIN2 em colunas de cadeia de caracteres criptografadas usando a criptografia determinística. Essa restrição também se aplica a colunas de cadeia de caracteres habilitadas para enclave.

O uso de ordenações não BIN2 é permitido para colunas de cadeia de caracteres criptografadas usando criptografia aleatória e chaves de criptografia de coluna habilitadas para enclave. No entanto, a única nova funcionalidade habilitada para essas colunas é a criptografia no local. Para habilitar cálculos avançados (correspondência de padrões, operações de comparação), a coluna criptografada exige a ordenação BIN2.

A tabela a seguir resume a funcionalidade das colunas de cadeia de caracteres habilitadas para enclave dependendo do tipo de criptografia e da ordem de classificação da ordenação.

| **Ordem de classificação da ordenação** | **Criptografia determinística** | **Criptografia aleatória**                 |
| ------------------------ | ---------------------------- | ----------------------------------------- |
| **Não BIN2**             | Sem suporte                | Criptografia no local                       |
| **BIN2**                 | Comparação de igualdade          | Criptografia no local e cálculos avançados |

### <a name="determining-and-changing-collations"></a>Determinando e alterando ordenações

No SQL Server, ordenações podem ser definidas no nível do servidor, do banco de dados ou da coluna. Para obter instruções gerais sobre como determinar a ordenação atual e alterar uma ordenação no nível de servidor, do banco de dados ou da coluna, consulte [Suporte a ordenações e a Unicode](../../collations/collation-and-unicode-support.md).

### <a name="special-considerations-for-non-unicode-string-columns"></a>Considerações especiais sobre colunas de cadeia de caracteres não UNICODE

A seguinte restrição adicional, imposta por uma limitação em drivers cliente SQL (não relacionada ao Always Encrypted), se aplica a colunas de cadeia de caracteres não UNICODE (ASCII). Se você substituir a ordenação do banco de dados por uma coluna de cadeia de caracteres não UNICODE (char, varchar), é necessário garantir que a ordenação da coluna use a mesma página de código que a ordenação de banco de dados.
Para listar todas as ordenações com seus identificadores de página de código, use a seguinte consulta:

```sql
SELECT [Name]
   , [Description]
   , [CodePage] = COLLATIONPROPERTY([Name], 'CodePage')
FROM ::fn_helpcollations();
```

Por exemplo, `Chinese_Traditional_Stroke_Order_100_CI_AI_WS` e `Chinese_Traditional_Stroke_Order_100_BIN2` têm a mesma página de código (950), mas `Chinese_Traditional_Stroke_Order_100_CI_AI_WS` e `Latin1_General_100_BIN2` têm diferentes páginas de código (950 e 1252, respectivamente). A restrição acima não se aplica a colunas de cadeia de caracteres UNICODE (`nchar`, `nvarchar`). Considere definir um tipo de dados UNICODE para as novas colunas criptografadas que você está criando ou alterar para um tipo UNICODE antes de criptografar uma coluna existente.

## <a name="create-a-new-table-with-enclave-enabled-columns"></a>Criar uma nova tabela com colunas habilitadas para enclave

Você pode criar uma nova tabela com colunas criptografadas usando a instrução [CREATE TABLE (Transact-SQL)](../../../t-sql/statements/create-table-transact-sql.md). O Always Encrypted com enclaves seguros não altera a sintaxe dessa instrução.

1. Usando o SSMS, conecte-se ao banco de dados e abra uma janela de consulta.

     > [!NOTE]
     > O Always Encrypted não precisa ser habilitado na cadeia de conexão para essa tarefa.

2. Na janela de consulta, emita uma instrução `CREATE TABLE` para criar sua nova tabela, especificando a cláusula `ENCRYPTED WITH` na [definição de coluna](../../../t-sql/statements/alter-table-column-definition-transact-sql.md) para cada coluna a criptografar. Para tornar uma coluna habilitada para enclave, certifique-se de especificar uma chave de criptografia de coluna habilitada para enclave. Talvez você também precise especificar uma ordenação BIN2 para colunas de cadeia de caracteres se a ordenação padrão do banco de dados não for uma ordenação BIN2. Consulte a seção Configuração de ordenação para obter detalhes.

### <a name="example-of-creating-a-new-table-with-enclave-enabled-columns"></a>Exemplo de criação de uma nova tabela com colunas habilitadas para enclave

A instrução abaixo cria uma nova tabela com duas colunas criptografadas, SSN e Salary. Supondo que CEK1 seja uma chave de criptografia de coluna habilitada para enclave, o Mecanismo do SQL Server dá suporte à criptografia no local e a cálculos avançados para ambas as colunas, pois as colunas usam criptografia aleatória. A instrução define a ordenação Latin1\_General\_BIN2 para a coluna UNICODE SSN, o que é necessário supondo que a ordenação de banco de dados padrão seja uma ordenação Latin1 não BIN2.

```sql
CREATE TABLE [dbo].[Employees]
(
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [SSN] [char](11) COLLATE Latin1_General_BIN2 ENCRYPTED WITH (
        COLUMN_ENCRYPTION_KEY = [CEK1],
        ENCRYPTION_TYPE = Randomized,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [Salary] [money] ENCRYPTED WITH (
        COLUMN_ENCRYPTION_KEY = [CEK1],
        ENCRYPTION_TYPE = Randomized,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
    CONSTRAINT [PK_dbo.Employees] PRIMARY KEY CLUSTERED (
[EmployeeID] ASC
)
) ON [PRIMARY];
GO
```

## <a name="add-a-new-enclave-enabled-column-to-an-existing-table"></a>Adicionar uma nova coluna habilitada para enclave a uma tabela existente

Você pode adicionar uma nova coluna criptografada a uma tabela existente usando a instrução [ALTER TABLE (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md) / ADD. O Always Encrypted com enclaves seguros não altera a sintaxe dessa instrução.

1. Usando o SSMS, conecte-se ao banco de dados e abra uma janela de consulta.

   O Always Encrypted não precisa ser habilitado na cadeia de conexão para essa tarefa.

2. Na janela de consulta, emita a instrução ALTER TABLE com a cláusula ADD, especificando a cláusula ENCRYPTED WITH na [definição da coluna](../../../t-sql/statements/alter-table-column-definition-transact-sql.md) e usando uma chave de criptografia de coluna habilitada para enclave. Talvez você também precise especificar uma ordenação BIN2 se a nova coluna for uma coluna de cadeia de caracteres e se a ordenação padrão do banco de dados não for uma ordenação BIN2. Consulte a seção Configuração de ordenação para obter detalhes.

### <a name="example-of-adding-a-new-enclave-enabled-column-to-an-existing-table"></a>Exemplo de adição de uma nova coluna habilitada para enclave a uma tabela existente

Supondo que CEK1 seja uma chave de criptografia de coluna habilitada para enclave, a instrução abaixo adiciona uma nova coluna criptografada, chamada BirthDate, que dá suporte à criptografia no local e a consultas avançadas (pois a coluna usa criptografia aleatória).

```sql
ALTER TABLE [dbo].[Employees]
ADD [BirthDate] [Date] ENCRYPTED WITH (
COLUMN_ENCRYPTION_KEY = [CEK1],
ENCRYPTION_TYPE = Randomized,
ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NULL;
```


## <a name="prepare-an-ssms-query-window-with-always-encrypted-enabled"></a>Preparar uma janela de consulta do SSMS com o Always Encrypted habilitado

Para adicionar os parâmetros de conexão necessários para habilitar cálculos de enclave:

1. Abra o SSMS.
2. Depois de especificar o nome do servidor e um nome do banco de dados na caixa de diálogo Conectar ao Servidor, clique em **Opções**. Navegue até a guia **Always Encrypted**, selecione **Habilitar o Always Encrypted** e especifique a URL do atestado do enclave.
    
    ![Configuração da criptografia de coluna](./media/always-encrypted-enclaves/column-encryption-setting.png)

3. Clique em Conectar.
4. Abra uma nova janela de consulta.

Como alternativa, se já tiver uma janela de consulta aberta, veja como você pode atualizar sua conexão de banco de dados para habilitar o Always Encrypted:

1. Clique com o botão direito do mouse em qualquer lugar em uma janela de consulta existente.
2. Selecione Conexão \> Alterar Conexão.
3. Clique em **Opções**. Navegue até a guia **Always Encrypted**, selecione **Habilitar o Always Encrypted** e especifique a URL do atestado do enclave.
4. Clique em Conectar.

## <a name="work-with-encrypted-columns"></a>Trabalhar com colunas criptografadas

### <a name="encrypt-an-existing-plaintext-column-in-place"></a>Criptografar uma coluna de texto sem formatação existente no local

Você pode criptografar uma coluna de texto sem formatação existente no local usando a instrução [ALTER TABLE (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md) / ALTER COLUMN, desde que use uma chave de criptografia de coluna habilitada para enclave.

Para criptografar uma coluna usando uma chave que não está habilitada para enclave, você precisará usar ferramentas do lado do cliente, como o assistente do Always Encrypted no SSMS ou o cmdlet Set-SqlColumnEncryption no módulo do SqlServer do PowerShell. Para obter detalhes, confira:

- [Assistente do Always Encrypted](always-encrypted-wizard.md)
- [Configurar a criptografia de coluna usando o PowerShell](configure-column-encryption-using-powershell.md)


#### <a name="prerequisites-for-encrypting-an-existing-plaintext-column-in-place"></a>Pré-requisitos para criptografar uma coluna de texto sem formatação existente no local

- A coluna existente não está criptografada.
- Você provisionou chaves habilitadas para enclave.
- Você tem acesso à chave mestra da coluna.

#### <a name="steps-for-encrypting-existing-plaintext-column-in-place"></a>Etapas para criptografar a coluna de texto sem formatação existente no local

1. Prepare uma janela de consulta do SSMS com Always Encrypted e cálculos de enclave habilitados na conexão de banco de dados. Para obter detalhes, consulte [Preparar uma janela de consulta do SSMS com o Always Encrypted habilitado](#prepare-an-ssms-query-window-with-always-encrypted-enabled).
2. Na janela de consulta, emita a instrução ALTER TABLE com a cláusula ALTER COLUMN, especificando uma chave de criptografia habilitada para enclave na cláusula ENCRYPTED WITH. Se a coluna for uma coluna de cadeia de caracteres (por exemplo, char, varchar, nchar, nvarchar), você também precisará alterar a ordenação para uma ordenação BIN2. Consulte a seção Configuração de ordenação para obter detalhes.
    
    > [!NOTE]
    > Se a chave mestra de coluna estiver armazenada no Azure Key Vault, talvez seja solicitado que você entre no Azure.

3. Limpe o cache do plano para todos os lotes e procedimentos armazenados que acessam a tabela, para atualizar as informações de criptografia de parâmetros. 
 
    ```sql
    ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
    ```
    > [!NOTE]
    > Se você não remover o plano da consulta afetada do cache, a primeira execução da consulta após a criptografia poderá falhar.

    > [!NOTE]
    > Use `ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE` ou `DBCC FREEPROCCACHE` para limpar o cache de planos com cuidado, pois isso pode resultar na degradação temporária do desempenho de consulta. Para minimizar o impacto negativo da limpeza do cache, você pode remover seletivamente somente os planos das consultas afetadas.

4.  Chame [sp_refresh_parameter_encryption](../../system-stored-procedures/sp-refresh-parameter-encryption-transact-sql.md) para atualizar os metadados dos parâmetros de cada módulo (procedimento armazenado, função, exibição, gatilho) que persistiu em [sys.parameters](../..//system-catalog-views/sys-parameters-transact-sql.md) e possa ter sido invalidado criptografando as colunas.

#### <a name="example-of-encrypting-existing-plaintext-column-in-place"></a>Exemplo de criptografia de uma coluna de texto sem formatação existente no local

O exemplo abaixo pressupõe que:

- CEK1 seja uma chave de criptografia de coluna habilitada para enclave.

- a coluna de SSN seja de texto sem formatação e atualmente esteja usando uma ordenação Latin1, não BIN2 (por exemplo, Latin1\_General\_CI\_AI\_KS\_WS).

A instrução criptografa a coluna de SSN usando criptografia aleatória e a chave de criptografia de coluna habilitada para enclave. Ela também substitui a ordenação do banco de dados padrão pela ordenação BIN2 correspondente (na mesma página de código).

A operação é executada online (ONLINE = ON). Observe também a chamada para **ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE**, que recria os planos das consultas afetadas pela alteração do esquema de tabela.

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char] COLLATE Latin1_General_BIN2
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
WITH
(ONLINE = ON);
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

### <a name="make-an-existing-encrypted-column-enclave-enabled"></a>Tornar uma coluna criptografada existente habilitada para enclave

Há várias maneiras de habilitar a funcionalidade de enclave para uma coluna existente que não está habilitada para enclave. O método escolhido depende de vários fatores:

- **Escopo/granularidade:** você deseja habilitar a funcionalidade de enclave para um subconjunto de colunas ou para todas as colunas protegidas por uma chave mestra de coluna especificada?
- **Tamanho dos dados:** qual é o tamanho das tabelas que contêm as colunas que você deseja habilitar para enclave?
- Você também deseja alterar o tipo de criptografia de suas colunas? Lembre-se de que somente a criptografia aleatória dá suporte a cálculos avançados (correspondência de padrões, operadores de comparação). Se a coluna for criptografada usando criptografia determinística, você também precisará criptografá-la novamente com criptografia aleatória para desbloquear a funcionalidade completa do enclave.

Estas são as três abordagens para habilitar enclaves para colunas existentes:

#### <a name="option-1-rotate-the-column-master-key-to-replace-it-with-an-enclave-enabled-column-master-key"></a>Opção 1: gire a chave mestra da coluna para substituí-la por uma chave mestra da coluna habilitada para enclave.
  
- Prós:
  - não envolve criptografar novamente os dados, portanto, normalmente é a abordagem mais rápida. é uma abordagem recomendada para colunas que contêm grandes quantidades de dados, desde que todas as colunas para as quais você precisa habilitar cálculos avançados já usem criptografia determinística e, portanto, não precisarão ser criptografadas novamente.
  - pode habilitar a funcionalidade de enclave para várias colunas em grande escala, pois torna todas as chaves de criptografia de coluna e todas as colunas criptografadas associadas à chave mestra da coluna original habilitadas para enclave.
  
- Contras:
  - não dá suporte para alterar o tipo de criptografia de determinística para aleatória, portanto, embora desbloqueie a criptografia no local para colunas criptografadas de forma determinística, não permite cálculos avançados.
  - não permite que você converta seletivamente algumas das colunas associadas a uma chave mestra de coluna especificada.
  - Introduz sobrecarga de gerenciamento de chaves – você precisará criar uma nova chave mestra da coluna e torná-la disponível para aplicativos que consultam as colunas afetadas.  

#### <a name="option-2-this-approach-involves-two-steps-1-rotating-the-column-master-key-as-in-option-1-and-2-re-encrypting-a-subset-of-deterministically-encrypted-columns-using-randomized-encryption-to-enable-rich-computations-for-those-columns"></a>Opção 2: Essa abordagem envolve duas etapas: 1) girar a chave mestra da coluna (como na Opção 1) e 2) criptografar novamente um subconjunto de colunas criptografadas de forma determinística usando criptografia aleatória, a fim de habilitar cálculos avançados para essas colunas.
  
- Prós:
  - criptografa novamente os dados no local e, portanto, é um método recomendado para habilitar consultas avançadas para colunas criptografadas de forma determinística que contêm grandes quantidades de dados. A Etapa 1 desbloqueia a criptografia no local para as colunas que usam a criptografia determinística e, portanto, a etapa 2 pode ser executada no local.
  - pode habilitar a funcionalidade de enclave para várias colunas em grande escala.
  
- Contras:
  - não permite que você converta seletivamente algumas das colunas associadas a uma chave mestra de coluna especificada.
  - Ele introduz sobrecarga de gerenciamento de chaves – você precisará criar uma nova chave mestra da coluna e torná-la disponível para aplicativos que consultam as colunas afetadas.

#### <a name="option-3-re-encrypting-selected-columns-with-a-new-enclave-enabled-column-encryption-key-and-randomized-encryption-if-needed-on-the-client-side"></a>Opção 3: criptografar novamente colunas selecionadas com uma nova chave de criptografia de coluna habilitada para enclave e com criptografia aleatória (se necessário) no lado do cliente.
  
- Os prós desse método:
  - permite que você habilite de forma seletiva a funcionalidade de enclave para uma coluna ou um pequeno subconjunto de colunas.
  - pode permitir cálculos avançados para uma coluna criptografada de forma determinística em uma única etapa.
  - não exige a criação de uma nova chave mestra de coluna, de modo que tem um menor impacto sobre os aplicativos.
  
- Contras:
  - todo o conteúdo da tabela que contém a coluna deve ser movido para fora do banco de dados para ser criptografado novamente e, portanto, é recomendável somente para tabelas pequenas.

Para obter mais informações, consulte as seguintes seções:
  - [Habilitando colunas para enclave girando a chave mestra da coluna](#make-columns-enclave-enabled-by-rotating-their-column-master-key)
  - [Recriptografando colunas no local](#re-encrypt-columns-in-place)
  - [Recriptografando colunas no lado do cliente](#re-encrypt-columns-on-the-client-side)

### <a name="make-columns-enclave-enabled-by-rotating-their-column-master-key"></a>Habilitar colunas para enclave girando a chave mestra da coluna

A rotação de uma chave mestra de coluna é o processo de substituição de uma chave mestra de coluna existente por uma nova chave mestra de coluna. Ele envolve criptografar novamente as chaves de criptografia de coluna, associadas à chave mestra de coluna antiga, usando a nova chave mestra de coluna. Esse fluxo de trabalho existe desde a versão inicial do Always Encrypted para dar suporte à substituição da chave mestra da coluna por motivos de segurança ou conformidade (caso a chave mestra da coluna existente seja comprometida).

O uso de enclaves pelo Always Encrypted dá uma nova finalidade ao fluxo de trabalho de rotação da chave mestra da coluna. Supondo que a chave mestra da coluna antiga não esteja habilitada para enclave e que a nova chave mestra da coluna esteja, o processo de rotação efetivamente habilita todas as chaves de criptografia de coluna associadas à chave mestra da coluna. A rotação de uma chave mestra da coluna não envolve criptografar os dados novamente e, portanto, é um processo recomendado para habilitar recursos de enclave para colunas existentes.

A rotação da chave mestra da coluna não altera o tipo de criptografia das colunas afetadas. Portanto, ela somente pode desbloquear a criptografia no local para colunas criptografadas de maneira determinística. Para desbloquear cálculos avançados para colunas usando a criptografia determinística, você precisará criptografá-las novamente (no local), depois de girar a chave mestra da coluna.

Talvez você também precise alterar a ordenação das colunas de cadeia de caracteres usando a criptografia aleatória para uma ordenação BIN2, a fim de desbloquear cálculos avançados. Consulte a seção Configuração de ordenação para obter detalhes.

O processo de girar a chave mestra da coluna é o mesmo, independentemente de a chave envolvida estar habilitada para enclave. Há detalhes de como girar a chave mestra da coluna nos seguintes artigos:

- [Girar uma chave mestra de coluna com o SSMS](configure-always-encrypted-using-sql-server-management-studio.md)
- [Girar uma chave mestra de coluna com o PowerShell](rotate-always-encrypted-keys-using-powershell.md)

Para sua conveniência, um exemplo de script do PowerShell para girar uma chave mestra de coluna é fornecido abaixo.

#### <a name="prerequisites-of-rotating-the-column-master-key-for-enclave-enabled-columns"></a>Pré-requisitos de girar a chave mestra de coluna para colunas habilitadas para enclave

- Você provisionou uma nova chave mestra da coluna habilitada para enclave.
- Você tem acesso à antiga e à nova chave mestra de coluna.
- Todas as colunas de cadeia de caracteres protegidas pela chave mestra de coluna antiga usam ordenações BIN2.

> [!NOTE]
> Como alternativa, você pode alterar a ordenação das colunas de cadeia de caracteres após girar a chave mestra de coluna.

#### <a name="steps-for-rotating-the-column-master-key-for-enclave-enabled-columns"></a>Etapas para girar a chave mestra de coluna para colunas habilitadas para enclave

Cole o seguinte script no ISE do Windows PowerShell, substituindo os \<espaços reservados\> por seus valores específicos:

```powershell
# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database. Modify server/db name or/and the connection string, if needed.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Data Source = " + $serverName + "; Initial Catalog = " +
$databaseName + "; Integrated Security = true"
$database = Get-SqlDatabase -ConnectionString $connStr

# Set the names of the old/current column master key and the new/target enclave-enabled column master key. (Change the names, if needed).
$oldCmkName = "<old column master key name>"
$newCmkName = "<new column master key name>"

# Authenticate to Azure. Needed only of either column master key is stored in Azure Key Vault.
Add-SqlAzureAuthenticationContext -Interactive

# Initiate the rotation from the current column master key to the new column master key.
Invoke-SqlColumnMasterKeyRotation -SourceColumnMasterKeyName $oldCmkName
-TargetColumnMasterKeyName $newCmkName -InputObject $database

# Complete the rotation of the old column master key.
Complete-SqlColumnMasterKeyRotation -SourceColumnMasterKeyName
$oldCmkName -InputObject $database

# Remove the old column master key metadata.
Remove-SqlColumnMasterKey -Name $oldCmkName -InputObject $database
```


### <a name="re-encrypt-columns-in-place"></a>Criptografar novamente as colunas no local

Depois de habilitar sua coluna para enclave, você pode executar as seguintes operações no local (dentro de enclave, sem precisar mover dados para fora do banco de dados):

- girar a chave de criptografia de coluna (para substituí-la por uma nova chave), por exemplo, para aderir a regulamentos de conformidade, alguns dos quais exigem a rotação periódica das chaves, ou por motivos de segurança (caso sua chave de criptografia de coluna seja comprometido).
- alterar o tipo de criptografia, por exemplo, de criptografia determinística para criptografia aleatória, para desbloquear cálculos avançados para a coluna.

#### <a name="prerequisites-for-re-encrypting-columns-in-place"></a>Pré-requisitos para criptografar novamente as colunas no local

- A coluna foi criptografada usando uma chave de criptografia de coluna habilitada para enclave.
- Você provisionou uma nova chave de criptografia de coluna habilitada para enclave (se sua meta for substituir a atual chave de criptografia de coluna habilitada para enclave, protegendo a coluna).
- Você tem acesso à chave mestra da coluna.

#### <a name="steps-for-re-encrypting-columns-in-place"></a>Etapas para criptografar novamente as colunas no local

1. Prepare uma janela de consulta do SSMS com Always Encrypted e cálculos de enclave habilitados para conexão de banco de dados. Para obter detalhes, consulte [Preparar uma janela de consulta do SSMS com o Always Encrypted habilitado](#prepare-an-ssms-query-window-with-always-encrypted-enabled).

2. Na janela de consulta, emita a instrução [ALTER TABLE (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md) com a cláusula ALTER COLUMN, especificando o seguinte na cláusula ENCRYPTED WITH:
    
    1. o nome da nova chave de criptografia de coluna habilitada para enclave se você estiver girando a chave atual. Se não estiver alterando a chave de criptografia da coluna, você precisará especificar o nome da chave atual.
    
    2. O novo tipo criptografia se alterá-lo. Se não estiver alterando o tipo de criptografia, você precisará especificar o tipo de criptografia atual.
        
       Se a coluna que você está criptografando novamente usar uma ordenação (BIN2) diferente da ordenação de banco de dados padrão, você precisará incluir a frase COLLATE e especificar a ordenação da coluna atual na definição de coluna (para manter a mesma ordenação).
        
       > [!NOTE]
       > Se a chave mestra de coluna estiver armazenada no Azure Key Vault, talvez seja solicitado que você entre no Azure.

3. Limpe o cache do plano para todos os lotes e procedimentos armazenados que acessam a tabela, para atualizar as informações de criptografia de parâmetros. 
 
    ```sql
    ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
    ```
    > [!NOTE]
    > Se você não remover o plano da consulta afetada do cache, a primeira execução da consulta após a criptografia poderá falhar.

    > [!NOTE]
    > Use ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE ou DBCC FREEPROCCACHE para limpar o cache de planos com cuidado, pois isso pode resultar na degradação temporária do desempenho de consulta. Para minimizar o impacto negativo da limpeza do cache, você pode remover seletivamente somente os planos das consultas afetadas.

4.  Chame [sp_refresh_parameter_encryption](../../system-stored-procedures/sp-refresh-parameter-encryption-transact-sql.md) para atualizar os metadados dos parâmetros de cada módulo (procedimento armazenado, função, exibição, gatilho) que persistiu em [sys.parameters](../..//system-catalog-views/sys-parameters-transact-sql.md) e possa ter sido invalidado criptografando novamente as colunas.

#### <a name="examples-of-re-encrypting-columns-in-place"></a>Exemplos de como criptografar novamente as colunas no local

Supondo que a coluna de SSN esteja criptografada usando uma chave de criptografia de coluna habilitada para enclave, chamada CEK1, e criptografia determinística, e que a ordenação atual, definida no nível da coluna, seja Latin1\_General\_BIN2, a instrução abaixo criptografa novamente a coluna com criptografia aleatória e com a mesma chave.

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) COLLATE Latin1_General_BIN2
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1]
, ENCRYPTION_TYPE = Randomized
, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL;
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

Supondo que a coluna de SSN esteja criptografada usando uma chave de criptografia de coluna habilitada para enclave, chamada CEK1, e criptografia determinística, e que a ordenação de banco de dados padrão seja uma ordenação BIN2 (que não foi definido no nível da coluna), a instrução abaixo criptografa novamente a coluna com uma nova chave habilitada para enclave, chamada CEK2 (sem alterar o tipo de criptografia).

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) 
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK2]
, ENCRYPTION\_TYPE = Deterministic
, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL;
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

Supondo que a coluna de SSN esteja criptografada usando uma chave de criptografia de coluna habilitada para enclave, chamada CEK1, e criptografia determinística, e que a ordenação de banco de dados padrão seja uma ordenação BIN2 (que não foi definido no nível da coluna), a instrução abaixo criptografa novamente a coluna com uma nova chave habilitada para enclave e com criptografia aleatória. Além disso, a operação é executada no modo online.

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) 
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1]
, ENCRYPTION_TYPE = Randomized
, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL 
WITH (ONLINE = ON);
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

### <a name="re-encrypt-columns-on-the-client-side"></a>Criptografar novamente as colunas no lado do cliente

O método herdado para criptografar novamente (e criptografar descriptografar) as colunas usa ferramentas de cliente, como o assistente Always Encrypted ou o PowerShell. De modo geral, usar esse método não é recomendável, exceto se a tabela que contém as colunas (que está sendo criptografada novamente) for pequena e se seu objetivo for combinar a recriptografia de uma coluna com uma nova chave habilitada para enclave e alterar o tipo de criptografia (de determinística para aleatória).

Se você criptografar novamente uma coluna que usa criptografia aleatória, talvez seja necessário alterar sua ordenação para uma ordenação BIN2 (antes ou depois de criptografar novamente), para desbloquear cálculos avançados. Consulte a seção Configuração de ordenação para obter detalhes.

Para obter detalhes, confira:

  - Girando chaves de criptografia de coluna usando SSMS: <https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-wizard>
  - Girando chaves de criptografia de coluna usando o PowerShell: <https://docs.microsoft.com/sql/relational-databases/security/encryption/configure-column-encryption-using-powershell>

### <a name="decrypt-a-column-in-place"></a>Descriptografar uma coluna no local

Se a coluna for criptografada com uma chave de criptografia de coluna habilitada para enclave, você poderá descriptografá-la (converter para uma coluna de texto sem formatação) no local, usando a instrução ALTER TABLE. Além disso, a operação é executada no modo online.

#### <a name="prerequisites-for-decrypting-a-column-in-place"></a>Pré-requisitos para descriptografar uma coluna no local

- A coluna foi criptografada usando uma chave de criptografia de coluna habilitada para enclave.
- Você tem acesso à chave mestra da coluna.

#### <a name="steps-for-decrypting-a-column-in-place"></a>Etapas para descriptografar uma coluna no local

1. Prepare uma janela de consulta do SSMS com Always Encrypted e cálculos de enclave habilitados para conexão de banco de dados. Para obter detalhes, consulte [Preparar uma janela de consulta do SSMS com o Always Encrypted habilitado](#prepare-an-ssms-query-window-with-always-encrypted-enabled).

2. Na janela de consulta, emita a instrução [ALTER TABLE (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md) com a cláusula ALTER COLUMN, especificando a configuração de coluna desejada **sem** a cláusula ENCRYPTED WITH.
    
    > [!NOTE]
    > Se a chave mestra de coluna estiver armazenada no Azure Key Vault, talvez seja solicitado que você entre no Azure.

3. Limpe o cache do plano para todos os lotes e procedimentos armazenados que acessam a tabela, para atualizar as informações de criptografia de parâmetros. 

    ```sql
    ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
    ```

    > [!NOTE]
    > Se você não remover o plano da consulta afetada do cache, a primeira execução da consulta após a criptografia poderá falhar.

    > [!NOTE]
    > Use ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE ou DBCC FREEPROCCACHE para limpar o cache de planos com cuidado, pois isso pode resultar na degradação temporária do desempenho de consulta. Para minimizar o impacto negativo da limpeza do cache, você pode remover seletivamente somente os planos das consultas afetadas.

4. Chame [sp_refresh_parameter_encryption](../../system-stored-procedures/sp-refresh-parameter-encryption-transact-sql.md) para atualizar os metadados dos parâmetros de cada módulo (procedimento armazenado, função, exibição, gatilho) que persistiu em [sys.parameters](../..//system-catalog-views/sys-parameters-transact-sql.md) e possa ter sido invalidado descriptografando as colunas.

#### <a name="example-for-decrypting-a-column-in-place"></a>Exemplo para descriptografar uma coluna no local

Supondo que a coluna SSN seja criptografada e que a ordenação atual, definida no nível de coluna, seja Latin1\_General\_BIN2, a instrução abaixo descriptografa a coluna (e mantém a ordenação inalterada – como alternativa, você pode optar por alterar a ordenação, por exemplo, para uma ordenação não BIN2 na mesma instrução).

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) COLLATE Latin1_General_BIN2
WITH (ONLINE = ON);
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

## <a name="issue-rich-queries-against-encrypted-columns-using-ssms"></a>Emitir consultas avançados em relação a colunas criptografadas usando o SSMS

A maneira mais rápida de testar consultas avançadas em suas colunas habilitadas para enclave é em uma janela de consulta do SSMS com a parametrização para Always Encrypted habilitada. Para obter detalhes sobre esse recurso útil no SSMS, consulte:

- [Parametrização para Always Encrypted – usando o SSMS para inserir, atualizar e filtrar por colunas criptografadas](https://blogs.msdn.microsoft.com/sqlsecurity/2016/12/13/parameterization-for-always-encrypted-using-ssms-to-insert-into-update-and-filter-by-encrypted-columns/)
- [Consultando colunas criptografadas](configure-always-encrypted-using-sql-server-management-studio.md#querying-encrypted-columns)

### <a name="prerequisites-for-issuing-rich-queries-against-encrypted-columns-using-ssms"></a>Pré-requisitos para emitir consultas avançados em relação a colunas criptografadas usando o SSMS

- As colunas a serem consultadas são habilitadas para enclave.
- Você tem acesso à chave (ou chaves) mestra da coluna.

### <a name="steps-for-issuing-rich-queries-against-encrypted-columns-using-ssms"></a>Etapas para emitir consultas avançados em relação a colunas criptografadas usando o SSMS

1. Prepare uma janela de consulta do SSMS com Always Encrypted e cálculos de enclave habilitados para conexão de banco de dados. Para obter detalhes, consulte [Preparar uma janela de consulta do SSMS com o Always Encrypted habilitado](#prepare-an-ssms-query-window-with-always-encrypted-enabled).

2. Habilitar parametrização de Always Encrypted.

    1. Selecione **Consultar** no menu principal do SSMS.
    2. Selecione **Opções de Consulta...** .
    3. Navegue para **Execução** > **Avançado**.
    4. Selecione ou desmarque a seleção de Habilitar Parametrização de Always Encrypted.
    5. Clique em OK.

3. Crie e execute suas consultas usando cálculos avançados ou colunas criptografadas. Você precisa declarar uma variável Transact-SQL para cada valor destinado a uma coluna criptografada em sua consulta. As variáveis devem usar inicializações embutidas (não podem ser definidas por meio da instrução SET).

    > [!NOTE]
    > Se a chave mestra de coluna estiver armazenada no Azure Key Vault, talvez seja solicitado que você entre no Azure.

### <a name="example-of-rich-queries-against-encrypted-columns"></a>Exemplo de consultas avançadas em colunas criptografadas

Este exemplo presume que seu banco de dados contém uma tabela criada usando a instrução a seguir.

```sql
CREATE TABLE [dbo].[Employees]
(
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [SSN] [char](11) COLLATE Latin1_General_BIN2 ENCRYPTED WITH (
        COLUMN_ENCRYPTION_KEY = [CEK1],
        ENCRYPTION_TYPE = Randomized,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [Salary] [money] ENCRYPTED WITH (
        COLUMN_ENCRYPTION_KEY = [CEK1],
        ENCRYPTION_TYPE = Randomized,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
    CONSTRAINT [PK_dbo.Employees] PRIMARY KEY CLUSTERED (
[EmployeeID] ASC
)
) ON [PRIMARY];
GO
```

CEK1 seja uma chave de criptografia de coluna habilitada para enclave.

Veja um exemplo de consulta que segue as diretrizes de parametrização, em relação a essa tabela:

```sql
DECLARE @SSNPattern [char](11) = '%1111%'
DECLARE @MinSalary [money] = 1000
SELECT *
FROM [dbo].[Employees]
WHERE SSN LIKE @SSNPattern
    AND [Salary] >= @MinSalary;
GO;
```

## <a name="create-and-use-indexes-on-enclave-enabled-columns-using-randomized-encryption"></a>Criar e usar índices em colunas habilitadas para enclave com criptografia aleatória

Como um índice em uma coluna habilitada para enclave com criptografia aleatória armazena os valores de chave de índice criptografados enquanto os valores são classificados com base em texto não criptografado, o Mecanismo do SQL Server tem que usar o enclave para todas as operações que envolvam a criação ou atualização de um índice, por exemplo:

- Criar ou recriar um índice.
- Inserir, atualizar ou excluir uma linha na tabela (contendo uma coluna indexada ou criptografada), que aciona a inserção e/ou remoção de uma chave de índice de/para o índice.
- Executar comandos DBCC que envolvam a verificação da integridade dos índices, por exemplo, [DBCC CHECKDB (Transact-SQL)](../../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) ou [DBCC CHECKTABLE (Transact-SQL)](../../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md).
- Recuperação de banco de dados (por exemplo, quando o SQL Server falha e é reiniciado), caso o SQL Server precise desfazer qualquer alteração no índice (veja mais detalhes abaixo).

Todas as operações descritas acima exigem que o enclave tenha a chave de criptografia de coluna para a coluna indexada, para que ela possa descriptografar as chaves de índice. Em geral, o enclave pode obter uma chave de criptografia de coluna de duas maneiras:
- Diretamente do aplicativo cliente.
- No cache das chaves de criptografia de coluna.

### <a name="invoke-indexing-operations-with-column-encryption-keys-provided-directly-by-the-client"></a>Invocar operações de indexação com chaves de criptografia de coluna fornecidas diretamente pelo cliente

Para esse método funcionar ao invocar as operações de indexação, o aplicativo emitindo a consulta que dispara uma operação em um índice precisa:

- Conectar-se ao banco de dados com Always Encrypted e os cálculos de enclave habilitados na conexão de banco de dados.
- O aplicativo precisa ter acesso à chave mestra da coluna que protege a chave de criptografia da coluna indexada.

Depois que o SQL Server Engine analisa a consulta do aplicativo e determina a necessidade de atualizar um índice em uma coluna criptografada para executar a consulta, ele instrui o driver cliente a fornecer o CEK necessário ao enclave por um canal seguro. Observe que isso é exatamente o mesmo mecanismo usado para fornecer o enclave com chaves de criptografia de coluna para processamento de consultas que não envolvam as operações de indexação.

Esse método é útil para garantir que a presença de índices em colunas criptografadas seja transparente para os aplicativos que já se conectam ao banco de dados com cálculos de enclave e Always Encrypted habilitados para a conexão e usam o enclave para o processamento de consulta. Depois de criar um índice em uma coluna, o driver dentro de seu aplicativo fornece de forma transparente as chaves de criptografia de coluna ao enclave para operações de indexação. Observe que a criação de índices pode aumentar o número de consultas que exigem que o aplicativo envie a as chaves de criptografia de coluna para o enclave.

Para obter instruções passo a passo sobre como usar esse método, confira o [Tutorial: Criando e usando índices em colunas habilitadas para enclave com criptografia aleatória](../tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md).

### <a name="invoke-indexing-operations-using-cached-column-encryption-keys"></a>Invocar operações de indexação usando chaves de criptografia de coluna armazenadas em cache

Depois que um aplicativo cliente envia uma chave de criptografia de coluna para o enclave (para processamento de qualquer consulta que exija cálculos de enclave), o enclave armazena a chave de criptografia de coluna em um cache interno, localizado dentro do enclave e inacessível externamente.

Se o mesmo aplicativo cliente ou um outro (usado pelo mesmo ou outro usuário) disparar uma operação em um índice sem fornecer diretamente a criptografia de coluna necessária, o enclave pesquisará a chave de criptografia de coluna no cache. Como resultado, a operação de índice é bem-sucedida, embora o aplicativo cliente ainda não tenha fornecido a chave.

Para que esse método de invocação de operações de indexação funcione, o aplicativo deve se conectar ao banco de dados sem o Always Encrypted habilitado para a conexão e a chave de criptografia de coluna necessária deve estar disponível no cache dentro do enclave.

Esse método de invocação de operações tem suporte apenas para consultas que não exigem chaves de criptografia de coluna para outras operações, não relacionadas a índices. Por exemplo, para que um aplicativo insira uma linha usando uma instrução INSERT em uma tabela que contém uma coluna criptografada, ele deve se conectar ao banco de dados com o Always Encrypted habilitado na cadeia de conexão e deve ter acesso às chaves, quer a coluna criptografada tenha um índice ou não.

Esse método é útil para:

- Garantir que a presença de índices em colunas habilitadas para enclave usando criptografia aleatória seja transparente para aplicativos e usuários que não tenham acesso a chaves e aos dados em texto não criptografado. Ele garante que a criação de um índice em uma coluna criptografada não interrompa as consultas existentes, ou seja, se um aplicativo emite consultas para uma tabela que contém colunas criptografadas sem ter acesso às chaves, depois que um DBA criar um índice, esse aplicativo pode continuar a executar sem ter acesso às chaves. Por exemplo, considere um aplicativo que executa a consulta abaixo na tabela **Funcionários** usada no exemplo anterior, antes que um DBA crie um índice em qualquer coluna criptografada. 

   ```sql
   DELETE FROM [dbo].[Employees] WHERE [EmployeeID] = 1;
   GO
   ```

   Se o aplicativo envia a consulta por uma conexão sem o Always Encrypted e os cálculos de enclave habilitados, a consulta terá êxito, pois ela não dispara cálculos em colunas criptografadas. Depois que um DBA cria um índice em colunas criptografadas, a consulta aciona a remoção das chaves dos índices para os quais o enclave precisa das chaves de criptografia de coluna. No entanto, o aplicativo poderá continuar a executar essa consulta na mesma conexão, desde que um proprietário de dados forneça as chaves de criptografia de coluna para o enclave.

- Para obter a separação de funções ao gerenciar índices, pois ele permite que os DBAs criem e alterem índices em colunas criptografadas sem a necessidade de acesso a dados confidenciais. 

Para obter instruções passo a passo sobre como usar esse método, confira o [Tutorial: Criando e usando índices em colunas habilitadas para enclave com criptografia aleatória](../tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md).

## <a name="develop-applications-issuing-rich-queries-in-visual-studio"></a>Desenvolver aplicativos emitindo consultas avançadas no Visual Studio

### <a name="set-up-your-visual-studio-project"></a>Configure seu projeto do Visual Studio

Para usar o Always Encrypted com enclaves seguros em um aplicativo .NET Framework, você precisa verificar se seu aplicativo foi compilado no .NET Framework 4.7.2 e está integrado ao [NuGet Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders](https://www.nuget.org/packages/Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders). Além disso, se armazenar a chave mestra da coluna no Azure Key Vault, você também precisará integrar seu aplicativo ao [NuGet Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider](https://www.nuget.org/packages/Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider), versão 2.2.0 ou posterior. 

1. Abra o Visual Studio.
2. Crie um novo projeto do Visual C\# ou abra um projeto existente.
3. Certifique-se de que seu projeto tenha como destino pelo menos o .NET Framework 4.7.2. Clique com o botão direito do mouse no projeto no Gerenciador de Soluções, selecione Propriedades e defina a estrutura de destino como o .NET Framework 4.7.2.

4. Instale o seguinte pacote NuGet acessando **Ferramentas** (menu principal) > **Gerenciador de Pacotes NuGet** > **Console do Gerenciador de Pacotes**. Execute o seguinte código no Console do Gerenciador de Pacotes.

   ```powershell
   Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders -IncludePrerelease
   ```

5. Se você usa o Azure Key Vault para armazenar chaves mestras de coluna, instale os seguintes pacotes NuGet acessando **Ferramentas** (menu principal) > **Gerenciador de Pacotes NuGet** > **Console do Gerenciador de Pacotes**. Execute o seguinte código no Console do Gerenciador de Pacotes.

   ```powershell
   Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider -IncludePrerelease -Version 2.2.0
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```

6. Selecione o projeto e clique em instalar.
7. Abra o arquivo de configuração de seu projeto (por exemplo, App.config ou Web.config).
8. Localize a seção de \<configuração\> e adicione ou atualize as seções \<configSections\>.

   A. Se a seção de \<configuração\> **não** contiver a seção \<configSections\>, adicione o conteúdo a seguir imediatamente abaixo da \<configuração\>.
   
      ```xml
      <configSections>
         <section name="SqlColumnEncryptionEnclaveProviders" type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
      </configSections>
      ```
   B. Se a seção de \<configuração\> já contiver a seção \<configSections\>, adicione a seguinte linha dentro de \<configSections\>:

   ```xml
   <section name="SqlColumnEncryptionEnclaveProviders"  type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data,  Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" /\>
   ```

9. Dentro da seção de configuração, abaixo de \<configSections\>, adicione a seguinte seção, que especifica um provedor de enclave a ser usado para atestar e interagir com enclaves VBS:

   ```xml
   <SqlColumnEncryptionEnclaveProviders>
       <providers>
           <add name="VBS"  type="Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders.VirtualizationBasedSecurityEnclaveProvider,  Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders,    Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91"/>
       </providers>
   </SqlColumnEncryptionEnclaveProviders>
   ```

Veja um exemplo completo de um arquivo app.config de um aplicativo de console simples.
```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <configSections>
    <section name="SqlColumnEncryptionEnclaveProviders" type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
  </configSections>
  <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.7.2" />
    </startup>

  <SqlColumnEncryptionEnclaveProviders>
    <providers>
      <add name="VBS" type="Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders.HostGuardianServiceEnclaveProvider, Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" />
    </providers>
  </SqlColumnEncryptionEnclaveProviders>
</configuration>
```
### <a name="develop-and-test-your-app"></a>Desenvolver e testar seu aplicativo

Para usar o Always Encrypted e cálculos de enclave, seu aplicativo precisa se conectar ao banco de dados com as duas palavras-chave a seguir na cadeia de conexão: `Column Encryption Setting = Enabled; Enclave Attestation Url=https://x.x.x.x/Attestation` (em que xxxx pode ser um ip, domínio, etc.).

Além disso, seu aplicativo precisa seguir diretrizes comuns que se aplicam a aplicativos que usam o Always Encrypted, por exemplo, o aplicativo precisa ter acesso a chaves mestras de coluna associadas com as colunas do banco de dados, referenciadas nas consultas do aplicativo.

Para obter detalhes sobre como desenvolver aplicativos do .NET Framework usando o Always Encrypted, consulte os seguintes artigos:

- [Desenvolver usando o Always Encrypted com o Provedor de Dados .NET Framework](develop-using-always-encrypted-with-net-framework-data-provider.md)
- [Always Encrypted: Proteger dados confidenciais no Banco de Dados SQL e armazenar chaves de criptografia no Azure Key Vault](https://docs.microsoft.com/azure/sql-database/sql-database-always-encrypted)

#### <a name="example-of-simple-application"></a>Exemplo de um aplicativo simples

O código abaixo é um exemplo simples de um aplicativo de console C\# que emite uma consulta LIKE na tabela com o esquema a seguir:

```sql
CREATE TABLE [dbo].[Employees]
(
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [SSN] [char](11) ENCRYPTED WITH (
        COLUMN_ENCRYPTION_KEY = [CEK1],
        ENCRYPTION_TYPE = Randomized,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [Salary] [money] ENCRYPTED WITH (
        COLUMN_ENCRYPTION_KEY = [CEK1],
        ENCRYPTION_TYPE = Randomized,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
    CONSTRAINT [PK_dbo.Employees] PRIMARY KEY CLUSTERED (
[EmployeeID] ASC
)
) ON [PRIMARY];
GO
```

Presume-se que CEK1 seja uma chave de criptografia de coluna habilitada para enclave.

```cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Data.SqlClient;
using System.Data;
namespace ConsoleApp1
{
   class Program
   {
      static void Main(string\[\] args)
   {

   string connectionString = "Data Source = myserver; Initial Catalog = ContosoHR; Column Encryption Setting = Enabled;Enclave Attestation Url = https://10.193.16.185/Attestation/attestationservice.svc/signingCertificates; Integrated Security = true";

using (SqlConnection connection = new SqlConnection(connectionString))
{
   connection.Open();
   
   SqlCommand cmd = connection.CreateCommand();
   cmd.CommandText = @"SELECT [SSN], [FirstName], [LastName], [Salary] FROM [dbo].[Employees] WHERE [SSN] LIKE @SSNPattern AND [Salary] > @MinSalary;";
   
   SqlParameter paramSSNPattern = cmd.CreateParameter();
   
   paramSSNPattern.ParameterName = @"@SSNPattern";
   paramSSNPattern.DbType = DbType.AnsiStringFixedLength;
   paramSSNPattern.Direction = ParameterDirection.Input;
   paramSSNPattern.Value = "%1111";
   paramSSNPattern.Size = 11;
   
   cmd.Parameters.Add(paramSSNPattern);
   
   SqlParameter MinSalary = cmd.CreateParameter();
   
   MinSalary.ParameterName = @"@MinSalary";
   MinSalary.DbType = DbType.Currency;
   MinSalary.Direction = ParameterDirection.Input;
   MinSalary.Value = 900;
   
   cmd.Parameters.Add(MinSalary);
   cmd.ExecuteNonQuery();
   
   SqlDataReader reader = cmd.ExecuteReader();
   while (reader.Read())
   
   {
     Console.WriteLine(reader);
     Console.WriteLine(reader\[0\] + ", " + reader\[1\] + ", " + reader\[2\] + ", " + reader\[3\]);
   }

   Console.ReadKey();

   }
  }
 }
}
```
