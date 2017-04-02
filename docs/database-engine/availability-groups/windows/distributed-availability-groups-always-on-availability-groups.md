---
title: "Grupos de Disponibilidade Distribu&#237;da (Grupos de Disponibilidade AlwaysOn) | Microsoft Docs"
ms.custom: ""
ms.date: "08/30/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f7c7acc5-a350-4a17-95e1-e689c78a0900
caps.latest.revision: 28
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 28
---
# Grupos de Disponibilidade Distribu&#237;da (Grupos de Disponibilidade AlwaysOn)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Grupos de Disponibilidade Distribuída permitem associar dois grupos de disponibilidade que residem em diferentes Clusters de Failover do Windows Server (WSFC). Um dos principais usos dos Grupos de Disponibilidade Distribuída é a recuperação de desastres nos quais o local primário é geograficamente distante do local de recuperação de desastres. Os dados devem ser replicados continuamente no local de DR, mas é necessário evitar possíveis problemas de rede ou no local de DR que possam desativar o local primário.  
  
 O diagrama a seguir ilustra a arquitetura de um grupo de disponibilidade distribuída.  
  
 ![AlwaysOn Distributed Availability Groups](../../../database-engine/availability-groups/windows/media/alwayson-distributed-availability-groups.png "AlwaysOn Distributed Availability Groups")  
  
 No diagrama anterior, há dois Clusters de Failover do Windows Server (WFSC 1 e WFSC 2) separados. Cada cluster tem seu próprio grupo de disponibilidade com configuração de bancos de dados correspondentes. Um grupo de disponibilidade distribuída pode ser considerado um "grupo de disponibilidade de grupos de disponibilidade". O AG 1 se torna o grupo de disponibilidade primário neste exemplo. Inserções e atualizações são feitas para a réplica primária, AG 1, e, depois, para as réplicas secundárias. No entanto, as alterações também são replicadas uma vez pela rede para o grupo de disponibilidade secundário no WSFC 2. O grupo de disponibilidade AG 2 replica essas alterações em suas réplicas secundárias.  
  
> [!IMPORTANT]  
>  Quando é estabelecida uma relação de grupo de disponibilidade distribuída entre dois grupos de disponibilidade, o grupo de disponibilidade secundário automaticamente se torna somente leitura. Atualizações e inserções só podem ser feitas para a réplica primária do grupo de disponibilidade primário (no exemplo, a réplica primária do AG 1).  
  
 Grupos de Disponibilidade Distribuída diferem de um grupo de disponibilidade em um único Cluster de Failover do Windows Server das seguintes maneiras:  
  
-   Cada WSFC mantém seu próprio modo de quorum e configuração de votação de nó. Isso significa que a integridade do WSFC secundário não afeta o WSFC primário.  
  
-   Os dados são enviados uma vez pela rede para o WSFC secundário e replicados dentro do próprio cluster. Em um único WSFC, os dados são enviados individualmente para cada réplica. Para um local secundário geograficamente disperso, grupos de disponibilidade distribuída são mais eficientes.  
  
-   A versão do sistema operacional usada nos clusters primários e secundários pode ser diferente. Em um único WSFC, todos os servidores devem ter a mesma versão do sistema operacional. Isso possibilita usar Grupos de Disponibilidade Distribuída com atualizações sem interrupção/atualizações do sistema operacional.  
  
-   Os grupos de disponibilidade primário e secundário devem ter a mesma configuração de bancos de dados.  
  
-   Não há suporte para failover automático para o grupo de disponibilidade secundário.  
  
## Criar um grupo de disponibilidade distribuída  
 Para criar um grupo de disponibilidade distribuída, você deve criar um grupo de disponibilidade e um ouvinte em cada WSFC. Em seguida, você os combina em um grupo de disponibilidade distribuída. As etapas a seguir fornecem um exemplo básico em Transact-SQL. Este exemplo não abrange todos os detalhes da criação de grupos de disponibilidade e ouvintes, focando apenas nos requisitos básicos.  
  
