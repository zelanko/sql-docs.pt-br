---
title: 'Tutorial: Introdução ao Always Encrypted com enclaves seguros usando o SSMS | Microsoft Docs'
ms.custom: ''
ms.date: 10/04/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: jaszymas
ms.author: jaszymas
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 75263ad68af90f0dfd8035cc943a194c344f90fa
ms.sourcegitcommit: ef78cc196329a10fc5c731556afceaac5fd4cb13
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49461022"
---
# <a name="tutorial-getting-started-with-always-encrypted-with-secure-enclaves-using-ssms"></a>Tutorial: Introdução ao Always Encrypted com enclaves seguros usando o SSMS
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este tutorial ensina como começar a usar o [Always Encrypted com enclaves seguros](encryption/always-encrypted-enclaves.md). Ela mostrará a você:
- Como criar um ambiente simples para testar e avaliar o Always Encrypted com enclaves seguros.
- Como criptografar dados no local e emitir consultas avançadas em relação a colunas criptografadas usando o SSMS (SQL Server Management Studio).

## <a name="prerequisites"></a>Prerequisites

Para começar com o Always Encrypted com enclaves seguros, você precisa de pelo menos dois computadores (podem ser máquinas virtuais):

- O computador do SQL Server para hospedar o SQL Server e o SSMS.
- O computador do HGS para executar o Serviço Guardião de Host, que é necessário para o atestado de enclave.

### <a name="sql-server-computer-requirements"></a>Requisitos do computador com SQL Server

- [!INCLUDE [sssqlv15-md](../../includes/sssqlv15-md.md)] ou posterior
- Windows 10 Enterprise versão 1809 ou Windows Server 2019 Datacenter
- [SSMS (SQL Server Management Studio) 18.0 ou posterior](../../ssms/download-sql-server-management-studio-ssms.md).

Como alternativa, você pode instalar o SSMS em outro computador.

>[!WARNING] 
>Em ambientes de produção, você nunca deve usar SSMS ou outras ferramentas para gerenciar chaves Always Encrypted ou executar consultas em dados criptografados no computador do SQL Server, pois isso pode reduzir ou eliminar completamente a razão para o uso do Always Encrypted.

### <a name="hgs-computer-requirements"></a>Requisitos do computador do HGS

- Windows Server 2019 edição Standard ou Datacenter
- 2 CPUs
- 8 GB RAM
- 100 GB de armazenamento

>[!NOTE]
>O computador do HGS não deve ser ingressado em um domínio antes de você começar.

## <a name="step-1-configure-the-hgs-computer"></a>Etapa 1: configurar o computador do HGS

Nesta etapa, você configurará o computador do HGS para executar o Serviço Guardião de Host, que dá suporte ao atestado de chave host.

1. Entre no computador do HGS como um administrador (administrador local), abra um console do Windows PowerShell com privilégios elevados e, executando o seguinte comando, adicione a função de Serviço Guardião de Host:

   ```powershell
   Install-WindowsFeature -Name HostGuardianServiceRole -IncludeManagementTools -Restart
   ```

2. Após a reinicialização do computador do HGS, entre com sua conta do administrador novamente, abra um console do Windows PowerShell com privilégios elevados e execute os comandos a seguir para instalar o Serviço Guardião de Host e configurar o respectivo domínio. A senha especificada aqui se aplicará somente à senha do Modo de Reparo de Serviços de Diretório do Active Directory; a senha de logon da conta do administrador não será alterada. Você pode fornecer qualquer nome de domínio de sua preferência para -HgsDomainName.

   ```powershell
   $adminPassword = ConvertTo-SecureString -AsPlainText '<password>' -Force
   Install-HgsServer -HgsDomainName 'bastion.local' -SafeModeAdministratorPassword $adminPassword -Restart
   ```

3. Após o computador reinicializar novamente, entre com sua conta do administrador (que agora também é um administrador de domínio), abra um console do Windows PowerShell com privilégios elevados e configure o atestado de chave host para sua instância do HGS. 

   ```powershell
   Initialize-HgsAttestation -HgsServiceName 'hgs' -TrustHostKey  
   ```

