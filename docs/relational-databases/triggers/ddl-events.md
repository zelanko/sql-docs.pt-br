---
title: Eventos DDL | Microsoft Docs
ms.custom: ''
ms.date: 11/01/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- DDL events
- DDL triggers, events
- events [SQL Server], DDL
ms.assetid: 62ef24b4-3553-4aed-b62a-670980bae501
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4281b67d44e7a1aa7404e89b07a505416f38260f
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243317"
---
# <a name="ddl-events"></a>Eventos DDL
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  As tabelas seguintes listam os eventos DDL que podem ser usados para um gatilho DDL ou notificação de eventos. Observe que cada evento corresponde a uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] ou procedimento armazenado, com a sintaxe de instrução modificada para incluir um caractere sublinhado (_) entre palavras-chave.  
  
> [!IMPORTANT]  
>  Os procedimentos armazenados do sistema que executam operações similares a DDL também podem acionar gatilhos DDL e notificações de eventos. Teste seus gatilhos e notificações de eventos DDL para determinar suas respostas aos procedimentos armazenados do sistema que são executados. Por exemplo, a instrução CREATE TYPE e o procedimento armazenado **sp_addtype** acionarão um gatilho DDL ou uma notificação de eventos que tenham sido criados em um evento CREATE_TYPE.  
  
## <a name="ddl-statements-that-have-server-or-database-scope"></a>Instruções DDL com escopo de servidor ou banco de dados  
 Os gatilhos DDL ou as notificações de eventos podem ser criados para serem acionados em resposta aos eventos a seguir, quando eles ocorrerem no banco de dados no qual o gatilho ou a notificação de eventos são criados ou em qualquer local na instância do servidor.  
  
