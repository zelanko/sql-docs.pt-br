Cada grupo de disponibilidade tem apenas uma réplica primária. A réplica primária permite leituras e gravações. Para alterar qual réplica é primária, você pode fazer failover. Em um grupo de disponibilidade para alta disponibilidade, o gerenciador de cluster automatiza o processo de failover. Em um grupo de disponibilidade de escala de leitura, o processo de failover é manual. 

Há duas maneiras de fazer failover a réplica primária em um grupo de disponibilidade de escala de leitura:

- Failover manual forçado com perda de dados
- Failover manual sem perda de dados

### <a name="forced-manual-failover-with-data-loss"></a>Failover manual forçado com perda de dados

Use este método quando a réplica primária não está disponível e não pode ser recuperada. 

Para forçar o failover com perda de dados, conecte-se à instância do SQL Server que hospeda a réplica secundária de destino e execute:

```SQL
ALTER AVAILABILITY GROUP [ag1] FORCE_FAILOVER_ALLOW_DATA_LOSS;
```

### <a name="manual-failover-without-data-loss"></a>Failover manual sem perda de dados

Use esse método quando a réplica primária estiver disponível, mas você precisar alterar a configuração temporária ou permanentemente e alterar a instância do SQL Server que hospeda a réplica primária. Antes de emitir o failover manual, certifique-se de que a réplica secundária de destino é atualizada para evitar a perda de dados. 

Para failover manual sem perda de dados:

1. Tornar a réplica secundária de destino `SYNCHRONOUS_COMMIT`.

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        MODIFY REPLICA ON N'**<node2>*' 
        WITH (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);
   ```

2. Execute a consulta a seguir para identificar o que as transações ativas são confirmadas para a réplica primária e pelo menos uma réplica secundária síncrona: 

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

3. Atualização `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` como 1.

   O script a seguir define `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` como 1 em um grupo de disponibilidade denominado `ag1`. Antes de executar o script a seguir, substitua `ag1` com o nome do seu grupo de disponibilidade:

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        SET REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT = 1;
   ```

   Essa configuração garante que todas as transações ativas é confirmada para a réplica primária e pelo menos uma réplica secundária síncrona. 

4. Rebaixe a réplica primária para uma réplica secundária. Depois que a réplica primária é rebaixada, ele é somente leitura. Execute este comando na instância do SQL Server que hospeda a réplica primária para atualizar a função `SECONDARY`:

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        SET (ROLE = SECONDARY); 
   ```

5. Promova a réplica secundária de destino para a primária. 

   ```SQL
   ALTER AVAILABILITY GROUP ag1 FORCE_FAILOVER_ALLOW_DATA_LOSS; 
   ```  

   > [!NOTE] 
   > Para excluir um grupo de disponibilidade, use [DROP AVAILABILITY GROUP](https://docs.microsoft.com/en-us/sql/t-sql/statements/drop-availability-group-transact-sql). Para um grupo de disponibilidade criado com CLUSTER_TYPE NONE ou externo, o comando deve ser executado em todas as réplicas que fazem parte do grupo de disponibilidade.