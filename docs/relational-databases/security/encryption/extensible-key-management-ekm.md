---
title: "EKM (Gerenciamento extensível de chaves) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Key Management
- Extensible Key Management
- EKM, described
ms.assetid: 9bfaf500-2d1e-4c02-b041-b8761a9e695b
caps.latest.revision: 46
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 632fec019b757d782e7bd54f6854e815ccd2afcf
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="extensible-key-management-ekm"></a>Gerenciamento extensível de chaves (EKM)
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oferece funcionalidades de criptografia de dados com o *EKM* (Gerenciador Extensível de Chaves), usando o provedor *Microsoft Cryptographic API* (MSCAPI) para criptografia e geração de chave. As chaves de criptografia de dados e a criptografia da chave são criadas em contêineres chaves e devem ser exportadas por um provedor antes de serem armazenadas no banco de dados. Essa abordagem habilita o gerenciamento de chave, que inclui uma hierarquia de chave de criptografia e backup da chave, para ser tratado pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Com a crescente demanda de conformidade reguladora e referente à privacidade dos dados, as organizações estão tirando vantagem da criptografia como meio de oferecer uma solução de "defesa aprofundada". Essa abordagem geralmente não é muito prática se usar só as ferramentas de gerenciamento de criptografia do banco de dados. Os fornecedores de hardware fornecem produtos que corrigem o gerenciamento de chave empresarial, usando o *HSM* (módulos de segurança do hardware). Os dispositivos HSM armazenam chaves de criptografia em módulos de software ou hardware. É uma solução mais segura porque as chaves de criptografia não estão com dados de criptografia.  
  
 Vários fornecedores oferecem HSM para gerenciamento de chave e aceleração de criptografia. Os dispositivos de HSM usam interfaces de hardware com um processo de servidor como um intermediário entre um aplicativo e um HSM. Os fornecedores também implementam provedores de MSCAPI nos seus módulos, que podem ser hardware ou software. O MSCAPI oferece frequentemente só um subconjunto da funcionalidade que é oferecida por um HSM. Os fornecedores também podem prover software de gerenciamento para HSM, configuração fundamental e acesso fundamental.  
  
 As implementações HSM variam conforme o fornecedor e usá-los com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] requer uma interface comum. Embora o MSCAPI ofereça esta interface, ele dá suporte apenas a um subconjunto das características do HSM. Também existem outras limitações, como incapacidade de persistir chaves simétricas, e uma falta de suporte orientado por sessão.  
  
 O Gerenciador Extensível de Chaves [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] permite que os fornecedores do EKM/HSM de terceiros registrem os seus módulos no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Quando registrado, os usuários [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] podem usar as chaves de criptografia armazenadas em módulos EKM. Isso permite o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] acessar os recursos avançados de criptografia, esses módulos oferecem suporte à criptografia em massa e à descriptografia e, às funções de gerenciamento de chave, como envelhecimento de chave e rotação de chave.  
  
 Ao executar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em uma VM do Azure, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pode usar chaves armazenadas no [Cofre da Chave do Azure](http://go.microsoft.com/fwlink/?LinkId=521401). Para obter mais informações, veja [Gerenciamento extensível de chaves usando o Cofre de Chaves do Azure &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md).  
  
## <a name="ekm-configuration"></a>Configuração de EKM  
 O gerenciamento extensível de chaves não está disponível em todas as edições do [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 Por padrão, o Gerenciador Extensível de Chaves está desativado. Para habilitar esse recurso, use o comando sp_configure que tem a seguinte opção e valor, conforme o exemplo a seguir:  
  
```  
sp_configure 'show advanced', 1  
GO  
RECONFIGURE  
GO  
sp_configure 'EKM provider enabled', 1  
GO  
RECONFIGURE  
GO  
```  
  
> [!NOTE]  
>  Se você usar o comando sp_configure para esta opção em edições do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que não dão suporte a EKM, receberá um erro.  
  
 Para desabilitar o recurso, defina o valor para **0**. Para mais informações sobre como definir opções de servidor, veja [sp_configure &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
## <a name="how-to-use-ekm"></a>Como usar EKM  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] O Gerenciamento Extensível de Chaves permite que as chaves de criptografia protejam os arquivos de banco de dados a serem armazenados em um dispositivo pronto para uso, como um smartcard, dispositivo USB ou o módulo EKM/HSM. O que também habilita proteção de dados a partir dos administradores de banco de dados (exceto os membros do grupo sysadmin ). Com o uso de chaves de criptografia, é possível criptografar dados aos quais somente o usuário do banco de dados tem acesso no módulo externo de EKM/HSM.  
  
 O Gerenciador Extensível de Chaves também oferece os seguintes benefícios:  
  
-   Verificação de autorização adicional (habilitando a separação de tarefas).  
  
-   Alto desempenho de criptografia/descriptografia com base em hardware.  
  
-   Geração de chave de criptografia externa.  
  
-   Armazenamento de chave de criptografia externa (separação física de dados e chaves).  
  
-   Recuperação de chave de criptografia.  
  
-   Retenção de chave de criptografia externa (habilita a rotação de chave de criptografia).  
  
-   Recuperação mais fácil da chave de criptografia.  
  
-   Distribuição de chave de criptografia manejável.  
  
-   Disposição segura de chave de criptografia.  
  
 Você pode usar o Gerenciamento Extensível de Chaves para uma combinação de nome de usuário e senha ou outros métodos definidos pelo driver de EKM.  
  
> [!CAUTION]  
>  Para solução de problemas, o suporte técnico do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] poderá solicitar a chave de criptografia do provedor EKM. Talvez seja necessário acessar os processos ou as ferramentas do fornecedor para ajudar a resolver um problema.  
  
### <a name="authentication-with-an-ekm-device"></a>Autenticação com um dispositivo EKM  
 Um módulo EKM pode oferecer suporte para mais de um tipo de autenticação. Cada provedor mostra apenas um tipo de autenticação para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], isto é, se o módulo oferecer suporte aos tipos de autenticação Básica ou a outros, ele mostrará um ou outro, mas não os dois.  
  
#### <a name="ekm-device-specific-basic-authentication-using-usernamepassword"></a>Nome do usuário/senha de Autenticação Básica Específica do Dispositivo EKM  
 Para esses módulos EKM que dão suporte à autenticação Básica usando um par *nome de usuário/senha* , o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fornece autenticação transparente que usa credenciais. Para mais informações sobre credenciais, consulte [Credenciais &#40;Mecanismo de Banco de Dados&#41;](../../../relational-databases/security/authentication-access/credentials-database-engine.md).  
  
 É possível criar uma credencial para um provedor EKM e mapear (ambas as contas do Windows e do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ) para acessar um módulo EKM por logon. O campo da credencial *Identify* contém o nome do usuário; o campo *secret* contém uma senha para conectar a um módulo de EKM.  
  
 Se não houver nenhuma credencial mapeada de logon para o provedor EKM, a credencial mapeada para conta de serviço [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] será usada.  
  
 Um logon pode ter várias credenciais mapeadas para isto, contanto que elas sejam usadas para provedores de EKM diferentes. Deve haver só uma credencial mapeada por provedor de EKM por logon. A mesma credencial pode ser mapeada para outros logons.  
  
#### <a name="other-types-of-ekm-device-specific-authentication"></a>Outros tipos de autenticação de dispositivo específico EKM  
 Para os módulos EKM que tenham autenticação diferente do Windows ou combinações de *usuário/senha* , a autenticação deve ser executada independentemente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
### <a name="encryption-and-decryption-by-an-ekm-device"></a>Criptografia e decodificação por um dispositivo EKM  
 É possível usar as seguintes funções e características para criptografar e descriptografar dados, usando chaves simétricas e assimétricas:  
  
|Função ou recurso|Referência|  
|-------------------------|---------------|  
|Criptografia de chave simétrica|[CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)|  
|Criptografia de chave assimétrica|[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)|  
|EncryptByKey(key_guid, 'cleartext', …)|[ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbykey-transact-sql.md)|  
|DecryptByKey(ciphertext, …)|[DECRYPTBYKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/decryptbykey-transact-sql.md)|  
|EncryptByAsmKey(key_guid, 'cleartext')|[ENCRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbyasymkey-transact-sql.md)|  
|DecryptByAsmKey(ciphertext)|[DECRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/decryptbyasymkey-transact-sql.md)|  
  
#### <a name="database-keys-encryption-by-ekm-keys"></a>Criptografia das chaves do banco de dados pelas chaves EKM  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pode usar as chaves EKM para criptografar outras chaves em um banco de dados. É possível criar e usar chaves simétricas e assimétricas em um dispositivo de EKM. Você pode criptografar chaves simétricas nativas (diferente de EKM) com chaves assimétricas do EKM.  
  
 O exemplo a seguir cria uma chave simétrica de banco de dados e criptografa a chave, usando uma chave em um módulo EKM.  
  
```  
CREATE SYMMETRIC KEY Key1  
WITH ALGORITHM = AES_256  
ENCRYPTION BY EKM_AKey1;  
GO  
--Open database key  
OPEN SYMMETRIC KEY Key1  
DECRYPTION BY EKM_AKey1  
```  
  
 Para mais informações sobre o Banco de Dados e as Chaves de Servidor no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], consulte [Chaves de criptografia do SQL Server e banco de dados &#40;Mecanismo de Banco de Dados&#41;](../../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md).  
  
> [!NOTE]  
>  Não é possível criptografar uma chave EKM com outra chave EKM.  
>   
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não dá suporte para assinar módulos com chaves assimétricas geradas a partir do provedor EKM.  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
 [Opção de configuração de servidor EKM provider enabled](../../../database-engine/configure-windows/ekm-provider-enabled-server-configuration-option.md)  
  
 [Habilitar TDE no SQL Server usando EKM](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
 [Gerenciamento extensível de chaves usando o Cofre de Chaves do Azure &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
## <a name="see-also"></a>Consulte também  
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-cryptographic-provider-transact-sql.md)   
 [DROP CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-cryptographic-provider-transact-sql.md)   
 [ALTER CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-cryptographic-provider-transact-sql.md)   
 [sys.cryptographic_providers &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-cryptographic-providers-transact-sql.md)   
 [sys.dm_cryptographic_provider_sessions &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-sessions-transact-sql.md)   
 [sys.dm_cryptographic_provider_properties &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-properties-transact-sql.md)   
 [sys.dm_cryptographic_provider_algorithms &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-algorithms-transact-sql.md)   
 [sys.dm_cryptographic_provider_keys &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-keys-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-login-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [Fazer backup e restaurar as chave de criptografia do Reporting Services](../../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [Excluir e recriar chaves de criptografia &#40;SSRS Configuration Manager&#41;](../../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [Adicionar e remover chaves de criptografia para implantação escalável &#40;Gerenciador de Configurações do SSRS&#41;](../../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md)   
 [Fazer backup da chave mestra de serviço](../../../relational-databases/security/encryption/back-up-the-service-master-key.md)   
 [Restaurar a chave mestra de serviço](../../../relational-databases/security/encryption/restore-the-service-master-key.md)   
 [Criar uma chave mestra de banco de dados](../../../relational-databases/security/encryption/create-a-database-master-key.md)   
 [Fazer backup da chave mestra de um banco de dados](../../../relational-databases/security/encryption/back-up-a-database-master-key.md)   
 [Restaurar uma chave mestra de banco de dados](../../../relational-databases/security/encryption/restore-a-database-master-key.md)   
 [Criar chaves simétricas idênticas em dois servidores](../../../relational-databases/security/encryption/create-identical-symmetric-keys-on-two-servers.md)  
  
  