4. Localize o endereço IP do computador do HGS executando o comando a seguir. Salve esse endereço IP para as etapas posteriores.

   ```powershell
   Get-NetIPAddress  
   ```

>[!NOTE]
>Como alternativa, se quiser se referir ao computador do HGS por um nome DNS, você pode configurar um encaminhador de seus servidores DNS corporativos para o novo controlador de domínio do HGS.  

## <a name="step-2-configure-the-sql-server-computer-as-a-guarded-host"></a>Etapa 2: configurar o computador do SQL Server como um host protegido
Nesta etapa, você configurará o computador do SQL Server como um host protegido registrado com HGS usando atestado de chave host.
>[!NOTE]
>O atestado de chave host só é recomendado para uso em ambientes de teste. Você deve usar o atestado de TPM para ambientes de produção.

1. Entre no computador do SQL Server como um administrador, abra um console do Windows PowerShell com privilégios elevados e instale o recurso de Host Protegido, o que também instalará o Hyper-V (se ainda não estiver instalado).

   ```powershell
   Enable-WindowsOptionalFeature -Online -FeatureName HostGuardian -All
   ```

2. Reinicie o computador do SQL Server quando for solicitado que você conclua a instalação do Hyper-V.
3. Recupere o valor da variável abaixo para determinar o nome do computador do SQL Server.

   ```powershell
   $env:computername 
   ```

4. Entre no computador do SQL Server como um administrador novamente, abra um console do Windows PowerShell com privilégios elevados, gere uma chave host exclusiva e exporte a chave pública resultante para um arquivo.

   ```powershell
   Set-HgsClientHostKey 
   Get-HgsClientHostKey -Path $HOME\Desktop\hostkey.cer
   ```

5. Copie o arquivo de chave host gerado na etapa anterior para o computador do HGS. As instruções abaixo supõem que seu nome do arquivo é hostkey.cer que você o está copiando para sua área de trabalho no computador do HGS.
6. No computador do HGS, abra um console do Windows PowerShell com privilégios elevados e registre a chave host do computador do SQL Server com o HGS:

   ```powershell
   Add-HgsAttestationHostKey -Name <your SQL Server computer name> -Path $HOME\Desktop\hostkey.cer
   ```

7. No computador do SQL Server, execute o seguinte comando em um console do Windows PowerShell com privilégios elevados para indicar ao computador do SQL Server o local em que atestar. Verifique se você especificou o endereço IP ou o nome DNS do seu computador do HGS. 

   ```powershell
   Set-HgsClientConfiguration -AttestationServerUrl http://<IP address or DNS name>/Attestation -KeyProtectionServerUrl http://<IP address or DNS name>/KeyProtection/  
   ```

O resultado do comando acima deve mostrar que AttestationStatus = Passed.

Se você receber um erro HostUnreachable, isso significa que o computador do SQL Server não pode se comunicar com o HGS. Verifique se você pode executar ping no computador do HGS.

Um erro UnauthorizedHost indica que a chave pública não foi registrada com o servidor do HGS – Repita as etapas 5 e 6 para resolver o erro.

Se todo o resto falhar, execute Clear-HgsClientHostKey e repita as etapas 4 a 7.

## <a name="step-3-enable-always-encrypted-with-secure-enclaves-in-sql-server"></a>Etapa 3: habilitar o Always Encrypted com enclaves seguros no SQL Server

Nesta etapa, você habilitará a funcionalidade de Always Encrypted usando enclaves na instância do SQL Server.

1. Abra o SSMS, conecte-se à instância do SQL Server como sysadmin e abra uma nova janela de consulta.
2. Configure o tipo do enclave seguro como VBS.

   ```sql
   EXEC sys.sp_configure 'column encryption enclave type', 1
   RECONFIGURE
   ```

3. Reinicie a instância do SQL Server para que as alterações anteriores entrem em vigor. Para reiniciar a instância no SSMS, clique nela com o botão direito do mouse no Pesquisador de Objetos e selecionando Reiniciar. Após a instância ser reiniciada, conecte-se a ela novamente.

