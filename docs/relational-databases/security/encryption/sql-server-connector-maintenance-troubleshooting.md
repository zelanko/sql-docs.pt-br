---
title: "Manutenção e solução de problemas &amp; do Conector do SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 04/05/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQL Server Connector, appendix
ms.assetid: 7f5b73fc-e699-49ac-a22d-f4adcfae62b1
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 076c31d89d907dbba144fec6be43267976cca733
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="sql-server-connector-maintenance-amp-troubleshooting"></a>Manutenção &amp; solução de problemas do Conector do SQL Server
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Informações complementares sobre o Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] são fornecidos neste tópico. Para obter mais informações sobre o conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], consulte [Extensible Key Management Using Azure Key Vault &#40;SQL Server&#41; (Gerenciamento extensível de chaves usando o Cofre de Chaves do Azure &#40;SQL Server&#41;)](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md), [Setup Steps for Extensible Key Management Using the Azure Key Vault (Etapas de instalação para o gerenciamento extensível de chaves usando o Cofre de Chaves do Azure)](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md) e [Use SQL Server Connector with SQL Encryption Features (Usar o Conector do SQL Server com recursos de criptografia do SQL)](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md).  
  
  
##  <a name="AppendixA"></a> A. Instruções de manutenção do Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
### <a name="key-rollover"></a>Substituição de Chave  
  
> [!IMPORTANT]  
>  O Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] exige que o nome da chave use somente os caracteres “a-z”, “A-Z”, “0-9” e “-”, com um limite de 26 caracteres.   
> Versões de chave diferentes com o mesmo nome de chave no Cofre de Chaves do Azure não funcionarão com o Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para girar um Cofre de Chaves do Azure que está sendo usado por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], uma nova chave com um novo nome de chave deve ser criada.  
  
 Normalmente, as chaves assimétricas do servidor para criptografia do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] precisam ter sua verão atualizada cada 1-2 anos. É importante observar que embora o cofre de chaves permita que as chaves tenham sua versão atualizada, os clientes não devem usar esse recurso para implementar o controle de versão. O Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não pode lidar com as alterações na versão das chaves do Cofre de Chaves. Para implementar o controle de versão de chaves, o cliente precisa criar uma nova chave no Cofre de Chaves e criptografar novamente a chave de criptografia de dados no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)].  
  
 Eis o modo como isso seria feito para TDE:  
  