### Criar o grupo de disponibilidade primário no primeiro cluster  
 Crie um grupo de disponibilidade primário no primeiro WSFC.   Neste exemplo, o grupo de disponibilidade é denominado `ag1` para o banco de dados `db1`.  
  
```tsql  
CREATE AVAILABILITY GROUP [ag1]   
FOR DATABASE db1   
REPLICA ON N'server1' WITH (ENDPOINT_URL = N'TCP://server1.contoso.com:5022',  
    FAILOVER_MODE = AUTOMATIC,  
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC),   
N'server2' WITH (ENDPOINT_URL = N'TCP://server2.contoso.com:5022',   
    FAILOVER_MODE = AUTOMATIC,   
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC);   
GO  
  
```  
  
 Observe que o exemplo usa a propagação direta, em que **SEEDING_MODE** é definido como **AUTOMATIC** para as réplicas e o grupo de disponibilidade distribuído. Isso significa que, uma vez estabelecidos, as réplicas secundárias e o grupo de disponibilidade secundário serão preenchidos automaticamente sem a necessidade de backup e restauração manual do banco de dados primário.  
  
### Unir as réplicas secundárias ao grupo de disponibilidade primário  
 Qualquer réplica secundária deve ser unida ao grupo de disponibilidade com **ALTER AVAILABILITY GROUP** usando a opção **JOIN** . Como a propagação direta é usada neste exemplo, você também deve chamar  **ALTER AVAILABILITY GROUP** com a opção **GRANT CREATE ANY DATABASE** . Isso permite que o grupo de disponibilidade crie o banco de dados e comece propagá-lo automaticamente a partir da réplica primária.  
  
 Neste exemplo, os seguintes comandos são executados na réplica secundária, `server2`, para unir o grupo de disponibilidade `ag1` . O grupo de disponibilidade então pode criar bancos de dados na réplica secundária.  
  
```tsql  
ALTER AVAILABILITY GROUP [ag1] JOIN   
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE  
GO  
```  
  
### Criar um ouvinte para o grupo de disponibilidade primário  
 Em seguida, crie um ouvinte para o grupo de disponibilidade primário no primeiro WSFC. Neste exemplo, o ouvinte é denominado `ag1-listener`. Para obter instruções detalhadas sobre como criar um ouvinte, veja [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).  
  
```  
ALTER AVAILABILITY GROUP [ag1]    
    ADD LISTENER 'ag1-listener' ( WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , PORT = 60173);    
GO  
```  
  
### Criar o grupo de disponibilidade secundário no segundo cluster  
 Em seguida, no segundo WSFC, crie um segundo grupo de disponibilidade, `ag2`. Nesse caso, o banco de dados não é especificado, pois ele será propagado automaticamente a partir do grupo de disponibilidade primário.  
  
```tsql  
CREATE AVAILABILITY GROUP [ag2]   
FOR   
REPLICA ON N'server3' WITH (ENDPOINT_URL = N'TCP://server3.contoso.com:5022',   
    FAILOVER_MODE = MANUAL,   
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC),   
N'server4' WITH (ENDPOINT_URL = N'TCP://server4.contoso.com:5022',   
    FAILOVER_MODE = MANUAL,   
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC);   
GO  
```  
  
> [!NOTE]  
>  Observe que o grupo de disponibilidade secundário deve usar o mesmo ponto de extremidade de espelhamento do banco de dados (no exemplo, a porta 5022). Caso contrário, a replicação será interrompida após um failover local.  
  
### Unir as réplicas secundárias ao grupo de disponibilidade secundário  
 Neste exemplo, os seguintes comandos são executados na réplica secundária, `server4`, para unir o grupo de disponibilidade `ag2` . O grupo de disponibilidade então pode criar bancos de dados na réplica secundária para oferecer suporte à propagação direta.  
  
```tsql  
ALTER AVAILABILITY GROUP [ag2] JOIN   
ALTER AVAILABILITY GROUP [ag2] GRANT CREATE ANY DATABASE  
GO  
```  
  
