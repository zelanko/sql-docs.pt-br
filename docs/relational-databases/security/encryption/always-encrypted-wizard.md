---
title: Assistente Always Encrypted | Microsoft Docs
ms.custom: ''
ms.date: 05/04/2016
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.alwaysencryptedwizard.encryption.f1
- sql13.swb.alwaysencryptedwizard.f1
- sql.swb.alwaysencryptedwizard.masterkey.f1
helpviewer_keywords:
- Wizard, Always Encrypted
ms.assetid: 68daddc9-ce48-49aa-917f-6dec86ad5af5
author: aliceku
ms.author: aliceku
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 38077378d0980d351c4c65ca25b1574b7a7d7bc2
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51673567"
---
# <a name="always-encrypted-wizard"></a>Assistente de Always Encrypted
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Use o **Assistente de Sempre Criptografado** para ajudar a proteger dados confidenciais armazenados em um banco de dados do SQL Server. Sempre Criptografado permite que os clientes criptografem os dados confidenciais em aplicativos de cliente e nunca revelem as chaves de criptografia para o SQL Server. Como resultado, o Sempre Criptografado fornece uma separação entre aqueles que possuem os dados (e podem exibi-lo) e aqueles que gerenciam os dados (mas que não devem ter acesso).  Para obter uma descrição completa do recurso, veja [Always Encrypted &#40;Mecanismo de Banco de Dados&#41;](../../../relational-databases/security/encryption/always-encrypted-database-engine.md).  
 
 - Para ver uma explicação passo a passo completa que mostra como configurar o Always Encrypted com o assistente e usá-lo em um aplicativo cliente, confira [Tutorial do Banco de Dados SQL: Proteger dados confidenciais com o Always Encrypted](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted/).  
 
 - Para obter um vídeo que inclui o uso do assistente, confira [Keeping Sensitive Data Secure with Always Encrypted](https://channel9.msdn.com/events/DataDriven/SQLServer2016/AlwaysEncrypted)(Manter os dados confidenciais seguros com o Sempre Criptografado). Confira também o Blog da Equipe de Segurança do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [SSMS Encryption Wizard - Enabling Always Encrypted in a Few Easy Steps](https://blogs.msdn.com/b/sqlsecurity/archive/2015/11/01/ssms-encryption-wizard-enabling-always-encrypted-made-easy.aspx)(Assistente de Criptografia do SSMS – Habilitando o Sempre Criptografado em algumas etapas simples).  
 
 - **Permissões:** para consultar colunas criptografadas e selecionar chaves usando este assistente, é necessário ter as permissões `VIEW ANY COLUMN MASTER KEY DEFINITION` e `VIEW ANY COLUMN ENCRYPTION KEY DEFINITION` . Para criar novas chaves, você também deve ter as permissões `ALTER ANY COLUMN MASTER KEY` e `ALTER ANY COLUMN ENCRYPTION KEY` .  
 
 #### <a name="to-open-the-always-encrypted-wizard"></a>Para abrir o Assistente de Sempre Criptografado  
 
 1.  Conecte-se ao seu [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com o componente do Pesquisador de objetos do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
   
 2.  Clique com o botão direito do mouse no banco de dados, aponte para **Tarefas**e clique em **Criptografar Colunas**.  
   
 ## <a name="column-selection-page"></a>Página de seleção de coluna  
 - Localize uma tabela e uma coluna e selecione um tipo de criptografia (determinístico ou aleatório) e uma chave de criptografia para as colunas selecionadas. Para descriptografar uma coluna criptografada, selecione **Texto não criptografado**. Para girar uma chave de criptografia de coluna, selecione uma chave de criptografia diferente e o assistente descriptografará a coluna e criptografará novamente a coluna com a nova chave. (Há suporte no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para a criptografia de tabelas temporais e na memória, mas ela não pode ser configurada por este assistente.)  
 
## <a name="master-key-configuration-page"></a>Página de configuração de chave mestra  
 - Crie uma nova chave mestra de coluna no Repositório de Certificados do Windows ou no Cofre de Chaves do Azure. Para saber mais, confira os links abaixo em Armazenamento de chaves.  
 
 - Se você escolher uma chave de criptografia de coluna gerada automaticamente na página Seleção de Coluna, configure uma chave mestra de coluna com a qual a chave de criptografia de coluna gerada será criptografada. Se você já tiver uma chave mestra de coluna definida no banco de dados, selecione-a. (Para usar uma chave mestra de coluna existente, o usuário deve ter permissão para acessar a chave). Ou, você pode gerar uma chave mestra de coluna em um armazenamento de chaves selecionado (Repositório de Certificados do Windows ou o Cofre de Chaves do Azure) e definir a chave no banco de dados.  
 
 ### <a name="key-storage"></a>**Armazenamento de chaves**  
 
 - Escolha onde a chave mestra de coluna será armazenada.  
 
   - **Armazenar uma chave mestre no certificado do Windows** Para saber mais, confira [Using Certificate Stores](/windows/desktop/SecCrypto/using-certificate-stores)  
 
   - **Armazenamento de uma chave mestra em AKV** Para saber mais, confira [Introdução ao Cofre de Chaves do Azure](https://azure.microsoft.com/documentation/articles/key-vault-get-started/).  
 
 - Para gerar uma chave mestra de coluna no Cofre de Chaves do Azure, o usuário deve ter as permissões **WrapKey**, **UnwrapKey**, **Verify**e **Sign** para o cofre de chaves. Os usuários também podem precisar das permissões **Get**, **List**, **Create**, **Delete**, **Update**, **Import**, **Backup**e **Restore** . Para obter mais informações, confira [O que é o Cofre de Chaves do Azure?](https://azure.microsoft.com/documentation/articles/key-vault-whatis/) e   [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).  
 
 - O assistente só oferecia suporte a duas opções. Os Módulos de Segurança de Hardware e os repositórios de cliente devem ser configurados com [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-column-master-key-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)].  
 
 ## <a name="always-encrypted-terms"></a>Termos do Always Encrypted  
 
 - **Criptografia determinística** usa um método que sempre gera o mesmo valor criptografado para qualquer valor de texto não criptografado. O uso de criptografia determinística permite agrupamento, filtragem por igualdade e junção de tabelas com base em valores criptografados, mas também poderia habilitar usuários não autorizados para estimar informações sobre valores criptografados examinando padrões na coluna criptografada. Esse problema aumenta quando há um pequeno conjunto de possíveis valores criptografados, como True/False ou região Norte/Sul/Leste/Oeste. A criptografia determinística deve usar uma ordenação de colunas com uma ordem de classificação binary2 para as colunas de caracteres.  
 
 - **Criptografia aleatória** usa um método que criptografa os dados de uma maneira menos previsível. Criptografia aleatória é mais segura, mas impede pesquisas de igualdade, agrupamento, indexação e junção em colunas criptografadas.  

 - **Chaves mestras de coluna** são chaves de proteção usadas para criptografar as chaves de criptografia de coluna. Chaves mestras de coluna devem ser armazenadas em um armazenamento de chave confiável. Informações sobre as chaves mestras de coluna, incluindo sua localização, são armazenadas no banco de dados dos modos de exibição de catálogo do sistema.  

 - **Chaves de criptografia de coluna** são usadas para criptografar dados confidenciais armazenados em colunas de banco de dados. Todos os valores em uma coluna podem ser criptografados usando uma chave de criptografia de coluna única. Valores criptografados de chaves de criptografia de coluna são armazenados no banco de dados nos modos de exibição de catálogo do sistema. Você deve armazenar chaves de criptografia de coluna em um local seguro/confiável para backup.  

 ## <a name="see-also"></a>Consulte Também  
 - [Always Encrypted &#40;Mecanismo de Banco de Dados&#41;](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 - [Gerenciamento extensível de chaves usando o Cofre de Chaves do Azure &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
