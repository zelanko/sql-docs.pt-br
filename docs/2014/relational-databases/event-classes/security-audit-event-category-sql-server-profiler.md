---
title: Categoria de evento de auditoria de segurança (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Security Audit event category [SQL Server]
- event classes [SQL Server], Security Audit event category
- SQL Server event classes, Security Audit event category
ms.assetid: e64f7695-2f23-4adb-b83d-52f147cc1a2f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 81b07c1eb33176533cedbf0d02a71a264419b11e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85052555"
---
# <a name="security-audit-event-category-sql-server-profiler"></a>Categoria de evento de auditoria de segurança (SQL Server Profiler)
  A categoria de evento **Security Audit** contém eventos de auditoria de segurança.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|DESCRIÇÃO|  
|-----------|-----------------|  
|[Classe de evento Audit Add DB User](audit-add-db-user-event-class.md)|Indica que um logon foi adicionado ou removido como um usuário de banco de dados para um banco de dados.|  
|[Classe de evento Audit Add Login to Server Role](audit-add-login-to-server-role-event-class.md)|Indica que um logon foi adicionado ou removido de uma função de servidor fixa.|  
|[Classe de evento Audit Add Member to DB Role](audit-add-member-to-db-role-event-class.md)|Indica que um logon foi adicionado ou removido de uma função.|  
|[Classe de evento Audit Add Role](audit-add-role-event-class.md)|Indica que uma função de banco de dados foi adicionada ou removida de um banco de dados.|  
|[Classe de evento Audit Addlogin](audit-addlogin-event-class.md)|Indica que um logon foi adicionado ou removido.|  
|[Classe de evento Audit App Role Change Password](audit-app-role-change-password-event-class.md)|Indica que uma senha foi alterada para uma função de aplicativo.|  
|[Classe de evento Audit Backup e Restore](audit-backup-and-restore-event-class.md)|Indica que uma instrução de backup ou restauração foi emitida.|  
|[Classe de evento Audit Broker Conversation](broker-conversation-event-class.md)|Informa mensagens de auditoria relacionadas à segurança do diálogo Service Broker.|  
|[Classe de evento Audit Broker Login](audit-broker-login-event-class.md)|Informa mensagens de auditoria relacionadas à segurança de transporte do Service Broker.|  
|[Classe de evento Audit Change Audit](audit-change-audit-event-class.md)|Indica que uma modificação de rastreamento de auditoria foi feita.|  
|[Classe de evento Audit Change Database Owner](audit-change-database-owner-event-class.md)|Indica que foram verificadas as permissões para alterar o proprietário de um banco de dados.|  
|[Classe de evento Audit Database Management](audit-database-management-event-class.md)|Indica que um banco de dados foi criado, alterado ou descartado.|  
|[Classe de evento Audit Database Mirroring Login](audit-database-mirroring-login-event-class.md)|Informa mensagens de auditoria relacionadas à segurança de transporte do espelhamento de banco de dados.|  
|[Classe de evento Audit Database Object Access](audit-database-object-access-event-class.md)|Indica que um objeto de banco de dados, como um esquema, foi acessado.|  
|[Classe de evento Audit Database Object GDR](audit-database-object-gdr-event-class.md)|Indica que um evento GDR para um objeto de banco de dados ocorreu.|  
|[Classe de evento Audit Database Object Management](audit-database-object-management-event-class.md)|Indica que uma instrução CREATE, ALTER ou DROP foi executada em um objeto de banco de dados.|  
|[Classe de evento Audit Database Object Take Ownership](audit-database-object-take-ownership-event-class.md)|Indica que houve uma alteração de proprietário para objetos no escopo do banco de dados.|  
|[Classe de evento Audit Database Operation](audit-database-operation-event-class.md)|Indica que ocorreram várias operações, como notificação de consulta de ponto de verificação ou assinatura.|  
|[Classe de evento Audit Database Principal Impersonation](audit-database-principal-impersonation-event-class.md)|Indica que uma representação ocorreu no escopo do banco de dados.|  
|[Classe de evento Audit Database Principal Management](audit-database-principal-management-event-class.md)|Indica que entidades foram criadas, alteradas ou descartadas de um banco de dados.|  
|[Classe de evento Audit Database Scope GDR](audit-database-scope-gdr-event-class.md)|Indica que um GRANT, REVOKE ou DENY foi emitido para uma permissão de instrução por um usuário no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Classe de evento Audit DBCC](audit-dbcc-event-class.md)|Indica que um comando DBCC foi emitido.|  
|[Classe de evento Audit Fulltext](audit-fulltext-event-class.md)|Indica que ocorreu um evento de texto completo.|  
|[Classe de evento Audit Login Change Password](audit-login-change-password-event-class.md)|Indica que um usuário alterou sua senha de logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Classe de evento Audit Login Change Property](audit-login-change-property-event-class.md)|Indica que **sp_defaultdb**, **sp_defaultlanguage**ou ALTER LOGIN foi usado para modificar uma propriedade de um logon.|  
|[Classe de evento Audit Login](audit-login-event-class.md)|Indica que um usuário efetuou logon com êxito no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Classe de evento Audit Login Failed](audit-login-failed-event-class.md)|Indica que um usuário tentou efetuar logon no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e falhou.|  
|[Classe de evento Audit Login GDR](audit-login-gdr-event-class.md)|Indica que um direito de logon no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows foi adicionado ou removido.|  
|[Classe de evento Audit Logout](audit-logout-event-class.md)|Indica que um usuário efetuou logoff no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Classe de evento Audit Object Derived Permission](audit-object-derived-permission-event-class.md)|Indica que um CREATE, ALTER ou DROP foi emitido para um objeto.|  
|[Classe de evento Audit Schema Object Access](audit-schema-object-access-event-class.md)|Indica que uma permissão de objeto (como SELECT) foi usada.|  
|[Classe de evento Audit Schema Object GDR](audit-schema-object-gdr-event-class.md)|Indica que um GRANT, REVOKE ou DENY foi emitido para uma permissão de objeto de esquema por um usuário no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Classe de evento Audit Schema Object Management](audit-schema-object-management-event-class.md)|Indica que um objeto de servidor foi criado, alterado ou descartado.|  
|[Classe de evento Audit Schema Object Take Ownership](audit-schema-object-take-ownership-event-class.md)|Indica que foram verificadas as permissões para alterar o proprietário de objeto de esquema.|  
|[Classe de evento Audit Server Alter Trace](audit-server-alter-trace-event-class.md)|Indica que a permissão ALTER TRACE foi verificada.|  
|[Classe de evento Audit Server Object GDR](audit-server-object-gdr-event-class.md)|Indica que um evento GDR ocorreu para um objeto de esquema.|  
|[Classe de evento Audit Server Object Management](audit-server-object-management-event-class.md)|Indica que um evento CREATE, ALTER ou DROP ocorreu para um objeto de servidor.|  
|[Classe de evento Audit Server Object Take Ownership](audit-server-object-take-ownership-event-class.md)|Indica que um proprietário de objeto de servidor foi alterado.|  
|[Classe de evento Audit Server Operation](audit-server-operation-event-class.md)|Indica que operações de Auditoria ocorreram no servidor.|  
|[Classe de evento Audit Server Principal Impersonation](audit-server-principal-impersonation-event-class.md)|Indica que uma representação ocorreu no escopo do servidor.|  
|[Classe de evento Audit Server Principal Management](audit-server-principal-management-event-class.md)|Indica que um CREATE, ALTER ou DROP ocorreu para uma entidade de servidor.|  
|[Classe de evento Audit Server Scope GDR](audit-server-scope-gdr-event-class.md)|Indica que um evento GDR ocorreu para permissões de servidor.|  
|[Classe de evento Audit Server Starts and Stops](audit-server-starts-and-stops-event-class.md)|Indica que o status do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi modificado.|  
|[Classe de evento Audit Statement Permission](audit-statement-permission-event-class.md)|Indica que uma permissão de instrução foi usada.|  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Eventos estendidos](../extended-events/extended-events.md)  
  
  