### Criar um ouvinte para o grupo de disponibilidade secundário  
 Em seguida, crie um ouvinte para o grupo de disponibilidade secundário no segundo WSFC. Neste exemplo, o ouvinte é denominado `ag2-listener`. Para obter instruções detalhadas sobre como criar um ouvinte, veja [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).  
  
```  
ALTER AVAILABILITY GROUP [ag2]    
    ADD LISTENER 'ag2-listener' ( WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , PORT = 60173);    
GO  
```  
  
### Criar o grupo de disponibilidade distribuída no primeiro cluster  
 No primeiro WSFC, crie um grupo de disponibilidade distribuído (denominado `distributedag` neste exemplo). Use o comando **CREATE AVAILABILITY GROUP** com a opção **DISTRIBUTED** . O parâmetro **AVAILABILITY GROUP ON** especifica os grupos de disponibilidade membros, `ag1` e `ag2`.  
  
```tsql  
CREATE AVAILABILITY GROUP [distributedag]  
   WITH (DISTRIBUTED)   
   AVAILABILITY GROUP ON  
      'ag1' WITH    
      (   
         LISTENER_URL = 'tcp://ag1-listener:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      ),   
      'ag2' WITH    
      (   
         LISTENER_URL = 'tcp://ag2-listener:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      );    
GO   
```  
  
> [!NOTE]  
>  O **LISTENER_URL** especifica o ouvinte para cada grupo de disponibilidade, juntamente com o ponto de extremidade de espelhamento de banco de dados do grupo de disponibilidade. Neste exemplo, esse ponto de extremidade é a porta `5022` (não a porta `60173` usada para criar o ouvinte).  
  
### Unir o grupo de disponibilidade distribuída no segundo cluster  
 Em seguida, una o grupo de disponibilidade distribuída no segundo WSFC.  
  
```tsql  
ALTER AVAILABILITY GROUP [distributedag]   
   JOIN   
   AVAILABILITY GROUP ON  
      'ag1' WITH    
      (   
         LISTENER_URL = 'tcp://ag1-listener:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      ),   
      'ag2' WITH    
      (   
         LISTENER_URL = 'tcp://ag2-listener:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      );    
GO  
```  

  
## Failover para um grupo de disponibilidade secundário  
 No momento, apenas o failover manual é permitido. A seguinte instrução Transact-SQL força o failover no grupo de disponibilidade distribuído denominado `distributedag`:  


1. Defina o modo de disponibilidade como confirmação síncrona para o grupo de disponibilidade secundário. 
    
      ```tsql  
      ALTER AVAILABILITY GROUP [distributedag] 
      MODIFY 
      AVAILABILITY GROUP ON
      'ag1' WITH  
         ( 
          LISTENER_URL = 'tcp://ag1-listener:5022',  
          AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT, 
          FAILOVER_MODE = MANUAL, 
          SEEDING_MODE = MANUAL 
          ), 
      'ag2' WITH  
        ( 
        LISTENER_URL = 'tcp://ag2-listener:5022', 
        AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
        FAILOVER_MODE = MANUAL, 
        SEEDING_MODE = MANUAL 
        );  
       
      ```  
  
1. Aguarde até que o status do grupo de disponibilidade distribuído seja alterado para `SYNCHRONIZED`. Execute a consulta a seguir no SQL Server que hospeda a réplica primária do grupo de disponibilidade primário. 
    
      ```tsql  
      SELECT ag.name
             , drs.database_id
             , drs.group_id
             , drs.replica_id
             , drs.synchronization_state_desc
             , drs.end_of_log_lsn 
        FROM sys.dm_hadr_database_replica_states drs,
        sys.availability_groups ag
          WHERE drs.group_id = ag.group_id;      
      ```  

    Continuar depois que o grupo de disponibilidade **synchronization_state_desc** for `SYNCHRONIZED`. Se **synchronization_state_desc** não for `SYNCHRONIZED`, execute o comando a cada cinco segundos até que ele seja alterado. Não continue até que **synchronization_state_desc** seja  = `SYNCHRONIZED`. 

