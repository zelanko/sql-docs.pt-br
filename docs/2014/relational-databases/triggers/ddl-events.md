---
title: Eventos DDL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- DDL events
- DDL triggers, events
- events [SQL Server], DDL
ms.assetid: 62ef24b4-3553-4aed-b62a-670980bae501
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 58b96e8ef7dfd0f2ef2d5f087c1ab73f3453b451
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37413235"
---
# <a name="ddl-events"></a>Eventos DDL
  As tabelas seguintes listam os eventos DDL que podem ser usados para um gatilho DDL ou notificação de eventos. Observe que cada evento corresponde a uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] ou procedimento armazenado, com a sintaxe de instrução modificada para incluir um caractere sublinhado (_) entre palavras-chave.  
  
> [!IMPORTANT]  
>  Os procedimentos armazenados do sistema que executam operações similares a DDL também podem acionar gatilhos DDL e notificações de eventos. Teste seus gatilhos e notificações de eventos DDL para determinar suas respostas aos procedimentos armazenados do sistema que são executados. Por exemplo, a instrução CREATE TYPE e o procedimento armazenado **sp_addtype** acionarão um gatilho DDL ou uma notificação de eventos que tenham sido criados em um evento CREATE_TYPE.  
  
## <a name="ddl-statements-that-have-server-or-database-scope"></a>Instruções DDL com escopo de servidor ou banco de dados  
 Os gatilhos DDL ou as notificações de eventos podem ser criados para serem acionados em resposta aos eventos a seguir, quando eles ocorrerem no banco de dados no qual o gatilho ou a notificação de eventos são criados ou em qualquer local na instância do servidor.  
  
