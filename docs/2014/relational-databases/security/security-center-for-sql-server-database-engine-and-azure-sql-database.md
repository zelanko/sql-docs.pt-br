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
ms.openlocfilehash: fc99b725f4c5895306d544df14bf2a9390189066
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75244531"
---
# <a name="security-center-for-sql-server-database-engine-and-azure-sql-database"></a>Central de segurança do Mecanismo de Banco de Dados do SQL Server e Banco de Dados SQL do Azure
  Esta página fornece links para ajudá-lo a localizar as informações necessárias sobre segurança e proteção no [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)].  
  
> [!NOTE]  
>  Os recursos do [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] continuam a melhorar. Consulte a versão mais recente deste tópico para obter as informações mais recentes sobre o [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
|Autenticação: quem é você?|Autorização: o que você pode fazer?|Criptografia: armazenando dados secretos|Segurança de conexão: restringir e proteger|Auditoria: acesso à gravação|  
|----------------------------------|-------------------------------------|-------------------------------------|---------------------------------------------------|--------------------------------|  
|**Quem autentica?**<br /><br /> [![Mapa da Central de Segurança - Autenticação do Windows](../../database-engine/media/security-center-map-windows-authenticaion.png "Mapa da Central de Segurança - Autenticação do Windows")](https://msdn.microsoft.com/library/ms144284.aspx)<br /><br /> <br /><br /> [![Mapa da Central de Segurança - Autenticação do SQL Server](../../database-engine/media/security-center-map-sql-authenticaion.png "Mapa da Central de Segurança - Autenticação do SQL Server")](https://msdn.microsoft.com/library/ms144284.aspx)<br /><br /> **Onde é autenticado?**<br /><br /> [![Mapa da Central de Segurança - Logons e usuários](../../database-engine/media/security-center-map-logins-users.png "Mapa da Central de Segurança - Logons e usuários")](https://msdn.microsoft.com/library/aa337562.aspx)<br /><br /> <br /><br /> [![Mapa da Central de Segurança - Usuários do banco de dados independente](../../database-engine/media/security-center-map-contained-users.png "Mapa da Central de Segurança - Usuários do banco de dados independente")](https://msdn.microsoft.com/library/ff929188.aspx)<br /><br /> **Usando outras identidades**<br /><br /> [![Mapa da Central de Segurança - Credenciais](../../database-engine/media/security-center-map-credentials.png "Mapa da Central de Segurança - Credenciais")](https://msdn.microsoft.com/library/ms161950.aspx)<br /><br /> [![Mapa da Central de Segurança - Executar como logon](../../database-engine/media/security-center-map-exec-as-login.png "Mapa da Central de Segurança - Executar como logon")](https://msdn.microsoft.com/library/ms181362.aspx)<br /><br /> [![Mapa da Central de Segurança - Executar como usuário](../../database-engine/media/security-center-map-exec-as-user.png "Mapa da Central de Segurança - Executar como usuário")](https://msdn.microsoft.com/library/ms181362.aspx)<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")|**Concedendo, revogando e negando permissões**<br /><br /> [![Mapa da Central de Segurança - Classes Protegíveis](../../database-engine/media/security-center-map-securable-classes.png "Mapa da Central de Segurança - Classes Protegíveis")](https://msdn.microsoft.com/library/ms190401.aspx)<br /><br /> [![Mapa da Central de Segurança - Permissões do Servidor](../../database-engine/media/security-center-map-srv-perms.png "Mapa da Central de Segurança - Permissões do Servidor")](https://msdn.microsoft.com/library/ms191291.aspx)<br /><br /> [![Mapa da Central de Segurança - Permissões de banco de dados](../../database-engine/media/security-center-map-db-perms.png "Mapa da Central de Segurança - Permissões de banco de dados")](https://msdn.microsoft.com/library/ms191291.aspx)<br /><br /> **Segurança por funções**<br /><br /> [![Mapa da Central de Segurança - Funções do Servidor](../../database-engine/media/security-center-map-srv-roles.png "Mapa da Central de Segurança - Funções do Servidor")](https://msdn.microsoft.com/library/ms188659.aspx)<br /><br /> [![Mapa da Central de Segurança - Funções de banco de dados](../../database-engine/media/security-center-map-db-roles.png "Mapa da Central de Segurança - Funções de banco de dados")](https://msdn.microsoft.com/library/ms189121.aspx)<br /><br /> `Restricting Data Access to Selected Data Elements`<br /><br /> [![Mapa da Central de Segurança - Procedimentos e Exibições](../../database-engine/media/security-center-map-view-procs.png "Mapa da Central de Segurança - Procedimentos e Exibições")](https://msdn.microsoft.com/library/ms175503.aspx)<br /><br /> [![Mapa da Central de Segurança - Segurança em Nível de Linha](../../database-engine/media/security-center-map-row-level-sec.png "Mapa da Central de Segurança - Segurança em Nível de Linha")](https://msdn.microsoft.com/library/dn765131.aspx)<br /><br /> [![Mapa da Central de Segurança - Mascaramento de dados dinâmicos](../../database-engine/media/security-center-map-data-masking.png "Mapa da Central de Segurança - Mascaramento de dados dinâmicos")](https://azure.microsoft.com/documentation/articles/sql-database-dynamic-data-masking-get-started/)<br /><br /> [![Mapa da Central de Segurança - Objetos Assinados](../../database-engine/media/security-center-map-signed-objects.png "Mapa da Central de Segurança - Objetos Assinados")](https://msdn.microsoft.com/library/ms181700.aspx)<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")|**Criptografando arquivos**<br /><br /> [![Mapa da Central de Segurança - BitLocker](../../database-engine/media/security-center-map-bitlocker.png "Mapa da Central de Segurança - BitLocker")](https://support.microsoft.com/kb/2855131)<br /><br /> [![Mapa da Central de Segurança - Criptografia de NTFS](../../database-engine/media/security-center-map-ntfs-encryp.png "Mapa da Central de Segurança - Criptografia de NTFS")](https://msdn.microsoft.com/library/dd163562.aspx)<br /><br /> [![Mapa da Central de Segurança - TDE](../../database-engine/media/security-center-map-tde.png "Mapa da Central de Segurança - TDE")](https://msdn.microsoft.com/library/bb934049.aspx)<br /><br /> [![Mapa da Central de Segurança - Criptografia de backup](../../database-engine/media/security-center-map-backup-encryp.png "Mapa da Central de Segurança - Criptografia de backup")](https://msdn.microsoft.com/library/dn449489.aspx)<br /><br /> **Criptografando fontes**<br /><br /> [![Mapa da Central de Segurança - EKM](../../database-engine/media/security-center-map-ekm.png "Mapa da Central de Segurança - EKM")](https://msdn.microsoft.com/library/bb895340.aspx)<br /><br /> [![Mapa da Central de Segurança - Azure Key Vault](../../database-engine/media/security-center-map-key-vault.png "Mapa da Central de Segurança - Azure Key Vault")](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)<br /><br /> **Criptografia de chave de & de dados de coluna**<br /><br /> [![Criptografia do mapa da central de segurança por certificado](../../database-engine/media/security-center-map-cert.png "Criptografia do mapa da central de segurança por certificado")](https://msdn.microsoft.com/library/ms188061.aspx)<br /><br /> [![Mapa da Central de Segurança - Criptografar por Chave Simétrica](../../database-engine/media/security-center-map-sym-key.png "Mapa da Central de Segurança - Criptografar por Chave Simétrica")](https://msdn.microsoft.com/library/ms174361.aspx)<br /><br /> [![Mapa da Central de Segurança - Criptografar por chave assimétrica](../../database-engine/media/security-center-map-asym-key.png "Mapa da Central de Segurança - Criptografar por chave assimétrica")](https://msdn.microsoft.com/library/ms186950.aspx)<br /><br /> [![Mapa da Central de Segurança - Criptografar por Senha](../../database-engine/media/security-center-map-passphrase.png "Mapa da Central de Segurança - Criptografar por Senha")](https://msdn.microsoft.com/library/ms190357.aspx)|**Proteção de firewall**<br /><br /> [![Mapa da Central de Segurança - Firewall do Windows](../../database-engine/media/security-center-map-windows-firewall.png "Mapa da Central de Segurança - Firewall do Windows")](https://msdn.microsoft.com/library/ms175043.aspx)<br /><br /> [![Mapa da Central de Segurança - Firewall do Serviço](../../database-engine/media/security-center-map-service-firewall.png "Mapa da Central de Segurança - Firewall do Serviço")](https://msdn.microsoft.com/library/azure/ee621782.aspx)<br /><br /> [![Mapa da Central de Segurança - Firewall de banco de dados](../../database-engine/media/security-center-map-db-firewall.png "Mapa da Central de Segurança - Firewall de banco de dados")](https://msdn.microsoft.com/library/azure/ee621782.aspx)<br /><br /> **Criptografando dados em trânsito**<br /><br /> [![Mapa da Central de Segurança - SSL forçado](../../database-engine/media/security-center-map-forced-ssl.png "Mapa da Central de Segurança - SSL forçado")](https://msdn.microsoft.com/library/ms191192.aspx)<br /><br /> [![Mapa da Central de Segurança - SSL Opcional](../../database-engine/media/security-center-map-opt-ssl.png "Mapa da Central de Segurança - SSL Opcional")](https://msdn.microsoft.com/library/ms191192.aspx)<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")|**Auditoria automatizada**<br /><br /> [![Mapa da Central de Segurança - Auditoria do SQL Server](../../database-engine/media/security-center-map-sql-audit.png "Mapa da Central de Segurança - Auditoria do SQL Server")](https://msdn.microsoft.com/library/cc280386.aspx)<br /><br /> [![Mapa da Central de Segurança - Auditoria do Banco de Dados do SQL](../../database-engine/media/security-center-map-sqldb-audit.png "Mapa da Central de Segurança - Auditoria do Banco de Dados do SQL")](https://azure.microsoft.com/documentation/articles/sql-database-auditing-get-started/)<br /><br /> **Auditoria personalizada**<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")<br /><br /> [![Mapa da Central de Segurança - Gatilhos](../../database-engine/media/security-center-map-triggers.png "Mapa da Central de Segurança - Gatilhos")](https://msdn.microsoft.com/library/ms175941.aspx)<br /><br /> **Conformidade**<br /><br /> [![SecCtrCompliance](../../database-engine/media/secctrcompliance.png "SecCtrCompliance")](https://azure.microsoft.com/support/trust-center/services/)<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "Espaço reservado")<br /><br /> ![Legenda da central de segurança](../../database-engine/media/security-center-map-legend.png "Legenda da central de segurança")|  
  
## <a name="links-to-specific-related-topics"></a>Links para tópicos relacionados específicos  
 ![Ícone de pasta de arquivo pequeno](../../integration-services/media/filefolder-small.gif "Ícone de pasta de arquivos pequeno") **autenticação: quem é você?**  
 **Quem se autentica? (Windows ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])**  
  
-   [Escolher um modo de autenticação](choose-an-authentication-mode.md)  
  
 **Autenticar no banco de dados mestre** (logons e usuários de banco de dados)  
  
-   [Criar um logon do SQL Server](authentication-access/create-a-login.md)  
  
-   [Gerenciando bancos de dados e logons no banco de dados do Azure SQL](https://msdn.microsoft.com/library/ee336235.aspx)  
  
-   [Criar um usuário de banco de dados](authentication-access/create-a-database-user.md)  
  
 **Autenticar em um banco de dados do usuário**  
  
-   [Usuários do Banco de Dados Independente - Tornando seu Banco de Dados Portátil](contained-database-users-making-your-database-portable.md)  
  
 **Usando outras identidades**  
  
-   [Credenciais &#40;Mecanismo de Banco de Dados&#41;](authentication-access/credentials-database-engine.md)  
  
-   [Executar como outro logon](/sql/t-sql/statements/execute-as-transact-sql)  
  
-   [Executar como outro usuário de banco de dados](/sql/t-sql/statements/execute-as-transact-sql)  
  
 ![Ícone de pasta de arquivo pequeno](../../integration-services/media/filefolder-small.gif "Ícone de pasta de arquivos pequeno") **criptografia: armazenando dados secretos**  
 **Criptografando arquivos**  
  
-   [BitLocker (nível de unidade)](https://support.microsoft.com/kb/2855131)  
  
-   [Criptografia de NTFS (nível de pasta)](https://msdn.microsoft.com/library/dd163562.aspx)  
  
-   [Criptografia transparente de dados (nível de arquivo)](encryption/transparent-data-encryption.md)  
  
-   [Criptografia de backup (nível de arquivo)](../backup-restore/backup-encryption.md)  
  
 **Criptografando fontes**  
  
-   [Módulo de Gerenciamento Extensível de Chaves](encryption/extensible-key-management-ekm.md)  
  
-   [Chaves armazenadas no cofre principal do Azure](encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
 **Criptografia de chaves, colunas e dados**  
  
-   [Criptografar por certificado](/sql/t-sql/functions/encryptbycert-transact-sql)  
  
-   [Criptografar por chave assimétrica](/sql/t-sql/functions/encryptbyasymkey-transact-sql)  
  
-   [Criptografar por chave simétrica](/sql/t-sql/functions/encryptbykey-transact-sql)  
  
-   [Criptografar por frase secreta](/sql/t-sql/functions/encryptbypassphrase-transact-sql)  
  
 ![Ícone de pasta de arquivo pequeno](../../integration-services/media/filefolder-small.gif "Ícone de pasta de arquivos pequeno") **autorização: o que você pode fazer?**  
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
  
 ![Ícone de pasta de arquivo pequeno](../../integration-services/media/filefolder-small.gif "Ícone de pasta de arquivos pequeno") **segurança de conexão: restringindo e protegendo**  
 **Proteção de firewall**  
  
-   [Configurar um Firewall do Windows para acesso ao Mecanismo de Banco de Dados](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)  
  
-   [Configurações de Firewall de banco de dados do SQL do Azure](/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database)  
  
-   [Configurações de Firewall de serviço do Azure](/sql/relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database)  
  
 **Criptografando dados em trânsito**  
  
-   [Protocolo SSL para o mecanismo de banco de dados](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)  
  
-   [Protocolo SSL para o banco de dados SQL](https://msdn.microsoft.com/library/azure/ff394108.aspx)  
  
 ![Ícone de pasta de arquivos pequena](../../integration-services/media/filefolder-small.gif "Ícone de pasta de arquivos pequeno") **auditoria: acesso de gravação**  
 **Auditoria automatizada**  
  
-   [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](auditing/sql-server-audit-database-engine.md)  
  
-   [Auditoria do banco de dados SQL](https://azure.microsoft.com/documentation/articles/sql-database-auditing-get-started/)  
  
 **Implementação de auditoria personalizada**  
  
-   Criando [DDL Triggers](../triggers/ddl-triggers.md) e [DML Triggers](../triggers/dml-triggers.md)  
  
 ![Ícone de pasta de arquivo pequeno](../../integration-services/media/filefolder-small.gif "Ícone de pasta de arquivos pequeno") **conformidade**  
 **SQL Server**  
  
-   [critérios comuns](https://go.microsoft.com/fwlink/?LinkId=616319)  
  
 **Banco de Dados SQL**  
  
-   [Central de Confiabilidade do Microsoft Azure: conformidade por recurso](https://azure.microsoft.com/support/trust-center/services/)  
  
## <a name="see-also"></a>Consulte Também  
 [Protegendo o SQL Server](securing-sql-server.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](authentication-access/principals-database-engine.md)   
 [Certificados e chaves assimétricas do SQL Server](sql-server-certificates-and-asymmetric-keys.md)   
 [Criptografia do SQL Server](encryption/sql-server-encryption.md)   
 [Configuração da Área de Superfície](surface-area-configuration.md)   
 [Senhas fortes](strong-passwords.md)   
 [propriedade TRUSTWORTHY do banco de dados](trustworthy-database-property.md)   
 [Recursos e tarefas do Mecanismo de Banco de Dados](../../database-engine/database-engine-features-and-tasks.md)  
  
  