1. No SQL Server que hospeda a réplica primária do grupo de disponibilidade primário, defina a função do grupo de disponibilidade distribuído como `SECONDARY`. 

      ```tsql
      ALTER AVAILABILITY GROUP distributedag SET (ROLE = SECONDARY); 
      ```  

    Observação: neste ponto, o grupo de disponibilidade distribuído não está disponível.

1. Teste a prontidão de failover. Execute a seguinte consulta:

      ```tsql
      SELECT ag.name, 
             drs.database_id, 
             drs.group_id, 
             drs.replica_id, 
             drs.synchronization_state_desc, 
             drs.end_of_log_lsn 
      FROM sys.dm_hadr_database_replica_states drs, sys.availability_groups ag
      WHERE drs.group_id = ag.group_id; 
      ```  
    O grupo de disponibilidade está pronto para failover quando o **synchronization_state_desc** é `SYNCHRONIZED` e **end_of_log_lsn** é igual para ambos os grupos de disponibilidade. 

1. Excute failover do grupo de disponibilidade primário para o grupo de disponibilidade secundário. Execute o comando a seguir no SQL Server que hospeda a réplica primária do grupo de disponibilidade secundário. 

      ```tsql
      ALTER AVAILABILITY GROUP distributedag FORCE_FAILOVER_ALLOW_DATA_LOSS; 
      ```  
      Observação: após essa etapa, o grupo de disponibilidade distribuído estará disponível.
      
Depois de concluir as etapas acima, será executado failover do grupo de disponibilidade distribuído sem perda de dados. A Microsoft recomenda alterar o modo de disponibilidade de volta para ASYNCHRONOUS_COMMIT se os grupos de disponibilidade estiverem em uma distância geográfica que causa latência. 
  
## Remover um grupo de disponibilidade distribuída  
 A seguinte instrução Transact-SQL remove um grupo de disponibilidade distribuído denominado `distributedag`:  
  
```tsql  
DROP AVAILABILITY GROUP [distributedag]  
```  

## Criar um grupo de disponibilidade distribuído com Instâncias de Cluster de Failover

Você pode criar um grupo de disponibilidade distribuído usando um grupo de disponibilidade em uma FCI (instância de cluster de failover). Nesse caso, não é necessário um ouvinte do grupo de disponibilidade. Use o VNN (nome de rede virtual) para a réplica primária da instância FCI. O exemplo a seguir mostra um grupo de disponibilidade distribuído chamado SQLFCIDAG. Um grupo de disponibilidade é SQLFCIAG. SQLFCIAG tem duas réplicas FCI. O VNN da réplica FCI primária é SQLFCIAG-1, e o VNN da réplica FCI secundária é SQLFCIAG-2. O grupo de disponibilidade distribuído também inclui o SQLAG-DR, para a recuperação de desastre.

![Grupo de Disponibilidade AlwaysOn distribuído](../../../database-engine/availability-groups/windows/media/always-on-availability-group-distributed.png)

 
 
 A DDL a seguir cria esse grupo de disponibilidade distribuído. 

```tsql  
CREATE AVAILABILITY GROUP [SQLFCIDAG]  
   WITH (DISTRIBUTED)   
   AVAILABILITY GROUP ON  
  'SQLFCIAG' WITH    
    (   
        LISTENER_URL = 'tcp://SQLFCIAG-1:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC
      ),   
  'SQLAG-DR' WITH    
       (   
         LISTENER_URL = 'tcp://SQLAG-DR:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC
      );   
```  

Observe que a URL de escuta é o VNN da instância FCI primária.

## Executar failover manual de FCI no grupo de disponibilidade distribuído

Para executar failover manual do grupo de disponibilidade de FCI, atualize o grupo de disponibilidade distribuído para que ele reflita a alteração da URL de escuta. Por exemplo, execute a seguinte DDL nos AGs primário e secundário de SQLFCIAG:

```tsql  
ALTER AVAILABILITY GROUP [SQLFCIDAG]  
   MODIFY AVAILABILITY GROUP ON  
 'SQLFCIAG' WITH    
    (   
        LISTENER_URL = 'tcp://SQLFCIAG-2:5022'
    )
```  
  
## Consulte também  
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  