---
title: Criar e testar uma função de classificador definida pelo usuário | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, classifier function create
- classifier function [SQL Server], test
- classifier function [SQL Server], create
- Resource Governor, classifier function test
ms.assetid: 7866b3c9-385b-40c6-aca5-32d3337032be
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5118ebcb3da31b97859ca0b2b38e3ad552604990
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68212007"
---
# <a name="create-and-test-a-classifier-user-defined-function"></a>Criar e testar uma função de classificação definida pelo usuário
  Este tópico mostra como criar e testar uma função de classificador definida pelo usuário (UDF). As etapas envolvem a execução das instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] no Editor de Consultas [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
 O exemplo mostrado no procedimento a seguir ilustra as possibilidades para criar uma função de classificador definida pelo usuário bastante complexa.  
  
 Em nosso exemplo:  
  
-   São criados um pool de recurso (pProductionProcessing) e grupo de carga de trabalho (gProductionProcessing) para processamento da produção durante um intervalo de hora especificado.  
  
-   Um pool de recursos (pOffHoursProcessing) e um grupo de carga de trabalho (gOffHoursProcessing) são criado para controlar as conexões que não atendem aos requisitos para processamento de produção.  
  
-   Uma tabela (TblClassificationTimeTable) é criada em mestre para manter as horas de início e término que podem ser avaliadas em relação à hora de logon. Isso deve ser criado em mestre porque o Governador de Recurso usa uma associação de esquema para funções de classificador.  
  
    > [!NOTE]  
    >  Como uma prática recomendada, você não deve armazenar tabelas grandes, frequentemente atualizadas em mestre.  
  
 A função de classificador estende a hora de logon. Uma função complexa pode fazer com que os logons alcancem o tempo limite ou reduzam a velocidade das conexões rápidas.  
  
### <a name="to-create-the-classifier-user-defined-function"></a>Para criar a função de classificador definida pelo usuário  
  
1.  Crie e configure os novos pools de recurso e os grupos de carga de trabalho. Atribua cada grupo de carga de trabalho ao pool de recurso apropriado.  
  
    ```  
    --- Create a resource pool for production processing  
    --- and set limits.  
    USE master  
    GO  
    CREATE RESOURCE POOL pProductionProcessing  
    WITH  
    (  
         MAX_CPU_PERCENT = 100,  
         MIN_CPU_PERCENT = 50  
    )  
    GO  
    --- Create a workload group for production processing  
    --- and configure the relative importance.  
    CREATE WORKLOAD GROUP gProductionProcessing  
    WITH  
    (  
         IMPORTANCE = MEDIUM  
    )  
    --- Assign the workload group to the production processing  
    --- resource pool.  
    USING pProductionProcessing  
    GO  
    --- Create a resource pool for off-hours processing  
    --- and set limits.  
  
    CREATE RESOURCE POOL pOffHoursProcessing  
    WITH  
    (  
         MAX_CPU_PERCENT = 50,  
         MIN_CPU_PERCENT = 0  
    )  
    GO  
    --- Create a workload group for off-hours processing  
    --- and configure the relative importance.  
    CREATE WORKLOAD GROUP gOffHoursProcessing  
    WITH  
    (  
         IMPORTANCE = LOW  
    )  
    --- Assign the workload group to the off-hours processing  
    --- resource pool.  
    USING pOffHoursProcessing  
    GO  
    ```  
  
2.  Atualize a configuração em-memória.  
  
    ```  
    ALTER RESOURCE GOVERNOR RECONFIGURE  
    GO  
    ```  
  
3.  Crie uma tabela e defina as horas de início e término para o intervalo de hora de processamento de produção.  
  
    ```  
    USE master  
    GO  
    CREATE TABLE tblClassificationTimeTable  
    (  
         strGroupName     sysname          not null,  
         tStartTime       time              not null,  
         tEndTime         time              not null  
    )  
    GO  
    --- Add time values that the classifier will use to  
    --- determine the workload group for a session.  
    INSERT into tblClassificationTimeTable VALUES('gProductionProcessing', '6:35 AM', '6:15 PM')  
    go  
    ```  
  
4.  Crie a função de classificador que usa as funções e os valores de hora que podem ser avaliados em relação aos tempos na tabela de consulta. Para obter informações sobre como usar Tabelas de pesquisa em uma função de classificador, confira "Práticas recomendadas para usar Tabelas de pesquisa em uma função de classificador", neste tópico.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] introduziu um conjunto expandido de tipos e funções de dados de data e hora. Para obter mais informações, veja [Tipos de dados e funções de data e hora &#40;Transact-SQL&#41;](/sql/t-sql/functions/date-and-time-data-types-and-functions-transact-sql).  
  
    ```  
    CREATE FUNCTION fnTimeClassifier()  
    RETURNS sysname  
    WITH SCHEMABINDING  
    AS  
    BEGIN  
         DECLARE @strGroup sysname  
         DECLARE @loginTime time  
         SET @loginTime = CONVERT(time,GETDATE())  
         SELECT TOP 1 @strGroup = strGroupName  
              FROM dbo.tblClassificationTimeTable  
              WHERE tStartTime <= @loginTime and tEndTime >= @loginTime  
         IF(@strGroup is not null)  
         BEGIN  
              RETURN @strGroup  
         END  
    --- Use the default workload group if there is no match  
    --- on the lookup.  
         RETURN N'gOffHoursProcessing'  
    END  
    GO  
    ```  
  
5.  Registre a função de classificador e atualize a configuração em-memória.  
  
    ```  
    ALTER RESOURCE GOVERNOR with (CLASSIFIER_FUNCTION = dbo.fnTimeClassifier)  
    ALTER RESOURCE GOVERNOR RECONFIGURE  
    GO  
    ```  
  
### <a name="to-verify-the-resource-pools-workload-groups-and-the-classifier-user-defined-function"></a>Para verificar os pools de recursos, os grupos de carga de trabalho e a função de classificador definida pelo usuário  
  
1.  Obtenha o pool de recurso e configuração do grupo de carga de trabalho usando a seguinte consulta.  
  
    ```  
    USE master  
    SELECT * FROM sys.resource_governor_resource_pools  
    SELECT * FROM sys.resource_governor_workload_groups  
    GO  
    ```  
  
2.  Verifique se a função de classificador existe e está habilitadas usando as consultas a seguir.  
  
    ```  
    --- Get the classifier function Id and state (enabled).  
    SELECT * FROM sys.resource_governor_configuration  
    GO  
    --- Get the classifer function name and the name of the schema  
    --- that it is bound to.  
    SELECT   
          object_schema_name(classifier_function_id) AS [schema_name],  
          object_name(classifier_function_id) AS [function_name]  
    FROM sys.dm_resource_governor_configuration  
  
    ```  
  
3.  Obtenha os dados de runtime atuais para os pools de recurso e os grupos de carga de trabalho usando a seguinte consulta.  
  
    ```  
    SELECT * FROM sys.dm_resource_governor_resource_pools  
    SELECT * FROM sys.dm_resource_governor_workload_groups  
    GO  
    ```  
  
4.  Descubra que sessões estão em cada grupo usando a seguinte consulta.  
  
    ```  
    SELECT s.group_id, CAST(g.name as nvarchar(20)), s.session_id, s.login_time, CAST(s.host_name as nvarchar(20)), CAST(s.program_name AS nvarchar(20))  
              FROM sys.dm_exec_sessions s  
         INNER JOIN sys.dm_resource_governor_workload_groups g  
              ON g.group_id = s.group_id  
    ORDER BY g.name  
    GO  
    ```  
  
5.  Descubra quais solicitações estão em cada grupo usando a seguinte consulta.  
  
    ```  
    SELECT r.group_id, g.name, r.status, r.session_id, r.request_id, r.start_time, r.command, r.sql_handle, t.text   
               FROM sys.dm_exec_requests r  
         INNER JOIN sys.dm_resource_governor_workload_groups g  
                ON g.group_id = r.group_id  
         CROSS APPLY sys.dm_exec_sql_text(r.sql_handle) AS t  
    ORDER BY g.name  
    GO  
    ```  
  
6.  Descubra que solicitações estão em execução no classificador usando a seguinte consulta.  
  
    ```  
    SELECT s.group_id, g.name, s.session_id, s.login_time, s.host_name, s.program_name   
               FROM sys.dm_exec_sessions s  
         INNER JOIN sys.dm_resource_governor_workload_groups g  
               ON g.group_id = s.group_id  
                     AND 'preconnect' = s.status  
    ORDER BY g.name  
    GO  
  
    SELECT r.group_id, g.name, r.status, r.session_id, r.request_id, r.start_time, r.command, r.sql_handle, t.text   
               FROM sys.dm_exec_requests r  
         INNER JOIN sys.dm_resource_governor_workload_groups g  
               ON g.group_id = r.group_id  
                     AND 'preconnect' = r.status  
         CROSS APPLY sys.dm_exec_sql_text(r.sql_handle) AS t  
    ORDER BY g.name  
    GO  
    ```  
  
### <a name="best-practices-for-using-lookup-tables-in-a-classifier-function"></a>Práticas recomendadas para usar Tabelas de Pesquisa em uma função de classificação  
  
1.  Não use uma tabela de pesquisa, a menos que seja absolutamente necessário. Se precisar usar uma tabela de pesquisa, ela poderá ser embutida em código na própria função. No entanto, ela precisará ser equilibrada com as alterações dinâmicas e de complexidade da função de classificação.  
  
2.  Limite a E/S executada para tabelas de pesquisa.  
  
    1.  Use o TOP 1 para retornar apenas uma linha.  
  
    2.  Minimize o número de linhas na tabela.  
  
    3.  Faça com que todas as linhas da tabela fiquem em uma única página ou em um número pequeno de páginas.  
  
    4.  Verifique se as linhas encontradas usando as operações Index Seek usam o maior número possível de colunas de busca.  
  
    5.  Desnormalize para uma única tabela se estiver pensando em usar várias tabelas com junções.  
  
3.  Evite o bloqueio na tabela de pesquisa.  
  
    1.  Use a dica `NOLOCK` para evitar o bloqueio ou use `SET LOCK_TIMEOUT` na função com um valor máximo de 1000 milissegundos.  
  
    2.  As tabelas devem estar no banco de dados mestre. (O banco de dados mestre é o único que tem a garantia de ser recuperado quando os computadores cliente tentam se conectar.)  
  
    3.  Sempre qualifique por completo o nome da tabela com o esquema. O nome do banco de dados não é necessário, uma vez que ele será o banco de dados mestre.  
  
    4.  Nenhum gatilho na tabela.  
  
    5.  Se você estiver atualizando o conteúdo da tabela, use uma transação no nível de isolamento do instantâneo para impedir que o Gravador bloqueie os Leitores. Observe que o uso da dica `NOLOCK` também deve reduzir isso.  
  
    6.  Se possível, desabilite a função de classificação ao alterar o conteúdo de tabela.  
  
        > [!WARNING]  
        >  É altamente recomendável seguir essas práticas recomendadas. Se houver problemas que o impeçam de seguir as práticas recomendadas, sugerimos que você contate o Suporte da Microsoft para evitar proativamente qualquer problema futuro.  
  
## <a name="see-also"></a>Consulte Também  
 [Administrador de Recursos](resource-governor.md)   
 [Habilitar Administrador de Recursos](enable-resource-governor.md)   
 [Pool de recursos do Administrador de Recursos](resource-governor-resource-pool.md)   
 [Grupos de carga de trabalho do Administrador de Recursos](resource-governor-workload-group.md)   
 [Configurar o administrador de recursos usando um modelo](configure-resource-governor-using-a-template.md)   
 [Exibir Propriedades do Administrador de Recursos](view-resource-governor-properties.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-resource-pool-transact-sql)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-workload-group-transact-sql)   
 [CREATE FUNCTION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-function-transact-sql)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
