---
title: Entidades de segurança (mecanismo de banco de dados) | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.roleproperties.selectroll.f1
- sql13.swb.databaseuser.permissions.user.f1--May use common.permissions
helpviewer_keywords:
- certificates [SQL Server], principals
- roles [SQL Server], principals
- permissions [SQL Server], principals
- '##MS_SQLAuthenticatorCertificate##'
- principals [SQL Server]
- '##MS_SQLResourceSigningCertificate##'
- groups [SQL Server], principals
- '##MS_AgentSigningCertificate##'
- authentication [SQL Server], principals
- schemas [SQL Server], principals
- principals [SQL Server], about principals
- security [SQL Server], principals
- users [SQL Server], principals
- '##MS_SQLReplicationSigningCertificate##'
ms.assetid: 3f7adbf7-6e40-4396-a8ca-71cbb843b5c2
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9bf4ae1f391a982294a14cb38bcdce879d0b2253
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47632685"
---
# <a name="principals-database-engine"></a>Entidades (Mecanismo de Banco de Dados)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  *Entidades* são entidades que podem solicitar recursos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Como outros componentes do modelo de autorização do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , as entidades podem ser organizadas em uma hierarquia. O escopo de influência de uma entidade depende do escopo de sua definição: Windows, servidor, banco de dados e, se a entidade é indivisível ou uma coleção. Um logon do Windows é um exemplo de um principal indivisível, enquanto um Grupo do Windows é um exemplo de um principal que é uma coleção. Todas as entidades têm um SID (identificador de segurança). Este tópico aplica-se a todas as versões do SQL Server, mas há algumas restrições para entidade de segurança no nível do servidor no banco de dados SQL ou no SQL Data Warehouse. 
  
## <a name="sql-server-level-principals"></a>Entidades de segurança no nível do SQL Server  
  
- Logon de autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]   
- Logon de autenticação do Windows para um usuário do Windows  
- Logon de autenticação do Windows para um grupo do Windows   
- Logon de autenticação do Azure Active Directory para um usuário do AD
- Logon de autenticação do Azure Active Directory para um grupo do AD
- Função do servidor  
  
## <a name="database-level-principals"></a>Entidades no nível do banco de dados
  
- Usuário de banco de dados (existem 11 tipos de usuários. Para obter mais informações, consulte [CREATE USER](../../../t-sql/statements/create-user-transact-sql.md).)
- Função de banco de dados
- Função de aplicativo
  
## <a name="sa-login"></a>Logon sa  
 O logon `sa` do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é uma entidade de segurança no nível do servidor. Por padrão, ele é criado quando uma instância é instalada. A partir do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], o banco de dados padrão de sa é o mestre. Essa é uma alteração de comportamento de versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O logon `sa` é membro da função de banco de dados fixa `sysadmin`. O logon `sa` tem todas as permissões no servidor e não pode ser limitado. O logon `sa` não pode ser descartado, mas pode ser desabilitado para que ninguém possa usá-lo.

## <a name="dbo-user-and-dbo-schema"></a>Usuário dbo e esquema dbo

O usuário do `dbo` é uma entidade de usuário especial em cada banco de dados. Todos os administradores do SQL Server, os membros da função de servidor fixa `sysadmin`, o logon `sa` e os proprietários do banco de dados, entram nos bancos de dados como o usuário `dbo`. O usuário `dbo` tem todas as permissões no banco de dados e não pode ser limitado ou descartado. `dbo` representa o proprietário do banco de dados, mas a conta de usuário `dbo` não é igual à função de banco de dados fixa `db_owner` e a função de banco de dados fixa `db_owner` não é o mesmo que a conta de usuário registrada como o proprietário do banco de dados.     
O usuário `dbo` tem o esquema `dbo`. O esquema `dbo` é o esquema padrão para todos os usuários, a menos que algum outro esquema seja especificado.  O esquema `dbo` não pode ser descartado.
  