:::row:::
    :::column:::
        CREATE_APPLICATION_ROLE (aplica-se à instrução CREATE APPLICATION ROLE e **sp_addapprole**. Se um novo esquema for criado, este evento também irá disparar um evento CREATE_SCHEMA.)
    :::column-end:::
    :::column:::
        ALTER_APPLICATION_ROLE (Aplica-se à instrução ALTER APPLICATION ROLE e a **sp_approlepassword**.)
    :::column-end:::
    :::column:::
        DROP_APPLICATION_ROLE (aplica-se à instrução DROP APPLICATION ROLE e **sp_dropapprole**.)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_ASSEMBLY
    :::column-end:::
    :::column:::
        ALTER_ASSEMBLY
    :::column-end:::
    :::column:::
        DROP_ASSEMBLY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_ASYMMETRIC_KEY
    :::column-end:::
    :::column:::
        ALTER_ASYMMETRIC_KEY
    :::column-end:::
    :::column:::
        DROP_ASYMMETRIC_KEY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ALTER_AUTHORIZATION
    :::column-end:::
    :::column:::
        ALTER_AUTHORIZATION_DATABASE (Aplica-se à instrução ALTER AUTHORIZATION, quando é especificado ON DATABASE e a **sp_changedbowner**.)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_BROKER_PRIORITY
    :::column-end:::
    :::column:::
        CREATE_BROKER_PRIORITY
    :::column-end:::
    :::column:::
        CREATE_BROKER_PRIORITY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_CERTIFICATE
    :::column-end:::
    :::column:::
        ALTER_CERTIFICATE
    :::column-end:::
    :::column:::
        DROP_CERTIFICATE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_CONTRACT
    :::column-end:::
    :::column:::
        DROP_CONTRACT
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_CREDENTIAL
    :::column-end:::
    :::column:::
        ALTER_CREDENTIAL
    :::column-end:::
    :::column:::
        DROP_CREDENTIAL
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        GRANT_DATABASE
    :::column-end:::
    :::column:::
        DENY_DATABASE
    :::column-end:::
    :::column:::
        REVOKE_DATABASE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_DATABASE_AUDIT_SPEFICIATION
    :::column-end:::
    :::column:::
        ALTER_DATABASE_AUDIT_SPEFICIATION
    :::column-end:::
    :::column:::
        DENY_DATABASE_AUDIT_SPEFICIATION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_DATABASE_ENCRYPTION_KEY
    :::column-end:::
    :::column:::
        ALTER_DATABASE_ENCRYPTION_KEY
    :::column-end:::
    :::column:::
        DROP_DATABASE_ENCRYPTION_KEY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_DEFAULT
    :::column-end:::
    :::column:::
        DROP_DEFAULT
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        BIND_DEFAULT (aplica-se a **sp_bindefault**.)
    :::column-end:::
    :::column:::
        UNBIND_DEFAULT (aplica-se a **sp_unbindefault**.)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_EVENT_NOTIFICATION
    :::column-end:::
    :::column:::
        DROP_EVENT_NOTIFICATION
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_EXTENDED_PROPERTY (aplica-se a **sp_addextendedproperty**.)
    :::column-end:::
    :::column:::
        ALTER_EXTENDED_PROPERTY (Aplica-se a **sp_updateextendedproperty**.)
    :::column-end:::
    :::column:::
        DROP_EXTENDED_PROPERTY (aplica-se a **sp_dropextendedproperty**.)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_FULLTEXT_CATALOG (aplica-se à instrução CREATE FULLTEXT CATALOG e **sp_fulltextcatalog** quando *create* é especificado.)
    :::column-end:::
    :::column:::
        ALTER_FULLTEXT_CATALOG (Aplica-se à instrução ALTER_FULLTEXT_CATALOG, a **sp_fulltextcatalog** , quando *start_incremental*, *start_full*, *Stop*ou *Rebuild* é especificado, e a **sp_fulltext_database** , quando *enable* é especificado.)
    :::column-end:::
    :::column:::
        DROP_FULLTEXT_CATALOG (aplica-se à instrução DROP FULLTEXT CATALOG e **sp_fulltextcatalog** , quando *drop* é especificado.)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_FULLTEXT_INDEX (aplica-se à instrução CREATE FULLTEXT INDEX e **sp_fulltexttable** , quando *create* é especificado.)
    :::column-end:::
    :::column:::
        ALTER_FULLTEXT_INDEX (Aplica-se à instrução ALTER_FULLTEXT_INDEX, a **sp_fulltextcatalog** quando *start_full*, *start_incremental*ou *stop* é especificado, e a **sp_fulltext_column**e **sp_fulltext_table** , quando qualquer ação que não seja *create* ou *drop* for especificada.)
    :::column-end:::
    :::column:::
        DROP_FULLTEXT_INDEX (aplica-se à instrução DROP FULLTEXT INDEX e **sp_fulltexttable** , quando *drop* é especificado.)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_FULLTEXT_STOPLIST
    :::column-end:::
    :::column:::
        ALTER_FULLTEXT_STOPLIST
    :::column-end:::
    :::column:::
        DROP_FULLTEXT_STOPLIST
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_FUNCTION
    :::column-end:::
    :::column:::
        ALTER_FUNCTION
    :::column-end:::
    :::column:::
        DROP_FUNCTION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_INDEX
    :::column-end:::
    :::column:::
        ALTER_INDEX (Aplica-se à instrução ALTER INDEX e a **sp_indexoption**.)
    :::column-end:::
    :::column:::
        DROP_INDEX
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_MASTER_KEY
    :::column-end:::
    :::column:::
        ALTER_MASTER_KEY
    :::column-end:::
    :::column:::
        DROP_MASTER_KEY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_MESSAGE_TYPE
    :::column-end:::
    :::column:::
        ALTER_MESSAGE_TYPE
    :::column-end:::
    :::column:::
        DROP_MESSAGE_TYPE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_PARTITION_FUNCTION
    :::column-end:::
    :::column:::
        ALTER_PARTITION_FUNCTION
    :::column-end:::
    :::column:::
        DROP_PARTITION_FUNCTION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_PARTITION_SCHEME
    :::column-end:::
    :::column:::
        ALTER_PARTITION_SCHEME
    :::column-end:::
    :::column:::
        DROP_PARTITION_SCHEME
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_PLAN_GUIDE (aplica-se a **sp_create_plan_guide**.)
    :::column-end:::
    :::column:::
        ALTER_PLAN_GUIDE (Aplica-se a **sp_control_plan_guide** quando ENABLE, ENABLE ALL, DISABLE ou DISABLE ALL é especificado.)
    :::column-end:::
    :::column:::
        DROP_PLAN_GUIDE (aplica-se a **sp_control_plan_guide** quando DROP ou DROP ALL é especificado.)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_PROCEDURE
    :::column-end:::
    :::column:::
        ALTER_PROCEDURE (Aplica-se à instrução ALTER PROCEDURE e a **sp_procoption**.)
    :::column-end:::
    :::column:::
        DROP_PROCEDURE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_QUEUE
    :::column-end:::
    :::column:::
        ALTER_QUEUE
    :::column-end:::
    :::column:::
        DROP_QUEUE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_REMOTE_SERVICE_BINDING
    :::column-end:::
    :::column:::
        ALTER_REMOTE_SERVICE_BINDING
    :::column-end:::
    :::column:::
        DROP_REMOTE_SERVICE_BINDING
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SPATIAL_INDEX
    :::column-end:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        RENAME (aplica-se a **sp_rename**)
    :::column-end:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_ROLE (aplica-se à instrução CREATE ROLE, **sp_addrole**e **sp_addgroup**.)
    :::column-end:::
    :::column:::
        ALTER_ROLE
    :::column-end:::
    :::column:::
        DROP_ROLE (aplica-se à instrução DROP ROLE, **sp_droprole**e **sp_dropgroup**.)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ADD_ROLE_MEMBER
    :::column-end:::
    :::column:::
        DROP_ROLE_MEMBER
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_ROUTE
    :::column-end:::
    :::column:::
        ALTER_ROUTE
    :::column-end:::
    :::column:::
        DROP_ROUTE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_RULE
    :::column-end:::
    :::column:::
        DROP_RULE
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        BIND_RULE (aplica-se a **sp_bindrule**.)
    :::column-end:::
    :::column:::
        UNBIND_RULE (aplica-se a **sp_unbindrule**.)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SCHEMA (aplica-se à instrução CREATE SCHEMA, **sp_addrole**, **sp_adduser**, **sp_addgroup**e **sp_grantdbaccess**.)
    :::column-end:::
    :::column:::
        ALTER_SCHEMA (Aplica-se à instrução ALTER SCHEMA e a **sp_changeobjectowner**.)
    :::column-end:::
    :::column:::
        DROP_SCHEMA
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SEARCH_PROPERTY_LIST
    :::column-end:::
    :::column:::
        ALTER_SEARCH_PROPERTY_LIST
    :::column-end:::
    :::column:::
        DROP_SEARCH_PROPERTY_LIST
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SEQUENCE_EVENTS
    :::column-end:::
    :::column:::
        CREATE_SEQUENCE_EVENTS
    :::column-end:::
    :::column:::
        CREATE_SEQUENCE_EVENTS
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SERVER_ROLE
    :::column-end:::
    :::column:::
        ALTER_SERVER_ROLE
    :::column-end:::
    :::column:::
        DROP_SERVER_ROLE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SERVICE
    :::column-end:::
    :::column:::
        ALTER_SERVICE
    :::column-end:::
    :::column:::
        DROP_SERVICE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ALTER_SERVICE_MASTER_KEY
    :::column-end:::
    :::column:::
        BACKUP_SERVICE_MASTER_KEY
    :::column-end:::
    :::column:::
        RESTORE_SERVICE_MASTER_KEY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ADD_SIGNATURE (para operações de assinatura em objetos de escopo sem esquema; banco de dados, assembly, gatilho)
    :::column-end:::
    :::column:::
        DROP_SIGNATURE
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ADD_SIGNATURE_SCHEMA_OBJECT (para objetos de escopo com esquema; procedimentos armazenados, funções)
    :::column-end:::
    :::column:::
        DROP_SIGNATURE_SCHEMA_OBJECT
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SPATIAL_INDEX
    :::column-end:::
    :::column:::
        ALTER_INDEX pode ser usado para índices espaciais.
    :::column-end:::
    :::column:::
        DROP_INDEX pode ser usado para índices de espaço.
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_STATISTICS
    :::column-end:::
    :::column:::
        DROP_STATISTICS
    :::column-end:::
    :::column:::
        UPDATE_STATISTICS
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SYMMETRIC_KEY
    :::column-end:::
    :::column:::
        ALTER_SYMMETRIC_KEY
    :::column-end:::
    :::column:::
        DROP_SYMMETRIC_KEY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SYNONYM
    :::column-end:::
    :::column:::
        DROP_SYNONYM
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_TABLE
    :::column-end:::
    :::column:::
        ALTER_TABLE (Aplica-se à instrução ALTER TABLE e a **sp_tableoption**.)
    :::column-end:::
    :::column:::
        DROP_TABLE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_TRIGGER
    :::column-end:::
    :::column:::
        ALTER_TRIGGER (Aplica-se à instrução ALTER TRIGGER e a **sp_settriggerorder**.)
    :::column-end:::
    :::column:::
        DROP_TRIGGER
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_TYPE (aplica-se à instrução CREATE TYPE e **sp_addtype**.)
    :::column-end:::
    :::column:::
        DROP_TYPE (aplica-se à instrução DROP TYPE e **sp_droptype**.)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_USER (aplica-se à instrução CREATE USER, **sp_adduser**e **sp_grantdbaccess**.)
    :::column-end:::
    :::column:::
        ALTER_USER (Aplica-se à instrução ALTER USER e a **sp_change_users_login**.)
    :::column-end:::
    :::column:::
        DROP_USER (aplica-se à instrução DROP USER, **sp_dropuser**e **sp_revokedbaccess**.)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_VIEW
    :::column-end:::
    :::column:::
        ALTER_VIEW
    :::column-end:::
    :::column:::
        DROP_VIEW
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_XML_INDEX
    :::column-end:::
    :::column:::
        ALTER_INDEX pode ser usado para índices XML.
    :::column-end:::
    :::column:::
        DROP_INDEX pode ser usado para índices XML.
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_XML_SCHEMA_COLLECTION
    :::column-end:::
    :::column:::
        ALTER_XML_SCHEMA_COLLECTION
    :::column-end:::
    :::column:::
        DROP_XML_SCHEMA_COLLECTION
    :::column-end:::
