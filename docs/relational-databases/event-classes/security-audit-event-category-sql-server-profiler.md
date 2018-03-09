---
title: "Categoria de evento de auditoria de segurança (SQL Server Profiler) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: event-classes
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Security Audit event category [SQL Server]
- event classes [SQL Server], Security Audit event category
- SQL Server event classes, Security Audit event category
ms.assetid: e64f7695-2f23-4adb-b83d-52f147cc1a2f
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5b93277d27d4a797fc5ca5924794a7631673445f
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2018
---
# <a name="security-audit-event-category-sql-server-profiler"></a>Categoria de evento de auditoria de segurança (SQL Server Profiler)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
A categoria de evento **Security Audit** contém eventos de auditoria de segurança.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Classe de evento Audit Add DB User](../../relational-databases/event-classes/audit-add-db-user-event-class.md)|Indica que um logon foi adicionado ou removido como um usuário de banco de dados para um banco de dados.|  
|[Classe de evento Audit Add Login to Server Role](../../relational-databases/event-classes/audit-add-login-to-server-role-event-class.md)|Indica que um logon foi adicionado ou removido de uma função de servidor fixa.|  
|[Classe de evento Audit Add Member to DB Role](../../relational-databases/event-classes/audit-add-member-to-db-role-event-class.md)|Indica que um logon foi adicionado ou removido de uma função.|  
|[Classe de evento Audit Add Role](../../relational-databases/event-classes/audit-add-role-event-class.md)|Indica que uma função de banco de dados foi adicionada ou removida de um banco de dados.|  
|[Classe de evento Audit Addlogin](../../relational-databases/event-classes/audit-addlogin-event-class.md)|Indica que um logon foi adicionado ou removido.|  
|[Classe de evento Audit App Role Change Password](../../relational-databases/event-classes/audit-app-role-change-password-event-class.md)|Indica que uma senha foi alterada para uma função de aplicativo.|  
|[Classe de evento Audit Backup e Restore](../../relational-databases/event-classes/audit-backup-and-restore-event-class.md)|Indica que uma instrução de backup ou restauração foi emitida.|  
|[Classe de evento Audit Broker Conversation](../../relational-databases/event-classes/audit-broker-conversation-event-class.md)|Informa mensagens de auditoria relacionadas à segurança do diálogo Service Broker.|  
|[Classe de evento Audit Broker Login](../../relational-databases/event-classes/audit-broker-login-event-class.md)|Informa mensagens de auditoria relacionadas à segurança de transporte do Service Broker.|  
|[Classe de evento Audit Change Audit](../../relational-databases/event-classes/audit-change-audit-event-class.md)|Indica que uma modificação de rastreamento de auditoria foi feita.|  
|[Classe de evento Audit Change Database Owner](../../relational-databases/event-classes/audit-change-database-owner-event-class.md)|Indica que foram verificadas as permissões para alterar o proprietário de um banco de dados.|  
|[Classe de evento Audit Database Management](../../relational-databases/event-classes/audit-database-management-event-class.md)|Indica que um banco de dados foi criado, alterado ou descartado.|  
|[Classe de evento Audit Database Mirroring Login](../../relational-databases/event-classes/audit-database-mirroring-login-event-class.md)|Informa mensagens de auditoria relacionadas à segurança de transporte do espelhamento de banco de dados.|  
|[Classe de evento Audit Database Object Access](../../relational-databases/event-classes/audit-database-object-access-event-class.md)|Indica que um objeto de banco de dados, como um esquema, foi acessado.|  
|[Classe de evento Audit Database Object GDR](../../relational-databases/event-classes/audit-database-object-gdr-event-class.md)|Indica que um evento GDR para um objeto de banco de dados ocorreu.|  
|[Classe de evento Audit Database Object Management](../../relational-databases/event-classes/audit-database-object-management-event-class.md)|Indica que uma instrução CREATE, ALTER ou DROP foi executada em um objeto de banco de dados.|  
|[Classe de evento Audit Database Object Take Ownership](../../relational-databases/event-classes/audit-database-object-take-ownership-event-class.md)|Indica que houve uma alteração de proprietário para objetos no escopo do banco de dados.|  
|[Classe de evento Audit Database Operation](../../relational-databases/event-classes/audit-database-operation-event-class.md)|Indica que ocorreram várias operações, como notificação de consulta de ponto de verificação ou assinatura.|  
|[Classe de evento Audit Database Principal Impersonation](../../relational-databases/event-classes/audit-database-principal-impersonation-event-class.md)|Indica que uma representação ocorreu no escopo do banco de dados.|  
|[Classe de evento Audit Database Principal Management](../../relational-databases/event-classes/audit-database-principal-management-event-class.md)|Indica que entidades foram criadas, alteradas ou descartadas de um banco de dados.|  
|[Classe de evento Audit Database Scope GDR](../../relational-databases/event-classes/audit-database-scope-gdr-event-class.md)|Indica que um GRANT, REVOKE ou DENY foi emitido para uma permissão de instrução por um usuário no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Classe de evento Audit DBCC](../../relational-databases/event-classes/audit-dbcc-event-class.md)|Indica que um comando DBCC foi emitido.|  
|[Classe de evento Audit Fulltext](../../relational-databases/event-classes/audit-fulltext-event-class.md)|Indica que ocorreu um evento de texto completo.|  
|[Classe de evento Audit Login Change Password](../../relational-databases/event-classes/audit-login-change-password-event-class.md)|Indica que um usuário alterou sua senha de logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Classe de evento Audit Login Change Property](../../relational-databases/event-classes/audit-login-change-property-event-class.md)|Indica que **sp_defaultdb**, **sp_defaultlanguage**ou ALTER LOGIN foi usado para modificar uma propriedade de um logon.|  
|[Classe de evento Audit Login](../../relational-databases/event-classes/audit-login-event-class.md)|Indica que um usuário efetuou logon com êxito no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Classe de evento Audit Login Failed](../../relational-databases/event-classes/audit-login-failed-event-class.md)|Indica que um usuário tentou efetuar logon no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e falhou.|  
|[Classe de evento Audit Login GDR](../../relational-databases/event-classes/audit-login-gdr-event-class.md)|Indica que um direito de logon no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows foi adicionado ou removido.|  
|[Classe de evento Audit Logout](../../relational-databases/event-classes/audit-logout-event-class.md)|Indica que um usuário efetuou logoff no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Classe de evento Audit Object Derived Permission](../../relational-databases/event-classes/audit-object-derived-permission-event-class.md)|Indica que um CREATE, ALTER ou DROP foi emitido para um objeto.|  
|[Classe de evento Audit Schema Object Access](../../relational-databases/event-classes/audit-schema-object-access-event-class.md)|Indica que uma permissão de objeto (como SELECT) foi usada.|  
|[Classe de evento Audit Schema Object GDR](../../relational-databases/event-classes/audit-schema-object-gdr-event-class.md)|Indica que um GRANT, REVOKE ou DENY foi emitido para uma permissão de objeto de esquema por um usuário no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Classe de evento Audit Schema Object Management](../../relational-databases/event-classes/audit-schema-object-management-event-class.md)|Indica que um objeto de servidor foi criado, alterado ou descartado.|  
|[Classe de evento Audit Schema Object Take Ownership](../../relational-databases/event-classes/audit-schema-object-take-ownership-event-class.md)|Indica que foram verificadas as permissões para alterar o proprietário de objeto de esquema.|  
|[Classe de evento Audit Server Alter Trace](../../relational-databases/event-classes/audit-server-alter-trace-event-class.md)|Indica que a permissão ALTER TRACE foi verificada.|  
|[Classe de evento Audit Server Object GDR](../../relational-databases/event-classes/audit-server-object-gdr-event-class.md)|Indica que um evento GDR ocorreu para um objeto de esquema.|  
|[Classe de evento Audit Server Object Management](../../relational-databases/event-classes/audit-server-object-management-event-class.md)|Indica que um evento CREATE, ALTER ou DROP ocorreu para um objeto de servidor.|  
|[Classe de evento Audit Server Object Take Ownership](../../relational-databases/event-classes/audit-server-object-take-ownership-event-class.md)|Indica que um proprietário de objeto de servidor foi alterado.|  
|[Classe de evento Audit Server Operation](../../relational-databases/event-classes/audit-server-operation-event-class.md)|Indica que operações de Auditoria ocorreram no servidor.|  
|[Classe de evento Audit Server Principal Impersonation](../../relational-databases/event-classes/audit-server-principal-impersonation-event-class.md)|Indica que uma representação ocorreu no escopo do servidor.|  
|[Classe de evento Audit Server Principal Management](../../relational-databases/event-classes/audit-server-principal-management-event-class.md)|Indica que um CREATE, ALTER ou DROP ocorreu para uma entidade de servidor.|  
|[Classe de evento Audit Server Scope GDR](../../relational-databases/event-classes/audit-server-scope-gdr-event-class.md)|Indica que um evento GDR ocorreu para permissões de servidor.|  
|[Classe de evento Audit Server Starts and Stops](../../relational-databases/event-classes/audit-server-starts-and-stops-event-class.md)|Indica que o status do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi modificado.|  
|[Classe de evento Audit Statement Permission](../../relational-databases/event-classes/audit-statement-permission-event-class.md)|Indica que uma permissão de instrução foi usada.|  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)  
  
  