||||  
|-|-|-|  
|CREATE_APPLICATION_ROLE (aplica-se à instrução CREATE APPLICATION ROLE e **sp_addapprole**. Se um novo esquema for criado, este evento também irá disparar um evento CREATE_SCHEMA.)|ALTER_APPLICATION_ROLE (Aplica-se à instrução ALTER APPLICATION ROLE e a **sp_approlepassword**.)|DROP_APPLICATION_ROLE (aplica-se à instrução DROP APPLICATION ROLE e **sp_dropapprole**.)|  
|CREATE_ASSEMBLY|ALTER_ASSEMBLY|DROP_ASSEMBLY|  
|CREATE_ASYMMETRIC_KEY|ALTER_ASYMMETRIC_KEY|DROP_ASYMMETRIC_KEY|  
|ALTER_AUTHORIZATION|ALTER_AUTHORIZATION_DATABASE (Aplica-se à instrução ALTER AUTHORIZATION, quando é especificado ON DATABASE e a **sp_changedbowner**.)||  
|CREATE_BROKER_PRIORITY|CREATE_BROKER_PRIORITY|CREATE_BROKER_PRIORITY|  
|CREATE_CERTIFICATE|ALTER_CERTIFICATE|DROP_CERTIFICATE|  
|CREATE_CONTRACT|DROP_CONTRACT||  
|CREATE_CREDENTIAL|ALTER_CREDENTIAL|DROP_CREDENTIAL|  
|GRANT_DATABASE|DENY_DATABASE|REVOKE_DATABASE|  
|CREATE_DATABASE_AUDIT_SPEFICIATION|ALTER_DATABASE_AUDIT_SPEFICIATION|DENY_DATABASE_AUDIT_SPEFICIATION|  
|CREATE_DATABASE_ENCRYPTION_KEY|ALTER_DATABASE_ENCRYPTION_KEY|DROP_DATABASE_ENCRYPTION_KEY|  
|CREATE_DEFAULT|DROP_DEFAULT||  
|BIND_DEFAULT (aplica-se a **sp_bindefault**.)|UNBIND_DEFAULT (aplica-se a **sp_unbindefault**.)||  
|CREATE_EVENT_NOTIFICATION|DROP_EVENT_NOTIFICATION||  
|CREATE_EXTENDED_PROPERTY (aplica-se a **sp_addextendedproperty**.)|ALTER_EXTENDED_PROPERTY (Aplica-se a **sp_updateextendedproperty**.)|DROP_EXTENDED_PROPERTY (aplica-se a **sp_dropextendedproperty**.)|  
|CREATE_FULLTEXT_CATALOG (aplica-se à instrução CREATE FULLTEXT CATALOG e **sp_fulltextcatalog** quando *create* é especificado.)|ALTER_FULLTEXT_CATALOG (Aplica-se à instrução ALTER_FULLTEXT_CATALOG, a **sp_fulltextcatalog** , quando *start_incremental*, *start_full*, *Stop*ou *Rebuild* é especificado, e a **sp_fulltext_database** , quando *enable* é especificado.)|DROP_FULLTEXT_CATALOG (aplica-se à instrução DROP FULLTEXT CATALOG e **sp_fulltextcatalog** , quando *drop* é especificado.)|  
|CREATE_FULLTEXT_INDEX (aplica-se à instrução CREATE FULLTEXT INDEX e **sp_fulltexttable** , quando *create* é especificado.)|ALTER_FULLTEXT_INDEX (Aplica-se à instrução ALTER_FULLTEXT_INDEX, a **sp_fulltextcatalog** quando *start_full*, *start_incremental*ou *stop* é especificado, e a **sp_fulltext_column**e **sp_fulltext_table** , quando qualquer ação que não seja *create* ou *drop* for especificada.)|DROP_FULLTEXT_INDEX (aplica-se à instrução DROP FULLTEXT INDEX e **sp_fulltexttable** , quando *drop* é especificado.)|  
|CREATE_FULLTEXT_STOPLIST|ALTER_FULLTEXT_STOPLIST|DROP_FULLTEXT_STOPLIST|  
|CREATE_FUNCTION|ALTER_FUNCTION|DROP_FUNCTION|  
|CREATE_INDEX|ALTER_INDEX (Aplica-se à instrução ALTER INDEX e a **sp_indexoption**.)|DROP_INDEX|  
|CREATE_MASTER_KEY|ALTER_MASTER_KEY|DROP_MASTER_KEY|  
|CREATE_MESSAGE_TYPE|ALTER_MESSAGE_TYPE|DROP_MESSAGE_TYPE|  
|CREATE_PARTITION_FUNCTION|ALTER_PARTITION_FUNCTION|DROP_PARTITION_FUNCTION|  
|CREATE_PARTITION_SCHEME|ALTER_PARTITION_SCHEME|DROP_PARTITION_SCHEME|  
|CREATE_PLAN_GUIDE (aplica-se a **sp_create_plan_guide**.)|ALTER_PLAN_GUIDE (Aplica-se a **sp_control_plan_guide** quando ENABLE, ENABLE ALL, DISABLE ou DISABLE ALL é especificado.)|DROP_PLAN_GUIDE (aplica-se a **sp_control_plan_guide** quando DROP ou DROP ALL é especificado.)|  
|CREATE_PROCEDURE|ALTER_PROCEDURE (Aplica-se à instrução ALTER PROCEDURE e a **sp_procoption**.)|DROP_PROCEDURE|  
|CREATE_QUEUE|ALTER_QUEUE|DROP_QUEUE|  
|CREATE_REMOTE_SERVICE_BINDING|ALTER_REMOTE_SERVICE_BINDING|DROP_REMOTE_SERVICE_BINDING|  
|CREATE_SPATIAL_INDEX|||  
|RENAME (aplica-se a **sp_rename**)|||  
|CREATE_ROLE (aplica-se à instrução CREATE ROLE, **sp_addrole**e **sp_addgroup**.)|ALTER_ROLE|DROP_ROLE (aplica-se à instrução DROP ROLE, **sp_droprole**e **sp_dropgroup**.)|  
|ADD_ROLE_MEMBER|DROP_ROLE_MEMBER||  
|CREATE_ROUTE|ALTER_ROUTE|DROP_ROUTE|  
|CREATE_RULE|DROP_RULE||  
|BIND_RULE (aplica-se a **sp_bindrule**.)|UNBIND_RULE (aplica-se a **sp_unbindrule**.)||  
|CREATE_SCHEMA (aplica-se à instrução CREATE SCHEMA, **sp_addrole**, **sp_adduser**, **sp_addgroup**e **sp_grantdbaccess**.)|ALTER_SCHEMA (Aplica-se à instrução ALTER SCHEMA e a **sp_changeobjectowner**.)|DROP_SCHEMA|  
|CREATE_SEARCH_PROPERTY_LIST|ALTER_SEARCH_PROPERTY_LIST|DROP_SEARCH_PROPERTY_LIST|  
|CREATE_SEQUENCE_EVENTS|CREATE_SEQUENCE_EVENTS|CREATE_SEQUENCE_EVENTS|  
|CREATE_SERVER_ROLE|ALTER_SERVER_ROLE|DROP_SERVER_ROLE|  
|CREATE_SERVICE|ALTER_SERVICE|DROP_SERVICE|  
|ALTER_SERVICE_MASTER_KEY|BACKUP_SERVICE_MASTER_KEY|RESTORE_SERVICE_MASTER_KEY|  
|ADD_SIGNATURE (para operações de assinatura em objetos de escopo sem esquema; banco de dados, assembly, gatilho)|DROP_SIGNATURE||  
|ADD_SIGNATURE_SCHEMA_OBJECT (para objetos de escopo com esquema; procedimentos armazenados, funções)|DROP_SIGNATURE_SCHEMA_OBJECT||  
|CREATE_SPATIAL_INDEX|ALTER_INDEX pode ser usado para índices espaciais.|DROP_INDEX pode ser usado para índices de espaço.|  
|CREATE_STATISTICS|DROP_STATISTICS|UPDATE_STATISTICS|  
|CREATE_SYMMETRIC_KEY|ALTER_SYMMETRIC_KEY|DROP_SYMMETRIC_KEY|  
|CREATE_SYNONYM|DROP_SYNONYM||  
|CREATE_TABLE|ALTER_TABLE (Aplica-se à instrução ALTER TABLE e a **sp_tableoption**.)|DROP_TABLE|  
|CREATE_TRIGGER|ALTER_TRIGGER (Aplica-se à instrução ALTER TRIGGER e a **sp_settriggerorder**.)|DROP_TRIGGER|  
|CREATE_TYPE (aplica-se à instrução CREATE TYPE e **sp_addtype**.)|DROP_TYPE (aplica-se à instrução DROP TYPE e **sp_droptype**.)||  
|CREATE_USER (aplica-se à instrução CREATE USER, **sp_adduser**e **sp_grantdbaccess**.)|ALTER_USER (Aplica-se à instrução ALTER USER e a **sp_change_users_login**.)|DROP_USER (aplica-se à instrução DROP USER, **sp_dropuser**e **sp_revokedbaccess**.)|  
|CREATE_VIEW|ALTER_VIEW|DROP_VIEW|  
|CREATE_XML_INDEX|ALTER_INDEX pode ser usado para índices XML.|DROP_INDEX pode ser usado para índices XML.|  
|CREATE_XML_SCHEMA_COLLECTION|ALTER_XML_SCHEMA_COLLECTION|DROP_XML_SCHEMA_COLLECTION|  
  
