---
title: Gerenciar a segurança dos gatilhos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- triggers [SQL Server], security
ms.assetid: e94720a8-a3a2-4364-b0a3-bbe86e3ce4d5
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: bcdc2af7f67c1ea4bda49e09cfe92eda43c9dea3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62524122"
---
# <a name="manage-trigger-security"></a>Gerenciar a segurança dos gatilhos
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
  
-   Lembre-se dos gatilhos DML e DDL que existem no banco de dados e na instância do servidor consultando as exibições de catálogo [sys.triggers](/sql/relational-databases/system-catalog-views/sys-triggers-transact-sql) e [sys.server_triggers](/sql/relational-databases/system-catalog-views/sys-server-triggers-transact-sql) . A consulta a seguir retorna todos os gatilhos DML e DDL no nível de banco de dados no banco de dados atual e todos os gatilhos DDL no nível de servidor na instância do servidor:  
  
    ```  
    SELECT type, name, parent_class_desc FROM sys.triggers  
    UNION  
    SELECT type, name, parent_class_desc FROM sys.server_triggers ;  
    ```  
  
-   Use [DISABLE TRIGGER](/sql/t-sql/statements/disable-trigger-transact-sql) para desabilitar os gatilhos que podem prejudicar a integridade do banco de dados ou do servidor caso sejam executados sob privilégios escalonados. A instrução a seguir desabilita todos os gatilhos DDL no nível do banco de dados no banco de dados atual:  
  
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
  
## <a name="see-also"></a>Consulte também  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)   
 [Gatilhos DML](../triggers/dml-triggers.md)   
 [Gatilhos DDL](../triggers/ddl-triggers.md)  
  
  
