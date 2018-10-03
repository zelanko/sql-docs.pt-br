---
title: Gerenciar a segurança dos gatilhos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- triggers [SQL Server], security
ms.assetid: e94720a8-a3a2-4364-b0a3-bbe86e3ce4d5
author: rothja
ms.author: jroth
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1e400ada65efa69dd1b3e5ccc7dbdc21f67e3674
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47690784"
---
# <a name="manage-trigger-security"></a>Gerenciar a segurança dos gatilhos
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  Por padrão, os gatilhos DML e DDL executam sob o contexto do usuário que aciona o gatilho. O chamador do gatilho é o usuário que executa a instrução que faz com que o gatilho execute. Por exemplo, se o usuário **Marina** executar uma instrução DELETE que faz com que o gatilho DML **DML_trigMarina** seja executado, o código dentro do **DML_trigMarina** executará no contexto dos privilégios do usuário para **Marina**. Esse comportamento padrão pode ser explorado pelos usuários que desejam apresentar um código mal-intencionado no banco de dados ou na instância do servidor. Por exemplo, o gatilho DDL a seguir é criado pelo usuário `JohnDoe`:  
  
 `CREATE TRIGGER DDL_trigJohnDoe`  
  
 `ON DATABASE`  
  
 `FOR ALTER_TABLE`  
  
 `AS`  
  
 `GRANT CONTROL SERVER TO JohnDoe ;`  
  
 `GO`  
  
 O que esse gatilho significa é que assim que um usuário tiver a permissão para executar uma instrução `GRANT CONTROL SERVER` , como um membro da função de servidor fixa **sysadmin** , ele executa uma instrução `ALTER TABLE` , `JohnDoe` recebe permissão `CONTROL SERVER` . Em outras palavras, embora `JohnDoe` não possa conceder permissão `CONTROL SERVER` para ele mesmo, ele habilita o código do gatilho que lhe concede essa permissão para executar sob privilégios escalados. Os gatilhos DML e DDL estão abertos para este tipo de ameaça à segurança.  
  
## <a name="trigger-security-best-practices"></a>Práticas recomendadas para a segurança dos gatilhos  
 Você pode tomar as medidas a seguir para impedir que o código do gatilho execute sob privilégios escalados:  
  
-   Lembre-se dos gatilhos DML e DDL que existem no banco de dados e na instância do servidor consultando as exibições de catálogo [sys.triggers](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md) e [sys.server_triggers](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md) . A consulta a seguir retorna todos os gatilhos DML e DDL no nível de banco de dados no banco de dados atual e todos os gatilhos DDL no nível de servidor na instância do servidor:  
  
    ```  
    SELECT type, name, parent_class_desc FROM sys.triggers  
    UNION  
    SELECT type, name, parent_class_desc FROM sys.server_triggers ;  
    ```  
  
-   Use [DISABLE TRIGGER](../../t-sql/statements/disable-trigger-transact-sql.md) para desabilitar os gatilhos que podem prejudicar a integridade do banco de dados ou do servidor caso sejam executados sob privilégios escalonados. A instrução a seguir desabilita todos os gatilhos DDL no nível do banco de dados no banco de dados atual:  
  
    ```  
    DISABLE TRIGGER ALL ON DATABASE  
    ```  
  
     Essa instrução desabilita todos os gatilhos DDL no nível de servidor na instância do servidor:  
  
    ```  
    DISABLE TRIGGER ALL ON ALL SERVER  
    ```  
  
     Essa instrução desabilita todos os gatilhos DML no banco de dados atual:  
  
    ```  
    DECLARE @schema_name sysname, @trigger_name sysname, @object_name sysname ;  
    DECLARE @sql nvarchar(max) ;  
    DECLARE trig_cur CURSOR FORWARD_ONLY READ_ONLY FOR  
        SELECT SCHEMA_NAME(schema_id) AS schema_name,  
            name AS trigger_name,  
            OBJECT_NAME(parent_object_id) as object_name  
        FROM sys.objects WHERE type in ('TR', 'TA') ;  
  
    OPEN trig_cur ;  
    FETCH NEXT FROM trig_cur INTO @schema_name, @trigger_name, @object_name ;  
  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
        SELECT @sql = 'DISABLE TRIGGER ' + QUOTENAME(@schema_name) + '.'  
            + QUOTENAME(@trigger_name) +  
            ' ON ' + QUOTENAME(@schema_name) + '.'   
            + QUOTENAME(@object_name) + ' ; ' ;  
        EXEC (@sql) ;  
        FETCH NEXT FROM trig_cur INTO @schema_name, @trigger_name, @object_name ;  
    END  
    GO  
  
    -- Verify triggers are disabled. Should return an empty result set.  
    SELECT * FROM sys.triggers WHERE is_disabled = 0 ;  
    GO  
  
    CLOSE trig_cur ;  
    DEALLOCATE trig_cur;  
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [Gatilhos DML](../../relational-databases/triggers/dml-triggers.md)   
 [Gatilhos DDL](../../relational-databases/triggers/ddl-triggers.md)  
  
  
