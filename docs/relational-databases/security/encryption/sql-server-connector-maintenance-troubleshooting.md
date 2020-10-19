---
title: Manutenção e solução de problemas do Conector do SQL Server
description: Saiba mais sobre as instruções de manutenção e as etapas comuns de solução de problemas para o Conector do SQL Server.
ms.custom: seo-lt-2019
ms.date: 10/08/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Connector, appendix
ms.assetid: 7f5b73fc-e699-49ac-a22d-f4adcfae62b1
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: 4c8a74d33e75ab19b283f3b9d1bfdaf47dc69240
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91869265"
---
# <a name="sql-server-connector-maintenance--troubleshooting"></a>Manutenção e solução de problemas do Conector do SQL Server

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

  Informações complementares sobre o Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] são fornecidos neste tópico. Para obter mais informações sobre o conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], consulte [Extensible Key Management Using Azure Key Vault &#40;SQL Server&#41; (Gerenciamento extensível de chaves usando o Cofre de Chaves do Azure &#40;SQL Server&#41;)](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md), [Setup Steps for Extensible Key Management Using the Azure Key Vault (Etapas de instalação para o gerenciamento extensível de chaves usando o Cofre de Chaves do Azure)](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md) e [Use SQL Server Connector with SQL Encryption Features (Usar o Conector do SQL Server com recursos de criptografia do SQL)](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md).  
  
##  <a name="a-maintenance-instructions-for-ssnoversion-connector"></a><a name="AppendixA"></a> A. Instruções de manutenção do Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
### <a name="key-rollover"></a>Substituição de Chave  
  
> [!IMPORTANT]  
> O Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] exige que o nome da chave use somente os caracteres “a-z”, “A-Z”, “0-9” e “-”, com um limite de 26 caracteres.
> Versões de chave diferentes com o mesmo nome de chave no Cofre de Chaves do Azure não funcionarão com o Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para girar uma chave do Azure Key Vault que está sendo usado por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], uma nova chave com um novo nome de chave deve ser criada.  
  
 Normalmente, as chaves assimétricas do servidor para criptografia do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] precisam ter controle de versão a cada 1 a 2 anos. É importante observar que embora o cofre de chaves permita que as chaves tenham sua versão atualizada, os clientes não devem usar esse recurso para implementar o controle de versão. O Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não pode lidar com as alterações na versão das chaves do Cofre de Chaves. Para implementar o controle de versão de chaves, crie uma chave no Key Vault e criptografe novamente a chave de criptografia de dados no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)].  
  
 Eis o modo como isso seria feito para TDE:  
  
