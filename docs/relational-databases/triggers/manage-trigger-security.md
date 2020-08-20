---
description: Gerenciar a segurança dos gatilhos
title: Gerenciar a segurança dos gatilhos | Microsoft Docs
ms.custom: ''
ms.date: 06/22/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- triggers [SQL Server], security
ms.assetid: e94720a8-a3a2-4364-b0a3-bbe86e3ce4d5
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 73e56eb0ffcc4996ddd6903f2e79c14947b9a450
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485370"
---
# <a name="manage-trigger-security"></a>Gerenciar a segurança dos gatilhos

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Por padrão, os gatilhos DML e DDL executam sob o contexto do usuário que aciona o gatilho. O chamador do gatilho é o usuário que executa a instrução que faz com que o gatilho execute. Por exemplo, se o usuário **Marina** executar uma instrução DELETE que faz com que o gatilho DML **DML_trigMarina** seja executado, o código dentro do **DML_trigMarina** executará no contexto dos privilégios do usuário para **Marina**. Esse comportamento padrão pode ser explorado pelos usuários que desejam apresentar um código mal-intencionado no banco de dados ou na instância do servidor. Por exemplo, o seguinte gatilho DDL é criado pelo usuário **JohnDoe**:  

```sql
CREATE TRIGGER DDL_trigJohnDoe
ON DATABASE
FOR ALTER_TABLE
AS
SET NOCOUNT ON;

BEGIN TRY
  EXEC(N'
    USE [master];
    GRANT CONTROL SERVER TO [JohnDoe];
');
END TRY
BEGIN CATCH
  DECLARE @DoNothing INT;
END CATCH;
GO
```

O que esse gatilho significa é que assim que um usuário tiver a permissão para executar uma instrução `GRANT CONTROL SERVER`, como um membro da função de servidor fixa **sysadmin**, ele executará uma instrução `ALTER TABLE`, **JohnDoe** receberá a permissão `CONTROL SERVER`. Em outras palavras, embora **JohnDoe** não possa conceder permissão `CONTROL SERVER` para ele mesmo, ele habilitou o código do gatilho que lhe concede essa permissão para executar sob privilégios escalados. Os gatilhos DML e DDL estão abertos para este tipo de ameaça à segurança.  
  
## <a name="trigger-security-best-practices"></a>Práticas recomendadas para a segurança dos gatilhos  
 Você pode tomar as medidas a seguir para impedir que o código do gatilho execute sob privilégios escalados:  
  
::: moniker range=">=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current"

-   Lembre-se dos gatilhos DML e DDL que existem no banco de dados e na instância do servidor consultando as exibições de catálogo [sys.triggers](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md) e [sys.server_triggers](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md) . A consulta a seguir retorna todos os gatilhos DML e DDL no nível de banco de dados no banco de dados atual e todos os gatilhos DDL no nível de servidor na instância do servidor:  
  
    ```sql
    SELECT type, name, parent_class_desc FROM sys.triggers
    UNION ALL
    SELECT type, name, parent_class_desc FROM sys.server_triggers;
    ```  

   > [!NOTE]
   > Somente **sys.triggers** está disponível para [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], a menos que você esteja usando [!INCLUDE[ssSDSMIfull](../../includes/sssdsmifull-md.md)].

::: moniker-end

::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"

-   Lembre-se dos gatilhos DML e DDL que existem no banco de dados ao consultar a exibição de catálogo [sys.triggers](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md). A consulta a seguir retorna todos os gatilhos DML e DDL no nível do banco de dados para o banco de dados atual:  
  
    ```sql
    SELECT type, name, parent_class_desc FROM sys.triggers;
    ```  
  
::: moniker-end

-   Use [DISABLE TRIGGER](../../t-sql/statements/disable-trigger-transact-sql.md) para desabilitar os gatilhos que podem prejudicar a integridade do banco de dados ou do servidor caso sejam executados sob privilégios escalonados. A instrução a seguir desabilita todos os gatilhos DDL no nível do banco de dados no banco de dados atual:  
  
    ```sql
    DISABLE TRIGGER ALL ON DATABASE;
    ```  
  
     Essa instrução desabilita todos os gatilhos DDL no nível de servidor na instância do servidor:  
  
    ```sql
    DISABLE TRIGGER ALL ON ALL SERVER;
    ```  
  
     Essa instrução desabilita todos os gatilhos DML no banco de dados atual:  
  
    ```sql
    DECLARE @schema_name sysname, @trigger_name sysname, @object_name sysname;
    DECLARE @sql nvarchar(max);
    DECLARE trig_cur CURSOR FORWARD_ONLY READ_ONLY FOR
        SELECT SCHEMA_NAME(schema_id) AS schema_name,
            name AS trigger_name,
            OBJECT_NAME(parent_object_id) AS object_name
        FROM sys.objects WHERE type IN ('TR', 'TA');

    OPEN trig_cur;
    FETCH NEXT FROM trig_cur INTO @schema_name, @trigger_name, @object_name;
  
    WHILE @@FETCH_STATUS = 0
    BEGIN
        SELECT @sql = N'DISABLE TRIGGER ' + QUOTENAME(@schema_name) + N'.'
            + QUOTENAME(@trigger_name)
            + N' ON ' + QUOTENAME(@schema_name) + N'.'
            + QUOTENAME(@object_name) + N'; ';
        EXEC (@sql);
        FETCH NEXT FROM trig_cur INTO @schema_name, @trigger_name, @object_name;
    END;
    GO

    -- Verify triggers are disabled. Should return an empty result set.
    SELECT * FROM sys.triggers WHERE is_disabled = 0;
    GO

    CLOSE trig_cur;
    DEALLOCATE trig_cur;
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [Gatilhos DML](../../relational-databases/triggers/dml-triggers.md)   
 [Gatilhos DDL](../../relational-databases/triggers/ddl-triggers.md)  
 [Gatilhos de logon](../../relational-databases/triggers/logon-triggers.md)  
  
