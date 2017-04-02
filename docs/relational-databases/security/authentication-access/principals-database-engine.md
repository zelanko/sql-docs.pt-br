---
title: "Entidades (Mecanismo de Banco de Dados) | Microsoft Docs"
ms.custom: ""
ms.date: "01/09/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.roleproperties.selectroll.f1"
  - "sql13.swb.databaseuser.permissions.user.f1--May use common.permissions"
helpviewer_keywords: 
  - "certificados [SQL Server], entidades"
  - "funções [SQL Server], entidades"
  - "permissões [SQL Server], entidades"
  - "##MS_SQLAuthenticatorCertificate ##"
  - "entidades [SQL Server]"
  - "##MS_SQLResourceSigningCertificate ##"
  - "grupos [SQL Server], entidades"
  - "##MS_AgentSigningCertificate ##"
  - "autenticação [SQL Server], entidades"
  - "esquemas [SQL Server], entidades"
  - "entidades [SQL Server], sobre entidades"
  - "segurança [SQL Server], entidades"
  - "usuários [SQL Server], entidades"
  - "##MS_SQLReplicationSigningCertificate ##"
ms.assetid: 3f7adbf7-6e40-4396-a8ca-71cbb843b5c2
caps.latest.revision: 57
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 55
---
# Entidades (Mecanismo de Banco de Dados)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../../includes/tsql-appliesto-ss2008-all-md.md)]

  *Entidades* são entidades que podem solicitar recursos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Como outros componentes do modelo de autorização do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], as entidades podem ser organizadas em uma hierarquia. O escopo de influência de uma entidade depende do escopo de sua definição: Windows, servidor, banco de dados e, se a entidade é indivisível ou uma coleção. Um logon do Windows é um exemplo de um principal indivisível, enquanto um Grupo do Windows é um exemplo de um principal que é uma coleção. Todas as entidades têm um SID (identificador de segurança).  
  
 **Entidades no nível do Windows**  
  
-   Logon de domínio do Windows  
  
-   Logon local do Windows  
  
 **Entidades de****nível** do **SQL Server**  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Logon  
  
-   Função do servidor  
  
 **Entidades no nível do banco de dados**  
  
-   Usuário de banco de dados  
  
-   Função de banco de dados  
  
-   Função de aplicativo  
  
## Logon sa do SQL Server  
 O logon sa do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é uma entidade de segurança no nível do servidor. Por padrão, ele é criado quando uma instância é instalada. A partir do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], o banco de dados padrão de sa é o mestre. Essa é uma alteração de comportamento de versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## Função de banco de dados pública  
 Cada usuário do banco de dados pertence à função do banco de dados público. Quando permissões específicas não são concedidas ou são negadas a um usuário em um objeto seguro, o usuário herda as permissões concedidas como públicas naquele objeto seguro.  
  
## INFORMATION_SCHEMA e sys  
 Todo o banco de dados inclui duas entidades exibidas como usuários em exibições do catálogo: INFORMATION_SCHEMA e sys. Essas entidades são exigidas pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Elas não são entidades, tampouco podem ser modificadas ou descartadas.  
  
## Logons do SQL Server com base em certificado  
 Entidades de servidor com nomes entre duas marcas hash (##) são somente para uso interno do sistema. As entidades a seguir são criadas com base em certificados quando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é instalado e não devem ser excluídas.  
  
-   \##MS_SQLResourceSigningCertificate##  
  
-   \##MS_SQLReplicationSigningCertificate##  
  
-   \##MS_SQLAuthenticatorCertificate##  
  
-   \##MS_AgentSigningCertificate##  
  
-   \##MS_PolicyEventProcessingLogin##  
  
-   \##MS_PolicySigningCertificate##  
  
-   \##MS_PolicyTsqlExecutionLogin##  
  
## O Usuário convidado  
 Cada banco de dados inclui um **convidado**. As permissões concedidas ao usuário **convidado** são herdadas pelos usuários que têm acesso ao banco de dados, mas que não têm uma conta de usuário no banco de dados. O usuário **convidado** não pode ser descartado, mas pode ser desabilitado revogando sua permissão **CONNECT**. A permissão **CONNECT** pode ser revogada executando `REVOKE CONNECT FROM GUEST` em qualquer banco de dados que não seja mestre ou tempdb.  
  
## Servidor de banco de dados e cliente  
 Por definição, um cliente e um servidor de banco de dados são entidades de segurança e podem ser protegidos. Essas entidades podem ser autenticadas mutuamente antes que uma conexão de rede segura seja estabelecida. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dá suporte ao protocolo de autenticação [Kerberos](http://go.microsoft.com/fwlink/?LinkId=100758), que define como os clientes interagem com um serviço de autenticação de rede.  
  
## Tarefas relacionadas  
 Para obter informações sobre como criar um sistema de permissões, veja [Introdução às permissões do mecanismo de banco de dados](../../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).  
  
 Os tópicos a seguir são incluídos nesta seção dos Manuais Online do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
-   [Tópicos de instruções sobre gerenciamento de logons, usuários e esquemas](../../../relational-databases/security/authentication-access/managing-logins-users-and-schemas-how-to-topics.md)  
  
-   [Funções de nível de servidor](../../../relational-databases/security/authentication-access/server-level-roles.md)  
  
-   [Funções de nível de banco de dados](../../../relational-databases/security/authentication-access/database-level-roles.md)  
  
-   [Funções de aplicativo](../../../relational-databases/security/authentication-access/application-roles.md)  
  
## Consulte também  
 [Protegendo o SQL Server](../../../relational-databases/security/securing-sql-server.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.sql_logins &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-sql-logins-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [Funções de nível de servidor](../../../relational-databases/security/authentication-access/server-level-roles.md)   
 [Funções de nível de banco de dados](../../../relational-databases/security/authentication-access/database-level-roles.md)  
  
  