- **No PowerShell:** crie uma chave assimétrica (com um nome diferente da sua chave assimétrica de TDE atual) no Key Vault.  
  
    ```powershell  
    Add-AzKeyVaultKey -VaultName 'ContosoDevKeyVault' `  
      -Name 'Key2' -Destination 'Software'  
    ```  
  
- **Usando [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] ou sqlcmd.exe:** use as instruções a seguir, conforme mostrado na etapa 3, seção 3.  
  
     Importe a nova chave assimétrica.  
  
    ```sql  
    USE master  
    CREATE ASYMMETRIC KEY [MASTER_KEY2]
    FROM PROVIDER [EKM]
    WITH PROVIDER_KEY_NAME = 'Key2',
    CREATION_DISPOSITION = OPEN_EXISTING
    GO  
    ```  
  
     Crie um novo logon a ser associado com a nova chave assimétrica (conforme mostrado em instruções de TDE).  
  
    ```sql  
    USE master  
    CREATE LOGIN TDE_Login2
    FROM ASYMMETRIC KEY [MASTER_KEY2]  
    GO  
    ```  
  
     Crie uma nova credencial a ser mapeada para o logon.  
  
    ```sql  
    CREATE CREDENTIAL Azure_EKM_TDE_cred2  
        WITH IDENTITY = 'ContosoDevKeyVault',
       SECRET = 'EF5C8E094D2A4A769998D93440D8115DAADsecret123456789='
    FOR CRYPTOGRAPHIC PROVIDER EKM;  
  
    ALTER LOGIN TDE_Login2  
    ADD CREDENTIAL Azure_EKM_TDE_cred2;  
    GO  
    ```  
  
     Escolha o banco de dados cuja chave de criptografia de banco de dados você deseja criptografar novamente.  
  
    ```sql  
    USE [database]  
    GO  
    ```  
  
     Criptografe novamente a chave de criptografia do banco de dados.  
  
    ```sql  
    ALTER DATABASE ENCRYPTION KEY
    ENCRYPTION BY SERVER ASYMMETRIC KEY [MASTER_KEY2];  
    GO  
    ```  
  
### <a name="upgrade-of-ssnoversion-connector"></a>Atualização do Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  

Versões 1.0.0.440 e anteriores foram substituídas e não têm mais suporte em ambientes de produção. Há suporte para versões 1.0.1.0 e mais recentes em ambientes de produção. Use as instruções a seguir para atualizar para a última versão disponível no [Centro de Download da Microsoft](https://www.microsoft.com/download/details.aspx?id=45344).

### <a name="upgrade"></a>Atualizar

1. Interrompa o serviço SQL Server usando o SQL Server Configuration Manager
1. Desinstale a versão antiga usando Painel de Controle\Programas\Programas e Recursos
    1. Nome do aplicativo: Conector do SQL Server para Microsoft Azure Key Vault
    1. Versão: 15.0.300.96 (ou anterior)
    1. Data do arquivo DLL: 30/01/2018 15:00 (ou anterior)
1. Instalar (atualizar) o novo Conector do SQL Server para Microsoft Azure Key Vault
    1. Versão: 15.0.2000.367
    1. Data do arquivo DLL: 11/09/2020 ‏‎5:17
1. Iniciar o serviço SQL Server
1. Os BDs criptografados de teste estão acessíveis

### <a name="rollback"></a>Reversão

1. Interrompa o serviço SQL Server usando o SQL Server Configuration Manager

1. Desinstale a nova versão usando Painel de Controle\Programas\Programas e Recursos
    1. Nome do aplicativo: Conector do SQL Server para Microsoft Azure Key Vault
    1. Versão: 15.0.2000.367
    1. Data do arquivo DLL: 11/09/2020 ‏‎5:17

1. Instalar a versão antiga do Conector do SQL Server para Microsoft Azure Key Vault
    1. Versão: 15.0.300.96
    1. Data do arquivo DLL: 30/01/2018 15:00
1. Iniciar o serviço SQL Server

1. Verifique se os bancos de dados usando TDE estão acessíveis.  
  
1. Depois de validar que a atualização funciona, você poderá excluir a antiga pasta do Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (se você optar por renomeá-la em vez de desinstalá-la na Etapa 3).

### <a name="older-versions-of-the-sql-server-connector"></a>Versões anteriores do Conector do SQL Server
  
Links profundos para versões anteriores do Conector do SQL Server

- Atualmente: [1.0.5.0 (versão 15.0.2000.367) – Data do arquivo: 11 de setembro de 2020](https://download.microsoft.com/download/8/0/9/809494F2-BAC9-4388-AD07-7EAF9745D77B/1033_15.0.2000.367/SQLServerConnectorforMicrosoftAzureKeyVault.msi)
- [1.0.5.0 (versão 15.0.300.96) – Data do arquivo: 30 de janeiro de 2018](https://download.microsoft.com/download/8/0/9/809494F2-BAC9-4388-AD07-7EAF9745D77B/ENU/SQLServerConnectorforMicrosoftAzureKeyVault.msi)
- [1.0.4.0: (versão 13.0.811.168)](https://download.microsoft.com/download/8/0/9/809494F2-BAC9-4388-AD07-7EAF9745D77B/SQLServerConnectorforMicrosoftAzureKeyVault.msi)

### <a name="rolling-the-ssnoversion-service-principal"></a>Revertendo a Entidade de Serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]

 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa entidades de serviço criadas no Azure Active Directory como credenciais para acessar o Cofre de Chaves. A entidade de serviço tem uma ID do Cliente e uma Chave de Autenticação. Uma credencial do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é configurada com o **VaultName**, a **ID do cliente**e a **Chave de Autenticação**. A **Chave de Autenticação** é válida por determinado período (um ou dois anos). Antes do período de tempo expirar, uma nova chave deve ser gerada no Azure AD para a Entidade de Serviço. Em seguida, a credencial deve ser alterada no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] mantém um cache de credencial na sessão atual, portanto, quando uma credencial é alterada, [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] deve ser reiniciado.  
  
### <a name="key-backup-and-recovery"></a>Backup e Recuperação de Chaves

O backup do cofre de chaves deve ser feito regularmente. Se uma chave assimétrica no cofre for perdida, ela poderá ser restaurada do backup. A chave deve ser restaurada usando o mesmo nome de antes, o que o comando Restore PowerShell fará (consulte etapas abaixo).  
Se o cofre tiver sido perdido, você precisará recriar um cofre e restaurar a chave assimétrica no cofre usando o mesmo nome de antes. O nome do cofre pode ser diferente (ou o mesmo de antes). Defina as permissões de acesso no novo cofre para conceder à entidade de serviço do SQL Server o acesso necessário para os cenários de criptografia do SQL Server e ajuste a credencial do SQL Server para que o nome do novo cofre seja refletido.

Resumindo, estas são as etapas:  
  
- Fazer backup do cofre de chaves (usando o cmdlet do PowerShell Backup-AzureKeyVaultKey).  
- Em caso de falha do cofre, crie um cofre na mesma região geográfica. O usuário que está criando o cofre deve estar no mesmo diretório padrão que a instalação da entidade de serviço para SQL Server.  
- Restaure a chave para o novo cofre usando o cmdlet do PowerShell Restore-AzureKeyVaultKey, que restaura a chave usando o mesmo nome de antes. Se já houver uma chave com o mesmo nome, a restauração falhará.  
- Conceder permissões para a entidade de serviço do SQL Server usar esse novo cofre.
- Modificar a credencial do SQL Server usada pelo Mecanismo de Banco de Dados para refletir o nome do novo cofre (se necessário).  
  
Os backups de chaves podem ser restaurados em todas as regiões do Azure, contanto que permaneçam na mesma região geográfica ou nuvem nacional: Alemanha, APAC, Austrália, Brasil, Canadá, China, EUA, Europa, Governo dos EUA, Índia ou Japão.  
  
##  <a name="b-frequently-asked-questions"></a><a name="AppendixB"></a> B. Perguntas frequentes

### <a name="on-azure-key-vault"></a>No Cofre de Chaves do Azure
  
**Como funcionam as operações de chave com o Cofre de Chaves do Azure?**  
 A chave assimétrica no cofre de chave é usada para proteger chaves de criptografia [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Somente a parte pública da chave assimétrica nunca deixa o cofre, a parte particular nunca é exportada pelo cofre. Todas as operações de criptografia usando a chave assimétrica são feitas no serviço do Azure Key Vault e são protegidas pela segurança do serviço.  
  
 **O que é um URI de chave?**  
 Cada chave no Cofre de Chaves do Azure tem um URI (Uniform Resource Identifier), que pode ser usado para fazer referência à chave em seu aplicativo. Use o formato `https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey` para obter a versão atual e use o formato `https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87` para obter uma versão específica.  
  
### <a name="on-configuring-ssnoversion"></a>Em Configurando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  

**Quais são os pontos de extremidade que o Conector do SQL Server precisa acessar?**
O Conector se comunica com dois pontos de extremidade que precisam ser permitidos. A única porta necessária para comunicação de saída a esses outros serviços é 443 para Https:

- login.microsoftonline.com/*:443
- *.vault.azure.net/* :443

**Como fazer para se conectar ao Azure Key Vault por meio de um servidor proxy HTTP(S)?**
O Conector usa as definições de configuração de proxy do Internet Explorer. Essas configurações podem ser controladas por meio da [Política de Grupo](/archive/blogs/askie/how-to-configure-proxy-settings-for-ie10-and-ie11-as-iem-is-not-available) ou por meio do Registro, mas é importante observar que elas não são configurações de todo o sistema e precisarão ser direcionadas para a conta de serviço que executa a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se Administradores de Banco de Dados exibirem ou editarem as configurações no Internet Explorer, elas só afetarão as contas dos Administradores de Banco de Dados em vez do mecanismo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Não é recomendável fazer logon no servidor de maneira interativa usando a conta de serviço. Isso é bloqueado em muitos ambientes seguros. As alterações nas configurações de proxy definidas podem exigir a reinicialização da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para entrarem em vigor, pois elas são armazenadas em cache quando o Conector tenta se conectar a um cofre de chaves pela primeira vez.

**Quais são os níveis de permissão mínimos necessários para cada etapa da configuração em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]?**  
 Embora você possa executar todas as etapas de configuração como um membro da função de servidor fixa sysadmin, o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] incentiva você a minimizar as permissões utilizadas. A lista a seguir define o nível mínimo de permissão para cada ação.  
  
- Para criar um provedor criptográfico, é necessária a permissão `CONTROL SERVER` ou associação na função de servidor fixa **sysadmin** .  
  
- Para alterar uma opção de configuração e executar a instrução `RECONFIGURE` , é necessário ter a permissão de nível de servidor `ALTER SETTINGS` . A permissão `ALTER SETTINGS` é implicitamente mantida pelas funções de servidor fixas sysadmin e **serveradmin** .  
  
- Para criar uma credencial, é exigida uma permissão `ALTER ANY CREDENTIAL` .  
  
- Para adicionar uma credencial a um logon, é necessária a permissão `ALTER ANY LOGIN` .  
  
- Para criar uma chave assimétrica, é exigida uma permissão `CREATE ASYMMETRIC KEY` .  

**Como posso alterar meu Active Directory padrão para que o cofre de chaves seja criado na mesma assinatura e o Active Directory como a entidade de serviço que criei para o Conector do [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] ?**

![aad change default directory helpsteps](../../../relational-databases/security/encryption/media/aad-change-default-directory-helpsteps.png)

1. Acesse o portal clássico do Azure: [https://manage.windowsazure.com](https://manage.windowsazure.com)  
2. No menu à esquerda, selecione **Configurações**.
3. Selecione a assinatura do Azure que você está usando e clique em **Editar Diretório** nos comandos da parte inferior da tela.
4. Na janela pop-up, use a lista suspensa **Diretório** para selecionar o Active Directory que você deseja usar. Isso tornará o Diretório padrão.
5. Verifique se você é o administrador global do Active Directory recém-selecionado. Se você não for o administrador global, poderá perder permissões de gerenciamento, pois você mudou de diretório.
6. Depois que a janela pop-up é fechada, se nenhuma de suas assinaturas estiver visível, talvez seja necessário atualizar o filtro **Filtrar por Diretório** no filtro **Assinaturas** do menu superior direito da tela para ver as assinaturas que usam o Active Directory recém-atualizado.

    > [!NOTE] 
    > Talvez você não tenha permissões para realmente alterar o diretório padrão na assinatura do Azure. Nesse caso, crie a entidade de serviço do AAD no diretório padrão para que ela esteja no mesmo diretório que o Cofre de Chaves do Azure que será usado mais tarde.

Para saber mais sobre o Active Directory, leia [Como a assinatura do Azure está relacionada ao Azure Active Directory](/azure/active-directory/fundamentals/active-directory-how-subscriptions-associated-directory)
  
##  <a name="c-error-code-explanations-for-ssnoversion-connector"></a><a name="AppendixC"></a> C. Explicações de Código de Erro do Conector do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]

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
401 | acquireToken | O servidor respondeu 401 para a solicitação. Verifique se a ID do cliente e o segredo estão corretos e se a cadeia de caracteres da credencial é uma concatenação da ID do cliente do AAD e do segredo sem hifens.
404 | getKeyByName | O servidor respondeu 404, pois o nome da chave não foi encontrado. Verifique se o nome da chave existe no cofre.
2049 | scp_err_KeyNameDoesNotFitThumbprint | O nome da chave é muito longo para caber na impressão digital do mecanismo do SQL. O nome da chave não deve exceder 26 caracteres.
2050 | scp_err_PasswordTooShort | A cadeia de caracteres secreta que é a concatenação de ID e do segredo do cliente do AAD é menor que 32 caracteres.
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
3100 | ErrorHttpCreateHttpClientOutOfMemory               | Não é possível criar um HttpClient para a operação AKV devido à memória insuficiente.
3101 | ErrorHttpOpenSession                               | Não é possível abrir uma sessão Http devido a um erro de rede.
3102 | ErrorHttpConnectSession                            | Não é possível conectar uma sessão Http devido a um erro de rede.
3103 | ErrorHttpAttemptConnect                            | Não é possível tentar uma conexão devido a um erro de rede.
3104 | ErrorHttpOpenRequest                               | Não é possível abrir uma solicitação devido a um erro de rede.
3105 | ErrorHttpAddRequestHeader                          | Não é possível adicionar o cabeçalho de solicitação.
3106 | ErrorHttpSendRequest                               | Não é possível enviar uma solicitação devido a um erro de rede.
3107 | ErrorHttpGetResponseCode                           | Não é possível obter um código de resposta devido a um erro de rede.
3108 | ErrorHttpResponseCodeUnauthorized                  | O servidor respondeu 401 para a solicitação. Verifique se a ID do cliente e o segredo estão corretos e se a cadeia de caracteres da credencial é uma concatenação da ID do cliente do AAD e do segredo sem hifens.
3109 | ErrorHttpResponseCodeThrottled                     | Servidor limitou a solicitação.
3110 | ErrorHttpResponseCodeClientError                    | A solicitação é inválida. Em geral, isso significa que o nome da chave é inválido ou contém caracteres inválidos.
3111 | ErrorHttpResponseCodeServerError                   | O servidor respondeu a um código de resposta entre 500 e 600.
3112 | ErrorHttpResourceNotFound                          | O servidor respondeu 404, pois o nome da chave não foi encontrado. Verifique se o nome da chave existe no cofre.
3113 | ErrorHttpOperationForbidden                         | O servidor respondeu 403, pois o usuário não tem permissão adequada para executar a ação. Verifique se você tem permissão para a operação especificada. No mínimo, as permissões "get, wrapKey, unwrapKey" são necessárias.
3114 | ErrorHttpQueryHeader                               | Não é possível consultar o cabeçalho de resposta.
3115 | ErrorHttpQueryHeaderOutOfMemoryCopyHeader          | Não é possível copiar o cabeçalho de resposta devido à memória insuficiente.
3116 | ErrorHttpQueryHeaderOutOfMemoryReallocBuffer       | Não é possível consultar o cabeçalho de resposta devido à memória insuficiente ao realocar um buffer.
3117 | ErrorHttpQueryHeaderNotFound                       | Não é possível localizar o cabeçalho de consulta na resposta.
3118 | ErrorHttpQueryHeaderUpdateBufferLength             | Não é possível atualizar o tamanho do buffer ao consultar o cabeçalho de resposta.
3119 | ErrorHttpReadData                                  | Não é possível ler dados de resposta devido a erro de rede.
3120 | ErrorHttpGetResponseOutOfMemoryCreateTempBuffer    | Não é possível obter o corpo da resposta devido à memória insuficiente ao criar um buffer temporário.
3121 | ErrorHttpGetResponseOutOfMemoryGetResultString     | Não é possível obter o corpo da resposta devido à memória insuficiente ao obter a cadeia de caracteres de resultado.
3122 | ErrorHttpGetResponseOutOfMemoryAppendResponse      | Não é possível obter o corpo da resposta devido à memória insuficiente ao acrescentar a resposta.
3200 | ErrorGetAADValuesOutOfMemoryConcatPath | Não é possível obter os valores de cabeçalho de desafio do Azure Active Directory devido à memória insuficiente ao concatenar o caminho.
3201 | ErrorGetAADDomainUrlStartPosition | Não é possível encontrar a posição inicial para a URL de domínio do Azure Active Directory no cabeçalho de desafio de resposta mal formatado.
3202 | ErrorGetAADDomainUrlStopPosition | Não é possível encontrar a posição final para a URL de domínio do Azure Active Directory no cabeçalho de desafio de resposta mal formatado.
3203 | ErrorGetAADDomainUrlMalformatted | O cabeçalho de desafio de resposta do Azure Active Directory está mal formatado e não contém a URL do domínio do AAD.
3204 | ErrorGetAADDomainUrlOutOfMemoryAlloc | Memória insuficiente ao alocar buffer para a URL de domínio do Azure Active Directory.
3205 | ErrorGetAADTenantIdOutOfMemoryAlloc | Memória insuficiente ao alocar buffer para a tenantId do Azure Active Directory.
3206 | ErrorGetAKVResourceUrlStartPosition | Não é possível encontrar a posição inicial para a URL de recurso do Azure Key Vault no cabeçalho de desafio de resposta mal formatado.
3207 | ErrorGetAKVResourceUrlStopPosition | Não é possível encontrar a posição final para a URL de recurso do Azure Key Vault no cabeçalho de desafio de resposta mal formatado.
3208 | ErrorGetAKVResourceUrlOutOfMemoryAlloc | Memória insuficiente ao alocar buffer para a URL de recurso do Azure Key Vault.
3.300 | ErrorGetTokenOutOfMemoryConcatPath | Não é possível obter o token devido à memória insuficiente ao concatenar o caminho da solicitação.
3301 | ErrorGetTokenOutOfMemoryConcatBody | Não é possível obter o token devido à memória insuficiente ao concatenar o corpo da resposta.
3302 | ErrorGetTokenOutOfMemoryConvertResponseString | Não é possível obter o token devido à memória insuficiente ao converter a cadeia de caracteres de resposta.
3303 | ErrorGetTokenBadCredentials | Não é possível obter o token devido a credenciais incorretas. Verifique se a cadeia de caracteres da credencial ou o certificado é válida.
3304 | ErrorGetTokenFailedToGetToken | Embora as credenciais estejam corretas, a operação ainda falhará em obter um token válido.
3305 | ErrorGetTokenRejected | O token é válido, mas foi rejeitado pelo servidor.
3306 | ErrorGetTokenNotFound | Não é possível localizar o token em resposta.
3307 | ErrorGetTokenJsonParser | Não é possível analisar a resposta JSON do servidor.
3308 | ErrorGetTokenExtractToken | Não é possível extrair o token da resposta JSON.
3400 | ErrorGetKeyByNameOutOfMemoryConvertResponseString | Não é possível obter a chave pelo nome devido à falta de memória ao converter a cadeia de caracteres de resposta.
3401 | ErrorGetKeyByNameOutOfMemoryConcatPath | Não é possível obter a chave pelo nome devido à memória insuficiente ao concatenar o caminho.
3402 | ErrorGetKeyByNameOutOfMemoryConcatHeader | Não é possível obter a chave pelo nome devido à memória insuficiente ao concatenar o cabeçalho.
3403 | ErrorGetKeyByNameNoResponse | Não é possível obter a chave pelo nome devido à ausência de resposta do servidor.
3404 | ErrorGetKeyByNameJsonParser | Não é possível obter a chave pelo nome devido à falha ao analisar a resposta JSON.
3405 | ErrorGetKeyByNameExtractKeyNode | Não é possível obter a chave pelo nome devido à falha ao extrair o nó da chave da resposta.
3406 | ErrorGetKeyByNameExtractKeyId | Não é possível obter a chave pelo nome devido à falha ao extrair a Id da chave da resposta.
3407 | ErrorGetKeyByNameExtractKeyType | Não é possível obter a chave pelo nome devido à falha ao extrair o tipo de chave da resposta.
3408 | ErrorGetKeyByNameExtractKeyN | Não é possível obter a chave pelo nome devido à falha ao extrair a chave N da resposta.
3409 | ErrorGetKeyByNameBase64DecodeN | Não é possível obter a chave pelo nome devido à falha na decodificação de N do Base64.
3410 | ErrorGetKeyByNameExtractKeyE | Não é possível obter a chave pelo nome devido à falha ao extrair a chave E da resposta.
3411 | ErrorGetKeyByNameBase64DecodeE | Não é possível obter a chave pelo nome devido à falha na decodificação de E do Base64.
3412 | ErrorGetKeyByNameExtractKeyUri | Não é possível extrair o URI da chave da resposta.
3500 | ErrorBackupKeyOutOfMemoryConvertResponseString | Não é possível fazer backup da chave devido à memória insuficiente ao converter a cadeia de caracteres de resposta.
3501 | ErrorBackupKeyOutOfMemoryConcatPath | Não é possível fazer backup da chave devido à memória insuficiente ao concatenar o caminho.
3502 | ErrorBackupKeyOutOfMemoryConcatHeader | Não é possível fazer backup da chave devido à memória insuficiente ao concatenar o cabeçalho da solicitação.
3503 | ErrorBackupKeyNoResponse | Não é possível fazer backup da chave devido a nenhuma resposta do servidor.
3504 | ErrorBackupKeyJsonParser | Não é possível fazer backup da chave devido a uma falha ao analisar a resposta JSON.
3505 | ErrorBackupKeyExtractValue | Não é possível fazer backup da chave devido a uma falha ao extrair o valor da resposta JSON.
3506 | ErrorBackupKeyBase64DecodeValue | Não é possível fazer backup da chave devido a uma falha na codificação Base64 do campo de valor.
3600 | ErrorWrapKeyOutOfMemoryConvertResponseString | Não é possível encapsular a chave devido à memória insuficiente ao converter a cadeia de caracteres de resposta.
3601 | ErrorWrapKeyOutOfMemoryConcatPath | Não é possível encapsular a chave devido à memória insuficiente ao concatenar o caminho.
3602 | ErrorWrapKeyOutOfMemoryConcatHeader | Não é possível encapsular a chave devido à memória insuficiente ao concatenar o cabeçalho.
3603 | ErrorWrapKeyOutOfMemoryConcatBody | Não é possível encapsular a chave devido à memória insuficiente ao concatenar o corpo.
3604 | ErrorWrapKeyOutOfMemoryConvertEncodedBody | Não é possível encapsular a chave devido à memória insuficiente ao converter o corpo codificado.
3605 | ErrorWrapKeyBase64EncodeKey | Não é possível encapsular a chave devido a falha do Base64 na codificação da chave.
3606 | ErrorWrapKeyBase64DecodeValue | Não é possível encapsular a chave devido à falha do Base64 na codificação do valor da resposta.
3607 | ErrorWrapKeyJsonParser | Não é possível encapsular a chave devido a uma falha ao analisar a resposta JSON.
3608 | ErrorWrapKeyExtractValue | Não é possível encapsular a chave devido à falha ao extrair o valor da resposta.
3609 | ErrorWrapKeyNoResponse | Não é possível encapsular a chave devido a nenhuma resposta do servidor.
3700 | ErrorUnwrapKeyOutOfMemoryConvertResponseString | Não é possível desencapsular a chave devido à memória insuficiente ao converter a cadeia de caracteres de resposta.
3701 | ErrorUnwrapKeyOutOfMemoryConcatPath | Não é possível desencapsular a chave devido à memória insuficiente ao concatenar o caminho.
3702 | ErrorUnwrapKeyOutOfMemoryConcatHeader | Não é possível desencapsular a chave devido à memória insuficiente ao concatenar o cabeçalho.
3703 | ErrorUnwrapKeyOutOfMemoryConcatBody | Não é possível desencapsular a chave devido à memória insuficiente ao concatenar o corpo.
3704 | ErrorUnwrapKeyOutOfMemoryConvertEncodedBody | Não é possível desencapsular a chave devido à memória insuficiente ao converter o corpo codificado.
3705 | ErrorUnwrapKeyBase64EncodeKey | Não é possível desencapsular a chave devido a falha do Base64 na codificação da chave.
3706 | ErrorUnwrapKeyBase64DecodeValue | Não é possível desencapsular a chave devido à falha do Base64 na codificação do valor da resposta.
3707 | ErrorUnwrapKeyJsonParser | Não é possível desencapsular a chave devido à falha ao extrair o valor da resposta.
3708 | ErrorUnwrapKeyExtractValue | Não é possível desencapsular a chave devido à falha ao extrair o valor da resposta.
3709 | ErrorUnwrapKeyNoResponse | Não é possível desencapsular a chave devido a nenhuma resposta do servidor.
3800 | ErrorSecretAuthParamsGetRequestBody | Erro ao criar o corpo da solicitação usando o clientId e o segredo do AAD.
3801 | ErrorJWTTokenCreateHeader | Erro ao criar o cabeçalho de token JWT para autenticação com o AAD.
3802 | ErrorJWTTokenCreatePayloadGUID | Erro ao criar GUID para conteúdo de token JWT para autenticação com o AAD.
3803 | ErrorJWTTokenCreatePayload | Erro ao criar o conteúdo de token JWT para autenticação com o AAD.
3804 | ErrorJWTTokenCreateSignature | Erro ao criar a assinatura de token JWT para autenticação com o AAD.
3805 | ErrorJWTTokenSignatureHashAlg | Erro ao obter o algoritmo de hash SHA256 para autenticação com o AAD.
3806 | ErrorJWTTokenSignatureHash | Erro ao criar hash SHA256 para autenticação do token JWT com o AAD.
3807 | ErrorJWTTokenSignatureSignHash | Erro ao assinar o hash do token JWT para autenticação com o AAD.
3808 | ErrorJWTTokenCreateToken | Erro ao criar o token JWT para autenticação com o AAD.
3809 | ErrorPfxCertAuthParamsImportPfx | Erro ao importar o certificado Pfx para autenticação com o AAD.
3810 | ErrorPfxCertAuthParamsGetThumbprint | Erro ao obter a impressão digital do certificado pfx para autenticação com o AAD.
3811 | ErrorPfxCertAuthParamsGetPrivateKey | Erro ao obter a chave privada do certificado pfx para autenticação com o AAD.
3812 | ErrorPfxCertAuthParamsSignAlg | Erro ao obter algoritmo de assinatura RSA para autenticação de certificado Pfx com o AAD.
3813 | ErrorPfxCertAuthParamsImportForSign | Erro ao importar a chave privada Pfx para assinatura RSA para autenticação com o AAD.
3814 | ErrorPfxCertAuthParamsCreateRequestBody | Erro ao criar o corpo da solicitação do certificado Pfx para autenticação com o AAD.
3815 | ErrorPEMCertAuthParamsGetThumbprint | Erro de decodificação de Impressão Digital do Base64 para autenticação com o AAD.
3816 | ErrorPEMCertAuthParamsGetPrivateKey | Erro ao obter a chave privada RSA do PEM para autenticação com o AAD.
3817 | ErrorPEMCertAuthParamsSignAlg | Erro ao obter algoritmo de assinatura RSA para autenticação de chave PEM herdada com o AAD.
3818 | ErrorPEMCertAuthParamsImportForSign | Erro ao importar a chave privada PEM para assinatura RSA para autenticação com o AAD.
3819 | ErrorPEMCertAuthParamsCreateRequestBody | Erro ao criar o corpo da solicitação da chave privada PEM para autenticação com o AAD.
3820 | ErrorLegacyPrivateKeyAuthParamsSignAlg | Erro ao obter algoritmo de assinatura RSA para autenticação de chave privada herdada com o AAD.
3821 | ErrorLegacyPrivateKeyAuthParamsImportForSign | Erro ao importar a chave privada Herdada para assinatura RSA para autenticação com o AAD.
3822 | ErrorLegacyPrivateKeyAuthParamsCreateRequestBody        | Erro ao criar o corpo da solicitação da chave privada Herdada para autenticação com o AAD.
3900 | ErrorAKVDoesNotExist | Erro de nome da Internet não resolvido. Isso normalmente indica que o Azure Key Vault está excluído.
4000 | ErrorCreateKeyVaultRetryManagerOutOfMemory | Não é possível criar um RetryManager para a operação AKV devido à memória insuficiente.

Se você não vir o código de erro nesta tabela, aqui estão algumas outras razões pelas quais o erro pode estar ocorrendo:
  
- Talvez você não tenha acesso à Internet e não possa acessar o seu Azure Key Vault. Verifique a sua conexão com a Internet.  
  
- O serviço do Cofre de Chaves do Azure pode estar desativado. Tente novamente em outro momento.  
  
- Você pode ter removido a chave assimétrica do Cofre de Chaves do Azure ou [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Restaure a chave.  
  
- Se você receber um erro “Não é possível carregar a biblioteca”, verifique se você tem a versão apropriada do Visual Studio C++ Redistributable instalada com base na versão do SQL Server que está sendo executada. A tabela abaixo especifica qual versão será instalada por meio do Centro de Download da Microsoft.

O log de eventos do Windows também registra em log os erros associados ao Conector do SQL Server, que podem ajudar oferecendo um contexto adicional sobre o motivo real do erro. A origem no Log de Eventos do Aplicativo do Windows será "Conector do SQL Server para Microsoft Azure Key Vault".
  
Versão do SQL Server  |Link de instalação redistribuível
---------|---------
2008, 2008 R2, 2012, 2014 | [Pacotes Visual C++ Redistributable Packages para Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784)
2016 | [Pacotes Redistribuíveis do Visual C++ para Visual Studio 2015](https://www.microsoft.com/download/details.aspx?id=48145)
  
## <a name="additional-references"></a>Referências adicionais

 Mais sobre o Gerenciamento Extensível de Chaves:  
  
- [Gerenciamento Extensível de Chaves &#40;EKM&#41;](../../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
 Criptografias de SQL com suporte ao EKM:  
  
- [Habilitar TDE no SQL Server usando EKM](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
- [Criptografia de backup](../../../relational-databases/backup-restore/backup-encryption.md)  
  
- [Criar um backup criptografado](../../../relational-databases/backup-restore/create-an-encrypted-backup.md)  
  
 Comandos do [!INCLUDE[tsql](../../../includes/tsql-md.md)] Relacionados:  
  
- [sp_configure &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
- [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-cryptographic-provider-transact-sql.md)  
  
- [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)  
  
- [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
  
- [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
- [CREATE LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/create-login-transact-sql.md)  
  
- [ALTER LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-login-transact-sql.md)  
  
 Documentação do Cofre de Chaves do Azure:  
  
- [O que é o Cofre da Chave do Azure?](/azure/key-vault/general/basic-concepts)  
  
- [Introdução ao Azure Key Vault](/azure/key-vault/general/overview)  
  
- Referência dos [Cmdlets do Cofre de Chaves do Azure](/powershell/module/azurerm.keyvault/) do PowerShell  
  
## <a name="see-also"></a>Consulte Também

 [Gerenciamento extensível de chaves usando o Azure Key Vault](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
 [Usar o Conector do SQL Server com recursos de criptografia do SQL](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)  
 [Opção de configuração de servidor EKM provider enabled](../../../database-engine/configure-windows/ekm-provider-enabled-server-configuration-option.md)  
 [Setup Steps for Extensible Key Management Using the Azure Key Vault (Etapas de instalação para o gerenciamento extensível de chaves usando o Cofre de Chaves do Azure)](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)

Para ver mais scripts de exemplo, confira o blog em [Transparent Data Encryption e Gerenciamento Extensível de Chaves do SQL Server com o Azure Key Vault](https://techcommunity.microsoft.com/t5/sql-server/intro-sql-server-transparent-data-encryption-and-extensible-key/ba-p/1427549)