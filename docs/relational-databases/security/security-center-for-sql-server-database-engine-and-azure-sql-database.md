---
title: Centro de segurança do Mecanismo de Banco de Dados do SQL Server e do Banco de Dados SQL do Azure | Microsoft Docs
ms.custom: ''
ms.date: 09/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 86d3f0bcc0d791a025165d8bda3188d443fce1e1
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874833"
---
# <a name="security-center-for-sql-server-database-engine-and-azure-sql-database"></a>Central de segurança do Mecanismo de Banco de Dados do SQL Server e Banco de Dados SQL do Azure
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Esta página fornece links para ajudá-lo a localizar as informações necessárias sobre Segurança e Proteção no [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)].  
  
 **Legenda**  
  
 ![security-center-legend](../performance/media/security-center-legend.PNG "security-center-legend")  
  
##  <a name="Who"></a> Autenticação: quem é você?  
  
|||  
|-|-|  
|**Quem autentica?**<br /><br /> ![security-center-sqlserver](../performance/media/security-center-sqlserver.png "security-center-sqlserver") Autenticação do Windows<br /><br /> ![security-center-both](../performance/media/security-center-both.png "security-center-both") Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> ![security-center-sqldb](../../relational-databases/security/media/security-center-sqldb.png "security-center-sqldb") Azure Active Directory|Quem autentica? (Windows ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])<br /><br /> [Escolher um modo de autenticação](../../relational-databases/security/choose-an-authentication-mode.md)<br /><br /> [Conectar-se ao Banco de Dados SQL usando a autenticação do Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)|  
|**Onde é autenticado?**<br /><br /> ![security-center-both](../performance/media/security-center-both.png "security-center-both") No banco de dados mestre: logons e usuários do BD<br /><br /> ![security-center-both](../performance/media/security-center-both.png "security-center-both") No banco de dados do usuário: usuários do BD independente|Autenticação no banco de dados mestre (logons e usuários de banco de dados)<br /><br /> [Criar um logon do SQL Server](../../relational-databases/security/authentication-access/create-a-login.md)<br /><br /> [Gerenciando bancos de dados e logons no banco de dados do Azure SQL](https://msdn.microsoft.com/library/ee336235.aspx)<br /><br /> [Criar um usuário de banco de dados](../../relational-databases/security/authentication-access/create-a-database-user.md)<br /><br /> <br /><br /> Autenticar em um banco de dados do usuário<br /><br /> [Usuários de bancos de dados independentes - Tornando seu banco de dados portátil](../../relational-databases/security/contained-database-users-making-your-database-portable.md)|  
|**Usando outras identidades**<br /><br /> ![security-center-both](../performance/media/security-center-both.png "security-center-both") Credenciais<br /><br /> ![security-center-sqlserver](../performance/media/security-center-sqlserver.png "security-center-sqlserver") Executar como outro logon<br /><br /> ![security-center-both](../performance/media/security-center-both.png "security-center-both") Executar como outro usuário de banco de dados|[Credenciais &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)<br /><br /> [Executar como outro logon](../../t-sql/statements/execute-as-transact-sql.md)<br /><br /> [Executar como outro usuário de banco de dados](../../t-sql/statements/execute-as-transact-sql.md)|  
  
##  <a name="What"></a> Autorização: o que você pode fazer?  
  
|||  
|-|-|  
|**Concedendo, revogando e negando permissões**<br /><br /> ![security-center-both](../performance/media/security-center-both.png "security-center-both") Classes protegíveis<br /><br /> ![security-center-sqlserver](../performance/media/security-center-sqlserver.png "security-center-sqlserver") Permissões de servidor granular<br /><br /> ![security-center-both](../performance/media/security-center-both.png "security-center-both") Permissões do banco de dados granular|[Hierarquia de permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)<br /><br /> [Permissões](../../relational-databases/security/permissions-database-engine.md)<br /><br /> [Protegíveis](../../relational-databases/security/securables.md)<br /><br /> [Guia de Introdução às permissões do mecanismo de banco de dados](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)|  
|**Segurança por funções**<br /><br /> ![security-center-sqlserver](../performance/media/security-center-sqlserver.png "security-center-sqlserver") Funções no nível de servidor<br /><br /> ![security-center-both](../performance/media/security-center-both.png "security-center-both") Funções no nível de banco de dados|[Funções de nível de servidor](../../relational-databases/security/authentication-access/server-level-roles.md)<br /><br /> [Funções de nível de banco de dados](../../relational-databases/security/authentication-access/database-level-roles.md)|  
|**Restringindo o acesso a dados aos elementos de dados selecionados**<br /><br /> ![security-center-both](../performance/media/security-center-both.png "security-center-both") Restringir acesso a dados com exibições/procedimentos<br /><br /> ![security-center-both](../performance/media/security-center-both.png "security-center-both") Segurança em nível de linha<br /><br /> ![security-center-both](../performance/media/security-center-both.png "security-center-both") Máscara de Dados Dinâmicos<br /><br /> ![security-center-both](../performance/media/security-center-both.png "security-center-both") Objetos assinados|Restringir acesso a dados usando [Exibições](../../relational-databases/views/views.md) e [Procedimentos](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)<br /><br /> [Segurança em nível de linha (SQL Server)](../../relational-databases/security/row-level-security.md)<br /><br /> [Segurança em nível de linha (banco de dados SQL do Azure)](https://msdn.microsoft.com/library/azure/dn765131.aspx)<br /><br /> [Mascaramento de dados dinâmicos (SQL Server)](../../relational-databases/security/dynamic-data-masking.md)<br /><br /> [Mascaramento de Dados Dinâmicos (Banco de Dados SQL do Azure)](https://azure.microsoft.com/documentation/articles/sql-database-dynamic-data-masking-get-started/)<br /><br /> [Objetos assinados](../../t-sql/statements/add-signature-transact-sql.md)|  
  
##  <a name="Encrypt"></a> Criptografia: armazenar dados secretos  
  
|||  
|-|-|  
|**Criptografando arquivos**<br /><br /> ![security-center-sqlserver](../performance/media/security-center-sqlserver.png "security-center-sqlserver") Criptografia de BitLocker (nível de unidade)<br /><br /> ![security-center-sqlserver](../performance/media/security-center-sqlserver.png "security-center-sqlserver") Criptografia NTFS (nível de pasta)<br /><br /> ![security-center-both](../performance/media/security-center-both.png "security-center-both") Transparent Data Encryption (nível de arquivo)<br /><br /> ![security-center-both](../performance/media/security-center-both.png "security-center-both") Criptografia de backup (nível de arquivo)|[BitLocker (nível de unidade)](https://support.microsoft.com/kb/2855131)<br /><br /> [Criptografia de NTFS (nível de pasta)](https://msdn.microsoft.com/library/dd163562.aspx)<br /><br /> [Criptografia transparente de dados (nível de arquivo)](../../relational-databases/security/encryption/transparent-data-encryption.md)<br /><br /> [Criptografia de backup (nível de arquivo)](../../relational-databases/backup-restore/backup-encryption.md)|  
|**Criptografando fontes**<br /><br /> ![security-center-sqlserver](../performance/media/security-center-sqlserver.png "security-center-sqlserver") Módulo de gerenciamento extensível de chaves<br /><br /> ![security-center-sqlserver](../performance/media/security-center-sqlserver.png "security-center-sqlserver") Chaves armazenadas no Azure Key Vault<br /><br /> ![security-center-both](../performance/media/security-center-both.png "security-center-both") Always Encrypted|[Módulo de Gerenciamento Extensível de Chaves](../../relational-databases/security/encryption/extensible-key-management-ekm.md)<br /><br /> [Chaves armazenadas no cofre principal do Azure](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)<br /><br /> [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)|  
|**Coluna, dados e criptografia de chave**<br /><br /> ![security-center-both](../performance/media/security-center-both.png "security-center-both") Criptografia por certificado<br /><br /> ![security-center-both](../performance/media/security-center-both.png "security-center-both") Criptografia por chave simétrica<br /><br /> ![security-center-both](../performance/media/security-center-both.png "security-center-both") Criptografia por chave assimétrica<br /><br /> ![security-center-both](../performance/media/security-center-both.png "security-center-both") Criptografia por frase secreta|[Criptografar por certificado](../../t-sql/functions/encryptbycert-transact-sql.md)<br /><br /> [Criptografar por chave assimétrica](../../t-sql/functions/encryptbyasymkey-transact-sql.md)<br /><br /> [Criptografar por chave simétrica](../../t-sql/functions/encryptbykey-transact-sql.md)<br /><br /> [Criptografar por frase secreta](../../t-sql/functions/encryptbypassphrase-transact-sql.md)<br /><br /> [Criptografar uma coluna de dados](../../relational-databases/security/encryption/encrypt-a-column-of-data.md)|  
  
##  <a name="Connect"></a> Segurança da conexão: restringir e proteger  
  
|||  
|-|-|  
|**Proteção de firewall**<br /><br /> ![security-center-sqlserver](../performance/media/security-center-sqlserver.png "security-center-sqlserver") Configurações do Firewall do Windows<br /><br /> ![security-center-sqldb](../../relational-databases/security/media/security-center-sqldb.png "security-center-sqldb") Configurações de Firewall do Azure Service<br /><br /> ![security-center-sqldb](../../relational-databases/security/media/security-center-sqldb.png "security-center-sqldb") Configurações de Firewall de Banco de Dados|[Configurar um Firewall do Windows para acesso ao Mecanismo de Banco de Dados](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)<br /><br /> [Configurações de Firewall de banco de dados do SQL do Azure](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)<br /><br /> [Configurações de Firewall de serviço do Azure](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)|  
|**Criptografando dados em trânsito**<br /><br /> ![security-center-both](../performance/media/security-center-both.png "security-center-both") Conexões de SSL forçadas<br /><br /> ![security-center-sqlserver](../performance/media/security-center-sqlserver.png "security-center-sqlserver") Conexões de SSL opcionais|[Protocolo SSL para o mecanismo de banco de dados](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)<br /><br /> [Protocolo SSL para o banco de dados SQL](https://msdn.microsoft.com/library/azure/ff394108.aspx)<br /><br /> [Suporte a TLS 1.2 para o Microsoft SQL Server](https://support.microsoft.com/kb/3135244)|  
  
##  <a name="Audit"></a> Auditoria: acesso de gravação  
  
|||  
|-|-|  
|**Auditoria automatizada**<br /><br /> ![security-center-sqlserver](../../relational-databases/performance/media/security-center-sqlserver.png "security-center-sqlserver") [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Auditoria (nível de servidor e de BD)<br /><br /> ![security-center-sqldb](../../relational-databases/security/media/security-center-sqldb.png "security-center-sqldb") [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Auditoria (nível de bando de dados)<br /><br /> ![security-center-sqldb](../../relational-databases/security/media/security-center-sqldb.png "security-center-sqldb") Detectar ameaças| <br /><br /> [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)<br /><br /> [Auditoria do banco de dados SQL](https://azure.microsoft.com/documentation/articles/sql-database-auditing-get-started/)<br /><br /> [Introdução à Proteção Avançada contra Ameaças do Banco de Dados SQL](https://azure.microsoft.com/documentation/articles/sql-database-threat-detection-get-started/) <br /><br /> [Avaliação de Vulnerabilidade do Banco de Dados SQL](https://docs.microsoft.com/azure/sql-database/sql-vulnerability-assessment) |  
|**Auditoria personalizada**<br /><br /> ![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") Gatilhos|Implementação de auditoria personalizada: Criando [DDL Triggers](../../relational-databases/triggers/ddl-triggers.md) e [DML Triggers](../../relational-databases/triggers/dml-triggers.md)|  
|**Conformidade**<br /><br /> ![security-center-both](../../relational-databases/performance/media/security-center-both.png "security-center-both") Conformidade|SQL Server:<br />                        [critérios comuns](https://go.microsoft.com/fwlink/?LinkId=616319)<br /><br /> Banco de dados SQL:<br />                        [Central de Confiabilidade do Microsoft Azure: conformidade por recurso](https://azure.microsoft.com/support/trust-center/services/)|  
  
##  <a name="SQLInjection"></a> Injeção SQL  
 Injeção de SQL é um ataque no qual um código mal-intencionado é inserido em cadeias de caracteres que são passadas posteriormente para o [!INCLUDE[ssDE](../../includes/ssde-md.md)] para análise e execução. Qualquer procedimento que construa instruções SQL deve ser verificado quanto a vulnerabilidades de injeção porque o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executará todas as consultas sintaticamente válidas que receber. Todos os sistemas de banco de dados têm algum risco de Injeção de SQL e muitas das vulnerabilidades são introduzidas no aplicativo que está consultando o [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Você pode impedir ataques de injeção de SQL usando procedimentos armazenados e comandos parametrizados, evitando o SQL dinâmico e restringindo as permissões de todos os usuários.  Para obter mais informações, consulte [SQL Injection](../../relational-databases/security/sql-injection.md).  
  
 Links adicionais para programadores de aplicativos:  
  
-   [Cenários de Segurança de Aplicativo no SQL Server](/dotnet/framework/data/adonet/sql/application-security-scenarios-in-sql-server)  
  
-   [Gravação de SQL Dinâmico Seguro no SQL Server](/dotnet/framework/data/adonet/sql/writing-secure-dynamic-sql-in-sql-server)  
  
-   [Como proteger-se contra ataques de injeção SQL no ASP.NET](https://msdn.microsoft.com/library/ff648339.aspx)  
  
## <a name="see-also"></a>Consulte Também  
 [Guia de Introdução às permissões do mecanismo de banco de dados](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)   
 [Protegendo o SQL Server](../../relational-databases/security/securing-sql-server.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Certificados e chaves assimétricas do SQL Server](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)   
 [Criptografia do SQL Server](../../relational-databases/security/encryption/sql-server-encryption.md)   
 [Configuração da Área de Superfície](../../relational-databases/security/surface-area-configuration.md)   
 [Senhas fortes](../../relational-databases/security/strong-passwords.md)   
 [Propriedade de banco de dados TRUSTWORTHY](../../relational-databases/security/trustworthy-database-property.md)   
 [Recursos e tarefas do Mecanismo de Banco de Dados](https://msdn.microsoft.com/library/d9efe145-3306-4d61-bd77-e2af43e19c34)  
 [Protegendo a propriedade intelectual do seu SQL Server](../../relational-databases/security/protecting-your-sql-server-intellectual-property.md)   
  
[!INCLUDE[get-help-security](../../includes/get-help-security.md)]
