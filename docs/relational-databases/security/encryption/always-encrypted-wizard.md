---
title: Configurar a criptografia de coluna usando o Assistente do Always Encrypted | Microsoft Docs
ms.custom: ''
ms.date: 10/30/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.alwaysencryptedwizard.encryption.f1
- sql13.swb.alwaysencryptedwizard.f1
- sql13.swb.alwaysencryptedwizard.masterkey.f1
helpviewer_keywords:
- Wizard, Always Encrypted
ms.assetid: 68daddc9-ce48-49aa-917f-6dec86ad5af5
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 71df93e5e7d628fadf5839e980f42a92138a5e0c
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594501"
---
# <a name="configure-column-encryption-using-always-encrypted-wizard"></a>Configurar a criptografia de coluna usando o Assistente do Always Encrypted
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

O Assistente do Always Encrypted é uma ferramenta poderosa que permite que você defina a configuração do [Always Encrypted](always-encrypted-database-engine.md) desejada para as colunas do banco de dados selecionadas. Dependendo da configuração atual e da configuração de destino desejada, o assistente pode criptografar uma coluna, descriptografá-la (remover a criptografia) ou criptografá-la novamente (por exemplo, usando uma nova chave de criptografia de coluna ou um tipo de criptografia diferente do tipo atual, configurado para a coluna). É possível configurar várias colunas em uma única execução do assistente.

O assistente permite criptografar colunas com chaves de criptografia de coluna existentes. Você também pode optar por gerar uma nova chave de criptografia de coluna ou, ainda, uma nova chave de criptografia de coluna e uma nova chave mestra de coluna. 

O assistente funciona movendo dados para fora do banco de dados e executando operações criptográficas no processo do SSMS. O assistente cria uma nova tabela (ou tabelas) com a configuração de criptografia desejada no banco de dados, carrega todos os dados das tabelas originais, executa as operações de criptografia solicitadas, carrega os dados nas novas tabelas e, em seguida, troca as tabelas originais pelas novas tabelas.

> [!NOTE]
> A execução de operações criptográficas pode levar muito tempo. Durante esse tempo, o banco de dados não estará disponível para gravar transações. O PowerShell é uma ferramenta recomendada para operações criptográficas em tabelas maiores. Confira [Configurar a criptografia de coluna usando o Always Encrypted com o PowerShell](configure-column-encryption-using-powershell.md).

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

> [!NOTE]
> Se estiver usando [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)] e sua instância do SQL Server estiver configurada com um enclave seguro, você poderá executar operações criptográficas in-loco, sem mover os dados para fora do banco de dados. Confira [Configurar a criptografia de coluna in-loco usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-configure-encryption.md). Observe que o assistente não dá suporte à criptografia in-loco.

::: moniker-end

