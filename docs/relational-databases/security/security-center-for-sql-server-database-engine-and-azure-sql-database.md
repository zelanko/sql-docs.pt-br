---
title: Documentação sobre segurança do SQL Server e do Banco de Dados SQL do Azure
description: Uma referência do conteúdo relacionado à segurança e à proteção do SQL Server e do Banco de Dados SQL do Azure.
ms.custom: seo-lt-2019
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e87b6682ed9e9d4d5c44a3fe198e949f3ac8cd19
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479377"
---
# <a name="security-center-for-sql-server-database-engine-and-azure-sql-database"></a>Central de segurança do Mecanismo de Banco de Dados do SQL Server e Banco de Dados SQL do Azure
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Esta página fornece links para ajudá-lo a localizar as informações necessárias sobre Segurança e Proteção no [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)].  
  
 **Legenda**  
  
 ![Captura de tela da legenda que explica os ícones de disponibilidade do recurso.](../performance/media/security-center-legend.PNG "security-center-legend")  
  
##  <a name="authentication-who-are-you"></a><a name="Who"></a> Autenticação: quem é você?  
  
|||  
|-|-|  
|**Quem autentica?**<br /><br /> :::image type="icon" source="../performance/media/security-center-sqlserver.png"::: Autenticação do Windows<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> :::image type="icon" source="../../relational-databases/security/media/security-center-sqldb.png"::: Azure Active Directory|Quem autentica? (Windows ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])<br /><br /> [Escolher um modo de autenticação](../../relational-databases/security/choose-an-authentication-mode.md)<br /><br /> [Conectar-se ao Banco de Dados SQL usando a autenticação do Azure Active Directory](/azure/azure-sql/database/authentication-aad-overview)|  
|**Onde é autenticado?**<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: No banco de dados mestre: logons e usuários do BD<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: No banco de dados de usuário: usuários do BD independente|Autenticação no banco de dados mestre (logons e usuários de banco de dados)<br /><br /> [Criar um logon do SQL Server](../../relational-databases/security/authentication-access/create-a-login.md)<br /><br /> [Gerenciando bancos de dados e logons no banco de dados do Azure SQL](/previous-versions/azure/ee336235(v=azure.100))<br /><br /> [Criar um usuário de banco de dados](../../relational-databases/security/authentication-access/create-a-database-user.md)<br /><br /> <br /><br /> Autenticar em um banco de dados do usuário<br /><br /> [Usuários do Banco de Dados Independente - Tornando seu Banco de Dados Portátil](../../relational-databases/security/contained-database-users-making-your-database-portable.md)|  
|**Usando outras identidades**<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: Credenciais<br /><br /> :::image type="icon" source="../performance/media/security-center-sqlserver.png"::: Executar como outro logon<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: Executar como outro usuário de banco de dados|[Credenciais &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)<br /><br /> [Executar como outro logon](../../t-sql/statements/execute-as-transact-sql.md)<br /><br /> [Executar como outro usuário de banco de dados](../../t-sql/statements/execute-as-transact-sql.md)|  
  
##  <a name="authorization-what-can-you-do"></a><a name="What"></a> Autorização: o que você pode fazer?  
  
|||  
|-|-|  
|**Concedendo, revogando e negando permissões**<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: Classes protegíveis<br /><br /> :::image type="icon" source="../performance/media/security-center-sqlserver.png"::: Permissões granulares de servidor<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: Permissões granulares de banco de dados|[Hierarquia de permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)<br /><br /> [Permissões](../../relational-databases/security/permissions-database-engine.md)<br /><br /> [Protegíveis](../../relational-databases/security/securables.md)<br /><br /> [Guia de Introdução às permissões do mecanismo de banco de dados](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)|  
|**Segurança por funções**<br /><br /> :::image type="icon" source="../performance/media/security-center-sqlserver.png"::: Funções de nível de servidor<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: Funções de nível de banco de dados|[Funções de nível de servidor](../../relational-databases/security/authentication-access/server-level-roles.md)<br /><br /> [Funções de nível de banco de dados](../../relational-databases/security/authentication-access/database-level-roles.md)|  
|**Restringindo o acesso a dados aos elementos de dados selecionados**<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: Restringir o acesso a dados com exibições/procedimentos<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: Segurança em Nível de Linha<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: Máscara Dinâmica de Dados<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: Objetos assinados|Restringir acesso a dados usando [Exibições](../../relational-databases/views/views.md) e [Procedimentos](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)<br /><br /> [Segurança em nível de linha (SQL Server)](../../relational-databases/security/row-level-security.md)<br /><br /> [Segurança em nível de linha (banco de dados SQL do Azure)](./row-level-security.md)<br /><br /> [Mascaramento de dados dinâmicos (SQL Server)](../../relational-databases/security/dynamic-data-masking.md)<br /><br /> [Mascaramento de Dados Dinâmicos (Banco de Dados SQL do Azure)](/azure/azure-sql/database/dynamic-data-masking-overview)<br /><br /> [Objetos assinados](../../t-sql/statements/add-signature-transact-sql.md)|  
  
