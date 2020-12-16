---
title: 'Tutorial: Always Encrypted com enclaves seguros usando SSMS'
description: Este tutorial ensina a criar um Always Encrypted básico com um ambiente de enclaves seguros, criptografar dados in-loco e emitir consultas avançadas em colunas criptografadas usando o SSMS (SQL Server Management Studio).
ms.custom: seo-lt-2019
ms.date: 04/10/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15'
ms.openlocfilehash: 99b04548244da3bda45346e7aa4a7c4d72481789
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97463087"
---
# <a name="tutorial-always-encrypted-with-secure-enclaves-using-ssms"></a>Tutorial: Always Encrypted com enclaves seguros usando SSMS
[!INCLUDE [sqlserver2019-windows-only](../../includes/applies-to-version/sqlserver2019-windows-only.md)]

Este tutorial ensina como começar a usar o [Always Encrypted com enclaves seguros](encryption/always-encrypted-enclaves.md). Ela mostrará a você:
- Como criar um ambiente básico para testar e avaliar o Always Encrypted com enclaves seguros.
- Como criptografar dados no local e emitir consultas avançadas em relação a colunas criptografadas usando o SSMS (SQL Server Management Studio).

## <a name="prerequisites"></a>Pré-requisitos

Para começar com o Always Encrypted com enclaves seguros, você precisa de pelo menos dois computadores (podem ser máquinas virtuais):

- O computador do SQL Server para hospedar o SQL Server e o SSMS.
- O computador do HGS para executar o Serviço Guardião de Host, que é necessário para o atestado de enclave.

### <a name="sql-server-computer-requirements"></a>Requisitos do computador com SQL Server

