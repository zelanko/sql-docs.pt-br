---
title: Configurar o Gerenciamento Extensível de Chave do TDE (Transparent Data Encryption) com o Azure Key Vault
description: Instalar e configurar o Conector do SQL Server para o Azure Key Vault.
ms.custom: seo-lt-2019
ms.date: 08/12/2020
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Extensible Key Management
- EKM, with key vault setup
- SQL Server Connector, setup
- SQL Server Connector
ms.assetid: c1f29c27-5168-48cb-b649-7029e4816906
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: e5b18c46f602d24339c092b8f3e622b2a915baeb
ms.sourcegitcommit: f7c9e562d6048f89d203d71685ba86f127d8d241
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/12/2020
ms.locfileid: "90042860"
---
# <a name="set-up-sql-server-tde-extensible-key-management-by-using-azure-key-vault"></a>Configurar o Gerenciamento Extensível de Chave do TDE do SQL Server usando o Azure Key Vault

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

Neste artigo, você instala e configura o Conector [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para o Azure Key Vault.  
  
## <a name="prerequisites"></a>Pré-requisitos

Antes de começar a usar o Azure Key Vault com sua instância do SQL Server, verifique se você atende aos seguintes pré-requisitos:  
  
- Você precisa ter uma assinatura do Azure.
  
- Instale o [Azure PowerShell, versão 5.2.0 ou posterior](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).  

- Crie uma instância do Azure AD (Azure Active Directory).

- Familiarize-se com os princípios de armazenamento do EKM (Gerenciamento Extensível de Chave) com o Azure Key Vault examinando [EKM com o Azure Key Vault (SQL Server)](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md).  

- Instale a versão do Pacote Redistribuível do C++ para Visual Studio baseada na versão do SQL Server que está sendo executada:
  
  Versão do SQL Server  | Versão do Pacote Redistribuível do Visual Studio C++
  ---------|---------
  2008, 2008 R2, 2012, 2014 | [Pacotes Redistribuíveis do Visual C++ para o Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784)
  2016 | [Pacotes Redistribuíveis do Visual C++ para Visual Studio 2015](https://www.microsoft.com/download/details.aspx?id=48145)

## <a name="step-1-set-up-an-azure-ad-service-principal"></a>Etapa 1: Configurar uma entidade de serviço do Azure AD

Para conceder à sua instância do SQL Server permissões de acesso ao Azure Key Vault, você precisará de uma conta de entidade de serviço no Azure AD.  
  
1. Entre no [portal do Azure](https://ms.portal.azure.com/) e siga uma destas etapas:

    - Selecione o botão **Azure Active Directory**.

      ![Captura de tela do painel "serviços do Azure"](../../../relational-databases/security/encryption/media/ekm/ekm-part1-login-portal.png)

    - Selecione **Mais serviços** e, na caixa **Todos os serviços**, digite **Azure Active Directory**.

      ![Captura de tela do painel "Todos os serviços do Azure"](../../../relational-databases/security/encryption/media/ekm/ekm-part1-select-aad.png)  

1. Registre um aplicativo no Azure Active Directory fazendo o seguinte. (Para obter instruções passo a passo detalhadas, confira a seção "Obter uma identidade para o aplicativo" da [postagem no blog do Azure Key Vault](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/).)

    a. No painel **Visão geral do Azure Active Directory**, selecione **Registros de aplicativo**.

    ![Captura de tela do painel "Visão geral do Azure Active Directory"](../../../relational-databases/security/encryption/media/ekm/ekm-part1-aad-app-register.png)

    b. No painel **Registros de aplicativo**, selecione **Novo registro**.

    ![Captura de tela do painel "Registros de aplicativo"](../../../relational-databases/security/encryption/media/ekm/ekm-part1-aad-new-registration.png)  

    c. No painel **Registrar um aplicativo**, insira o nome do aplicativo voltado para o usuário e selecione **Registrar**.

    ![Captura de tela do painel "Registrar um aplicativo"](../../../relational-databases/security/encryption/media/ekm/ekm-part1-aad-register.png)

    d. No painel esquerdo, selecione **Certificados e segredos** e escolha **Novo segredo do cliente**.

    ![Captura de tela do painel "Certificados e segredos"](../../../relational-databases/security/encryption/media/ekm/ekm-part1-aad-certs-secrets.png)  

    e. Em **Adicionar um segredo do cliente**, insira uma descrição e uma validade apropriada e selecione **Adicionar**.

    ![Captura de tela da seção "Adicionar um segredo do cliente"](../../../relational-databases/security/encryption/media/ekm/ekm-part1-aad-add-secret.png)  

    f. No painel **Certificados e segredos**, em **"Valor"** , selecione o botão **Copiar** ao lado do valor do segredo do cliente a ser usado para criar uma chave assimétrica no SQL Server.

    ![Captura de tela do painel "Certificados e segredos"](../../../relational-databases/security/encryption/media/ekm/ekm-part1-aad-new-secret.png)  

    g. No painel esquerdo, selecione **Visão geral** e, na caixa **ID do aplicativo (cliente)** , copie o valor a ser usado para criar uma chave assimétrica no SQL Server.

    ![Captura de tela do valor "ID do Aplicativo (cliente)" no painel Visão geral](../../../relational-databases/security/encryption/media/ekm/ekm-part1-aad-appid.png)  

## <a name="step-2-create-a-key-vault"></a>Etapa 2: Criar um cofre de chave

Selecione o método que deseja usar para criar um cofre de chaves.

## <a name="azure-portal"></a>[Azure portal](#tab/portal)

### <a name="create-a-key-vault-by-using-the-azure-portal"></a>Criar um cofre de chaves usando o portal do Azure

Você pode usar o portal do Azure para criar o cofre de chaves e, então, adicionar uma entidade de segurança do Azure AD a ele.

1. Crie um grupos de recursos.

   Todos os recursos do Azure criados usando o portal do Azure devem estar contidos em um grupo de recursos, que você cria para alojar seu cofre de chaves. O nome do recurso neste exemplo é *ContosoDevRG*. Escolha seu grupo de recursos e o nome do cofre de chaves, pois todos os nomes de cofre de chaves devem ser globalmente exclusivos.

   No painel **Criar um grupo de recursos**, em **Detalhes do projeto**, insira os valores e selecione **Examinar + criar**.

      ![Captura de tela do painel "Criar um grupo de recursos"](../../../relational-databases/security/encryption/media/ekm/ekm-part2-create-resource-group.png)  

1. Crie um cofre da chave.

    No painel **Criar cofre de chaves**, selecione a guia **Básico**, insira os valores apropriados e selecione **Examinar + criar**.

    ![Captura de tela do painel "Criar cofre de chaves"](../../../relational-databases/security/encryption/media/ekm/ekm-part2-create-key-vault.png)  

1. No painel **Políticas de acesso**, selecione **Adicionar Política de Acesso**.

    ![Captura de tela do link "Adicionar Política de Acesso" no painel "Políticas de acesso"](../../../relational-databases/security/encryption/media/ekm/ekm-part2-add-access-policy.png)  

1. No painel **Adicionar política de acesso**, faça o seguinte:
  
    a. Na lista suspensa **Configurar do modelo (opcional)** , selecione **Gerenciamento de Chaves**.

    b. No painel esquerdo, selecione a guia **Permissões de chave** e verifique se as caixas de seleção **Obter**, **Listar**, **Decodificar Chave** e **Encapsular Chave** estão marcadas.

    c. Selecione **Adicionar**.

    ![Captura de tela do painel "Adicionar política de acesso"](../../../relational-databases/security/encryption/media/ekm/ekm-part2-access-policy-permission.png)

1. No painel esquerdo, selecione a guia **Selecionar entidade de segurança** e faça o seguinte:

    a. No painel **Entidade de segurança**, em **Selecionar**, comece a digitar o nome do aplicativo do Azure AD e, na lista de resultados, selecione o aplicativo que deseja adicionar.

    ![Captura de tela da caixa de pesquisa do aplicativo no painel Entidade de segurança](../../../relational-databases/security/encryption/media/ekm/ekm-part2-select-principal.png)  

    b. Selecione o botão **Selecionar** para adicionar a entidade de segurança ao cofre de chaves.

    ![Captura de tela do botão Selecionar no painel Entidade de segurança](../../../relational-databases/security/encryption/media/ekm/ekm-part2-save-principal.png)

    c. No canto inferior esquerdo, selecione **Adicionar** para salvar as alterações.

    ![Captura de tela do botão Adicionar no painel "Adicionar política de acesso"](../../../relational-databases/security/encryption/media/ekm/ekm-part2-select-principal-new.png)

1. No painel **Key Vault**, selecione **Chaves** e insira um nome para o cofre de chaves. Use o tipo de chave **RSA** e o tamanho da chave RSA **2048**. Defina as datas de ativação e término conforme apropriado e defina **Habilitado?** como **Sim**.

   ![Captura de tela do painel "Criar Chave"](../../../relational-databases/security/encryption/media/ekm/ekm-part2-add-key-vault-key.png)  

1. No painel **Políticas de acesso**, selecione **Salvar**.
  
   ![Captura de tela do botão Salvar no painel "Adicionar política de acesso"](../../../relational-databases/security/encryption/media/ekm/ekm-part2-save-access-policy.png)  

## <a name="powershell"></a>[PowerShell](#tab/powershell)

### <a name="create-a-key-vault-and-key-by-using-powershell"></a>Criar um cofre de chaves e uma chave usando o PowerShell

O cofre de chaves e a chave criados aqui são usados pelo Mecanismo de Banco de Dados do SQL Server para proteção da chave de criptografia.  
  
> [!IMPORTANT]
> A assinatura na qual o cofre de chaves é criado deve estar na mesma instância padrão do Azure AD em que a entidade de serviço do Azure AD foi criada. Se quiser usar uma instância do Azure AD diferente da instância padrão para criar uma entidade de serviço para o Conector do SQL Server, você precisará alterar a instância padrão do Azure AD em sua conta do Azure antes de criar o cofre de chaves. Para saber como alterar a instância padrão do Azure AD para aquela que deseja usar, confira a seção "Perguntas frequentes" em [Manutenção e solução de problemas do Conector do SQL Server](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixB).  
  
1. Instale e entre no [Azure PowerShell 5.2.0 ou posterior](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) usando o seguinte comando:  
  
    ```powershell  
    Connect-AzAccount  
    ```  
  
    A instrução retorna:  
  
    ```console  
    Environment           : AzureCloud  
    Account               : <account_name>  
    TenantId              : <tenant_id>  
    SubscriptionId        : <subscription_id>  
    CurrentStorageAccount :  
    ```  
  
    > [!NOTE]  
    > Se tiver várias assinaturas e quiser especificar uma delas para usar para o cofre, execute `Get-AzSubscription` para ver as assinaturas e `Select-AzSubscription` para escolher a assinatura correta. Caso contrário, o PowerShell selecionará um para você por padrão.  
  
1. Crie um grupos de recursos.

    Todos os recursos do Azure criados usando o PowerShell devem estar contidos em um grupo de recursos, que você cria para alojar seu cofre de chaves. O nome do recurso neste exemplo é *ContosoDevRG*. Escolha seu grupo de recursos e o nome do cofre de chaves, pois todos os nomes de cofre de chaves devem ser globalmente exclusivos.  
  
    ```powershell  
    New-AzResourceGroup -Name ContosoDevRG -Location 'East Asia'  
    ```  
  
    A instrução retorna:  
  
    ```console
    ResourceGroupName: ContosoDevRG  
    Location         : eastasia  
    ProvisioningState: Succeeded  
    Tags             :
    ResourceId       : /subscriptions/<subscription_id>/  
                        resourceGroups/ContosoDevRG  
    ```  
  
    > [!NOTE]
    > Para o parâmetro `-Location`, use o comando `Get-AzureLocation` para identificar como especificar uma localização diferente do que está neste exemplo. Se precisar de mais informações, digite **Get-Help Get-AzureLocation**.  
  
1. Crie um cofre da chave.

    O cmdlet `New-AzKeyVault` requer um nome de grupo de recursos, um nome de cofre de chaves e uma localização geográfica. Por exemplo, para um cofre de chaves chamado `ContosoEKMKeyVault`, execute:  
  
    ```powershell  
    New-AzKeyVault -VaultName 'ContosoEKMKeyVault' `  
       -ResourceGroupName 'ContosoDevRG' -Location 'East Asia'  
    ```  
  
    Registre o nome do seu cofre de chaves.  
  
    A instrução retorna:

    ```console
    Vault Name                       : ContosoEKMKeyVault  
    Resource Group Name              : ContosoDevRG  
    Location                         : East Asia  
    ResourceId                       : /subscriptions/<subscription_id>/  
                                        resourceGroups/ContosoDevRG/providers/  
                                        Microsoft/KeyVault/vaults/ContosoEKMKeyVault  
    Vault URI: https://ContosoEKMKeyVault.vault.azure.net  
    Tenant ID                        : <tenant_id>  
    SKU                              : Standard  
    Enabled For Deployment?          : False  
    Enabled For Template Deployment? : False  
    Enabled For Disk Encryption?     : False  
    Access Policies                  :  
             Tenant ID              : <tenant_id>  
             Object ID              : <object_id>  
             Application ID         :
             Display Name           : <display_name>  
             Permissions to Keys    : get, create, delete, list, update, import,
                                      backup, restore  
             Permissions to Secrets : all  
    Tags                             :  
    ```  
  
1. Conceda permissões à entidade de serviço do Azure AD para acessar o Azure Key Vault.  
  
    Você pode autorizar outros usuários e aplicativos a usarem o cofre de chaves.  Para nosso exemplo, vamos usar a entidade de serviço criada na [Etapa 1: Configurar uma entidade de serviço do Azure AD](#step-1-set-up-an-azure-ad-service-principal) para autorizar a instância de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
    > [!IMPORTANT]
    > A entidade de serviço do Azure AD deve ter, pelo menos, as permissões *get*, *list*,*wrapKey*, and *unwrapKey* para o cofre de chaves.  
  
    Conforme mostrado no seguinte comando, você usa a **ID do Aplicativo (Cliente)** da [Etapa 1: Configurar uma entidade de serviço do Azure AD](#step-1-set-up-an-azure-ad-service-principal) para o parâmetro `ServicePrincipalName`. `Set-AzKeyVaultAccessPolicy` será executado silenciosamente sem saída se for executado com êxito.  
  
    ```powershell  
    Set-AzKeyVaultAccessPolicy -VaultName 'ContosoEKMKeyVault' `  
      -ServicePrincipalName 9A57CBC5-4C4C-40E2-B517-EA677 `  
      -PermissionsToKeys get, list, wrapKey, unwrapKey  
    ```  
  
    Chamar o cmdlet `Get-AzKeyVault` para confirmar as permissões. Na saída da instrução em `Access Policies`, você verá o nome do aplicativo do Azure AD listado como outro locatário que tem acesso a este cofre de chaves.  
  
1. Gere uma chave assimétrica no cofre de chaves. Você pode fazer isso de duas maneiras: importar uma chave existente ou criar uma.  

     > [!NOTE]
     > O SQL Server dá suporte apenas a chaves RSA de 2048 bits.

### <a name="best-practices"></a>Práticas recomendadas

Para garantir a recuperação rápida da chave e poder acessar seus dados fora do Azure, recomendamos as seguintes melhores práticas:

- Crie a chave de criptografia localmente, em um dispositivo HSM (módulo de segurança de hardware) local. Certifique-se de usar uma chave RSA 2048 assimétrica, para que ela seja compatível com o SQL Server.
- Importe a chave de criptografia para o Azure Key Vault. Esse processo é descrito nas seções a seguir.
- Antes de usar a chave em seu Azure Key Vault pela primeira vez, faça um backup da chave do Azure Key Vault. Para obter mais informações, confira o comando [Backup-AzureKeyVaultKey](/sql/relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault).
- Sempre que fizer qualquer alteração na chave (por exemplo, adicionar ACLs, marcas ou atributos de chave), faça outro backup da chave do Azure Key Vault.

  > [!NOTE]
  > Fazer backup de uma chave é uma operação de chave do Azure Key Vault que retorna um arquivo que pode ser salvo em qualquer lugar.

### <a name="types-of-keys"></a>Tipos de chaves

Você pode gerar dois tipos de chaves no Azure Key Vault que funcionarão com o SQL Server. Os dois tipos são chaves RSA de 2048 bits assimétricas.  
  
- **Protegida por software**: Processado no software e criptografado em repouso. Operações em chaves protegidas por software ocorrem nas máquinas virtuais do Azure. Recomendamos esse tipo para chaves que não são usadas em uma implantação de produção.  

- **Protegida por HSM:** criada e protegida por um módulo de segurança de hardware para proporcionar mais segurança. O custo é de cerca de US$ 1 por versão de chave.  
  
    > [!IMPORTANT]
    > Para o Conector do SQL Server, use somente os caracteres a-z, A-Z, 0-9 e hifens (-), com um limite de 26 caracteres.
    > Diferentes versões de chave com o mesmo nome de chave no Azure Key Vault não funcionam com o Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para girar uma chave do Azure Key Vault que está sendo usada por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], confira as etapas de Substituição de chave na seção "A. Instruções de Manutenção para o Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]" de [Conector do SQL Server manutenção & solução de problemas](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md).  

### <a name="import-an-existing-key"></a>Importar uma chave existente
  
Se tiver uma chave protegida por software RSA de 2048 bits, você poderá carregá-la no Azure Key Vault. Por exemplo, se você tem um arquivo PFX salvo em sua unidade `C:\\` em um arquivo chamado *softkey.pfx* e deseja carregá-lo para o Azure Key Vault, execute o seguinte comando para definir a variável `securepfxpwd` com uma senha de `12987553` para o arquivo PFX:  
  
``` powershell  
$securepfxpwd = ConvertTo-SecureString -String '12987553' `  
  -AsPlainText -Force  
```  

Em seguida, execute o seguinte comando para importar a chave do arquivo PFX, que a protege pelo hardware (recomendado) no serviço do Key Vault:  
  
``` powershell  
    Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' `  
      -Name 'ContosoFirstKey' -KeyFilePath 'c:\softkey.pfx' `  
      -KeyFilePassword $securepfxpwd $securepfxpwd  -Destination 'HSM'  
```  

> [!CAUTION]
> É altamente recomendável importar a chave assimétrica para cenários de produção, pois fazer isso permite que o administrador garanta a chave em um sistema de caução de chaves. Se a chave assimétrica for criada no cofre, ela não poderá ser mantida em garantia porque a chave privada nunca pode deixar o cofre. Chaves usadas para proteger dados críticos devem ser mantidas em garantia. A perda de uma chave assimétrica resultará em perda permanente de dados.  

### <a name="create-a-new-key"></a>Criar uma nova chave

Como alternativa, você pode criar uma chave de criptografia diretamente no Azure Key Vault e protegê-la por software ou por HSM.  Neste exemplo, vamos criar uma chave protegida por software usando o cmdlet `Add-AzureKeyVaultKey`:  

``` powershell  
Add-AzureKeyVaultKey -VaultName 'ContosoEKMKeyVault' `  
  -Name 'ContosoRSAKey0' -Destination 'Software'  
```  
  
A instrução retorna:  
  
```console
Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes  
Key        :  {"kid":"https:contosoekmkeyvault.azure.net/keys/  
                ContosoRSAKey0/<guid>","dty":"RSA:,"key_ops": ...  
VaultName  : contosodevkeyvault  
Name       : contosoRSAKey0  
Version    : <guid>  
Id         : https://contosoekmkeyvault.vault.azure.net:443/  
              keys/ContosoRSAKey0/<guid>  
```  

> [!IMPORTANT]
> O cofre de chaves dá suporte a várias versões da mesma chave nomeada, mas as chaves usadas pelo Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não devem estar com controle de versão nem revertidas. Se o administrador deseja distribuir a chave usada para criptografia [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], uma chave com um nome diferente deve ser criada no cofre de chaves e usada para criptografar DEK.  

---

## <a name="step-3-install-the-ssnoversion-connector"></a>Etapa 3: instalar o Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]

Baixe o Conector do SQL Server no [Centro de Download da Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=521700). O download deve ser feito pelo administrador do computador [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  

> [!NOTE]
> - O Conector do SQL Server versões 1.0.0.440 e anteriores foram substituído e não têm mais suporte em ambientes de produção e usando as instruções na página [Manutenção e Solução de Problemas do Conector do SQL Server](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md) em [Atualização do Conector do SQL Server](sql-server-connector-maintenance-troubleshooting.md#upgrade-of--connector).
> - Da versão 1.0.3.0 em diante, o Conector do SQL Server relata mensagens de erro relevantes para os logs de eventos do Windows para solução de problemas.
> - Da versão 1.0.4.0 e m diante, há suporte para nuvens privadas do Azure, incluindo o Azure China, o Azure Alemanha e o Azure Government.
> - Há uma alteração da falha na versão 1.0.5.0, em termos do algoritmo de impressão digital. Você pode enfrentar falhas de restauração do banco de dados após atualizar para a 1.0.5.0. Para obter mais informações, confira o [artigo KB 447099](https://support.microsoft.com/help/4470999/db-backup-problems-to-sql-server-connector-for-azure-1-0-5-0).
> - **Da versão 1.0.7.0 em diante, o Conector do SQL Server dá suporte a mensagens de filtragem e lógica de repetição de solicitação de rede.**
  
  ![Captura de tela do assistente de instalação do Conector do SQL Server](../../../relational-databases/security/encryption/media/ekm/ekm-connector-install.png)  
  
Por padrão, o Conector é instalado em C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault. Esse local pode ser alterado durante a instalação. Se alterá-lo, ajuste os scripts na próxima seção.  
  
Não há interface para o Conector, mas se ele for instalado com êxito, *Microsoft.AzureKeyVaultService.EKM.dll* estará instalado no computador. Esse assembly é o DLL do provedor EKM criptográfico que precisa ser registrado com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando a instrução `CREATE CRYPTOGRAPHIC PROVIDER`.  
  
A instalação do Conector do SQL Server também permite que você baixe opcionalmente os scripts de exemplo para criptografia do SQL Server.  
  
Para ver explicações de códigos de erro, definições de configuração ou tarefas de manutenção do SQL Server Connector, confira:  
  
- [A. Instruções de manutenção do Conector do SQL Server](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixA)  
- [C. Explicações de código de erro do Conector do SQL Server](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixC)  
  
## <a name="step-4-configure-ssnoversion"></a>Etapa 4: configurar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  

Confira [B. Perguntas frequentes](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixB) para ver uma observação sobre os níveis de permissão mínimos necessários para cada ação nesta seção.  
  
1. Execute *sqlcmd.exe* ou abra o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Studio.  
  
1. Configure [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para usar o EKM executando o seguinte script do [!INCLUDE[tsql](../../../includes/tsql-md.md)]:  
  
    ```sql  
    -- Enable advanced options.  
    USE master;  
    GO  

    EXEC sp_configure 'show advanced options', 1;  
    GO  
    RECONFIGURE;  
    GO  

    -- Enable EKM provider  
    EXEC sp_configure 'EKM provider enabled', 1;  
    GO  
    RECONFIGURE;  
    ```  
  
1. Registre o Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como um provedor EKM com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
    Crie um provedor criptográfico usando o Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], que é um provedor EKM do Azure Key Vault.
    Neste exemplo, o nome do provedor é `AzureKeyVault_EKM`.  
  
    ```sql  
    CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM
    FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';  
    GO  
    ```  

    > [!NOTE]
    > O tamanho do caminho do arquivo não pode ultrapassar 256 caracteres.  
  
1. Configure uma credencial do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para um logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para usar o cofre de chaves.  
  
    Uma credencial deve ser adicionada a cada logon que executará a criptografia usando uma chave do cofre de chaves. Isso pode incluir:  
  
    - Um logon do administrador [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que usa o cofre de chaves para instalar e gerenciar cenários de criptografia do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
    - Outros logons do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que podem habilitar o TDE ou outros recursos de criptografia do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
    Há um mapeamento um para um entre as credenciais e logons. Ou seja, cada logon deve ter uma credencial exclusiva.  
  
    Modifique o script [!INCLUDE[tsql](../../../includes/tsql-md.md)] abaixo das seguintes maneiras:  
  
    - Edite o argumento `IDENTITY` (`ContosoEKMKeyVault`) para apontar para o Azure Key Vault.
      - Se estiver usando o *Azure global*, substitua o argumento `IDENTITY` pelo nome do seu Azure Key Vault da [Etapa 2: Criar um cofre de chaves](#step-2-create-a-key-vault).
      - Se estiver usando uma *nuvem do Azure privada*, (por exemplo, o Azure Government, o Azure China 21Vianet ou o Azure Alemanha), substitua o argumento `IDENTITY` pelo URI do Cofre que é retornado na etapa 3 da seção [Criar um cofre de chaves e uma chave usando o PowerShell](#create-a-key-vault-and-key-by-using-powershell). Não inclua “https://” no URI do Cofre.
    - Substitua a primeira parte do argumento `SECRET` pela ID do Cliente do Azure Active Directory da [Etapa 1: Configurar uma entidade de serviço do Azure AD](#step-1-set-up-an-azure-ad-service-principal). Nesse exemplo, a **ID do Cliente** é `9A57CBC54C4C40E2B517EA677E0EFA00`.  
  
      > [!IMPORTANT]
      > Remova os hifens da ID do Aplicativo (Cliente).  
  
    - Conclua a segunda parte do argumento `SECRET` com o **Segredo do Cliente** da [Etapa 1: Configurar uma entidade de serviço do Azure AD](#step-1-set-up-an-azure-ad-service-principal).  Neste exemplo, o Segredo do Cliente é `08:k?[:XEZFxcwIPvVVZhTjHWXm7w1?m`. A cadeia de caracteres final do argumento `SECRET` será uma sequência longa de letras e números, sem hifens.  
  
    ```sql  
    USE master;  
    CREATE CREDENTIAL sysadmin_ekm_cred
        WITH IDENTITY = 'ContosoEKMKeyVault',                            -- for public Azure
        -- WITH IDENTITY = 'ContosoEKMKeyVault.vault.usgovcloudapi.net', -- for Azure Government
        -- WITH IDENTITY = 'ContosoEKMKeyVault.vault.azure.cn',          -- for Azure China 21Vianet
        -- WITH IDENTITY = 'ContosoEKMKeyVault.vault.microsoftazure.de', -- for Azure Germany
               --<----Application (Client) ID ---><--Azure AD app (Client) ID secret-->
        SECRET = '9A57CBC54C4C40E2B517EA677E0EFA0008:k?[:XEZFxcwIPvVVZhTjHWXm7w1?m'
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM;  
  
    -- Add the credential to the SQL Server administrator's domain login
    ALTER LOGIN [<domain>\<login>]  
    ADD CREDENTIAL sysadmin_ekm_cred;  
    ```  
  
    Para obter um exemplo do uso de variáveis para o argumento `CREATE CREDENTIAL` e remover programaticamente os hifens da ID do Cliente, confira [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md).  
  
1. Abra sua chave do Azure Key Vault em sua instância do SQL Server.  

    Quer tenha criado uma chave ou importado uma chave assimétrica, conforme descrito na [Etapa 2: Crie um cofre de chaves](#step-2-create-a-key-vault), você precisará abrir a chave. Abra a chave fornecendo o nome dela no script [!INCLUDE[tsql](../../../includes/tsql-md.md)] a seguir.  
  
    - Substitua `EKMSampleASYKey` com o nome que deseja que a chave tenha em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
    - Substitua `ContosoRSAKey0` pelo nome da chave no Azure Key Vault.  
  
    ```sql  
    CREATE ASYMMETRIC KEY EKMSampleASYKey
    FROM PROVIDER [AzureKeyVault_EKM]  
    WITH PROVIDER_KEY_NAME = 'ContosoRSAKey0',  
    CREATION_DISPOSITION = OPEN_EXISTING;  
    ```  

1. Crie um logon usando a chave assimétrica no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que você criou na etapa anterior.

     ```sql  
    --Create a Login that will associate the asymmetric key to this login
    CREATE LOGIN TDE_Login
    FROM ASYMMETRIC KEY EKMSampleASYKey;
    ```  

1. Crie um logon da chave assimétrica no SQL Server. Remova o mapeamento de credenciais da Etapa 4: Configurar SQL Server para que as credenciais possam ser mapeadas para o novo logon.

     ```sql  
    --Now drop the credential mapping from the original association
    ALTER LOGIN [<domain>\<login>]
    DROP CREDENTIAL sysadmin_ekm_cred;
    ```

1. Altere o novo logon e mapeie as credenciais do EKM para o novo logon.

     ```sql  
    --Now drop the credential mapping from the original association
    ALTER LOGIN TDE_Login
    ADD CREDENTIAL sysadmin_ekm_cred;
    ```  

1. Crie um banco de dados de teste que será criptografado com a chave do Azure Key Vault.

     ```sql
    --Create a test database that will be encrypted with the Azure key vault key
    CREATE DATABASE TestTDE
    ```  

1. Crie uma chave de criptografia do banco de dados usando a chave assimétrica (EKMSampleASYKey).

    ```sql  
    --Create an ENCRYPTION KEY using the ASYMMETRIC KEY (EKMSampleASYKey)
    CREATE DATABASE ENCRYPTION KEY
    WITH ALGORITHM = AES_256
    ENCRYPTION BY SERVER ASYMMETRIC KEY EKMSampleASYKey;
    ```
  
1. Criptografe o banco de dados de teste. Habilite o TDE definindo ENCRYPTION ON.

     ```sql  
    --Enable TDE by setting ENCRYPTION ON
    ALTER DATABASE TestTDE
    SET ENCRYPTION ON;  
     ```  

1. Limpe os objetos de teste. Exclua todos os objetos criados neste script de teste.

    ```sql  
    -- CLEAN UP
    USE Master
    ALTER DATABASE [TestTDE] SET SINGLE_USER WITH ROLLBACK IMMEDIATE
    DROP DATABASE [TestTDE]

    ALTER LOGIN [TDE_Login] DROP CREDENTIAL [sysadmin_ekm_cred]
    DROP LOGIN [TDE_Login]

    DROP CREDENTIAL [sysadmin_ekm_cred]  

    USE MASTER
    DROP ASYMMETRIC KEY [EKMSampleASYKey]
    DROP CRYPTOGRAPHIC PROVIDER [AzureKeyVault_EKM]
    ```  

Para ver scripts de exemplo, confira o blog em [Transparent Data Encryption e Gerenciamento Extensível de Chaves do SQL Server com o Azure Key Vault](https://techcommunity.microsoft.com/t5/sql-server/intro-sql-server-transparent-data-encryption-and-extensible-key/ba-p/1427549).

## <a name="next-steps"></a>Próximas etapas  
  
Agora que você concluiu a configuração básica, confira [Usar o Conector do SQL Server com recursos de criptografia do SQL](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md).
  
## <a name="see-also"></a>Confira também  

- [Gerenciamento Extensível de Chave com o Azure Key Vault](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)
- [Manutenção e solução de problemas do Conector do SQL Server](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)
