---
title: Implantar o Serviço Guardião de Host
description: Implante o Serviço Guardião de Host para Always Encrypted com o enclaves seguros.
ms.custom: ''
ms.date: 11/15/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: rpsqrd
ms.author: ryanpu
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6794f5fd57d1c89e7c1989e79b5072a8c15cf43e
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "74320049"
---
# <a name="deploy-the-host-guardian-service-for-ssnoversion-md"></a>Implantar o Serviço Guardião de Host para [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]

[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

Este artigo descreve como implantar o HGS (Serviço Guardião de Host) como um serviço de atestado para [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)].
Antes de começar, leia o artigo [Planejar o atestado do Serviço Guardião de Host](./always-encrypted-enclaves-host-guardian-service-plan.md) para obter uma lista completa de pré-requisitos e diretrizes arquitetônicas.

## <a name="step-1-set-up-the-first-hgs-computer"></a>Etapa 1: Configurar o primeiro computador HGS

O HGS (Serviço Guardião de Host) é executado como um serviço clusterizado em um ou mais computadores.
Nesta etapa, você vai configurar um novo cluster do HGS no primeiro computador.
Se você já tiver um cluster do HGS e estiver adicionando outros computadores a ele para alta disponibilidade, pule para [Etapa 2: Adicionar mais computadores do HGS ao cluster](#step-2-add-more-hgs-computers-to-the-cluster).

Antes de começar, garanta que o computador que você está usando esteja executando o Windows Server 2019 Standard ou Datacenter Edition, se você tem privilégios de administrador local e se o computador ainda não ingressou em um domínio do Active Directory.

1. Entre no primeiro computador do HGS como administrador local e abra um console elevado do Windows PowerShell. Execute o comando a seguir para instalar a função do Serviço Guardião de Host. O computador será reiniciado automaticamente para aplicar as alterações.

    ```powershell
    Install-WindowsFeature -Name HostGuardianServiceRole -IncludeManagementTools -Restart
    ```

2. Após a reinicialização do computador do HGS, execute os seguintes comandos em um console do Windows PowerShell com privilégios elevados para instalar a nova floresta do Active Directory:

    ```powershell
    # Select the name for your new Active Directory root domain.
    # Make sure the name does not conflict with, and is not subordinate to, any existing domains on your network.
    $HGSDomainName = 'bastion.local'

    # Specify a Directory Services Restore Mode password that can be used to recover your domain in safe mode.
    # This password is not, and will not change, your admin account password.
    # Save this password somewhere safe and include it in your disaster recovery plan.
    $DSRMPassword = Read-Host -AsSecureString -Prompt "Directory Services Restore Mode Password"

    Install-HgsServer -HgsDomainName $HgsDomainName -SafeModeAdministratorPassword $DSRMPassword -Restart
    ```

    O computador HGS será reiniciado novamente para concluir a configuração da floresta do Active Directory. Na próxima vez que você fizer logon, sua conta do administrador será uma conta de administrador de domínio. É recomendável ler o [documento de Operações do Active Directory Domain Services](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/component-updates/ad-ds-operations) para saber mais sobre como gerenciar e proteger sua nova floresta.

3. Em seguida, você vai configurar o cluster HGS e instalar o serviço de atestado executando o seguinte comando em um console do Windows PowerShell com privilégios elevados:

    ```powershell
    # Note: the name you provide here will be shared by all HGS nodes and used to point your SQL Server computers to the HGS cluster.
    # For example, if you provide "attsvc" here, a DNS record for "attsvc.yourdomain.com" will be created for every HGS computer.
    Initialize-HgsAttestation -HgsServiceName 'hgs'
    ```

## <a name="step-2-add-more-hgs-computers-to-the-cluster"></a>Etapa 2: Adicionar mais computadores HGS ao cluster

Depois que seu primeiro computador e cluster do HGS estiver configurado, você poderá adicionar outros servidores HGS para fornecer alta disponibilidade.
Se você estiver configurando apenas um servidor HGS (em um ambiente de desenvolvimento/teste, por exemplo), poderá pular para a Etapa 3.

Assim como no primeiro computador HGS, verifique se o computador que você está unindo ao cluster está executando o Windows Server 2019 Standard ou Datacenter Edition, se você tem privilégios de administrador local e se o computador ainda não ingressou em um domínio do Active Directory.

1. Entre no computador como administrador local e abra um console elevado do Windows PowerShell. Execute o comando a seguir para instalar a função do Serviço Guardião de Host. O computador será reiniciado automaticamente para aplicar as alterações.

    ```powershell
    Install-WindowsFeature -Name HostGuardianServiceRole -IncludeManagementTools -Restart
    ```

2. Verifique a configuração do cliente DNS no seu computador para garantir que ele possa resolver o domínio HGS. O comando a seguir deve retornar um endereço IP para o servidor HGS. Se você não puder resolver o domínio HGS, talvez seja necessário atualizar as informações do servidor DNS em seu adaptador de rede para usar o servidor DNS HGS para resolução de nomes.

    ```powershell
    # Change 'bastion.local' to the domain name you specified in Step 1.2
    nslookup bastion.local

    # If it fails, use sconfig.exe, option 8, to set the first HGS computer as your preferred DNS server.
    ```

3. Depois que o computador for reiniciado, execute o seguinte comando em um console elevado do Windows PowerShell para ingressar o computador no domínio do Active Directory criado pelo primeiro servidor HGS. Você precisará de credenciais de administrador de domínio para o domínio do AD para executar esse comando. Quando o comando for concluído, o computador será reiniciado e o computador se tornará um controlador de domínio do Active Directory para o domínio HGS.

    ```powershell
    # Provide the fully qualified HGS domain name
    $HGSDomainName = 'bastion.local'

    # Provide a domain administrator's credential for the HGS domain
    $DomainAdminCred = Get-Credential

    # Specify a Directory Services Restore Mode password that can be used to recover your domain in safe mode.
    # This password is not, and will not change, your admin account password.
    # Save this password somewhere safe and include it in your disaster recovery plan.
    $DSRMPassword = Read-Host -AsSecureString -Prompt "Directory Services Restore Mode Password"

    Install-HgsServer -HgsDomainName $HgsDomainName -HgsDomainCredential $DomainAdminCred -SafeModeAdministratorPassword $DSRMPassword -Restart
    ```

4. Faça logon com credenciais de administrador de domínio após a reinicialização do computador. Abra um console do Windows PowerShell com privilégios elevados e execute os comandos a seguir para configurar o serviço de atestado. Como o serviço de atestado tem reconhecimento de cluster, ele replicará sua configuração de outros membros do cluster. As alterações feitas nas políticas de atestado em qualquer nó do HGS serão aplicadas a todos os outros nós.

    ```powershell
    # Provide the IP address of an existing, initialized HGS server
    # If you are using separate networks for cluster and application traffic, choose an IP address on the cluster network.
    # You can find the IP address of your HGS server by signing in and running "ipconfig /all"
    Initialize-HgsAttestation -HgsServerIPAddress '172.16.10.20'
    ```

5. Repita a etapa 2 para cada computador que você deseja adicionar ao cluster HGS.

## <a name="step-3-configure-a-dns-forwarder-to-your-hgs-cluster"></a>Etapa 3: Configurar um encaminhador de DNS para seu cluster HGS

O HGS executa o próprio servidor DNS, que contém os registros de nome necessários para resolver o serviço de atestado.
Seus computadores SQL Server não poderão resolver esses registros até que você configure o servidor DNS da rede para encaminhar solicitações para os servidores DNS HGS.

O processo para configurar encaminhadores de DNS é específico do fornecedor, portanto, recomendamos entrar em contato com o administrador da rede para obter as diretrizes corretas para sua rede específica.

Se você estiver usando a função de servidor DNS do Windows Server para sua rede corporativa, o administrador de DNS poderá criar um encaminhador condicional para o domínio do HGS para que somente as solicitações para o domínio do HGS sejam encaminhadas.
Por exemplo, se seus servidores HGS usarem o nome de domínio "bastion.local" e tiverem os endereços IP 172.16.10.20, 172.16.10.21 e 172.16.10.22, você poderá executar o seguinte comando no servidor DNS corporativo para configurar um encaminhador condicional:

```powershell
# Tip: make sure to provide every HGS server's IP address
# If you use separate NICs for cluster and application traffic, use the application traffic NIC IP addresses here
Add-DnsServerConditionalForwarderZone -Name 'bastion.local' -ReplicationScope "Forest" -MasterServers "172.16.10.20", "172.16.10.21", "172.16.10.22"
```

## <a name="step-4-configure-the-attestation-service"></a>Etapa 4: Configurar o serviço de atestado

O HGS é compatível com dois modos de atestado: Atestado de TPM para verificação criptográfica da integridade e da identidade de cada computador [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] e atestado de chave de host para verificação simples da identidade do computador [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)].
Se você ainda não tiver selecionado um modo de atestado, confira as informações de atestado no [guia de planejamento](./always-encrypted-enclaves-host-guardian-service-plan.md#attestation-modes) para obter mais detalhes sobre as garantias de segurança e os casos de uso para cada modo.

As etapas nesta seção vão configurar as políticas básicas de atestado para um modo de atestado específico.
Você registrará informações específicas do host na Etapa 4.
Se você precisar alterar seu modo de atestado no futuro, repita as Etapas 3 e 4 usando o modo de atestado desejado.

### <a name="switch-to-tpm-attestation"></a>Alternar para atestado de TPM

Para configurar o atestado de TPM no HGS, você precisará de um computador com acesso à Internet e pelo menos um computador [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] com um chip TPM 2.0 Rev 1.16.

Para configurar o HGS para usar o modo TPM, abra um console do PowerShell com privilégios elevados e execute o seguinte comando:

```powershell
Set-HgsServer -TrustTpm
```

Todos os computadores do HGS no seu cluster agora usarão o modo TPM quando um computador [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] tentar atestar.

Antes de registrar as informações de TPM de seus computadores SQL Server com HGS, você precisa instalar os certificados raiz de EK (chave de endosso) de seus fornecedores de TPM.
Cada TPM físico é configurado de fábrica com uma chave de endosso exclusiva acompanhada por um certificado de chave de endosso que identifica o fabricante.
Esse certificado garante que o TPM seja original.
O HGS verifica o certificado de chave de endosso ao registrar um novo TPM com HGS comparando a cadeia de certificados com uma lista de certificados raiz confiáveis.

A Microsoft publica uma lista de certificados raiz de fornecedor de TPM que você pode importar para o repositório de certificados raiz TPM confiável do HGS.
Se seus computadores SQL Server forem virtualizados, você precisará entrar em contato com seu provedor de serviços de nuvem ou fornecedor de plataforma de virtualização para obter informações sobre como obter a cadeia de certificados para a chave de endosso do TPM virtual.

Para baixar o pacote de certificados raiz do TPM confiável da Microsoft para TPMs físicos, conclua as seguintes etapas:

1. Em um computador com acesso à Internet, baixe o pacote mais recente de certificados raiz do TPM de [https://go.microsoft.com/fwlink/?linkid=2097925](https://go.microsoft.com/fwlink/?linkid=2097925)

2. Verifique a assinatura do arquivo cab para garantir que ele seja autêntico.

    ```powershell
    # Note: replace the path below with the correct one to the file you downloaded in step 1
    Get-AuthenticodeSignature ".\TrustedTpm.cab"
    ```

    > [!WARNING]
    > Não prossiga se a assinatura for inválida e contate o suporte da Microsoft para obter assistência.

3. Expanda o arquivo cab para um novo diretório.

    ```powershell
    mkdir .\TrustedTpmCertificates
    expand.exe -F:* ".\TrustedTpm.cab" ".\TrustedTpmCertificates"
    ```

4. No novo diretório, você verá os diretórios para cada fornecedor do TPM. Você pode excluir os diretórios para fornecedores que você não usa.

5. Copie todo o diretório "TrustedTpmCertificates" para o servidor do HGS.

6. Abra um console do PowerShell com privilégios elevados no servidor do HGS e execute o seguinte comando para importar todos os certificados raiz e intermediários do TPM:

    ```powershell
    # Note: replace the path below with the correct location of the TrustedTpmCertificates folder on your HGS computer
    cd "C:\scratch\TrustedTpmCertificates"
    .\setup.cmd
    ```

7. Repita as Etapas 5 e 6 para cada computador do HGS.

Se você tiver obtido certificados de AC raiz e intermediários do seu OEM, provedor de serviços de nuvem ou fornecedor de plataforma de virtualização, poderá importar diretamente os certificados para o respectivo repositório de certificados do computador local: `TrustedHgs_RootCA` ou `TrustedHgs_IntermediateCA`. Por exemplo, no PowerShell:

```powershell
# Imports MyCustomTpmVendor_Root.cer to the local machine's "TrustedHgs_RootCA" store
Import-Certificate -FilePath ".\MyCustomTpmVendor_Root.cer" -CertStoreLocation "Cert:\LocalMachine\TrustedHgs_RootCA"
```

### <a name="switch-to-host-key-attestation"></a>Mude para o atestado de chave de host

Para usar o atestado de chave de host, execute o seguinte comando em um servidor do HGS em um console do PowerShell com privilégios elevados:

```powershell
Set-HgsServer -TrustHostKey
```

Todos os computadores do HGS no seu cluster agora usarão o modo de chave de host quando um computador [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] tentar atestar.

## <a name="step-5-configure-the-hgs-https-binding"></a>Etapa 5: Configurar a associação HTTPS do HGS

Em uma instalação padrão, o HGS expõe apenas uma associação HTTP (porta 80).
Você pode configurar uma associação HTTPS (porta 443) para criptografar todas as comunicações entre [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] computadores e o HGS.
É recomendável que todas as instâncias de produção do HGS usem uma associação HTTPS.

1. Obtenha um certificado TLS de sua autoridade de certificação usando o nome do serviço HGS totalmente qualificado da Etapa 1.3 como o nome da entidade. Se você não souber o nome do serviço, poderá encontrá-lo executando `Get-HgsServer` em qualquer computador do HGS. Você pode adicionar nomes DNS alternativos à lista de Nomes Alternativos da Entidade caso seus computadores [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] usem um nome DNS diferente para acessar seu cluster HGS (por exemplo, se o HGS estiver atrás de um balanceador de carga de rede com um endereço diferente).

2. No computador do HGS, use [Set-HgsServer](https://docs.microsoft.com/powershell/module/hgsserver/set-hgsserver) para habilitar a associação HTTPS e especifique o certificado TLS obtido na etapa anterior. Se o certificado já estiver instalado no computador no repositório de certificados local, use o seguinte comando para registrá-lo com o HGS:

    ```powershell
    # Note: you'll need to know the thumbprint for your certificate to configure HGS this way
    Set-HgsServer -Http -Https -HttpsCertificateThumbprint "54A043386555EB5118DB367CFE38776F82F4A181"
    ```

    Se você tiver exportado seu certificado (com uma chave privada) para um arquivo PFX protegido por senha, poderá registrá-lo com o HGS executando o seguinte comando:

    ```powershell
    $PFXPassword = Read-Host -AsSecureString -Prompt "PFX Password"
    Set-HgsServer -Http -Https -HttpsCertificatePath "C:\path\to\hgs_tls.pfx" -HttpsCertificatePassword $PFXPassword
    ```

3. Repita as Etapas 1 e 2 para cada computador HGS no cluster. Os certificados TLS não são replicados automaticamente entre os nós do HGS. Além disso, cada computador HGS pode ter o próprio certificado TLS exclusivo, contanto que o assunto corresponda ao nome do serviço HGS.

## <a name="next-steps"></a>Próximas etapas

- [Registrar computadores com o HGS](./always-encrypted-enclaves-host-guardian-service-register.md)
