---
title: Adicionar um item da coleção a um conjunto de coleta (T-SQL)
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- collection items [SQL Server]
- collection sets [SQL Server], adding items
ms.assetid: 9fe6454e-8c0e-4b50-937b-d9871b20fd13
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8b6a17bf6732221787bda5e34d42b01046b3f828
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "74055586"
---
# <a name="add-a-collection-item-to-a-collection-set-transact-sql"></a>Adicionar um item de coleta a um conjunto de coletas (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Você pode adicionar um item de coleta a um conjunto de coleta existente usando os procedimentos armazenados fornecidos com o coletor de dados.  
  
 Complete os seguintes passos usando o Editor de Consultas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
### <a name="add-a-collection-item-to-a-collection-set"></a>Adicione um item de coleta a um conjunto de coleta  
  
1.  Interrompa o conjunto de coleta ao qual você deseja adicionar o item executando o procedimento armazenado **sp_syscollector_stop_collection_set** . Por exemplo, para parar um conjunto de coleta denominado "Conjunto de Coleta de Teste", execute as seguintes instruções:  
  
    ```sql  
    USE msdb  
    DECLARE @csid int  
    SELECT @csid = collection_set_id  
    FROM syscollector_collection_sets  
    WHERE name = 'Test Collection Set'  
    SELECT @csid  
    EXEC dbo.sp_syscollector_stop_collection_set @collection_set_id = @csid  
    ```  
  
    > [!NOTE]  
    >  Você também pode parar o conjunto de coleta usando o Pesquisador de Objetos no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações, veja [Iniciar ou interromper um conjunto de coleta](../../relational-databases/data-collection/start-or-stop-a-collection-set.md).  
  
2.  Declare o conjunto de coleta ao qual você deseja adicionar o item de coleta. O código a seguir fornece um exemplo de como declarar a ID do conjunto de coleta.  
  
    ```sql  
    DECLARE @collection_set_id_1 int  
    SELECT @collection_set_id_1 = collection_set_id FROM [msdb].[dbo].[syscollector_collection_sets]  
    WHERE name = N'Test Collection Set'; -- name of collection set  
    ```  
  
3.  Declare o tipo de coletor. O código a seguir fornece um exemplo de como declarar o tipo de coletor de Consultas T-SQL Genérico.  
  
    ```sql  
    DECLARE @collector_type_uid_1 uniqueidentifier  
    SELECT @collector_type_uid_1 = collector_type_uid FROM [msdb].[dbo].[syscollector_collector_types]   
       WHERE name = N'Generic T-SQL Query Collector Type';  
    ```  
  
     Execute o código a seguir para obter uma lista dos tipos de coletores instalados:  
  
    ```sql  
    USE msdb  
    SELECT * from syscollector_collector_types  
    GO  
    ```  
  
4.  Execute o procedimento armazenado **sp_syscollector_create_collection_item** para criar o item de coleta. Você deve declarar o esquema do item de coleta para que ele seja mapeado para o esquema necessário para o tipo de coletor desejado. O exemplo a seguir usa o esquema de entrada de Consultas T-SQL Genérico.  
  
    ```sql  
    DECLARE @collection_item_id int;  
    EXEC [msdb].[dbo].[sp_syscollector_create_collection_item]   
    @name=N'OS Wait Stats', --name of collection item  
    @parameters=N'  
    <ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
     <Query>  
      <Value>select * from sys.dm_os_wait_stats</Value>  
      <OutputTable>os_wait_stats</OutputTable>  
    </Query>  
    </ns:TSQLQueryCollector>',  
    @collection_item_id = @collection_item_id OUTPUT,  
    @frequency = 60,  
    @collection_set_id = @collection_set_id_1, --- Provides the collection set ID number  
    @collector_type_uid = @collector_type_uid_1 -- Provides the collector type UID  
    SELECT @collection_item_id     
    ```  
  
5.  Antes de iniciar o conjunto de coleta atualizado, execute a consulta a seguir para verificar se o novo item de coleta foi criado:  
  
    ```xaml  
    USE msdb  
    SELECT * from syscollector_collection_sets  
    SELECT * from syscollector_collection_items  
    GO  
    ```  
  
     Os conjuntos de coleta e seus itens de coleta são exibidos na guia **Resultados** .  
  
## <a name="see-also"></a>Consulte Também  
 [Criar um conjunto de coleta personalizado que usa o tipo de coletor de Consultas T-SQL genérico &#40;Transact-SQL&#41;](../../relational-databases/data-collection/create-custom-collection-set-generic-t-sql-query-collector-type.md)   
 [Procedimentos armazenados de coletor de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)  
  
  