## <a name="ddl-statements-that-have-server-scope"></a>Instruções DDL com escopo de servidor  
 Gatilhos DDL ou notificações de eventos podem ser criados para serem acionados em resposta aos eventos a seguir, sempre que eles ocorrerem na instância do servidor.  
  
||||  
|-|-|-|  
|ALTER_AUTHORIZATION_SERVER|ALTER_SERVER_CONFIGURATION|ALTER_INSTANCE (Aplica-se a **sp_configure** e **sp_addserver** quando uma instância de servidor local é especificada.)|  
|CREATE_AVAILABILITY_GROUP|ALTER_AVAILABILITY_GROUP|DROP_AVAILABILITY_GROUP|  
|CREATE_CREDENTIAL|ALTER_CREDENTIAL|DROP_CREDENTIAL|  
|CREATE_CRYPTOGRAPHIC_PROVIDER|ALTER_CRYPTOGRAPHIC_PROVIDER|DROP_CRYPTOGRAPHIC_PROVIDER|  
|CREATE_DATABASE|ALTER_DATABASE (Aplica-se à instrução ALTER DATABASE e a **sp_fulltext_database**.)|DROP_DATABASE|  
|CREATE_ENDPOINT|ALTER_ENDPOINT|DROP_ENDPOINT|  
|CREATE_EVENT_SESSION|ALTER_EVENT_SESSION|DROP_EVENT_SESSION|  
|CREATE_EXTENDED_PROCEDURE (aplica-se a **sp_addextendedproc**.)|DROP_EXTENDED_PROCEDURE (aplica-se a **sp_dropextendedproc**.)||  
|CREATE_LINKED_SERVER (aplica-se a **sp_addlinkedserver**.)|ALTER_LINKED_SERVER (Aplica-se a **sp_serveroption**.)|DROP_LINKED_SERVER (aplica-se a **sp_dropserver** quando um servidor vinculado é especificado.)|  
|CREATE_LINKED_SERVER_LOGIN (aplica-se a **sp_addlinkedsrvlogin**.)|DROP_LINKED_SERVER_LOGIN (aplica-se a **sp_droplinkedsrvlogin**.)||  
|CREATE_LOGIN (aplica-se à instrução CREATE LOGIN, **sp_addlogin**, **sp_grantlogin**, **xp_grantlogin**e **sp_denylogin** quando usado em um logon não inexistente que deve ser criado implicitamente.)|ALTER_LOGIN (Aplica-se à instrução ALTER LOGIN, **sp_defaultdb**, **sp_defaultlanguage**, **sp_password**e **sp_change_users_login** , quando *Auto_Fix* é especificado.)|DROP_LOGIN (aplica-se à instrução DROP LOGIN, **sp_droplogin**, **sp_revokelogin**e **xp_revokelogin**.)|  
|CREATE_MESSAGE (aplica-se a **sp_addmessage**.)|ALTER_MESSAGE (Aplica-se a **sp_altermessage**.)|DROP_MESSAGE (aplica-se a **sp_dropmessage**.)|  
|CREATE_REMOTE_SERVER (aplica-se a **sp_addserver**.)|ALTER_REMOTE_SERVER (Aplica-se a **sp_setnetname**.)|DROP_REMOTE_SERVER (aplica-se a **sp_dropserver** quando um servidor remoto é especificado.)|  
|CREATE_RESOURCE_POOL|ALTER_RESOURCE_POOL|DROP_RESOURCE_POOL|  
|GRANT_SERVER|DENY_SERVER|REVOKE_SERVER|  
|ADD_SERVER_ROLE_MEMBER|DROP_SERVER_ROLE_MEMBER||  
|CREATE_SERVER_AUDIT|ALTER_SERVER_AUDIT|DROP_SERVER_AUDIT|  
|CREATE_SERVER_AUDIT_SPECIFICATION|ALTER_SERVER_AUDIT_SPECIFICATION|DROP_SERVER_AUDIT_SPECIFICATION|  
|CREATE_WORKLOAD_GROUP|CREATE_WORKLOAD_GROUP|CREATE_WORKLOAD_GROUP|  
  
## <a name="see-also"></a>Consulte também  
 [Gatilhos DDL](ddl-triggers.md)   
 [Notificações de eventos](../service-broker/event-notifications.md)   
 [Grupos de eventos DDL](ddl-event-groups.md)  
  
  
