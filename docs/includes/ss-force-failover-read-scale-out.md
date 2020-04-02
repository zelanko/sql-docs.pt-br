---
title: Failover forçado do SQL Server para grupos de disponibilidade
description: Force o failover para grupos de disponibilidade com o tipo de cluster NONE
services: ''
author: MikeRayMSFT
ms.topic: include
ms.date: 02/05/2018
ms.author: mikeray
ms.custom: include file
ms.openlocfilehash: 90c7c7863228ce210e56e76ab3e12c77e7ccc902
ms.sourcegitcommit: fc5b757bb27048a71bb39755648d5cefe25a8bc6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "80408011"
---
Cada grupo de disponibilidade tem apenas uma réplica primária. A réplica primária permite leituras e gravações. Para alterar qual réplica é a primária, faça failover. Em um grupo de disponibilidade para alta disponibilidade, o gerenciador de cluster automatiza o processo de failover. Em um grupo de disponibilidade com o tipo de cluster NONE, o processo de failover é manual. 

Há duas maneiras de fazer failover da réplica primária em um grupo de disponibilidade com o tipo de cluster NONE:

- Failover manual forçado com perda de dados
- Failover manual sem perda de dados

### <a name="forced-manual-failover-with-data-loss"></a>Failover manual forçado com perda de dados

Use esse método quando a réplica primária não estiver disponível e não puder ser recuperada. 

Para forçar o failover com perda de dados, conecte-se à instância do SQL Server que hospeda a réplica secundária de destino e execute o comando a seguir:

```SQL
ALTER AVAILABILITY GROUP [ag1] FORCE_FAILOVER_ALLOW_DATA_LOSS;
```

Quando a réplica primária anterior for recuperada, ela também assumirá a função primária. Para garantir que a réplica primária anterior faça a transição para uma função secundária, execute o comando a seguir na réplica primária anterior.

```SQL
ALTER AVAILABILITY GROUP [ag1]  SET (ROLE = SECONDARY);
```

### <a name="manual-failover-without-data-loss"></a>Failover manual sem perda de dados

Use esse método quando a réplica primária estiver disponível, mas você precisar alterar a configuração temporária ou permanentemente e alterar a instância do SQL Server que hospeda a réplica primária. Para evitar a perda potencial de dados, antes de emitir o failover manual, verifique se a réplica secundária de destino está atualizada. 

Para fazer failover manualmente sem perda de dados:

1. Crie a réplica secundária de destino `SYNCHRONOUS_COMMIT`.

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        MODIFY REPLICA ON N'<node2>' 
        WITH (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);
   ```

2. Para identificar que as transações ativas foram confirmadas na réplica primária e em pelo menos uma réplica secundária síncrona, execute a consulta a seguir: 

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
        SET (REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT = 1);
   ```

   Essa configuração garante que todas as transações ativas são confirmadas na réplica primária e em, pelo menos, uma réplica secundária síncrona. 
   >[!NOTE]
   >Essa configuração não é específica do failover e deve ser definida com base nos requisitos do ambiente.
   
4. Coloque a réplica primária offline em preparação para as alterações de função.
   ```SQL
   ALTER AVAILABILITY GROUP [ag1] OFFLINE
   ```

5. Promova a réplica secundária de destino para a primária. 

   ```SQL
   ALTER AVAILABILITY GROUP ag1 FORCE_FAILOVER_ALLOW_DATA_LOSS; 
   ``` 

6. Atualize a função da antiga primária para `SECONDARY`, execute o seguinte comando na instância do SQL Server que hospeda a réplica primária:

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        SET (ROLE = SECONDARY); 
   ```

   > [!NOTE] 
   > Para excluir um grupo de disponibilidade, use [DROP AVAILABILITY GROUP](https://docs.microsoft.com/sql/t-sql/statements/drop-availability-group-transact-sql). Para um grupo de disponibilidade criado com o tipo de cluster NONE ou EXTERNAL, execute o comando em todas as réplicas que fazem parte do grupo de disponibilidade.
