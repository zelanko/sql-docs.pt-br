---
title: Centro de segurança do Mecanismo de Banco de Dados do SQL Server e do Banco de Dados SQL do Azure | Microsoft Docs
ms.custom: ''
ms.date: 09/23/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-security
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- Security [SQL Server]
helpviewer_keywords:
- SQL Server, security
- security [SQL Server]
- database security [SQL Server]
- databases [SQL Server], security
ms.assetid: dfb39d16-722a-4734-94bb-98e61e014ee7
caps.latest.revision: 50
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: fa006590558cf94095d37f009102da753a5464ed
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006308"
---
# <a name="security-center-for-sql-server-database-engine-and-azure-sql-database"></a>Central de segurança do Mecanismo de Banco de Dados do SQL Server e Banco de Dados SQL do Azure
  Esta página fornece links para ajudá-lo a localizar as informações necessárias sobre segurança e proteção no [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)].  
  
> [!NOTE]  
>  Os recursos do [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] continuam a melhorar. Consulte a versão mais recente deste tópico para obter as informações mais recentes sobre o [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
|Autenticação: quem é você?|Autorização: o que você pode fazer?|Criptografia: armazenando dados secretos|Segurança de conexão: restringir e proteger|Auditoria: acesso à gravação|  
|----------------------------------|-------------------------------------|-------------------------------------|---------------------------------------------------|--------------------------------|  
|**Quem autentica?**<br /><br /> [![Mapa da Central de segurança autenticação do Windows](../../database-engine/media/security-center-map-windows-authenticaion.png "mapa da Central de segurança autenticação do Windows")](http://msdn.microsoft.com/library/ms144284.aspx)<br /><br /> <br /><br /> [![Mapa da Central de segurança SQL Server autenticação](../../database-engine/media/security-center-map-sql-authenticaion.png "Central de segurança mapa a autenticação do SQL Server")](http://msdn.microsoft.com/library/ms144284.aspx)<br /><br /> **Onde é autenticado?**<br /><br /> [![Central de segurança mapear logons e usuários](../../database-engine/media/security-center-map-logins-users.png "Central de segurança mapear logons e usuários")](http://msdn.microsoft.com/library/aa337562.aspx)<br /><br /> <br /><br /> [![Mapa da Central de segurança contidos usuários de banco de dados](../../database-engine/media/security-center-map-contained-users.png "mapa da Central de segurança contidos usuários de banco de dados")](http://msdn.microsoft.com/library/ff929188.aspx)<br /><br /> **Usando outras identidades**<br /><br /> [![Credenciais de mapa da Central de segurança](../../database-engine/media/security-center-map-credentials.png "credenciais de mapa da Central de segurança")](http://msdn.microsoft.com/library/ms161950.aspx)<br /><br /> [![Mapa da Central de segurança-executar como logon](../../database-engine/media/security-center-map-exec-as-login.png "mapa da Central de segurança-executar como logon")](http://msdn.microsoft.com/library/ms181362.aspx)<br /><br /> [![Mapa da Central de segurança-executar como usuário](../../database-engine/media/security-center-map-exec-as-user.png "mapa da Central de segurança-executar como usuário")](http://msdn.microsoft.com/library/ms181362.aspx)<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "espaço reservado")|**Concedendo, revogando e negando permissões**<br /><br /> [![Mapa da Central de segurança Classes protegíveis](../../database-engine/media/security-center-map-securable-classes.png "Classes protegíveis mapa da Central de segurança")](http://msdn.microsoft.com/library/ms190401.aspx)<br /><br /> [![Servidor de mapa da Central de segurança permissões](../../database-engine/media/security-center-map-srv-perms.png "Server de mapa da Central de segurança permissões")](http://msdn.microsoft.com/library/ms191291.aspx)<br /><br /> [![Banco de dados de mapa da Central de segurança permissões](../../database-engine/media/security-center-map-db-perms.png "permissões de banco de dados de mapa de Central de segurança")](http://msdn.microsoft.com/library/ms191291.aspx)<br /><br /> **Segurança por funções**<br /><br /> [![Funções de servidor central de segurança mapa](../../database-engine/media/security-center-map-srv-roles.png "funções de servidor de mapa de Central de segurança")](http://msdn.microsoft.com/library/ms188659.aspx)<br /><br /> [![Funções de banco de dados de mapa de Central de segurança](../../database-engine/media/security-center-map-db-roles.png "funções de banco de dados de mapa de Central de segurança")](http://msdn.microsoft.com/library/ms189121.aspx)<br /><br /> `Restricting Data Access to Selected Data Elements`<br /><br /> [![Exibições de mapa da Central de segurança e procedimentos](../../database-engine/media/security-center-map-view-procs.png "procedimentos e exibições de mapa da Central de segurança")](http://msdn.microsoft.com/library/ms175503.aspx)<br /><br /> [![A segurança de nível de linha de mapa da Central de segurança](../../database-engine/media/security-center-map-row-level-sec.png "a segurança de nível de linha de mapa da Central de segurança")](http://msdn.microsoft.com/library/dn765131.aspx)<br /><br /> [![Mascaramento de dados dinâmicos do mapa de Central de segurança](../../database-engine/media/security-center-map-data-masking.png "mascaramento de dados dinâmicos do mapa de Central de segurança")](http://azure.microsoft.com/documentation/articles/sql-database-dynamic-data-masking-get-started/)<br /><br /> [![Mapa da Central de segurança assinado objetos](../../database-engine/media/security-center-map-signed-objects.png "objetos assinados do mapa da Central de segurança")](http://msdn.microsoft.com/library/ms181700.aspx)<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "espaço reservado")|**Criptografando arquivos**<br /><br /> [![BitLocker de mapa da Central de segurança](../../database-engine/media/security-center-map-bitlocker.png "BitLocker de mapa da Central de segurança")](http://support.microsoft.com/en-us/kb/2855131)<br /><br /> [![Mapa da Central de segurança criptografia de NTFS](../../database-engine/media/security-center-map-ntfs-encryp.png "mapa da Central de segurança criptografia de NTFS")](http://msdn.microsoft.com/library/dd163562.aspx)<br /><br /> [![Mapa da Central de segurança TDE](../../database-engine/media/security-center-map-tde.png "mapa da Central de segurança TDE")](http://msdn.microsoft.com/library/bb934049.aspx)<br /><br /> [![Mapa da Central de segurança-criptografia Backup](../../database-engine/media/security-center-map-backup-encryp.png "mapa da Central de segurança-criptografia Backup")](http://msdn.microsoft.com/library/dn449489.aspx)<br /><br /> **Criptografando fontes**<br /><br /> [![Mapa da Central de segurança EKM](../../database-engine/media/security-center-map-ekm.png "mapa da Central de segurança EKM")](http://msdn.microsoft.com/library/bb895340.aspx)<br /><br /> [![Mapa da Central de segurança Azure Key Vault](../../database-engine/media/security-center-map-key-vault.png "mapa da Central de segurança Cofre de chaves do Azure")](http://azure.microsoft.com/documentation/articles/key-vault-get-started/)<br /><br /> **Coluna, dados e criptografia de chave**<br /><br /> [![Mapa da Central de segurança-criptografar por certificado](../../database-engine/media/security-center-map-cert.png "mapa da Central de segurança-criptografar por certificado")](http://msdn.microsoft.com/library/ms188061.aspx)<br /><br /> [![Mapa da Central de segurança-criptografar por chave simétrica](../../database-engine/media/security-center-map-sym-key.png "mapa da Central de segurança-criptografar por chave simétrica")](http://msdn.microsoft.com/library/ms174361.aspx)<br /><br /> [![Mapa da Central de segurança-criptografar por chave assimétrica](../../database-engine/media/security-center-map-asym-key.png "mapa da Central de segurança-criptografar por chave assimétrica")](http://msdn.microsoft.com/library/ms186950.aspx)<br /><br /> [![Mapa da Central de segurança-criptografar por frase secreta](../../database-engine/media/security-center-map-passphrase.png "mapa da Central de segurança-criptografar por frase secreta")](http://msdn.microsoft.com/library/ms190357.aspx)|**Proteção de firewall**<br /><br /> [![Mapa da Central de segurança Windows Firewall](../../database-engine/media/security-center-map-windows-firewall.png "mapa da Central de segurança Windows Firewall")](http://msdn.microsoft.com/library/ms175043.aspx)<br /><br /> [![Serviço de mapa da Central de segurança Firewall](../../database-engine/media/security-center-map-service-firewall.png "serviço de mapa da Central de segurança Firewall")](http://msdn.microsoft.com/library/azure/ee621782.aspx)<br /><br /> [![Banco de dados de mapa da Central de segurança Firewall](../../database-engine/media/security-center-map-db-firewall.png "banco de dados de mapa da Central de segurança Firewall")](http://msdn.microsoft.com/library/azure/ee621782.aspx)<br /><br /> **Criptografando dados em trânsito**<br /><br /> [![Mapa da Central de segurança SSL forçado](../../database-engine/media/security-center-map-forced-ssl.png "mapa da Central de segurança SSL forçado")](http://msdn.microsoft.com/library/ms191192.aspx)<br /><br /> [![Mapa da Central de segurança SSL opcional](../../database-engine/media/security-center-map-opt-ssl.png "mapa da Central de segurança SSL opcionais")](http://msdn.microsoft.com/library/ms191192.aspx)<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "espaço reservado")|**Auditoria automatizada**<br /><br /> [![Mapa da Central de segurança SQL Server auditoria](../../database-engine/media/security-center-map-sql-audit.png "mapa da Central de segurança SQL Server auditoria")](http://msdn.microsoft.com/library/cc280386.aspx)<br /><br /> [![Mapa da Central de segurança auditoria banco de dados SQL](../../database-engine/media/security-center-map-sqldb-audit.png "mapa da Central de segurança auditoria banco de dados SQL")](http://azure.microsoft.com/documentation/articles/sql-database-auditing-get-started/)<br /><br /> **Auditoria personalizada**<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "espaço reservado")<br /><br /> [![Gatilhos de mapa da Central de segurança](../../database-engine/media/security-center-map-triggers.png "gatilhos de mapa da Central de segurança")](http://msdn.microsoft.com/library/ms175941.aspx)<br /><br /> **Conformidade**<br /><br /> [![SecCtrCompliance](../../database-engine/media/secctrcompliance.png "SecCtrCompliance")](http://azure.microsoft.com/support/trust-center/services/)<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "espaço reservado")<br /><br /> ![Espaço reservado](../../database-engine/media/security-center-map-blankplaceholder.png "espaço reservado")<br /><br /> ![Legenda da Central de segurança](../../database-engine/media/security-center-map-legend.png "legenda da Central de segurança")|  
  
## <a name="links-to-specific-related-topics"></a>Links para tópicos relacionados específicos  
 ![Ícone de pasta de arquivo pequeno](../../integration-services/media/filefolder-small.gif "pequeno ícone de pasta do arquivo") **autenticação: quem é você?**  
 **Quem autentica? (Windows ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])**  
  
-   [Escolher um modo de autenticação](choose-an-authentication-mode.md)  
  
 **Autenticação no banco de dados mestre** (logons e usuários de banco de dados)  
  
-   [Criar um logon do SQL Server](authentication-access/create-a-login.md)  
  
-   [Gerenciando bancos de dados e logons no banco de dados do Azure SQL](http://msdn.microsoft.com/library/ee336235.aspx)  
  
-   [Criar um usuário de banco de dados](authentication-access/create-a-database-user.md)  
  
 **Autenticar em um banco de dados do usuário**  
  
-   [Usuários de bancos de dados independentes - Tornando seu banco de dados portátil](contained-database-users-making-your-database-portable.md)  
  
 **Usando outras identidades**  
  
-   [Credenciais &#40;Mecanismo de Banco de Dados&#41;](authentication-access/credentials-database-engine.md)  
  
-   [Executar como outro logon](/sql/t-sql/statements/execute-as-transact-sql)  
  
-   [Executar como outro usuário de banco de dados](/sql/t-sql/statements/execute-as-transact-sql)  
  
 ![Ícone de pasta do arquivo pequeno](../../integration-services/media/filefolder-small.gif "arquivo pequeno ícone da pasta") **criptografia: armazenando dados secretos**  
 **Criptografando arquivos**  
  
-   [BitLocker (nível de unidade)](http://support.microsoft.com/kb/2855131)  
  
-   [Criptografia de NTFS (nível de pasta)](http://msdn.microsoft.com/library/dd163562.aspx)  
  
-   [Criptografia transparente de dados (nível de arquivo)](encryption/transparent-data-encryption.md)  
  
-   [Criptografia de backup (nível de arquivo)](../backup-restore/backup-encryption.md)  
  
 **Criptografando fontes**  
  
-   [Módulo de Gerenciamento Extensível de Chaves](encryption/extensible-key-management-ekm.md)  
  
-   [Chaves armazenadas no cofre principal do Azure](encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
 **Criptografia de chave, colunas e dados**  
  
-   [Criptografar por certificado](/sql/t-sql/functions/encryptbycert-transact-sql)  
  
-   [Criptografar por chave assimétrica](/sql/t-sql/functions/encryptbyasymkey-transact-sql)  
  
-   [Criptografar por chave simétrica](/sql/t-sql/functions/encryptbykey-transact-sql)  
  
-   [Criptografar por frase secreta](/sql/t-sql/functions/encryptbypassphrase-transact-sql)  
  
 ![Ícone de pasta de arquivo pequeno](../../integration-services/media/filefolder-small.gif "pequeno ícone de pasta do arquivo") **autorização: o que você pode fazer?**  
 **Concedendo, revogando e negando permissões**  
  
-   [Hierarquia de permissões &#40;Mecanismo de Banco de Dados&#41;](permissions-hierarchy-database-engine.md)  
  
-   [Permissões](permissions-database-engine.md)  
  
-   [Protegíveis](securables.md)  
  
 **Segurança por funções**  
  
-   [Funções de nível de servidor](authentication-access/server-level-roles.md)  
  
-   [Funções de nível de banco de dados](authentication-access/database-level-roles.md)  
  
 `Restricting Data Access to Selected Data Elements`  
  
-   Restringir acesso a dados usando [Exibições](../views/views.md) e [Procedimentos](../stored-procedures/stored-procedures-database-engine.md)  
  
-   [Segurança em nível de linha](http://msdn.microsoft.com/library/azure/dn765131.aspx)  
  
-   [Mascaramento de dados dinâmicos](http://azure.microsoft.com/documentation/articles/sql-database-dynamic-data-masking-get-started/)  
  
-   [Objetos assinados](/sql/t-sql/statements/add-signature-transact-sql)  
  
 ![Ícone de pasta do arquivo pequeno](../../integration-services/media/filefolder-small.gif "arquivo pequeno ícone da pasta") **segurança de Conexão: restringir e proteger**  
 **Proteção de firewall**  
  
-   [Configurar um Firewall do Windows para acesso ao Mecanismo de Banco de Dados](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)  
  
-   [Configurações de Firewall de banco de dados do SQL do Azure](/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database)  
  
-   [Configurações de Firewall de serviço do Azure](/sql/relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database)  
  
 **Criptografando dados em trânsito**  
  
-   [Protocolo SSL para o mecanismo de banco de dados](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)  
  
-   [Protocolo SSL para o banco de dados SQL](https://msdn.microsoft.com/library/azure/ff394108.aspx)  
  
 ![Ícone de pasta do arquivo pequeno](../../integration-services/media/filefolder-small.gif "arquivo pequeno ícone da pasta") **auditoria: acesso à gravação**  
 **Auditoria automatizada**  
  
-   [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](auditing/sql-server-audit-database-engine.md)  
  
-   [Auditoria do banco de dados SQL](http://azure.microsoft.com/documentation/articles/sql-database-auditing-get-started/)  
  
 **Implementação de auditoria personalizada**  
  
-   Criando [DDL Triggers](../triggers/ddl-triggers.md) e [DML Triggers](../triggers/dml-triggers.md)  
  
 ![Ícone de pasta do arquivo pequeno](../../integration-services/media/filefolder-small.gif "arquivo pequeno ícone da pasta") **conformidade**  
 **SQL Server**  
  
-   [critérios comuns](http://go.microsoft.com/fwlink/?LinkId=616319)  
  
 **Banco de Dados SQL**  
  
-   [Central de Confiabilidade do Microsoft Azure: conformidade por recurso](http://azure.microsoft.com/support/trust-center/services/)  
  
## <a name="see-also"></a>Consulte também  
 [Protegendo o SQL Server](securing-sql-server.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](authentication-access/principals-database-engine.md)   
 [Certificados e chaves assimétricas do SQL Server](sql-server-certificates-and-asymmetric-keys.md)   
 [Criptografia do SQL Server](encryption/sql-server-encryption.md)   
 [Configuração da Área de Superfície](surface-area-configuration.md)   
 [Senhas fortes](strong-passwords.md)   
 [Propriedade de banco de dados TRUSTWORTHY](trustworthy-database-property.md)   
 [Recursos e tarefas do Mecanismo de Banco de Dados](../../database-engine/database-engine-features-and-tasks.md)  
  
  
