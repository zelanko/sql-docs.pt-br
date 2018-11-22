---
title: Gerenciamento extensível de chaves do TDE do SQL Server usando o Azure Key Vault – Etapas de Configuração | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2018
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- EKM, with key vault setup
- SQL Server Connector, setup
- SQL Server Connector
ms.assetid: c1f29c27-5168-48cb-b649-7029e4816906
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: 422b8e8d8436430ec01cd92045e951850ee913ff
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51663346"
---
# <a name="sql-server-tde-extensible-key-management-using-azure-key-vault---setup-steps"></a>Gerenciamento extensível de chaves do TDE do SQL Server usando o Azure Key Vault – Etapas de Configuração
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  As etapas a seguir dão um passo a passo da instalação e configuração do Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para o Azure Key Vault.  
  
## <a name="before-you-start"></a>Antes de iniciar  
 Para usar o Cofre de Chaves do Azure com o SQL Server, há alguns pré-requisitos:  
  
-   Você deve ter uma assinatura do Azure  
  
-   Instale a versão mais recente do [Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/), (5.2.0 ou superior).  

-   Criar um locatário do Azure Active Directory  

-   Familiarize-se com as entidades de armazenamento EKM usando o Cofre de Chaves do Azure examinando [Extensible Key Management Using Azure Key Vault &#40;SQL Server&#41; (Gerenciamento extensível de chaves usando o Cofre de Chaves do Azure &#40;SQL Server&#41;)](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md).  

-   Instale a versão apropriada do Visual Studio C++ Redistributable com base na versão do SQL Server que está sendo executada:
  
Versão do SQL Server  |Link de instalação redistribuível    
---------|--------- 
2008, 2008 R2, 2012, 2014 | [Pacotes Visual C++ Redistributable Packages para Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784)    
2016 | [Pacotes Redistribuíveis do Visual C++ para Visual Studio 2015](https://www.microsoft.com/download/details.aspx?id=48145)    
 
  
## <a name="part-i-set-up-an-azure-active-directory-service-principal"></a>Parte I: configurar uma entidade de serviço do Azure Active Directory  
 Para conceder permissões de acesso do SQL Server ao Cofre de Chaves do Azure, você precisará de uma conta de entidade de serviço no AAD (Azure Active Directory).  
  
1.  Vá para o [portal do Azure](https://ms.portal.azure.com/) e entre.  
  
2.  Registre um aplicativo com o Azure Active Directory. Para obter instruções passo a passo detalhadas para registrar um aplicativo, veja a seção **Obter uma identidade para o aplicativo** da [postagem no blog do Cofre de Chaves do Azure](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/).  
  
3.  Copie a **ID do Cliente** e o **Segredo do Cliente** para uma etapa posterior, em que eles serão usados para conceder acesso ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para o seu cofre de chaves.  
  
 ![ekm-client-id](../../../relational-databases/security/encryption/media/ekm-client-id.png "ekm-client-id")  
  
 ![ekm-key-id](../../../relational-databases/security/encryption/media/ekm-key-id.png "ekm-key-id")  
  
## <a name="part-ii-create-a-key-vault-and-key"></a>Parte II: Criar um cofre de chaves e a chave  
 O cofre de chaves e a chave criados aqui serão usados pelo Mecanismo de Banco de Dados do SQL Server para proteção de chave de criptografia.  
  
> [!IMPORTANT]  
>  A assinatura na qual o cofre de chaves é criado deve estar no mesmo Azure Active Directory padrão em que a entidade de serviço do Azure Active Directory foi criada. Se você quiser usar um Active Directory que não seja o Active Directory padrão para criar uma entidade de serviço para o Conector do SQL Server, você deverá alterar o Active Directory padrão em sua conta do Azure antes de criar o cofre de chaves. Para saber como alterar o Active Directory padrão para o que você gostaria de usar, veja as [Perguntas frequentes](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixB)do Conector do SQL Server.  
  
1.  **Abrir o PowerShell e Entrar**  
  
     Instale e inicie a [versão mais recente do Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) (5.2.0 ou superior). Entrar na conta do Azure com o seguinte comando:  
  
    ```powershell  
    Login-AzureRmAccount  
    ```  
  
     A instrução retorna:  
  
    ```  
    Environment           : AzureCloud  
    Account               : <account_name>  
    TenantId              : <tenant_id>  
    SubscriptionId        : <subscription_id>  
    CurrentStorageAccount :  
    ```  
  
    > [!NOTE]  
    >  Se você tiver várias assinaturas e desejar especificar uma para usar para o cofre, use `Get-AzureRmSubscription` para ver as assinaturas e `Select-AzureRmSubscription` para escolher a assinatura correta. Caso contrário, o PowerShell selecionará um para você por padrão.  
  
2.  **Criar um novo grupo de recursos**  
  
     Todos os recursos do Azure criados por meio do Azure Resource Manager devem estar contidos em grupos de recursos. Crie um grupo de recursos para hospedar o cofre de chaves. Este exemplo usa o `ContosoDevRG`. Escolha seu próprio grupo de recursos **exclusivo** e o nome do cofre de chaves, levando em conta que todos os nomes de cofre de chaves são globalmente exclusivos.  
  
    ```powershell  
    New-AzureRmResourceGroup -Name ContosoDevRG -Location 'East Asia'  
    ```  
  
     A instrução retorna:  
  
    ```  
    ResourceGroupName: ContosoDevRG  
    Location         : eastasia  
    ProvisioningState: Succeeded  
    Tags             :   
    ResourceId       : /subscriptions/<subscription_id>/  
                        resourceGroups/ContosoDevRG  
    ```  
  
    > [!NOTE]  
    >  Para o `-Location parameter`, use o comando `Get-AzureLocation` para identificar como especificar um local alternativo àquele neste exemplo. Se precisar de mais informações, digite: `Get-Help Get-AzureLocation`  
  
3.  **Criar um cofre de chaves**  
  
     O cmdlet `New-AzureRmKeyVault` requer um nome de grupo de recursos, um nome de cofre de chaves e uma localização geográfica. Por exemplo, para um cofre de chaves chamado `ContosoDevKeyVault`, digite:  
  
    ```powershell  
    New-AzureRmKeyVault -VaultName 'ContosoDevKeyVault' `  
       -ResourceGroupName 'ContosoDevRG' -Location 'East Asia'  
    ```  
  
     Registre o nome do seu cofre de chaves.  
  
     A instrução retorna:  
  
    ```  
    Vault Name                       : ContosoDevKeyVault  
    Resource Group Name              : ContosoDevRG  
    Location                         : East Asia  
    ResourceId                       : /subscriptions/<subscription_id>/  
                                        resourceGroups/ContosoDevRG/providers/  
                                        Microsoft/KeyVault/vaults/ContosoDevKeyVault  
    Vault URI: https://ContosoDevKeyVault.vault.azure.net  
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
  
4.  **Conceda permissão para a Entidade de Serviço do Azure Active Directory acessar o Cofre de Chaves**  
  
     Você pode autorizar outros usuários e aplicativos a usarem o cofre de chaves.   
    Nesse caso, vamos usar a entidade de serviço do Azure Active Directory criada na Parte I para autorizar a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
    > [!IMPORTANT]  
    >  A entidade de serviço do Azure Active Directory deve ter, pelo menos, as permissões `get`, `wrapKey` e `unwrapKey` para o cofre de chaves.  
  
     Conforme mostrado abaixo, use a **ID do Cliente** da Parte I para o parâmetro `ServicePrincipalName` . O `Set-AzureRmKeyVaultAccessPolicy` será executado silenciosamente sem saída se for executado com êxito.  
  
    ```powershell  
    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoDevKeyVault'`  
      -ServicePrincipalName EF5C8E09-4D2A-4A76-9998-D93440D8115D `  
      -PermissionsToKeys get, wrapKey, unwrapKey  
    ```  
  
     Chamar o cmdlet `Get-AzureRmKeyVault` para confirmar as permissões. Na saída da instrução em 'Políticas de Acesso', você verá o nome do aplicativo AAD listado como outro locatário que tem acesso a este cofre de chaves.  
  
       
5.  **Gerar uma chave assimétrica no cofre de chaves**  
  
     Há duas maneiras de gerar uma chave no Cofre de Chaves do Azure: 1) importar uma chave existente ou 2) criar uma nova chave.  
                  
      > [!NOTE]
        >  O SQL Server dá suporte apenas a chaves RSA de 2.048 bits.
        
    ### <a name="best-practice"></a>Prática recomendada:
    
    Para garantir a rápida recuperação da chave e poder acessar os seus dados fora do Azure, recomendamos a seguinte prática recomendada:
 
    1. Crie sua chave de criptografia localmente em um dispositivo HSM local. (Certifique-se de que ela é uma chave RSA 2048 assimétrica, para que ela seja compatível com o SQL Server.)
    2. Importe a chave de criptografia no Cofre de Chaves do Azure. Veja as etapas abaixo para saber como fazer isso.
    3. Antes de usar a chave no Cofre de Chaves do Azure pela primeira vez, faça um backup da chave do Cofre de Chaves do Azure. Saiba mais sobre o comando [Backup-AzureKeyVaultKey](https://msdn.microsoft.com/library/mt126292.aspx) .
    4. Sempre que qualquer alteração for feita na chave (por exemplo, adicionar ACLs, adicionar marcas, adicionar atributos da chave), certifique-se de fazer outro backup da chave do Azure Key Vault.

        > [!NOTE]  
        >  Fazer backup de uma chave é uma operação de chave do Azure Key Vault que retorna um arquivo que pode ser salvo em qualquer lugar.

    ### <a name="types-of-keys"></a>Tipos de chaves:
    Há dois tipos de chaves que você pode gerar no Azure Key Vault que funcionarão com o SQL Server. Ambas são chaves RSA de 2.048 bits assimétricas.  
  
    -   **Protegido por software:** processado no software e criptografado em repouso. Operações em chaves protegidas por software ocorrem nas Máquinas Virtuais do Azure. Recomendado para as chaves que não são usadas em uma implantação de produção.  
  
    -   **Protegido por HSM:** criado e protegido por um HSM (módulo de segurança de hardware) para segurança adicional. Custa cerca de US$ 1 por versão de chave.  
  
        > [!IMPORTANT]  
        >  O Conector do SQL Server exige que o nome da chave use somente os caracteres “a-z”, “A-Z”, “0-9” e “-”, com um limite de 26 caracteres.   
        > Versões de chave diferentes com o mesmo nome de chave no Cofre de Chaves do Azure não funcionarão com o Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para girar uma chave do Cofre de Chaves do Azure que está sendo usada por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], veja as etapas de Substituição de chave em [Manutenção e solução de problemas do Conector do SQL Server](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md).  

    ### <a name="import-an-existing-key"></a>Importar uma chave existente   
  
    Se você tiver uma chave protegida por software RSA de 2048 bits, poderá carregar a chave no Cofre de Chaves do Azure. Por exemplo, se você tem um arquivo .PFX salvo em sua unidade `C:\\` em um arquivo chamado `softkey.pfx` e deseja carregá-lo no Cofre de Chaves do Azure, digite o seguinte para definir a variável `securepfxpwd` com uma senha de `12987553` para o arquivo .PFX:  
  
    ``` powershell  
    $securepfxpwd = ConvertTo-SecureString –String '12987553' `  
      –AsPlainText –Force  
    ```  
  
    Em seguida, digite o seguinte para importar a chave do arquivo .PFX, que a protege pelo hardware (recomendado) no serviço de Cofre de Chaves:  
  
    ``` powershell  
        Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' `  
          -Name 'ContosoFirstKey' -KeyFilePath 'c:\softkey.pfx' `  
          -KeyFilePassword $securepfxpwd $securepfxpwd  -Destination 'HSM'  
    ```  
 
    > [!IMPORTANT]  
    > Importar a chave assimétrica é altamente recomendável para cenários de produção, pois ela permite que o administrador garanta a chave em um sistema de caução de chaves. Se a chave assimétrica for criada no cofre, ela não pode ser mantida em garantia porque a chave privada nunca pode deixar o cofre. As chaves usadas para proteger dados críticos devem ser mantidas em garantia. A perda de uma chave assimétrica resultará em perda permanente de dados.  

    ### <a name="create-a-new-key"></a>Criar uma nova chave
    #### <a name="example"></a>Exemplo:  
    Alternativamente, você poderá criar uma nova chave de criptografia diretamente no Azure Key Vault e protegê-la por software ou por HSM.  Neste exemplo, vamos criar uma chave protegida por software usando o `Add-AzureKeyVaultKey cmdlet`:  

    ``` powershell  
    Add-AzureKeyVaultKey -VaultName 'ContosoDevKeyVault' `  
      -Name 'ContosoRSAKey0' -Destination 'Software'  
    ```  
  
    A instrução retorna:  
  
    ```  
    Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes  
    Key        :  {"kid":"https:contosodevKeyVault.azure.net/keys/  
                   ContosoRSAKey0/<guid>","dty":"RSA:,"key_ops": ...  
    VaultName  : contosodevkeyvault  
    Name       : contosoRSAKey0  
    Version    : <guid>  
    Id         : https://contosodevkeyvault.vault.azure.net:443/  
                 keys/ContosoRSAKey0/<guid>  
    ```  
 > [!IMPORTANT]  
    >  O cofre de chaves dá suporte a várias versões da mesma chave nomeada, mas as chaves usadas pelo Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não devem estar com controle de versão ou revertidas. Se o administrador deseja distribuir a chave usada para criptografia [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , uma nova chave com um nome diferente deve ser criada no cofre e usada para criptografar DEK.  
   
  
## <a name="part-iii-install-the-includessnoversionincludesssnoversion-mdmd-connector"></a>Parte III: instalar o Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
 Baixe o Conector do SQL Server no [Centro de Download da Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=521700). (Isso deve ser feito pelo administrador do computador [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .)  

> [!NOTE]  
>  Versões 1.0.0.440 e anteriores foram substituídas e não têm mais suporte em ambientes de produção. Atualize para a versão 1.0.1.0 ou posterior visitando o [Centro de Download da Microsoft](https://www.microsoft.com/download/details.aspx?id=45344) e usando as instruções da página [Manutenção e solução de problemas do Conector do SQL Server](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md) em "Atualização do Conector do SQL Server".

> [!NOTE]  
> Há uma alteração da falha na versão 1.0.5.0, em termos do algoritmo de impressão digital. Você pode enfrentar falhas de restauração do banco de dados após atualizar para a versão 1.0.5.0. Veja o artigo KB [447099](https://support.microsoft.com/help/4470999/db-backup-problems-to-sql-server-connector-for-azure-1-0-5-0).
  
 ![ekm-connector-install](../../../relational-databases/security/encryption/media/ekm-connector-install.png "ekm-connector-install")  
  
 Por padrão, o conector será instalado em C:\Arquivos de Programas\Conector do SQL Server para Cofre de Chaves do Microsoft Azure. Esse local pode ser alterado durante a instalação. (Se alterado, ajuste os scripts a seguir).  
  
 Não há interface para o Conector, mas se ele for instalado com êxito, **Microsoft.AzureKeyVaultService.EKM.dll** estará instalado no computador. Esse é o DLL de provedor EKM criptográfico que precisa ser registrado com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando a instrução `CREATE CRYPTOGRAPHIC PROVIDER` .  
  
 A instalação do Conector do SQL Server também permite que você baixe opcionalmente os scripts de exemplo para criptografia do SQL Server.  
  
 Para exibir explicações do código de erro, definições de configuração ou tarefas de manutenção, do SQL Server Connector, visite os apêndices no final deste tópico:  
  
-   [A. Instruções de manutenção do SQL Server Connector](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixA)  
  
-   [C. Explicações de código de erro do SQL Server Connector](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixC)  
  
  
## <a name="part-iv-configure-includessnoversionincludesssnoversion-mdmd"></a>Parte IV: configurar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
 Confira [B. Perguntas frequentes](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixB) para ver uma observação sobre os níveis de permissão mínimos necessários para cada ação desta seção.  
  
1.  **Inicie o sqlcmd.exe ou o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Studio**  
  
2.  **Configurar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para usar EKM**  
  
     Execute o seguinte script [!INCLUDE[tsql](../../../includes/tsql-md.md)] para configurar o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] para usar um provedor EKM.  
  
    ```sql  
    -- Enable advanced options.  
    USE master;  
    GO  
  
    sp_configure 'show advanced options', 1;  
    GO  
    RECONFIGURE;  
    GO  
  
    -- Enable EKM provider  
    sp_configure 'EKM provider enabled', 1;  
    GO  
    RECONFIGURE;  
    ```  
  
3.  **Registre (crie) o Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como um provedor EKM com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**  
  
     – Crie um provedor criptográfico usando o Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], que é um provedor EKM do Azure Key Vault.    
    Este exemplo usa o nome `AzureKeyVault_EKM_Prov`.  
  
    ```sql  
    CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov   
    FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';  
    GO  
    ```  
  
    > [!NOTE]  
    >  O tamanho do caminho do arquivo não pode exceder a 256 caracteres.  
  
  
4.  **Instalar uma credencial do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para um logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usar o cofre de chaves**  
  
     Uma credencial deve ser adicionada a cada logon que execute criptografia usando uma chave do cofre de chaves. Isso pode incluir:  
  
    -   Um logon do administrador [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que usará o cofre de chaves para instalar e gerenciar cenários de criptografia do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
    -   Outros logons do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que podem habilitar a TDE (Transparent Data Encryption) ou outros recursos de criptografia do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
     Há um mapeamento um para um entre as credenciais e logons. Ou seja, cada logon deve ter uma credencial exclusiva.  
  
     Modificar o script [!INCLUDE[tsql](../../../includes/tsql-md.md)] abaixo das seguintes maneiras:  
  
    -   Edite o argumento `IDENTITY` (`ContosoDevKeyVault`) para apontar para o Cofre de Chaves do Azure.
        - Se você estiver usando o **Azure global**, substitua o argumento `IDENTITY` pelo nome do seu Azure Key Vault da Parte II.
        - Se você estiver usando uma **nuvem privada do Azure** (por ex:. Azure Governamental, Azure China ou Azure Alemanha), substitua o argumento `IDENTITY` pelo URI do Cofre retornado na Parte II, etapa 3. Não inclua “https://” no URI do Cofre.   
    -   Substitua a primeira parte do argumento do `SECRET` pela **ID do Cliente** do Azure Active Directory da Parte I. Neste exemplo, a **ID do Cliente** é `EF5C8E094D2A4A769998D93440D8115D`.  
  
        > [!IMPORTANT]  
        >  É necessário remover os hifens da **ID do Cliente**.  
  
    -   Conclua a segunda parte do argumento `SECRET` com o **Segredo do Cliente** da Parte I. Neste exemplo, o **Segredo do Cliente** da Parte 1 é `Replace-With-AAD-Client-Secret`. A cadeia de caracteres final do argumento `SECRET` será uma sequência longa de letras e números, *sem hifens*.  
  
    ```sql  
    USE master;  
    CREATE CREDENTIAL sysadmin_ekm_cred   
        WITH IDENTITY = 'ContosoDevKeyVault', -- for public Azure
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.usgovcloudapi.net', -- for Azure Government
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.azure.cn', -- for Azure China
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.microsoftazure.de', -- for Azure Germany   
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DReplace-With-AAD-Client-Secret'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;  
  
    -- Add the credential to the SQL Server administrator's domain login   
    ALTER LOGIN [<domain>\<login>]  
    ADD CREDENTIAL sysadmin_ekm_cred;  
    ```  
  
     Para obter um exemplo do uso de variáveis para os argumentos **CREATE CREDENTIAL** e remover programaticamente os hifens da ID do cliente, consulte [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md).  
  
5.  **Abra sua chave do Cofre de Chaves do Azure em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**  
  
     Se você importou uma chave assimétrica, conforme descrito anteriormente na Parte II, abra a chave fornecendo o nome da chave no seguinte script [!INCLUDE[tsql](../../../includes/tsql-md.md)] .  
  
    -   Substitua `CONTOSO_KEY` com o nome que deseja que a chave tenha em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
    -   Substitua `ContosoRSAKey0` pelo nome da chave no Cofre de Chaves do Azure.  
  
    ```sql  
    CREATE ASYMMETRIC KEY CONTOSO_KEY   
    FROM PROVIDER [AzureKeyVault_EKM_Prov]  
    WITH PROVIDER_KEY_NAME = 'ContosoRSAKey0',  
    CREATION_DISPOSITION = OPEN_EXISTING;  
    ```  
## <a name="next-step"></a>Próxima etapa  
  
Agora que você concluiu a configuração básica, consulte [Use SQL Server Connector with SQL Encryption Features](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)(Usar o Conector do SQL Server com recursos de criptografia do SQL)   
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciamento extensível de chaves usando o Azure Key Vault](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)   
[Manutenção e solução de problemas do Conector do SQL Server](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)
