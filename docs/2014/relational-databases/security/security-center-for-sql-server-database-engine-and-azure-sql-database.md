---
title: Centro de segurança do Mecanismo de Banco de Dados do SQL Server e do Banco de Dados SQL do Azure | Microsoft Docs
ms.custom: ''
ms.date: 09/23/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- Security [SQL Server]
helpviewer_keywords:
- SQL Server, security
- security [SQL Server]
- database security [SQL Server]
- databases [SQL Server], security
ms.assetid: dfb39d16-722a-4734-94bb-98e61e014ee7
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 131fb3639f84c1b59796d59bcfff17159da8f063
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028665"
---
# <a name="security-center-for-sql-server-database-engine-and-azure-sql-database"></a>Central de segurança do Mecanismo de Banco de Dados do SQL Server e Banco de Dados SQL do Azure
  Esta página fornece links para ajudá-lo a localizar as informações necessárias sobre segurança e proteção no [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)].  
  
> [!NOTE]  
>  Os recursos do [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] continuam a melhorar. Consulte a versão mais recente deste tópico para obter as informações mais recentes sobre o [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
|Authentication quem é você?|Nesse o que você pode fazer?|Encripta armazenar dados secretos|Segurança da conexão: restringir e proteger|Auditoria do: acesso de gravação|  
|----------------------------------|-------------------------------------|-------------------------------------|---------------------------------------------------|--------------------------------|  
|**Quem autentica?**<br /><br /> [![Central de segurança mapear autenticação do Windows](../../database-engine/media/security-center-map-windows-authenticaion.png "Central de segurança mapear autenticação do Windows")](https://msdn.microsoft.com/library/ms144284.aspx)<br /><br /> <br /><br /> [![SQL Server autenticação do mapa da central de segurança](../../database-engine/media/security-center-map-sql-authenticaion.png "SQL Server autenticação do mapa da central de segurança")](https://msdn.microsoft.com/library/ms144284.aspx)<br /><br /> **Onde é autenticado?**<br /><br /> [![Usuários e logons do mapa da central de segurança](../../database-engine/media/security-center-map-logins-users.png "Usuários e logons do mapa da central de segurança")](https://msdn.microsoft.com/library/aa337562.aspx)<br /><br /> <br /><br /> [![Mapa da central de segurança-usuários de banco de dados independentes](../../database-engine/media/security-center-map-contained-users.png "Mapa da central de segurança-usuários de banco de dados independentes")](https://msdn.microsoft.com/library/ff929188.aspx)<br /><br /> **Usando outras identidades**<br /><br /> [![Mapear credenciais da central de segurança](../../database-engine/media/security-center-map-credentials.png "Mapear credenciais da central de segurança")](https://msdn.microsoft.com/library/ms161950.aspx)<br /><br /> [![Executar como logon do mapa da central de segurança](../../database-engine/media/security-center-map-exec-as-login.png "Executar como logon do mapa da central de segurança")](https://msdn.microsoft.com/library/ms181362.aspx)<br /><br /> [![Executar como usuário do mapa da central de segurança](../../database-engine/media/security-center-map-exec-as-user.png "Executar como usuário do mapa da central de segurança")](https://msdn.microsoft.com/library/ms181362.aspx)<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")|**Concedendo, revogando e negando permissões**<br /><br /> [![Mapear classes protegíveis de central de segurança](../../database-engine/media/security-center-map-securable-classes.png "Mapear classes protegíveis de central de segurança")](https://msdn.microsoft.com/library/ms190401.aspx)<br /><br /> [![Permissões do servidor de mapa da central de segurança](../../database-engine/media/security-center-map-srv-perms.png "Permissões do servidor de mapa da central de segurança")](https://msdn.microsoft.com/library/ms191291.aspx)<br /><br /> [![Permissões de banco de dados do mapa da central de segurança](../../database-engine/media/security-center-map-db-perms.png "Permissões de banco de dados do mapa da central de segurança")](https://msdn.microsoft.com/library/ms191291.aspx)<br /><br /> **Segurança por funções**<br /><br /> [![Funções de servidor do mapa da central de segurança](../../database-engine/media/security-center-map-srv-roles.png "Funções de servidor do mapa da central de segurança")](https://msdn.microsoft.com/library/ms188659.aspx)<br /><br /> [![Central de segurança mapear funções de banco de dados](../../database-engine/media/security-center-map-db-roles.png "Central de segurança mapear funções de banco de dados")](https://msdn.microsoft.com/library/ms189121.aspx)<br /><br /> `Restricting Data Access to Selected Data Elements`<br /><br /> [![Exibições e procedimentos do mapa da central de segurança](../../database-engine/media/security-center-map-view-procs.png "Exibições e procedimentos do mapa da central de segurança")](https://msdn.microsoft.com/library/ms175503.aspx)<br /><br /> [![Segurança em nível de linha de mapa da central de segurança](../../database-engine/media/security-center-map-row-level-sec.png "Segurança em nível de linha de mapa da central de segurança")](https://msdn.microsoft.com/library/dn765131.aspx)<br /><br /> [![Máscara de dados dinâmicos de mapa da central de segurança](../../database-engine/media/security-center-map-data-masking.png "Máscara de dados dinâmicos de mapa da central de segurança")](https://azure.microsoft.com/documentation/articles/sql-database-dynamic-data-masking-get-started/)<br /><br /> [![Objetos assinados do mapa da central de segurança](../../database-engine/media/security-center-map-signed-objects.png "Objetos assinados do mapa da central de segurança")](https://msdn.microsoft.com/library/ms181700.aspx)<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")|**Criptografando arquivos**<br /><br /> [![Mapa da central de segurança BitLocker](../../database-engine/media/security-center-map-bitlocker.png "Mapa da central de segurança BitLocker")](https://support.microsoft.com/en-us/kb/2855131)<br /><br /> [![Central de segurança mapear criptografia NTFS](../../database-engine/media/security-center-map-ntfs-encryp.png "Central de segurança mapear criptografia NTFS")](https://msdn.microsoft.com/library/dd163562.aspx)<br /><br /> [![TDE do mapa da central de segurança](../../database-engine/media/security-center-map-tde.png "TDE do mapa da central de segurança")](https://msdn.microsoft.com/library/bb934049.aspx)<br /><br /> [![Central de segurança mapear criptografia de backup](../../database-engine/media/security-center-map-backup-encryp.png "Central de segurança mapear criptografia de backup")](https://msdn.microsoft.com/library/dn449489.aspx)<br /><br /> **Criptografando fontes**<br /><br /> [![Mapa da central de segurança EKM](../../database-engine/media/security-center-map-ekm.png "Mapa da central de segurança EKM")](https://msdn.microsoft.com/library/bb895340.aspx)<br /><br /> [![Azure Key Vault de mapa da central de segurança](../../database-engine/media/security-center-map-key-vault.png "Azure Key Vault de mapa da central de segurança")](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)<br /><br /> **Criptografia de chave de & de dados de coluna**<br /><br /> [![Criptografia do mapa da central de segurança por certificado](../../database-engine/media/security-center-map-cert.png "Criptografia do mapa da central de segurança por certificado")](https://msdn.microsoft.com/library/ms188061.aspx)<br /><br /> [![Mapeamento da central de segurança criptografar por chave simétrica](../../database-engine/media/security-center-map-sym-key.png "Mapeamento da central de segurança criptografar por chave simétrica")](https://msdn.microsoft.com/library/ms174361.aspx)<br /><br /> [![Mapeamento da central de segurança criptografar por chave assimétrica](../../database-engine/media/security-center-map-asym-key.png "Mapeamento da central de segurança criptografar por chave assimétrica")](https://msdn.microsoft.com/library/ms186950.aspx)<br /><br /> [![Criptografia do mapa da central de segurança por senha](../../database-engine/media/security-center-map-passphrase.png "Criptografia do mapa da central de segurança por senha")](https://msdn.microsoft.com/library/ms190357.aspx)|**Proteção de firewall**<br /><br /> [![Central de segurança mapear Firewall do Windows](../../database-engine/media/security-center-map-windows-firewall.png "Central de segurança mapear Firewall do Windows")](https://msdn.microsoft.com/library/ms175043.aspx)<br /><br /> [![Firewall do serviço de mapa da central de segurança](../../database-engine/media/security-center-map-service-firewall.png "Firewall do serviço de mapa da central de segurança")](https://msdn.microsoft.com/library/azure/ee621782.aspx)<br /><br /> [![Central de segurança mapear o Firewall do banco de dados](../../database-engine/media/security-center-map-db-firewall.png "Central de segurança mapear o Firewall do banco de dados")](https://msdn.microsoft.com/library/azure/ee621782.aspx)<br /><br /> **Criptografando dados em trânsito**<br /><br /> [![Mapa da central de segurança-SSL forçado](../../database-engine/media/security-center-map-forced-ssl.png "Mapa da central de segurança-SSL forçado")](https://msdn.microsoft.com/library/ms191192.aspx)<br /><br /> [![Central de segurança mapear SSL opcional](../../database-engine/media/security-center-map-opt-ssl.png "Central de segurança mapear SSL opcional")](https://msdn.microsoft.com/library/ms191192.aspx)<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")|**Auditoria automatizada**<br /><br /> [![Auditoria de SQL Server de mapa da central de segurança](../../database-engine/media/security-center-map-sql-audit.png "Auditoria de SQL Server de mapa da central de segurança")](https://msdn.microsoft.com/library/cc280386.aspx)<br /><br /> [![Auditoria do banco de dados SQL do mapa da central de segurança](../../database-engine/media/security-center-map-sqldb-audit.png "Auditoria do banco de dados SQL do mapa da central de segurança")](https://azure.microsoft.com/documentation/articles/sql-database-auditing-get-started/)<br /><br /> **Auditoria personalizada**<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")<br /><br /> [![Gatilhos de mapa da central de segurança](../../database-engine/media/security-center-map-triggers.png "Gatilhos de mapa da central de segurança")](https://msdn.microsoft.com/library/ms175941.aspx)<br /><br /> **Conformidade**<br /><br /> [![SecCtrCompliance](../../database-engine/media/secctrcompliance.png "SecCtrCompliance")](https://azure.microsoft.com/support/trust-center/services/)<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")<br /><br /> ![Legenda da central de segurança](../../database-engine/media/security-center-map-legend.png "Legenda da central de segurança")|  
  
## <a name="links-to-specific-related-topics"></a>Links para tópicos relacionados específicos  
 ![Ícone de pasta de arquivo pequeno](../../integration-services/media/filefolder-small.gif "Ícone de pasta de arquivo pequeno") **Autenticação: Quem é você?**  
 **Quem se autentica? (Windows ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])**  
  
-   [Escolher um modo de autenticação](choose-an-authentication-mode.md)  
  
 **Autenticação no banco de dados mestre** (logons e usuários de banco de dados)  
  
-   [Criar um logon do SQL Server](authentication-access/create-a-login.md)  
  
-   [Gerenciando bancos de dados e logons no banco de dados do Azure SQL](https://msdn.microsoft.com/library/ee336235.aspx)  
  
-   [Criar um usuário de banco de dados](authentication-access/create-a-database-user.md)  
  
 **Autenticar em um banco de dados de usuário**  
  
-   [Usuários de bancos de dados independentes - Tornando seu banco de dados portátil](contained-database-users-making-your-database-portable.md)  
  
 **Usando outras identidades**  
  
-   [Credenciais &#40;Mecanismo de Banco de Dados&#41;](authentication-access/credentials-database-engine.md)  
  
-   [Executar como outro logon](/sql/t-sql/statements/execute-as-transact-sql)  
  
-   [Executar como outro usuário de banco de dados](/sql/t-sql/statements/execute-as-transact-sql)  
  
 ![Ícone de pasta de arquivo pequeno](../../integration-services/media/filefolder-small.gif "Ícone de pasta de arquivo pequeno") **Criptografia: Armazenando dados secretos**  
 **Criptografando arquivos**  
  
-   [BitLocker (nível de unidade)](https://support.microsoft.com/kb/2855131)  
  
-   [Criptografia de NTFS (nível de pasta)](https://msdn.microsoft.com/library/dd163562.aspx)  
  
-   [Criptografia transparente de dados (nível de arquivo)](encryption/transparent-data-encryption.md)  
  
-   [Criptografia de backup (nível de arquivo)](../backup-restore/backup-encryption.md)  
  
 **Criptografando fontes**  
  
-   [Módulo de Gerenciamento Extensível de Chaves](encryption/extensible-key-management-ekm.md)  
  
-   [Chaves armazenadas no cofre principal do Azure](encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
 **Coluna, dados e criptografia de chave**  
  
-   [Criptografar por certificado](/sql/t-sql/functions/encryptbycert-transact-sql)  
  
-   [Criptografar por chave assimétrica](/sql/t-sql/functions/encryptbyasymkey-transact-sql)  
  
-   [Criptografar por chave simétrica](/sql/t-sql/functions/encryptbykey-transact-sql)  
  
-   [Criptografar por frase secreta](/sql/t-sql/functions/encryptbypassphrase-transact-sql)  
  
 ![Ícone de pasta de arquivo pequeno](../../integration-services/media/filefolder-small.gif "Ícone de pasta de arquivo pequeno") **Autorização: O que você pode fazer?**  
 **Concedendo, revogando e negando permissões**  
  
-   [Hierarquia de permissões &#40;Mecanismo de Banco de Dados&#41;](permissions-hierarchy-database-engine.md)  
  
-   [Permissões](permissions-database-engine.md)  
  
-   [Protegíveis](securables.md)  
  
 **Segurança por funções**  
  
-   [Funções de nível de servidor](authentication-access/server-level-roles.md)  
  
-   [Funções de nível de banco de dados](authentication-access/database-level-roles.md)  
  
 `Restricting Data Access to Selected Data Elements`  
  
-   Restringir acesso a dados usando [Exibições](../views/views.md) e [Procedimentos](../stored-procedures/stored-procedures-database-engine.md)  
  
-   [Segurança em nível de linha](https://msdn.microsoft.com/library/azure/dn765131.aspx)  
  
-   [Mascaramento de dados dinâmicos](https://azure.microsoft.com/documentation/articles/sql-database-dynamic-data-masking-get-started/)  
  
-   [Objetos assinados](/sql/t-sql/statements/add-signature-transact-sql)  
  
 ![Ícone de pasta de arquivo pequeno](../../integration-services/media/filefolder-small.gif "Ícone de pasta de arquivo pequeno") **Segurança da conexão: Restringindo e protegendo**  
 **Proteção de firewall**  
  
-   [Configurar um Firewall do Windows para acesso ao Mecanismo de Banco de Dados](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)  
  
-   [Configurações de Firewall de banco de dados do SQL do Azure](/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database)  
  
-   [Configurações de Firewall de serviço do Azure](/sql/relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database)  
  
 **Criptografando dados em trânsito**  
  
-   [Protocolo SSL para o mecanismo de banco de dados](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)  
  
-   [Protocolo SSL para o banco de dados SQL](https://msdn.microsoft.com/library/azure/ff394108.aspx)  
  
 ![Ícone de pasta de arquivo pequeno](../../integration-services/media/filefolder-small.gif "Ícone de pasta de arquivo pequeno") **Auditoria: Registro de acesso**  
 **Auditoria automatizada**  
  
-   [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](auditing/sql-server-audit-database-engine.md)  
  
-   [Auditoria do banco de dados SQL](https://azure.microsoft.com/documentation/articles/sql-database-auditing-get-started/)  
  
 **Implementação de auditoria personalizada**  
  
-   Criando [DDL Triggers](../triggers/ddl-triggers.md) e [DML Triggers](../triggers/dml-triggers.md)  
  
 ![Ícone de pasta de arquivo pequeno](../../integration-services/media/filefolder-small.gif "Ícone de pasta de arquivo pequeno") **Conformidade** com o  
 **SQL Server**  
  
-   [critérios comuns](https://go.microsoft.com/fwlink/?LinkId=616319)  
  
 **Banco de Dados SQL**  
  
-   [Central de Confiabilidade do Microsoft Azure: conformidade por recurso](https://azure.microsoft.com/support/trust-center/services/)  
  
## <a name="see-also"></a>Consulte também  
 [Protegendo o SQL Server](securing-sql-server.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](authentication-access/principals-database-engine.md)   
 [Certificados e chaves assimétricas do SQL Server](sql-server-certificates-and-asymmetric-keys.md)   
 [Criptografia do SQL Server](encryption/sql-server-encryption.md)   
 [Configuração da Área de Superfície](surface-area-configuration.md)   
 [Senhas fortes](strong-passwords.md)   
 [Propriedade de banco de dados TRUSTWORTHY](trustworthy-database-property.md)   
 [Recursos e tarefas do Mecanismo de Banco de Dados](../../database-engine/database-engine-features-and-tasks.md)  
  
  