4. Confirme que o enclave seguro está carregado executando a consulta a seguir:

   ```sql
   SELECT [name], [value], [value_in_use] FROM sys.configurations
   WHERE [name] = 'column encryption enclave type'
   ```

    A consulta deve retornar uma linha semelhante à seguinte:  

    | NAME                           | value | value_in_use |
    | ------------------------------ | ----- | -------------- |
    | column encryption enclave type | 1     | 1              |

5. Para habilitar cálculos avançados em colunas criptografadas, execute a consulta a seguir:

   ```sql
   DBCC traceon(127,-1)
   ```

    > [!NOTE]
    > Cálculos avançados são desabilitados por padrão no [!INCLUDE [sssqlv15-md](../../includes/sssqlv15-md.md)]. Eles precisam ser habilitados usando a instrução acima após cada reinicialização de sua instância do SQL Server.

## <a name="step-4-create-a-sample-database"></a>Etapa 4: criar banco de dados de exemplo
Nesta etapa você criará um banco de dados com alguns dados de exemplo, os quais você criptografará mais tarde.

1. Conecte-se à instância do SQL Server usando o SSMS.
2. Crie um novo banco de dados denominado ContosoHR.

    ```sql
    CREATE DATABASE [ContosoHR] COLLATE Latin1_General_BIN2
    ```

3. Assegure-se de estar conectado ao banco de dados recém-criado. Crie uma nova tabela denominada Funcionários.

    ```sql
    CREATE TABLE [dbo].[Employees]
    (
        [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
        [SSN] [char](11) NOT NULL,
        [FirstName] [nvarchar](50) NOT NULL,
        [LastName] [nvarchar](50) NOT NULL,
        [Salary] [money] NOT NULL
    ) ON [PRIMARY]
    GO
    ```

4. Adicione alguns registros de funcionários à tabela Funcionários.

    ```sql
    INSERT INTO [dbo].[Employees]
            ([SSN]
            ,[FirstName]
            ,[LastName]
            ,[Salary])
        VALUES
            ('795-73-9838'
            , N'Catherine'
            , N'Abel'
            , $31692)
    GO

    INSERT INTO [dbo].[Employees]
            ([SSN]
            ,[FirstName]
            ,[LastName]
            ,[Salary])
        VALUES
            ('990-00-6818'
            , N'Kim'
            , N'Abercrombie'
            , $55415)
    GO
    ```

## <a name="step-5-provision-enclave-enabled-keys"></a>Etapa 5: provisionar chaves habilitadas para enclave

Nesta etapa, você criará uma chave mestra da coluna e uma chave de criptografia de coluna que permitirão cálculos de enclave.

