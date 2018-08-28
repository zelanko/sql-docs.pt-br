---
title: Criar conjunto de coleta personalizado – Tipo de coletor de consultas T-SQL genérico | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- T-SQL Query collector type
- collection sets [SQL Server], creating custom
ms.assetid: 6b06db5b-cfdc-4ce0-addd-ec643460605b
caps.latest.revision: 26
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 774307434a3d005a64a64e69b3f7786c98ecbdc9
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40405750"
---
# <a name="create-custom-collection-set---generic-t-sql-query-collector-type"></a>Criar conjunto de coleta personalizado – Tipo de coletor de consultas T-SQL genérico
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  É possível criar um conjunto de coleta personalizado com itens de coleta que usam o tipo de coletor de Consultas T-SQL Genérico, usando os procedimentos armazenados fornecidos com o coletor de dados. A execução dessa tarefa envolve o uso do Editor de Consultas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para aplicar os seguintes procedimentos:  
  
-   Configurar as agendas de carregamento.  
  
-   Definir e criar o conjunto de coleta.  
  
-   Definir e criar um item de coleta.  
  
-   Verificar se o conjunto de coleta e os itens de coleta existem.  
  
> [!NOTE]  
>  Antes de criar um conjunto de coleta personalizado, configure os parâmetros da coleta de dados. Para obter mais informações, veja [Configurar parâmetros de coleta de dados &#40;Transact-SQL&#41;](../../relational-databases/data-collection/configure-data-collection-parameters-transact-sql.md).  
  
### <a name="define-and-create-the-collection-set"></a>Definir e criar o conjunto de coleta  
  
1.  Defina um novo conjunto de coleta usando o procedimento armazenado sp_syscollector_create_collection_set.  
  
    ```  
    USE msdb;  
    DECLARE @collection_set_id int;  
    DECLARE @collection_set_uid uniqueidentifier;  
    EXEC sp_syscollector_create_collection_set   
        @name=N'DMV Test 1',   
        @collection_mode=0,   
        @description=N'This is a test collection set',   
        @logging_level=1,   
        @days_until_expiration=14,   
        @schedule_name=N'CollectorSchedule_Every_15min',   
        @collection_set_id=@collection_set_id OUTPUT,   
        @collection_set_uid=@collection_set_uid OUTPUT;  
    SELECT @collection_set_id, @collection_set_uid;  
    ```  
  
     O modo de coleta pode ser definido como 0 (armazenado em cache) ou como 1 (não armazenado em cache).  
  
     O nível de log pode ser definido como 0, 1 ou 2.  
  
     As agendas pré-configuradas a seguir são fornecidas com o coletor de dados:  
  
    -   CollectorSchedule_Every_5min  
  
    -   CollectorSchedule_Every_10min  
  
    -   CollectorSchedule_Every_15min  
  
    -   CollectorSchedule_Every_30min  
  
    -   CollectorSchedule_Every_60min  
  
    -   CollectorSchedule_Every_6h  
  
     Se você não desejar usar uma das agendas fornecidas, poderá criar uma nova agenda e usá-la no conjunto de coleta. Para obter mais informações, veja [Criar e anexar agendamentos a trabalhos](../../ssms/agent/create-and-attach-schedules-to-jobs.md).  
  
### <a name="define-and-create-a-collection-item"></a>Definir e criar um item de coleta  
  
1.  Como o novo item de coleta é baseado em um tipo de coletor genérico já instalado, você pode executar o código a seguir para definir o GUID que corresponde ao tipo de coletor de Consultas T-SQL Genérico.  
  
    ```sql  
    DECLARE @collector_type_uid uniqueidentifier;  
    SELECT @collector_type_uid = collector_type_uid FROM [msdb].[dbo].[syscollector_collector_types]   
    WHERE name = N'Generic T-SQL Query Collector Type';  
    DECLARE @collection_item_id int;  
    ```  
  
2.  Use o procedimento armazenado sp_syscollector_create_collection_item para criar o item de coleta. Declare o esquema do item de coleta para que ele seja mapeado para o esquema exigido para o tipo de coletor de Consultas T-SQL Genérico.  
  
    ```sql  
    EXEC sp_syscollector_create_collection_item   
        @name=N'Query Stats - Test 1',   
        @parameters=N'  
            <ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
            <Query>  
            <Value>SELECT * FROM sys.dm_exec_query_stats</Value>  
            <OutputTable>dm_exec_query_stats</OutputTable>  
            </Query>  
            </ns:TSQLQueryCollector>',   
        @collection_item_id=@collection_item_id OUTPUT,   
        @frequency=5,   
        @collection_set_id=@collection_set_id,   
        @collector_type_uid=@collector_type_uid;  
    SELECT @collection_item_id;  
    ```  
  
### <a name="verify-that-the-new-collection-set-and-collection-item-exist"></a>Verificar se o novo conjunto de coleta e o item de coleta existem  
  
1.  Antes de iniciar o novo conjunto de coleta, execute a consulta a seguir para verificar se o novo conjunto de coleta e seu item de coleta foram criados.  
  
    ```sql  
    USE msdb;  
    SELECT * FROM syscollector_collection_sets;  
    SELECT * FROM syscollector_collection_items;  
    GO  
    ```  
  
     Você também pode fazer uma verificação visual no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. No Pesquisador de Objetos, expanda o nó **Gerenciamento** e expanda **Coleta de Dados**. O novo conjunto de coleta será exibido. O ícone de círculo vermelho do conjunto de coleta indica que o conjunto de coleta está parado.  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir combina os exemplos documentados nas etapas anteriores. Observe que a frequência da coleta definida para o item de coleta (5 segundos) é ignorada porque o modo de coleta do conjunto de coleta está definido como 0, que é um modo de armazenamento em cache. Para obter mais informações, consulte [Data Collection](../../relational-databases/data-collection/data-collection.md).  
  
```sql  
USE msdb;  
  
DECLARE @collection_set_id int;  
DECLARE @collection_set_uid uniqueidentifier  
  
EXEC dbo.sp_syscollector_create_collection_set  
    @name = N'DMV Stats Test 1',  
    @collection_mode = 0,  
    @description = N'This is a test collection set',  
    @logging_level=1,  
    @days_until_expiration = 14,  
    @schedule_name=N'CollectorSchedule_Every_15min',  
    @collection_set_id = @collection_set_id OUTPUT,  
    @collection_set_uid = @collection_set_uid OUTPUT;  
SELECT @collection_set_id,@collection_set_uid;  
  
DECLARE @collector_type_uid uniqueidentifier;  
SELECT @collector_type_uid = collector_type_uid FROM syscollector_collector_types   
WHERE name = N'Generic T-SQL Query Collector Type';  
  
DECLARE @collection_item_id int;  
EXEC sp_syscollector_create_collection_item  
@name= N'Query Stats - Test 1',  
@parameters=N'  
<ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
<Query>  
  <Value>select * from sys.dm_exec_query_stats</Value>  
  <OutputTable>dm_exec_query_stats</OutputTable>  
</Query>  
 </ns:TSQLQueryCollector>',  
    @collection_item_id = @collection_item_id OUTPUT,  
    @frequency = 5, -- This parameter is ignored in cached mode  
    @collection_set_id = @collection_set_id,  
    @collector_type_uid = @collector_type_uid;  
SELECT @collection_item_id;  
  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de coletor de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Gerenciar Agendas](../../ssms/agent/manage-schedules.md)   
 [Iniciar ou parar um conjunto de coleta](../../relational-databases/data-collection/start-or-stop-a-collection-set.md)  
  
  