## <a name="public-server-role-and-database-role"></a>Função de servidor e a função de banco de dados pública  
Cada logon pertence à função de servidor fixa `public` e cada usuário de banco de dados pertence à função de banco de dados `public`. Quando um usuário ou logon não foi concedido ou teve permissões específicas negadas em um protegível, o logon ou o usuário herda as permissões concedidas como públicas naquele protegível. A função fixa de servidor `public` e a função fixa de banco de dados `public` não podem ser descartadas. No entanto, você pode revogar as permissões das funções `public`. Há várias permissões que são atribuídas às funções `public` por padrão. A maioria dessas permissões é necessária para operações de rotina no banco de dados, ou seja, o tipo de coisas que todos devem ser capazes de fazer. Tenha cuidado ao revogar permissões de logon ou usuário público, pois isso afetará todos os logons e usuários. Geralmente você não deve negar permissões para o público, porque a instrução deny substitui todas as instruções grant que possam ser feitas para indivíduos. 
  
## <a name="informationschema-and-sys-users-and-schemas"></a>INFORMATION_SCHEMA e usuários e esquemas sys 
 Todo banco de dados inclui duas entidades que são exibidas como usuários em exibições do catálogo: `INFORMATION_SCHEMA` e `sys`. Essas entidades são necessárias para uso interno do mecanismo de banco de dados. Elas não podem ser modificadas ou descartadas.  
  
## <a name="certificate-based-sql-server-logins"></a>Logons do SQL Server com base em certificado  
 Entidades de servidor com nomes entre duas marcas hash (##) são somente para uso interno do sistema. As entidades a seguir são criadas com base em certificados quando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é instalado e não devem ser excluídas.  
  
-   \##MS_SQLResourceSigningCertificate##    
-   \##MS_SQLReplicationSigningCertificate##    
-   \##MS_SQLAuthenticatorCertificate##    
-   \##MS_AgentSigningCertificate##   
-   \##MS_PolicyEventProcessingLogin##   
-   \##MS_PolicySigningCertificate##   
-   \##MS_PolicyTsqlExecutionLogin##   
 
 Essas contas de entidade de segurança não têm senhas que podem ser alteradas por administradores, pois são baseadas em certificados emitidos para a Microsoft.
  
## <a name="the-guest-user"></a>O Usuário convidado  
 Cada banco de dados inclui um `guest`. As permissões concedidas ao usuário `guest` são herdadas pelos usuários que têm acesso ao banco de dados, mas que não têm uma conta de usuário no banco de dados. O usuário `guest` não pode ser descartado, mas pode ser desabilitado revogando sua permissão CONNECT. A permissão CONNECT pode ser revogada executando `REVOKE CONNECT FROM GUEST;` em qualquer banco de dados diferente de `master` ou `tempdb`.  
  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter informações sobre como criar um sistema de permissões, veja [Introdução às permissões do mecanismo de banco de dados](../../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).  
  
 Os tópicos a seguir são incluídos nesta seção dos Manuais Online do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
-   [Tópicos de instruções sobre gerenciamento de logons, usuários e esquemas](../../../relational-databases/security/authentication-access/managing-logins-users-and-schemas-how-to-topics.md)  
  
-   [Funções de nível de servidor](../../../relational-databases/security/authentication-access/server-level-roles.md)  
  
-   [Funções de nível de banco de dados](../../../relational-databases/security/authentication-access/database-level-roles.md)  
  
-   [Funções de aplicativo](../../../relational-databases/security/authentication-access/application-roles.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Protegendo o SQL Server](../../../relational-databases/security/securing-sql-server.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.sql_logins &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-sql-logins-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [Funções de nível de servidor](../../../relational-databases/security/authentication-access/server-level-roles.md)   
 [Funções de nível de banco de dados](../../../relational-databases/security/authentication-access/database-level-roles.md)  
  
  
