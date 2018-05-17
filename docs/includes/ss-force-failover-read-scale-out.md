---
title: Failover forçado do SQL Server para o grupo de disponibilidade
description: Force o failover para o grupo de disponibilidade com o tipo de cluster de NONE
services: ''
author: MikeRayMSFT
ms.topic: include
ms.date: 02/05/2018
ms.author: mikeray
ms.custom: include file
ms.openlocfilehash: f5655e73481d830c848aea34c4a4f49613be0913
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
Cada grupo de disponibilidade tem apenas uma réplica primária. A réplica primária permite leituras e gravações. Para alterar qual réplica é a primária, faça failover. Em um grupo de disponibilidade para alta disponibilidade, o gerenciador de cluster automatiza o processo de failover. Em um grupo de disponibilidade com o tipo de cluster NONE, o processo de failover é manual. 

Há duas maneiras de fazer failover da réplica primária em um grupo de disponibilidade com o tipo de cluster NONE:

- Failover manual forçado com perda de dados
- Failover manual sem perda de dados

### <a name="forced-manual-failover-with-data-loss"></a>Failover manual forçado com perda de dados

Use esse método quando a réplica primária não estiver disponível e não puder ser recuperada. 

Para forçar o failover com perda de dados, conecte-se à instância do SQL Server que hospeda a réplica secundária de destino e execute:

```SQL
ALTER AVAILABILITY GROUP [ag1] FORCE_FAILOVER_ALLOW_DATA_LOSS;
```

### <a name="manual-failover-without-data-loss"></a>Failover manual sem perda de dados

Use esse método quando a réplica primária estiver disponível, mas você precisar alterar a configuração temporária ou permanentemente e alterar a instância do SQL Server que hospeda a réplica primária. Antes de emitir o failover manual, certifique-se de que a réplica secundária de destino está atualizada para evitar perda de dados potencial. 

Para fazer failover manualmente sem perda de dados:

1. Crie a réplica secundária de destino `SYNCHRONOUS_COMMIT`.

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        MODIFY REPLICA ON N'<node2>' 
        WITH (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);
   ```

2. Execute a consulta a seguir para identificar que as transações ativas foram confirmadas na réplica primária e em, pelo menos, uma réplica secundária síncrona: 

   ```SQL
   SELECT ag.name, 
      drs.database_id, 
      drs.group_id, 
      drs.replica_id, 
      drs.synchronization_state_desc, 
      ag.sequence_number
   FROM sys.dm_hadr_database_replica_states drs, sys.availability_groups ag
   WHERE drs.group_id = ag.group_id; 
   ```

   A réplica secundária é sincronizada quando `synchronization_state_desc` é `SYNCHRONIZED`.

3. Atualize `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` para 1.

   O script a seguir define `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` como 1 em um grupo de disponibilidade chamado `ag1`. Antes de executar o script a seguir, substitua `ag1` pelo nome do seu grupo de disponibilidade:

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        SET REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT = 1;
   ```

   Essa configuração garante que todas as transações ativas são confirmadas na réplica primária e em, pelo menos, uma réplica secundária síncrona. 

4. Rebaixe a réplica primária para uma réplica secundária. Depois que a réplica primária for rebaixada, ela será somente leitura. Execute este comando na instância do SQL Server que hospeda a réplica primária para atualizar a função para `SECONDARY`:

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        SET (ROLE = SECONDARY); 
   ```

5. Promova a réplica secundária de destino para a primária. 

   ```SQL
   ALTER AVAILABILITY GROUP ag1 FORCE_FAILOVER_ALLOW_DATA_LOSS; 
   ```  

   > [!NOTE] 
   > Para excluir um grupo de disponibilidade, use [DROP AVAILABILITY GROUP](https://docs.microsoft.com/en-us/sql/t-sql/statements/drop-availability-group-transact-sql). Para um grupo de disponibilidade criado com o tipo de cluster NONE ou EXTERNAL, o comando deverá ser executado em todas as réplicas que fazem parte do grupo de disponibilidade.