Usar o PowerShell é recomendado 

 - Para ter uma explicação passo a passo e de ponta a ponta que mostra como configurar o Always Encrypted com o assistente e usá-lo em um aplicativo cliente, confira os seguintes tutoriais sobre o Banco de Dados SQL do Azure:
    - [Proteger dados confidenciais no Banco de Dados SQL do Azure com Always Encrypted e chaves mestras de coluna no repositório de certificados do Windows](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted/)
    - [Proteger dados confidenciais no Banco de Dados SQL do Azure com Always Encrypted e chaves mestras de coluna no Azure Key Vault](https://docs.microsoft.com/azure/sql-database/sql-database-always-encrypted-azure-key-vault)

 - Para obter um vídeo que inclui o uso do assistente, confira [Keeping Sensitive Data Secure with Always Encrypted](https://channel9.msdn.com/events/DataDriven/SQLServer2016/AlwaysEncrypted)(Manter os dados confidenciais seguros com o Sempre Criptografado). Confira também o Blog da Equipe de Segurança do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [SSMS Encryption Wizard - Enabling Always Encrypted in a Few Easy Steps](https://techcommunity.microsoft.com/t5/SQL-Server/SSMS-Encryption-Wizard-Enabling-Always-Encrypted-in-a-Few-Easy/ba-p/384545)(Assistente de Criptografia do SSMS – Habilitando o Sempre Criptografado em algumas etapas simples).  
 - Para obter informações sobre as chaves do Always Encrypted, confira [Visão geral do gerenciamento de chaves do Always Encrypted](overview-of-key-management-for-always-encrypted.md).
 - Para obter informações sobre os tipos de criptografia com suporte no Always Encrypted, confira [Seleção de criptografia determinística ou aleatória](always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption).
 
 ## <a name="permissions"></a>Permissões
Para executar operações criptográficas usando o assistente, você precisa ter as permissões **VIEW ANY COLUMN MASTER KEY DEFINITION** e **VIEW ANY COLUMN ENCRYPTION KEY DEFINITION**. Você também precisa ter permissões para acessar as chaves mestras de coluna que está usando nos repositórios de chaves que contêm as chaves:
- **Repositório de Certificados – Computador local**: você precisa ter acesso de leitura para o certificado que é usado como a chave mestra da coluna ou ser o administrador do computador.
- **Azure Key Vault**: você precisa das permissões get, unwrapKey e verify no cofre que contém a chave mestra da coluna.
- **Provedor do Repositório de Chaves (CNG)** : a permissão e as credenciais necessárias poderão ser solicitadas quando você usar um repositório de chaves ou uma chave, dependendo do repositório e da configuração do KSP.
- **Provedor de Serviços de Criptografia (CAPI)** : a permissão e as credenciais necessárias poderão ser solicitadas quando você usar um repositório de chaves ou uma chave, dependendo do repositório e da configuração do CSP.

Além disso, se estiver criando novas chaves usando o assistente, você deverá ter as permissões adicionais listadas em [Provisionar chaves mestras de coluna com a caixa de diálogo Nova Chave Mestra da Coluna](configure-always-encrypted-keys-using-ssms.md#provision-column-master-keys-with-the-new-column-master-key-dialog) e [Provisionar chaves de criptografia de coluna com a caixa de diálogo Nova Chave de Criptografia da Coluna](configure-always-encrypted-keys-using-ssms.md#provision-column-encryption-keys-with-the-new-column-encryption-key-dialog).

## <a name="open-the-always-encrypted-wizard"></a>Abrir o Assistente do Always Encrypted
Você pode iniciar o assistente em três níveis diferentes: 
- No nível do banco de dados, se quiser criptografar várias colunas localizadas em tabelas diferentes.
- No nível da tabela, se quiser criptografar várias colunas localizadas na mesma tabela.
- No nível da coluna, se quiser criptografar uma coluna específica.
 
 1. Conecte-se ao seu [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com o componente do Pesquisador de objetos do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
   
 2. Para criptografar:
     1. Várias colunas localizadas em tabelas diferentes em um banco de dados, clique com o botão direito do mouse no banco de dados, aponte para **Tarefas** e, em seguida, selecione **Criptografar Colunas**.
     1. Várias colunas localizadas na mesma tabela, navegue até a tabela, clique nela com o botão direito do mouse e selecione **Criptografar Colunas**.
     1. Uma coluna individual, navegue até a coluna, clique nela com o botão direito do mouse e, em seguida, selecione **Criptografar Colunas**.


   
 ## <a name="column-selection-page"></a>Página de seleção de coluna
Nessa página, você seleciona as colunas que deseja criptografar, criptografar novamente ou descriptografar e define a configuração de criptografia de destino para as colunas selecionadas.

Para criptografar uma coluna de texto não criptografado (uma coluna que não está criptografada), selecione um tipo de criptografia (**Determinística** ou **Aleatória**) e uma chave de criptografia para a coluna. 

Para alterar um tipo de criptografia ou girar (alterar) uma chave de criptografia de coluna para uma coluna já criptografada, selecione o tipo de criptografia desejado e a chave. 

Se quiser que o assistente criptografe ou criptografe novamente uma ou mais colunas usando uma nova chave de criptografia de coluna, escolha uma chave que contenha **(Novo)** no nome. O assistente gerará a chave.

Para descriptografar uma coluna criptografada, selecione **Texto não criptografado** para o tipo de criptografia.


> [!NOTE]
> O assistente não dá suporte a operações criptográficas em tabelas temporais e na memória. Você pode criar tabelas temporais ou na memória vazias usando Transact-SQL e inserir dados usando seu aplicativo.

## <a name="master-key-configuration-page"></a>Página de configuração de chave mestra
Se tiver selecionado uma chave de criptografia de coluna gerada automaticamente para qualquer coluna na página anterior, nesta página, você precisará selecionar uma chave mestra de coluna existente ou configurar uma nova chave mestra de coluna que criptografará a chave de criptografia de coluna. 

Ao configurar uma nova chave mestra de coluna, você pode escolher uma chave existente no Repositório de Certificados do Windows ou no Azure Key Vault e fazer com que o assistente crie apenas um objeto de metadados para a chave no banco de dados ou pode optar por gerar a chave e o objeto de metadados que descreve a chave no banco de dados. 

Para obter mais informações sobre como criar e armazenar chaves mestras de coluna no Repositório de Certificados do Windows, no Azure Key Vault ou em outros repositórios de chaves, confira [Criar e armazenar chaves mestras de coluna para o Always Encrypted](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md).

> [!TIP]
> O assistente permite que você procure e crie chaves somente no Repositório de Certificados do Windows e no Azure Key Vault. Ele também gera automaticamente os nomes das novas chaves e dos objetos de metadados do banco de dados que descrevem as chaves. Se precisar ter mais controle sobre como as chaves são provisionadas (e mais opções para um repositório de chaves que contém uma chave mestra de coluna), você poderá usar as caixas de diálogo **Nova Chave Mestra da Coluna** e **Nova Chave de Criptografia da Coluna** para criar as chaves primeiro e, em seguida, executar o assistente e escolher as chaves criadas. Confira [Provisionar chaves mestras de coluna com a caixa de diálogo Nova Chave Mestra da Coluna](configure-always-encrypted-keys-using-ssms.md#provision-column-master-keys-with-the-new-column-master-key-dialog) e [Provisionar chaves de criptografia de coluna com a caixa de diálogo Nova Chave de Criptografia da Coluna](configure-always-encrypted-keys-using-ssms.md#provision-column-encryption-keys-with-the-new-column-encryption-key-dialog). 

## <a name="next-steps"></a>Next Steps
- [Consultar colunas usando o Always Encrypted com o SQL Server Management Studio](always-encrypted-query-columns-ssms.md)
- [Desenvolver aplicativos usando o Always Encrypted](always-encrypted-client-development.md)

## <a name="see-also"></a>Consulte Também  
 - [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
 - [Visão geral do gerenciamento de chaves do Always Encrypted](overview-of-key-management-for-always-encrypted.md) 
 - [Configurar o Always Encrypted usando o SQL Server Management Studio](configure-always-encrypted-using-sql-server-management-studio.md)
 - [Provisionar chaves do Always Encrypted usando o PowerShell](configure-always-encrypted-keys-using-powershell.md)
 - [Configurar a criptografia de coluna usando o Always Encrypted com o PowerShell](configure-column-encryption-using-powershell.md)
 - [Configurar a criptografia de coluna usando o Always Encrypted com um pacote de DAC](configure-always-encrypted-using-dacpac.md)