-   **No PowerShell:** crie uma chave assimétrica (com um nome diferente da sua chave assimétrica de TDE atual) no Cofre de Chaves.  
  
    ```powershell  
    Add-AzureRmKeyVaultKey -VaultName 'ContosoDevKeyVault' `  
      -Name 'Key2' -Destination 'Software'  
    ```  
  
-   **Usando [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] ou sqlcmd.exe:** Use as instruções a seguir, conforme mostrado na etapa 3, seção 3.  
  
     Importe a nova chave assimétrica.  
  
    ```tsql  
    USE master  
    CREATE ASYMMETRIC KEY [MASTER_KEY2]   
    FROM PROVIDER [EKM]   
    WITH PROVIDER_KEY_NAME = 'Key2',   
    CREATION_DISPOSITION = OPEN_EXISTING   
    GO  
    ```  
  
     Crie um novo logon a ser associado com a nova chave assimétrica (conforme mostrado em instruções de TDE).  
  
    ```tsql  
    USE master  
    CREATE LOGIN TDE_Login2   
    FROM ASYMMETRIC KEY [MASTER_KEY2]  
    GO  
    ```  
  
     Crie uma nova credencial a ser mapeada para o logon.  
  
    ```tsql  
    CREATE CREDENTIAL Azure_EKM_TDE_cred2  
        WITH IDENTITY = 'ContosoDevKeyVault',   
       SECRET = 'EF5C8E094D2A4A769998D93440D8115DAADsecret123456789=’   
    FOR CRYPTOGRAPHIC PROVIDER EKM;  
  
    ALTER LOGIN TDE_Login2  
    ADD CREDENTIAL Azure_EKM_TDE_cred2;  
    GO  
    ```  
  
     Escolha o banco de dados cuja chave de criptografia de banco de dados você deseja criptografar novamente.  
  
    ```tsql  
    USE [database]  
    GO  
    ```  
  
     Criptografe novamente a chave de criptografia do banco de dados.  
  
    ```tsql  
    ALTER DATABASE ENCRYPTION KEY   
    ENCRYPTION BY SERVER ASYMMETRIC KEY [MASTER_KEY2];  
    GO  
    ```  
  
### <a name="upgrade-of-includessnoversionincludesssnoversion-mdmd-connector"></a>Atualização do Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  

Versões 1.0.0.440 e anteriores foram substituídas e não têm mais suporte em ambientes de produção. Há suporte para versões 1.0.1.0 e mais recentes em ambientes de produção. Use as instruções a seguir para atualizar para a última versão disponível no [Centro de Download da Microsoft](https://www.microsoft.com/download/details.aspx?id=45344).

Se você estiver usando a Versão 1.0.1.0 ou mais recente, realize as etapas a seguir para atualizar para a última versão do Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Essas instruções evitem a necessidade de reiniciar a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .
 
1. Instale a versão mais nova do Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no [Centro de Download da Microsoft](https://www.microsoft.com/download/details.aspx?id=45344). No assistente de instalação, salve o novo arquivo DLL em um caminho de arquivo diferente do caminho do arquivo da DLL original do Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Por exemplo, o novo caminho do arquivo poderá ser: `C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\<latest version number>\Microsoft.AzureKeyVaultService.EKM.dll`
 
2. Na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], execute o seguinte comando Transact-SQL para apontar a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para a nova versão do Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :

    ``` 
    ALTER CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov   
    FROM FILE =   
    'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\<latest version number>\Microsoft.AzureKeyVaultService.EKM.dll'
    GO  
    ```

Se você estiver usando a Versão 1.0.0.440 ou mais antiga, siga estas etapas para atualizar para a última versão do Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .
  
1.  Pare a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
2.  Pare o serviço do Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
3.  Desinstale o Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando o recurso Programas e Recursos do Windows.  
  
     (Como alternativa, você pode renomear a pasta em que o arquivo DLL está localizado. O nome padrão da pasta é “[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] for Microsoft Azure Key Vault”.  
  
4.  Instale a versão mais recente do Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Centro de Download da Microsoft.  
  
5.  Reinicie a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
6.  Execute a seguinte instrução para alterar o provedor EKM para começar a usar a versão mais recente do Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Certifique-se de que o caminho do arquivo está apontando para o local em que você baixou a versão mais recente. (Essa etapa poderá ser ignorada se a nova versão estiver sendo instalada no mesmo local que a versão original.) 
  
    ```tsql  
    ALTER CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov   
    FROM FILE =   
    'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';  
    GO  
    ```  
  
7.  Verifique se os bancos de dados usando TDE estão acessíveis.  
  
8.  Depois de validar que a atualização funciona, você poderá excluir a antiga pasta do Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (se você optar por renomeá-la em vez de desinstalá-la na Etapa 3).  
  
### <a name="rolling-the-includessnoversionincludesssnoversion-mdmd-service-principal"></a>Revertendo a Entidade de Serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa entidades de serviço criadas no Azure Active Directory como credenciais para acessar o Cofre de Chaves.  A entidade de serviço tem uma ID do Cliente e uma Chave de Autenticação.  Uma credencial do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é configurada com o **VaultName**, a **ID do cliente**e a **Chave de Autenticação**.  A **Chave de Autenticação** é válida por um determinado período de tempo (1 ou 2 anos).   Antes do período de tempo expirar, uma nova chave deve ser gerada no Azure AD para a Entidade de Serviço.  Em seguida, a credencial deve ser alterada no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].    [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] mantém um cache de credencial na sessão atual, portanto, quando uma credencial é alterada, [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] deve ser reiniciado.  
  
### <a name="key-backup-and-recovery"></a>Backup e Recuperação de Chaves  
O backup do cofre de chaves deve ser feito regularmente. Se uma chave assimétrica no cofre for perdida, ela poderá ser restaurada do backup. A chave deve ser restaurada usando o mesmo nome de antes, o que o comando Restore PowerShell fará (consulte etapas abaixo).  
Se o cofre tiver sido perdido, você precisará recriar um cofre e restaurar a chave assimétrica no cofre usando o mesmo nome de antes. O nome do cofre pode ser diferente (ou o mesmo de antes). Você também deve definir as permissões de acesso no novo cofre para conceder à entidade de serviço do SQL Server o acesso necessário para os cenários de criptografia do SQL Server e, em seguida, ajustar a credencial do SQL Server para que o nome do novo cofre seja refletido.  
Resumindo, estas são as etapas:  
  
* Fazer backup do cofre de chaves (usando o cmdlet do PowerShell Backup-AzureKeyVaultKey).  
* Em caso de falha do cofre, crie um novo cofre na mesma região geográfica*. O usuário criando-o deve estar no mesmo diretório padrão que a entidade de serviço configurada para SQL Server.  
* Restaure a chave para o novo cofre (usando o cmdlet do PowerShell Restore-AzureKeyVaultKey – isso restaura a chave usando o mesmo nome de antes). Se já houver uma chave com o mesmo nome, a restauração falhará.  
* Conceder permissões para a entidade de serviço do SQL Server usar esse novo cofre.  
* Modificar a credencial do SQL Server usada pelo Mecanismo de Banco de Dados para refletir o nome do novo cofre (se necessário).  
  
Backups de chaves podem ser restaurados em regiões do Azure, desde que eles permaneçam na mesma região geográfica ou nuvem nacional: EUA, Canadá, Japão, Austrália, Índia, APAC, Europa, Brasil, China, Governo dos EUA ou Alemanha.  
  
  
##  <a name="AppendixB"></a> B. Perguntas frequentes  
### <a name="on-azure-key-vault"></a>No Cofre de Chaves do Azure  
  
**Como funcionam as operações de chave com o Cofre de Chaves do Azure?**  
 A chave assimétrica no cofre de chave é usada para proteger chaves de criptografia [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Somente a parte pública da chave assimétrica nunca deixa o cofre, a parte particular nunca é exportada pelo cofre. Todas as operações de criptografia usando a chave assimétrica são feitas no serviço do Cofre de Chaves do Azure e são protegidas pela segurança do serviço.  
  
 **O que é um URI de chave?**  
 Cada chave no Cofre de Chaves do Azure tem um URI (Uniform Resource Identifier), que pode ser usado para fazer referência à chave em seu aplicativo. Use o formato `https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey` para obter a versão atual e use o formato `https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87` para obter uma versão específica.  
  
### <a name="on-configuring-includessnoversionincludesssnoversion-mdmd"></a>Em Configurando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  

**Quais são os pontos de extremidade que o Conector do SQL Server precisa acessar?** O Conector se comunica com dois pontos de extremidade que precisam ser incluídos na lista de permissões. A única porta necessária para comunicação de saída a esses outros serviços é 443 para Https:
-  login.microsoftonline.com/*:443
-  *.vault.azure.net/*:443
  
**Quais são os níveis de permissão mínimos necessários para cada etapa da configuração em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]?**  
 Embora você possa executar todas as etapas de configuração como um membro da função de servidor fixa sysadmin, o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] incentiva você a minimizar as permissões utilizadas. A lista a seguir define o nível mínimo de permissão para cada ação.  
  
-   Para criar um provedor criptográfico, é necessária a permissão `CONTROL SERVER` ou associação na função de servidor fixa **sysadmin** .  
  
-   Para alterar uma opção de configuração e executar a instrução `RECONFIGURE` , é necessário ter a permissão de nível de servidor `ALTER SETTINGS` . A permissão `ALTER SETTINGS` é implicitamente mantida pelas funções de servidor fixas sysadmin e **serveradmin** .  
  
-   Para criar uma credencial, é exigida uma permissão `ALTER ANY CREDENTIAL` .  
  
-   Para adicionar uma credencial a um logon, é necessária a permissão `ALTER ANY LOGIN` .  
  
-   Para criar uma chave assimétrica, é exigida uma permissão `CREATE ASYMMETRIC KEY` .  

**Como posso alterar meu Active Directory padrão para que o cofre de chaves seja criado na mesma assinatura e o Active Directory como a entidade de serviço que criei para o Conector do [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] ?**

![aad-change-default-directory-helpsteps](../../../relational-databases/security/encryption/media/aad-change-default-directory-helpsteps.png)

1. Vá para o portal clássico do Azure: [https://manage.windowsazure.com](https://manage.windowsazure.com)  
2. No menu à esquerda, role a tela para baixo e selecione **Configurações**.
3. Selecione a assinatura do Azure que você está usando e clique em **Editar Diretório** nos comandos da parte inferior da tela.
4. Na janela pop-up, use a lista suspensa **Diretório** para selecionar o Active Directory que você deseja usar. Isso tornará o Diretório padrão.
5. Verifique se você é o administrador global do Active Directory recém-selecionado. Se você não for o administrador global, poderá perder permissões de gerenciamento, pois você mudou de diretório.
6. Depois que a janela pop-up for fechada, se nenhuma de suas assinaturas estiver visível, talvez seja necessário atualizar o filtro **Filtrar por Diretório** no filtro **Assinaturas** do menu superior direito da tela para ver as assinaturas que usam o Active Directory recém-atualizado.

    > [!NOTE] 
    > Talvez você não tenha permissões para realmente alterar o diretório padrão na assinatura do Azure. Nesse caso, crie a entidade de serviço do AAD no diretório padrão para que ela esteja no mesmo diretório que o Cofre de Chaves do Azure que será usado mais tarde.

Para saber mais sobre o Active Directory, leia [Como a assinatura do Azure está relacionada ao Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-how-subscriptions-associated-directory/)
  
##  <a name="AppendixC"></a> C. Explicações de Código de Erro do Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
 **Códigos de erro do provedor:**  
  
Código do erro  |Símbolo  |Descrição    
---------|---------|---------  
0 | scp_err_Success | Êxito na operação.    
1 | scp_err_Failure | A operação falhou.    
2 | scp_err_InsufficientBuffer | Este erro informa ao mecanismo para alocar mais memória para o buffer.    
3 | scp_err_NotSupported | A operação não tem suporte. Por exemplo, o tipo de chave ou o algoritmo especificado não tem suporte pelo provedor EKM.    
4 | scp_err_NotFound | O algoritmo ou chave especificada não pôde ser localizado pelo provedor EKM.    
5 | scp_err_AuthFailure | A autenticação falhou com o provedor EKM.    
6 | scp_err_InvalidArgument | O argumento fornecido é inválido.    
7 | scp_err_ProviderError | Há um erro não especificado ocorrendo no provedor EKM detectado pelo mecanismo SQL.    
2049 | scp_err_KeyNameDoesNotFitThumbprint | O nome da chave é muito longo para caber na impressão digital do mecanismo do SQL. O nome da chave não deve exceder 26 caracteres.    
2050 | scp_err_PasswordTooShort | A cadeia de caracteres secreta que é a concatenação da ID de cliente do AAD e o segredo é menor que 32 caracteres.    
2051 | scp_err_OutOfMemory | A memória do mecanismo SQL acabou e não foi possível alocar memória para o provedor EKM.    
2052 | scp_err_ConvertKeyNameToThumbprint | Falha ao converter o nome da chave para impressão digital.    
2053 | scp_err_ConvertThumbprintToKeyName|  Falha ao converter a impressão digital para o nome da chave.    
3000 | ErrorSuccess | Êxito na operação de AKV.    
3001 | ErrorUnknown | A operação de AKV falhou com um erro não especificado.    
3002 | ErrorHttpCreateHttpClientOutOfMemory | Não é possível criar um HttpClient para a operação AKV devido à memória insuficiente.    
3003 | ErrorHttpOpenSession | Não é possível abrir uma sessão Http devido a um erro de rede.    
3004 | ErrorHttpConnectSession | Não é possível conectar uma sessão Http devido a um erro de rede.    
3005 | ErrorHttpAttemptConnect | Não é possível tentar uma conexão devido a um erro de rede.    
3006 | ErrorHttpOpenRequest | Não é possível abrir uma solicitação devido a um erro de rede.    
3007 | ErrorHttpAddRequestHeader | Não é possível adicionar o cabeçalho de solicitação.    
3008 | ErrorHttpSendRequest | Não é possível enviar uma solicitação devido a um erro de rede.    
3009 | ErrorHttpGetResponseCode | Não é possível obter um código de resposta devido a um erro de rede.    
3010 | ErrorHttpResponseCodeUnauthorized | O servidor respondeu 401 para a solicitação.    
3011 | ErrorHttpResponseCodeThrottled | Servidor limitou a solicitação.    
3012 | ErrorHttpResponseCodeClientError | A solicitação enviada do conector é inválida. Em geral, isso significa que o nome da chave é inválido ou contém caracteres inválidos.
3013 | ErrorHttpResponseCodeServerError | O servidor respondeu a um código de resposta entre 500 e 600.    
3014 | ErrorHttpQueryHeader | Não é possível consultar o cabeçalho de resposta.    
3015 | ErrorHttpQueryHeaderOutOfMemoryCopyHeader | Não é possível copiar o cabeçalho de resposta devido à memória insuficiente.    
3016 | ErrorHttpQueryHeaderOutOfMemoryReallocBuffer | Não é possível consultar o cabeçalho de resposta devido à memória insuficiente ao realocar um buffer.    
3017 | ErrorHttpQueryHeaderNotFound | Não é possível localizar o cabeçalho de consulta na resposta.    
3018 | ErrorHttpQueryHeaderUpdateBufferLength | Não é possível atualizar o tamanho do buffer ao consultar o cabeçalho de resposta.    
3019 | ErrorHttpReadData | Não é possível ler dados de resposta devido a erro de rede. 
3076 | ErrorHttpResourceNotFound | O servidor respondeu 404, pois o nome da chave não foi encontrado. Verifique se o nome da chave existe no cofre.
3077 | ErrorHttpOperationForbidden | O servidor respondeu 403, pois o usuário não tem permissão adequada para executar a ação. Verifique se você tem permissão para a operação especificada. No mínimo, o conector exige as permissões “get, list, wrapKey e unwrapKey” para funcionar corretamente.   
  
Se você não ver o código de erro nesta tabela, aqui estão algumas outras razões pelas quais o erro pode estar ocorrendo:   
  
-   Você pode não ter acesso à Internet e não pode acessar seu Cofre de Chaves do Azure – Verifique sua conexão de Internet.  
  
-   O serviço do Cofre de Chaves do Azure pode estar desativado. Tente novamente em outro momento.  
  
-   Você pode ter removido a chave assimétrica do Cofre de Chaves do Azure ou [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Restaure a chave.  
  
-   Se você receber um erro “Não é possível carregar a biblioteca”, verifique se você tem a versão apropriada do Visual Studio C++ Redistributable instalada com base na versão do SQL Server que está sendo executada. A tabela abaixo especifica qual versão será instalada por meio do Centro de Download da Microsoft.   
  
Versão do SQL Server  |Link de instalação redistribuível    
---------|--------- 
2008, 2008 R2, 2012, 2014 | [Pacotes Visual C++ Redistributable Packages para Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784)    
2016 | [Pacotes Redistribuíveis do Visual C++ para Visual Studio 2015](https://www.microsoft.com/download/details.aspx?id=48145)    
  
  
## <a name="additional-references"></a>Referências adicionais  
 Mais sobre o Gerenciamento Extensível de Chaves:  
  
-   [Gerenciamento Extensível de Chaves &#40;EKM&#41;](../../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
 Criptografias de SQL com suporte ao EKM:  
  
-   [Habilitar TDE no SQL Server usando EKM](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
-   [Criptografia de backup](../../../relational-databases/backup-restore/backup-encryption.md)  
  
-   [Criar um backup criptografado](../../../relational-databases/backup-restore/create-an-encrypted-backup.md)  
  
 Comandos do [!INCLUDE[tsql](../../../includes/tsql-md.md)] Relacionados:  
  
-   [sp_configure &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
-   [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-cryptographic-provider-transact-sql.md)  
  
-   [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)  
  
-   [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
  
-   [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
-   [CREATE LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/create-login-transact-sql.md)  
  
-   [ALTER LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-login-transact-sql.md)  
  
 Documentação do Cofre de Chaves do Azure:  
  
-   [O que é o Azure Key Vault?](https://azure.microsoft.com/documentation/articles/key-vault-whatis/)  
  
-   [Introdução ao Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)  
  
-   Referência dos [Cmdlets do Cofre de Chaves do Azure](https://msdn.microsoft.com/library/dn868052.aspx) do PowerShell  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciamento extensível de chaves usando o Cofre de Chaves do Azure](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  [Use SQL Server Connector with SQL Encryption Features (Usar o Conector do SQL Server com recursos de criptografia do SQL)](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)   
 [Opção de configuração de servidor EKM provider enabled](../../../database-engine/configure-windows/ekm-provider-enabled-server-configuration-option.md)   
 [Setup Steps for Extensible Key Management Using the Azure Key Vault (Etapas de instalação para o gerenciamento extensível de chaves usando o Cofre de Chaves do Azure)](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)  
  
  