##  <a name="encryption-storing-secret-data"></a><a name="Encrypt"></a> Criptografia: armazenar dados secretos  
  
|||  
|-|-|  
|**Criptografando arquivos**<br /><br /> :::image type="icon" source="../performance/media/security-center-sqlserver.png"::: Criptografia BitLocker (nível de unidade)<br /><br /> :::image type="icon" source="../performance/media/security-center-sqlserver.png"::: Criptografia de NTFS (nível de pasta)<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: Transparent Data Encryption (nível de arquivo)<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: Criptografia de backup (nível de arquivo)|[BitLocker (nível de unidade)](https://support.microsoft.com/kb/2855131)<br /><br /> [Criptografia de NTFS (nível de pasta)](/previous-versions/tn-archive/dd163562(v=technet.10))<br /><br /> [Criptografia transparente de dados (nível de arquivo)](../../relational-databases/security/encryption/transparent-data-encryption.md)<br /><br /> [Criptografia de backup (nível de arquivo)](../../relational-databases/backup-restore/backup-encryption.md)|  
|**Criptografando fontes**<br /><br /> :::image type="icon" source="../performance/media/security-center-sqlserver.png"::: Módulo de Gerenciamento Extensível de Chaves<br /><br /> :::image type="icon" source="../performance/media/security-center-sqlserver.png"::: Chaves armazenadas no Azure Key Vault<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: Always Encrypted|[Módulo de Gerenciamento Extensível de Chaves](../../relational-databases/security/encryption/extensible-key-management-ekm.md)<br /><br /> [Chaves armazenadas no cofre principal do Azure](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)<br /><br /> [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)|  
|**Coluna, dados e criptografia de chave**<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: Criptografia por certificado<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: Criptografia por chave simétrica<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: Criptografia por chave assimétrica<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: Criptografia por frase secreta|[Criptografar por certificado](../../t-sql/functions/encryptbycert-transact-sql.md)<br /><br /> [Criptografar por chave assimétrica](../../t-sql/functions/encryptbyasymkey-transact-sql.md)<br /><br /> [Criptografar por chave simétrica](../../t-sql/functions/encryptbykey-transact-sql.md)<br /><br /> [Criptografar por frase secreta](../../t-sql/functions/encryptbypassphrase-transact-sql.md)<br /><br /> [Criptografar uma coluna de dados](../../relational-databases/security/encryption/encrypt-a-column-of-data.md)|  
  
##  <a name="connection-security-restricting-and-securing"></a><a name="Connect"></a> Segurança da conexão: restringir e proteger  
  
|||  
|-|-|  
|**Proteção de firewall**<br /><br /> :::image type="icon" source="../performance/media/security-center-sqlserver.png"::: Configurações de Firewall do Windows<br /><br /> :::image type="icon" source="../../relational-databases/security/media/security-center-sqldb.png"::: Configurações de firewall do serviço do Azure<br /><br /> :::image type="icon" source="../../relational-databases/security/media/security-center-sqldb.png"::: Configurações de firewall do banco de dados|[Configurar um Firewall do Windows para acesso ao Mecanismo de Banco de Dados](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)<br /><br /> [Configurações de Firewall de banco de dados do SQL do Azure](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)<br /><br /> [Configurações de Firewall de serviço do Azure](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)|  
|**Criptografando dados em trânsito**<br /><br /> :::image type="icon" source="../performance/media/security-center-both.png"::: Conexões SSL forçadas<br /><br /> :::image type="icon" source="../performance/media/security-center-sqlserver.png"::: Conexões SSL opcionais|[Habilitar conexões criptografadas com o Mecanismo de Banco de Dados](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)<br /><br /> [Habilitar conexões criptografadas com o Mecanismo de Banco de Dados](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md), [Segurança de rede](/azure/sql-database/sql-database-security-best-practice#network-security) <br /><br /> [Suporte a TLS 1.2 para o Microsoft SQL Server](https://support.microsoft.com/kb/3135244)|  
  
##  <a name="auditing-recording-access"></a><a name="Audit"></a> Auditoria: acesso de gravação  
  
|||  
|-|-|  
|**Auditoria automatizada**<br /><br /> :::image type="icon" source="../../relational-databases/performance/media/security-center-sqlserver.png"::: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Auditoria (nível de banco de dados e servidor)<br /><br /> :::image type="icon" source="../../relational-databases/security/media/security-center-sqldb.png"::: [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Auditoria (nível de banco de dados)<br /><br /> :::image type="icon" source="../../relational-databases/security/media/security-center-sqldb.png"::: Detectar ameaças| <br /><br /> [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)<br /><br /> [Auditoria do banco de dados SQL](/azure/azure-sql/database/auditing-overview)<br /><br /> [Introdução à Proteção Avançada contra Ameaças do Banco de Dados SQL](/azure/azure-sql/database/threat-detection-configure) <br /><br /> [Avaliação de Vulnerabilidade do Banco de Dados SQL](/azure/sql-database/sql-vulnerability-assessment) |  
|**Auditoria personalizada**<br /><br /> :::image type="icon" source="../../relational-databases/performance/media/security-center-both.png"::: Gatilhos|Implementação de auditoria personalizada: Criando [DDL Triggers](../../relational-databases/triggers/ddl-triggers.md) e [DML Triggers](../../relational-databases/triggers/dml-triggers.md)|  
|**Conformidade**<br /><br /> :::image type="icon" source="../../relational-databases/performance/media/security-center-both.png"::: Conformidade|SQL Server:<br />                        [critérios comuns](https://go.microsoft.com/fwlink/?LinkId=616319)<br /><br /> Banco de dados SQL:<br />                        [Central de Confiabilidade do Microsoft Azure: conformidade por recurso](https://azure.microsoft.com/support/trust-center/services/)|  
  
##  <a name="sql-injection"></a><a name="SQLInjection"></a> Injeção SQL  
 Injeção de SQL é um ataque no qual um código mal-intencionado é inserido em cadeias de caracteres que são passadas posteriormente para o [!INCLUDE[ssDE](../../includes/ssde-md.md)] para análise e execução. Qualquer procedimento que construa instruções SQL deve ser verificado quanto a vulnerabilidades de injeção porque o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executará todas as consultas sintaticamente válidas que receber. Todos os sistemas de banco de dados têm algum risco de Injeção de SQL e muitas das vulnerabilidades são introduzidas no aplicativo que está consultando o [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Você pode impedir ataques de injeção de SQL usando procedimentos armazenados e comandos parametrizados, evitando o SQL dinâmico e restringindo as permissões de todos os usuários.  Para obter mais informações, consulte [SQL Injection](../../relational-databases/security/sql-injection.md).  
  
 Links adicionais para programadores de aplicativos:  
  
-   [Cenários de Segurança de Aplicativo no SQL Server](/dotnet/framework/data/adonet/sql/application-security-scenarios-in-sql-server)  
  
-   [Gravação de SQL Dinâmico Seguro no SQL Server](/dotnet/framework/data/adonet/sql/writing-secure-dynamic-sql-in-sql-server)  
  
-   [Como proteger-se contra ataques de injeção SQL no ASP.NET](/previous-versions/msp-n-p/ff648339(v=pandp.10))  
  
## <a name="see-also"></a>Consulte Também  
 [Guia de Introdução às permissões do mecanismo de banco de dados](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)   
 [Protegendo o SQL Server](../../relational-databases/security/securing-sql-server.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Certificados e chaves assimétricas do SQL Server](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)   
 [Criptografia do SQL Server](../../relational-databases/security/encryption/sql-server-encryption.md)   
 [Configuração da Área de Superfície](../../relational-databases/security/surface-area-configuration.md)   
 [Senhas fortes](../../relational-databases/security/strong-passwords.md)   
 [propriedade TRUSTWORTHY do banco de dados](../../relational-databases/security/trustworthy-database-property.md)   
 [Recursos e tarefas do Mecanismo de Banco de Dados](../../sql-server/what-s-new-in-sql-server-ver15.md)  
 [Protegendo a propriedade intelectual do seu SQL Server](../../relational-databases/security/protecting-your-sql-server-intellectual-property.md)   
  
[!INCLUDE[get-help-security](../../includes/get-help-security.md)]