- [!INCLUDE [sssqlv15-md](../../includes/sssqlv15-md.md)] ou posterior.
- Windows 10 Enterprise versão 1809 ou posterior; ou Windows Server 2019 Datacenter Edition. Outras edições do Windows 10 e do Windows Server não dão suporte a atestado com HGS.
- Suporte de CPU para tecnologias de virtualização:
  - Intel VT-x com Tabelas de Página Estendida.
  - AMD-V com Indexação de Virtualização Rápida.
  - Se você estiver executando [!INCLUDE [ssnoversion-md](../../includes/ssnoversion-md.md)] em uma VM, o hipervisor e a CPU física deverão oferecer recursos de virtualização aninhados. 
    - No Hyper-V 2016 ou posterior, [habilite as extensões de virtualização aninhadas no processador da VM](/virtualization/hyper-v-on-windows/user-guide/nested-virtualization#configure-nested-virtualization).
    - No Azure, selecione um tamanho de VM que dê suporte à virtualização aninhada. Isso inclui todas as VMs da série v3, por exemplo, Dv3 e Ev3. Confira [Criar uma VM do Azure compatível com aninhamento](/azure/virtual-machines/windows/nested-virtualization#create-a-nesting-capable-azure-vm).
    - No VMWare vSphere 6.7 ou posterior, habilite o suporte de segurança baseada em virtualização para a VM conforme descrito na [documentação do VMware](https://docs.vmware.com/en/VMware-vSphere/6.7/com.vmware.vsphere.vm_admin.doc/GUID-C2E78F3E-9DE2-44DB-9B0A-11440800AADD.html).
    - Outros hipervisores e nuvens públicas podem dar suporte a recursos de virtualização aninhados que também permitem Always Encrypted com enclaves de VBS. Verifique a documentação da solução de virtualização para obter instruções sobre compatibilidade e configuração.
- [SSMS (SQL Server Management Studio) 18.3 ou posterior](../../ssms/download-sql-server-management-studio-ssms.md).

Como alternativa, é possível instalar o SSMS em outro computador.

> [!WARNING]
> Em ambientes de produção, você nunca deve usar SSMS ou outras ferramentas para gerenciar chaves Always Encrypted ou executar consultas em dados criptografados no computador do SQL Server, pois isso pode reduzir ou eliminar completamente a razão para o uso do Always Encrypted. Confira [Considerações de segurança para gerenciamento de chaves](encryption/overview-of-key-management-for-always-encrypted.md#security-considerations-for-key-management) para obter mais detalhes.

### <a name="hgs-computer-requirements"></a>Requisitos do computador de HGS

- Windows Server 2019 edição Standard ou Datacenter
- 2 CPUs
- 8 GB RAM
- 100 GB de armazenamento

> [!NOTE]
> O computador do HGS não deve ser ingressado em um domínio antes de você começar.

## <a name="step-1-configure-the-hgs-computer"></a>Etapa 1: Configurar o computador do HGS

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

> [!NOTE]
> Como alternativa, se quiser se referir ao computador do HGS por um nome DNS, você pode configurar um encaminhador de seus servidores DNS corporativos para o novo controlador de domínio do HGS.  

## <a name="step-2-configure-the-sql-server-computer-as-a-guarded-host"></a>Etapa 2: Configurar o computador do SQL Server como um host protegido
Nesta etapa, você configurará o computador do SQL Server como um host protegido registrado com HGS usando atestado de chave host.

> [!WARNING]
> O atestado de chave host só é recomendado para uso em ambientes de teste. Você deve usar o atestado de TPM para ambientes de produção.

1. Entre no computador do SQL Server como um administrador, abra um console do Windows PowerShell com privilégios elevados e recupere o nome do seu computador acessando a variável computername.

   ```powershell
   $env:computername 
   ```

2. Instale o recurso de Host protegido, que também instalará o Hyper-V (se ele não estiver instalado).

   ```powershell
   Enable-WindowsOptionalFeature -Online -FeatureName HostGuardian -All
   ```

3. Reinicie o computador do SQL Server quando for solicitado que você conclua a instalação do Hyper-V.

4. Se o computador do SQL Server for uma máquina virtual, um computador físico não compatível com a inicialização segura de UEFI ou um computador físico não equipado com IOMMU, será preciso remover o requisito de VBS dos recursos de segurança da plataforma.
    1. Remova o requisito de inicialização segura e IOMMU executando o seguinte comando em seu computador SQL Server em um console do PowerShell com privilégios elevados:

        ```powershell
       Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Control\DeviceGuard -Name RequirePlatformSecurityFeatures -Value 0
       ```

    1. Reinicie o computador SQL Server novamente para que o VBS fique online com os requisitos reduzidos.

        ```powershell
       Restart-Computer
       ```

5. Entre no computador do SQL Server como um administrador novamente, abra um console do Windows PowerShell com privilégios elevados, gere uma chave host exclusiva e exporte a chave pública resultante para um arquivo.

   ```powershell
   Set-HgsClientHostKey 
   Get-HgsClientHostKey -Path $HOME\Desktop\hostkey.cer
   ```

6. Copie manualmente o arquivo de chave host gerado na etapa anterior para o computador do HGS. As instruções abaixo supõem que seu nome do arquivo é hostkey.cer que você o está copiando para sua área de trabalho no computador do HGS.

7. No computador do HGS, abra um console do Windows PowerShell com privilégios elevados e registre a chave host do computador do SQL Server com o HGS:

   ```powershell
   Add-HgsAttestationHostKey -Name <your SQL Server computer name> -Path $HOME\Desktop\hostkey.cer
   ```

8. No computador do SQL Server, execute o seguinte comando em um console do Windows PowerShell com privilégios elevados para indicar ao computador do SQL Server o local em que atestar. Verifique se você especificou o endereço IP ou o nome DNS do seu computador do HGS nos dois locais. 

   ```powershell
   # use http, and not https
   Set-HgsClientConfiguration -AttestationServerUrl http://<IP address or DNS name>/Attestation -KeyProtectionServerUrl http://<IP address or DNS name>/KeyProtection/  
   ```

O resultado do comando acima deve mostrar que AttestationStatus = Passed.

Se você receber um erro HostUnreachable, isso significa que o computador do SQL Server não pode se comunicar com o HGS. Verifique se você pode executar ping no computador do HGS.

Um erro UnauthorizedHost indica que a chave pública não foi registrada com o servidor do HGS – Repita as etapas 5 e 6 para resolver o erro.

Se todo o resto falhar, execute Remove-HgsClientHostKey e repita as etapas 4 a 7.

## <a name="step-3-enable-always-encrypted-with-secure-enclaves-in-sql-server"></a>Etapa 3: Habilitar o Always Encrypted com enclaves seguros no SQL Server

Nesta etapa, você habilitará a funcionalidade de Always Encrypted usando enclaves na instância do SQL Server.

1. Usando o SSMS, conecte-se à instância do SQL Server como sysadmin **sem** Always Encrypted habilitado para a conexão de banco de dados.
    1. Inicie o SSMS.
    1. Na caixa de diálogo **Conectar ao servidor**, especifique o nome do servidor, selecione um método de autenticação e especifique suas credenciais.
    1. Clique em **Opções >>** e selecione a guia **Always Encrypted**.
    1. Verifique se a caixa de seleção **Habilitar o Always Encrypted (criptografia de coluna)** **não** está selecionada.
    1. Selecione **Conectar**.

2. Abra uma nova janela de consulta e execute a instrução abaixo para definir o tipo de enclave seguro para VBS (Segurança com base em virtualização).

   ```sql
   EXEC sys.sp_configure 'column encryption enclave type', 1;
   RECONFIGURE;
   ```

3. Reinicie a instância do SQL Server para que as alterações anteriores entrem em vigor. Para reiniciar a instância no SSMS, clique nela com o botão direito do mouse no Pesquisador de Objetos e selecionando Reiniciar. Após a instância ser reiniciada, conecte-se a ela novamente.

4. Confirme que o enclave seguro está carregado executando a consulta a seguir:

   ```sql
   SELECT [name], [value], [value_in_use] FROM sys.configurations
   WHERE [name] = 'column encryption enclave type';
   ```

    A consulta deve retornar o resultado a seguir:  

    | name                           | value | value_in_use |
    | ------------------------------ | ----- | -------------- |
    | column encryption enclave type | 1     | 1              |

5. Para habilitar cálculos avançados em colunas criptografadas, execute a consulta a seguir:

   ```sql
   DBCC traceon(127,-1);
   ```

    > [!NOTE]
    > Cálculos avançados são desabilitados por padrão no [!INCLUDE [sssqlv15-md](../../includes/sssqlv15-md.md)]. Eles precisam ser habilitados usando a instrução acima após cada reinicialização de sua instância do SQL Server.

## <a name="step-4-create-a-sample-database"></a>Etapa 4: Criar banco de dados de exemplo
Nesta etapa você criará um banco de dados com alguns dados de exemplo, os quais você criptografará mais tarde.

1. Usando a instância do SSMS da etapa anterior, execute a instrução abaixo em uma janela de consulta para criar um novo banco de dados denominado **ContosoHR**.

    ```sql
    CREATE DATABASE [ContosoHR];
    ```

1. Crie uma nova tabela denominada **Funcionários**.

    ```sql
    USE [ContosoHR];
    GO

    CREATE TABLE [dbo].[Employees]
    (
        [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
        [SSN] [char](11) NOT NULL,
        [FirstName] [nvarchar](50) NOT NULL,
        [LastName] [nvarchar](50) NOT NULL,
        [Salary] [money] NOT NULL
    ) ON [PRIMARY];
    ```

1. Adicione alguns registros de funcionários à tabela **Funcionários**.

    ```sql
    USE [ContosoHR];
    GO

    INSERT INTO [dbo].[Employees]
            ([SSN]
            ,[FirstName]
            ,[LastName]
            ,[Salary])
        VALUES
            ('795-73-9838'
            , N'Catherine'
            , N'Abel'
            , $31692);

    INSERT INTO [dbo].[Employees]
            ([SSN]
            ,[FirstName]
            ,[LastName]
            ,[Salary])
        VALUES
            ('990-00-6818'
            , N'Kim'
            , N'Abercrombie'
            , $55415);
    ```

## <a name="step-5-provision-enclave-enabled-keys"></a>Etapa 5: Provisionar chaves habilitadas para enclave

Nesta etapa, você criará uma chave mestra da coluna e uma chave de criptografia de coluna que permitirão cálculos de enclave.

1. Usando a instância de SSMS da etapa anterior, no **Pesquisador de Objetos**, expanda o banco de dados e navegue até **Segurança** > **Chaves Always Encrypted**.
1. Provisione uma nova chave mestra da coluna habilitada para enclave:
    1. Clique com o botão direito do mouse em **Chaves Always Encrypted** e selecione **Nova chave mestra da coluna...** .
    2. Selecione o nome da chave mestra da coluna: **CMK1**.
    3. Certifique-se de selecionar **Repositório de certificados do Windows (usuário atual ou computador local)** ou **Azure Key Vault**.
    4. Selecione **Permitir computações de enclave**.
    5. Se tiver selecionado o Azure Key Vault, entre no Azure e selecione seu cofre de chaves. Para obter mais informações sobre como criar um cofre de chaves para Always Encrypted, veja [Gerenciar cofres de chaves do portal do Azure](/archive/blogs/kv/manage-your-key-vaults-from-new-azure-portal).
    6. Selecione seu certificado ou chave do Azure Key Value se ela já existir, ou clique no botão **Gerar Certificado** para criar um novo.
    7. Selecione **OK**.

        ![Permitir computações de enclave](encryption/media/always-encrypted-enclaves/allow-enclave-computations.png)

1. Crie uma nova chave de criptografia de coluna habilitada para enclave:

    1. Clique com o botão direito do mouse em **Chaves Always Encrypted** e selecione **Nova chave de criptografia da coluna**.
    2. Insira um nome para a nova chave de criptografia da coluna: **CEK1**.
    3. No menu suspenso **Chave mestra da coluna**, selecione a chave mestra da coluna criada nas etapas anteriores.
    4. Selecione **OK**.

## <a name="step-6-encrypt-some-columns-in-place"></a>Etapa 6: Criptografar algumas colunas em vigor

Nesta etapa, você criptografará os dados armazenados nas colunas **SSN** e **Salário** dentro do enclave do lado do servidor e, em seguida, testará uma consulta SELECT nos dados.

1. Abra uma nova instância do SSMS e conecte-se à instância do SQL Server **com** Always Encrypted habilitado para a conexão de banco de dados.
    1. Inicie uma nova instância do SSMS.
    1. Na caixa de diálogo **Conectar ao servidor**, especifique o nome do servidor, selecione um método de autenticação e especifique suas credenciais.
    1. Clique em **Opções >>** e selecione a guia **Always Encrypted**.
    1. Marque a caixa de seleção **Habilitar o Always Encrypted (criptografia de coluna)** e especifique a URL do atestado do enclave (por exemplo, ht <span>tp://</span>hgs.bastion.local/Attestation).
    1. Selecione **Conectar**.
    1. Se solicitado a habilitar a parametrização para consultas Always Encrypted, selecione **Habilitar**.

1. Usando a mesma SSMS da instância (com Always Encrypted habilitado), abra uma nova janela de consulta e criptografe as colunas **SSN** e **Salário** executando as consultas abaixo.

    ```sql
    USE [ContosoHR];
    GO

    ALTER TABLE [dbo].[Employees]
    ALTER COLUMN [SSN] [char] (11) COLLATE Latin1_General_BIN2
    ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
    WITH
    (ONLINE = ON);

    ALTER TABLE [dbo].[Employees]
    ALTER COLUMN [Salary] [money]
    ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
    WITH
    (ONLINE = ON);

    ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
    ```

    > [!NOTE]
    > Observe a instrução ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE para limpar o cache do plano de consulta para o banco de dados no script acima. Depois que você tiver alterado a tabela, será necessário limpar os planos para todos os lotes e procedimentos armazenados que acessam a tabela, para atualizar as informações de criptografia de parâmetros. 

1. Para verificar se agora as colunas **SSN** e **Salário** estão criptografadas, abra uma nova janela de consulta na instância do SSMS **sem** Always Encrypted habilitado para a conexão de banco de dados e execute a instrução abaixo. A janela de consulta deve retornar valores criptografados nas colunas **SSN** e **Salário**. Se você executar a mesma consulta usando a instância do SSMS com o Always Encrypted habilitado, você deve ver os dados descriptografados.

    ```sql
    SELECT * FROM [dbo].[Employees];
    ```

## <a name="step-7-run-rich-queries-against-encrypted-columns"></a>Etapa 7: Executar consultas avançadas em colunas criptografadas

Agora você pode executar consultas avançadas nas colunas criptografadas. Algum processamento de consulta será executado dentro de seu enclave do lado do servidor. 

1. Na instância do SSMS **com** Always Encrypted habilitado, verifique se a parametrização de Always Encrypted também está habilitada.
    1. Selecione **Ferramentas** no menu principal do SSMS.
    2. Selecione **Opções...** .
    3. Navegue para **Execução da Consulta** > **SQL Server** > **Avançado**.
    4. A opção **Habilitar Parametrização do Always Encrypted** precisa estar marcada.
    5. Selecione **OK**.
2. Abra uma nova janela de consulta, cole e execute a consulta abaixo. A consulta deve retornar valores de texto sem formatação e linhas que atendem a critérios de pesquisa especificados.

    ```sql
    DECLARE @SSNPattern [char](11) = '%6818';
    DECLARE @MinSalary [money] = $1000;
    SELECT * FROM [dbo].[Employees]
    WHERE SSN LIKE @SSNPattern AND [Salary] >= @MinSalary;
    ```

3. Tente fazer a mesma consulta novamente na instância do SSMS que não tem o Always Encrypted habilitado e observe a falha que ocorre.

## <a name="next-steps"></a>Próximas etapas
Depois de concluir este tutorial, você pode ir para um dos seguintes tutoriais:
- [Tutorial: Desenvolver um aplicativo .NET Framework usando o Always Encrypted com enclaves seguros](tutorial-always-encrypted-enclaves-develop-net-framework-apps.md)
- [Tutorial: Como criar e usar índices em colunas habilitadas para enclave com criptografia aleatória](./tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md)

## <a name="see-also"></a>Consulte Também
- [Configurar o tipo de enclave para a Opção de Configuração de Servidor Always Encrypted](../../database-engine/configure-windows/configure-column-encryption-enclave-type.md)
- [Provisionar chaves habilitadas para enclave](encryption/always-encrypted-enclaves-provision-keys.md)
- [Configurar criptografia de coluna in-loco com Transact-SQL](encryption/always-encrypted-enclaves-configure-encryption-tsql.md)
- [Consultar colunas usando o Always Encrypted com enclaves seguros](encryption/always-encrypted-enclaves-query-columns.md)