1. Conecte-se a seu banco de dados usando o SSMS.
2. No **Pesquisador de Objetos**, expanda o banco de dados e navegue até **Segurança** > **Chaves Always Encrypted**.
3. Provisione uma nova chave mestra da coluna habilitada para enclave:
    1. Clique com o botão direito do mouse em **Chaves Always Encrypted** e selecione **Nova chave mestra da coluna…**.
    2. Selecione o nome de sua chave mestra da coluna: CMK1.
    3. Certifique-se de selecionar **Repositório de certificados do Windows (usuário atual ou computador local)** ou **Azure Key Vault**.
    4. Selecione **Permitir computações de enclave**.
    5. Se tiver selecionado o Azure Key Vault, entre no Azure e selecione seu cofre de chaves. Para obter mais informações sobre como criar um cofre de chaves para Always Encrypted, veja [Gerenciar cofres de chaves do portal do Azure](https://blogs.technet.microsoft.com/kv/2016/09/12/manage-your-key-vaults-from-new-azure-portal/).
    6. Selecione a chave se ela já existir ou siga as instruções no formulário para criar uma nova chave.
    7. Escolha **OK**.

        ![Permitir computações de enclave](encryption/media/always-encrypted-enclaves/allow-enclave-computations.png)

4. Crie uma nova chave de criptografia de coluna habilitada para enclave:

    1. Clique com o botão direito do mouse em **Chaves Always Encrypted** e selecione **Nova chave de criptografia da coluna**.
    2. Insira um nome para a nova chave de criptografia da coluna: CEK1.
    3. No menu suspenso **Chave mestra da coluna**, selecione a chave mestra da coluna criada nas etapas anteriores.
    4. Escolha **OK**.

## <a name="step-6-encrypt-some-columns-in-place"></a>Etapa 6: Criptografar algumas colunas em vigor

Nesta etapa, você criptografará os dados armazenados nas colunas SSN e Salário dentro do enclave do lado do servidor e, em seguida, testará uma consulta SELECT dos dados.

1. No SSMS, configure uma nova janela de consulta com o Always Encrypted habilitado para a conexão de banco de dados.
    1. No SSMS, abra uma nova janela de consulta.
    2. Clique com o botão direito do mouse em qualquer lugar na nova janela de consulta.
    3. Selecione Conexão \> Alterar Conexão.
    4. Selecione **Opções**. Navegue até a guia **Always Encrypted**, selecione **Habilitar o Always Encrypted** e especifique a URL do atestado do enclave.
    5. Selecione **Conectar**.
2. No SSMS, configure outra janela de consulta com o Always Encrypted desabilitado para a conexão de banco de dados.
    1. No SSMS, abra uma nova janela de consulta.
    2. Clique com o botão direito do mouse em qualquer lugar na nova janela de consulta.
    3. Selecione Conexão \> Alterar Conexão.
    4. Selecione **Opções**. Navegue até a guia **Always Encrypted** e confirme que a opção **Habilitar o Always Encrypted** não está selecionada.
    5. Selecione **Conectar**.
3. Criptografe as colunas SSN e Salário. Na janela de consulta, com o Always Encrypted habilitado, cole e execute as instruções abaixo:

    ```sql
    ALTER TABLE [dbo].[Employees]
    ALTER COLUMN [SSN] [char] (11)
    ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
    WITH
    (ONLINE = ON)
    GO
    DBCC FREEPROCCACHE
    GO

    ALTER TABLE [dbo].[Employees]
    ALTER COLUMN [Salary] [money]
    ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
    WITH
    (ONLINE = ON)
    GO
    DBCC FREEPROCCACHE
    GO
    ```

4. Para verificar se as colunas SSN e Salário agora estão criptografadas, cole e execute a instrução abaixo na janela de consulta com o Always Encrypted desabilitado. A janela de consulta deve retornar valores criptografados nas colunas SSN e Salário. Com a janela de consulta com o Always Encrypted habilitado, tente realizar a mesma consulta para ver os dados descriptografados.

    ```sql
    SELECT * FROM [dbo].[Employees]
    ```

## <a name="step-7-run-rich-queries-against-encrypted-columns"></a>Etapa 7: executar consultas avançadas em colunas criptografadas

Agora você pode executar consultas avançadas nas colunas criptografadas. Algum processamento de consulta será executado dentro de seu enclave do lado do servidor. 

1. Habilite a parametrização de Always Encrypted.
    1. Selecione **Consultar** no menu principal do SSMS.
    2. Selecione **Opções de Consulta…**.
    3. Navegue para **Execução** > **Avançado**.
    4. Selecione ou desmarque a seleção de Habilitar Parametrização de Always Encrypted.
    5. Selecione OK.
2. Na janela de consulta, com o Always Encrypted habilitado, cole e execute a consulta abaixo. A consulta deve retornar valores de texto sem formatação e linhas que atendem a critérios de pesquisa especificados.

    ```sql
    DECLARE @SSNPattern [char](11) = '%6818'
    DECLARE @MinSalary [money] = $1000
    SELECT * FROM [dbo].[Employees]
    WHERE SSN LIKE @SSNPattern AND [Salary] >= @MinSalary;
    ```

## <a name="next-steps"></a>Next Steps
Ver [Configurar o Always Encrypted com enclaves seguros](encryption/configure-always-encrypted-enclaves.md) para ideias sobre outros casos de uso. Você também pode tentar fazer o seguinte:

- [Configurar o atestado de TPM.](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-initialize-hgs-tpm-mode)
- [Configurar o HTTPS para a instância do HGS.](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-configure-hgs-https)
- Desenvolver aplicativos que emitem consultas avançadas a colunas criptografadas.