:::row-end:::
 
## <a name="ddl-statements-that-have-server-scope"></a>Instruções DDL com escopo de servidor  
 Gatilhos DDL ou notificações de eventos podem ser criados para serem acionados em resposta aos eventos a seguir, sempre que eles ocorrerem na instância do servidor.  
  
:::row:::
    :::column:::
        ALTER_AUTHORIZATION_SERVER
    :::column-end:::
    :::column:::
        ALTER_SERVER_CONFIGURATION
    :::column-end:::
    :::column:::
        ALTER_INSTANCE (Aplica-se a **sp_configure** e **sp_addserver** quando uma instância de servidor local é especificada.)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_AVAILABILITY_GROUP
    :::column-end:::
    :::column:::
        ALTER_AVAILABILITY_GROUP
    :::column-end:::
    :::column:::
        DROP_AVAILABILITY_GROUP
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_CREDENTIAL
    :::column-end:::
    :::column:::
        ALTER_CREDENTIAL
    :::column-end:::
    :::column:::
        DROP_CREDENTIAL
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_CRYPTOGRAPHIC_PROVIDER
    :::column-end:::
    :::column:::
        ALTER_CRYPTOGRAPHIC_PROVIDER
    :::column-end:::
    :::column:::
        DROP_CRYPTOGRAPHIC_PROVIDER
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_DATABASE
    :::column-end:::
    :::column:::
        ALTER_DATABASE (Aplica-se à instrução ALTER DATABASE e a **sp_fulltext_database**.)
    :::column-end:::
    :::column:::
        DROP_DATABASE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_ENDPOINT
    :::column-end:::
    :::column:::
        ALTER_ENDPOINT
    :::column-end:::
    :::column:::
        DROP_ENDPOINT
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_EVENT_SESSION
    :::column-end:::
    :::column:::
        ALTER_EVENT_SESSION
    :::column-end:::
    :::column:::
        DROP_EVENT_SESSION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_EXTENDED_PROCEDURE (aplica-se a **sp_addextendedproc**.)
    :::column-end:::
    :::column:::
        DROP_EXTENDED_PROCEDURE (aplica-se a **sp_dropextendedproc**.)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_LINKED_SERVER (aplica-se a **sp_addlinkedserver**.)
    :::column-end:::
    :::column:::
        ALTER_LINKED_SERVER (Aplica-se a **sp_serveroption**.)
    :::column-end:::
    :::column:::
        DROP_LINKED_SERVER (aplica-se a **sp_dropserver** quando um servidor vinculado é especificado.)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_LINKED_SERVER_LOGIN (aplica-se a **sp_addlinkedsrvlogin**.)
    :::column-end:::
    :::column:::
        DROP_LINKED_SERVER_LOGIN (aplica-se a **sp_droplinkedsrvlogin**.)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_LOGIN (aplica-se à instrução CREATE LOGIN, **sp_addlogin**, **sp_grantlogin**, **xp_grantlogin**e **sp_denylogin** quando usado em um logon não inexistente que deve ser criado implicitamente.)
    :::column-end:::
    :::column:::
        ALTER_LOGIN (Aplica-se à instrução ALTER LOGIN, **sp_defaultdb**, **sp_defaultlanguage**, **sp_password**e **sp_change_users_login** , quando *Auto_Fix* é especificado.)
    :::column-end:::
    :::column:::
        DROP_LOGIN (aplica-se à instrução DROP LOGIN, **sp_droplogin**, **sp_revokelogin**e **xp_revokelogin**.)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_MESSAGE (aplica-se a **sp_addmessage**.)
    :::column-end:::
    :::column:::
        ALTER_MESSAGE (Aplica-se a **sp_altermessage**.)
    :::column-end:::
    :::column:::
        DROP_MESSAGE (aplica-se a **sp_dropmessage**.)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_REMOTE_SERVER (aplica-se a **sp_addserver**.)
    :::column-end:::
    :::column:::
        ALTER_REMOTE_SERVER (Aplica-se a **sp_setnetname**.)
    :::column-end:::
    :::column:::
        DROP_REMOTE_SERVER (aplica-se a **sp_dropserver** quando um servidor remoto é especificado.)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_RESOURCE_POOL
    :::column-end:::
    :::column:::
        ALTER_RESOURCE_POOL
    :::column-end:::
    :::column:::
        DROP_RESOURCE_POOL
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        GRANT_SERVER
    :::column-end:::
    :::column:::
        DENY_SERVER
    :::column-end:::
    :::column:::
        REVOKE_SERVER
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ADD_SERVER_ROLE_MEMBER
    :::column-end:::
    :::column:::
        DROP_SERVER_ROLE_MEMBER
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SERVER_AUDIT
    :::column-end:::
    :::column:::
        ALTER_SERVER_AUDIT
    :::column-end:::
    :::column:::
        DROP_SERVER_AUDIT
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SERVER_AUDIT_SPECIFICATION
    :::column-end:::
    :::column:::
        ALTER_SERVER_AUDIT_SPECIFICATION
    :::column-end:::
    :::column:::
        DROP_SERVER_AUDIT_SPECIFICATION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_WORKLOAD_GROUP
    :::column-end:::
    :::column:::
        ALTER_WORKLOAD_GROUP
    :::column-end:::
    :::column:::
        DROP_WORKLOAD_GROUP
    :::column-end:::
:::row-end:::
 
## <a name="see-also"></a>Consulte Também  
 [Gatilhos DDL](../../relational-databases/triggers/ddl-triggers.md)   
 [Notificações de eventos](../../relational-databases/service-broker/event-notifications.md)   
 [Grupos de eventos DDL](../../relational-databases/triggers/ddl-event-groups.md)  
  
  
