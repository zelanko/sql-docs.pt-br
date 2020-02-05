---
title: Configurar um grupo de disponibilidade distribuído
description: 'Descreve como criar e configurar um grupo de disponibilidade Always On distribuído. '
ms.custom: seodec18
ms.date: 08/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: f7c7acc5-a350-4a17-95e1-e689c78a0900
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c49fb6ad9ad1d824a91f2a91c399770f3032b8aa
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75952492"
---
# <a name="configure-an-always-on-distributed-availability-group"></a>Configurar um grupo de disponibilidade Always On distribuído  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Para criar um grupo de disponibilidade distribuído, você deve criar dois grupos de disponibilidade, cada um com seu próprio ouvinte. Em seguida, você combina esses grupos de disponibilidade em um grupo de disponibilidade distribuída. As etapas a seguir fornecem um exemplo básico em Transact-SQL. Este exemplo não abrange todos os detalhes da criação de grupos de disponibilidade e ouvintes, focando apenas nos requisitos básicos.

Para obter uma visão geral técnica dos grupos de disponibilidade distribuídos, consulte [Grupos de disponibilidade distribuídos](distributed-availability-groups.md).

## <a name="prerequisites"></a>Prerequisites

### <a name="set-the-endpoint-listeners-to-listen-to-all-ip-addresses"></a>Definir os ouvintes do ponto de extremidade para escutar em todos os endereços IP

Verifique se os pontos de extremidade podem se comunicar entre os diferentes grupos de disponibilidade no grupo de disponibilidade distribuído. Se um grupo de disponibilidade for definido como uma rede específica no ponto de extremidade, o grupo de disponibilidade distribuída não funcionará corretamente. Em cada servidor que hospeda uma réplica no grupo de disponibilidade distribuído, configure o ouvinte para ouvir em todos os endereços IP (`LISTENER_IP = ALL`).

#### <a name="create-a-listener-to-listen-to-all-ip-addresses"></a>Criar um ouvinte para escutar em todos os endereços IP

Por exemplo, o script a seguir cria um ponto de extremidade do ouvinte na porta TCP 5022 que escuta em todos os endereços IP.  

```sql
CREATE ENDPOINT [aodns-hadr] 
    STATE=STARTED
    AS TCP (LISTENER_PORT = 5022, LISTENER_IP = ALL)
FOR DATA_MIRRORING (
   ROLE = ALL, 
   AUTHENTICATION = WINDOWS NEGOTIATE,
   ENCRYPTION = REQUIRED ALGORITHM AES
)
GO
```

#### <a name="alter-a-listener-to-listen-to-all-ip-addresses"></a>Alterar um ouvinte para escutar em todos os endereços IP

Por exemplo, o script a seguir altera um ponto de extremidade do ouvinte para que ele escute em todos os endereços IP.  

```sql
ALTER ENDPOINT [aodns-hadr] 
    AS TCP (LISTENER_IP = ALL)
GO
```

## <a name="create-first-availability-group"></a>Criar o primeiro grupo de disponibilidade

### <a name="create-the-primary-availability-group-on-the-first-cluster"></a>Criar o grupo de disponibilidade primário no primeiro cluster  
Crie um grupo de disponibilidade no primeiro WSFC (cluster de failover do Windows Server).   Neste exemplo, o grupo de disponibilidade é denominado `ag1` para o banco de dados `db1`. A réplica primária do grupo de disponibilidade primário é conhecida como a **primária global** em um grupo de disponibilidade distribuído. Neste exemplo, a primária global é o servidor1.        
  
```sql  
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
  
>[!NOTE]
>O exemplo anterior usa a propagação automática, em que **SEEDING_MODE** é definido como **AUTOMATIC** para as réplicas e o grupo de disponibilidade distribuído. Essa configuração define que as réplicas secundárias e o grupo de disponibilidade secundário serão preenchidos automaticamente sem a necessidade de backup e restauração manual do banco de dados primário.  
  
### <a name="join-the-secondary-replicas-to-the-primary-availability-group"></a>Unir as réplicas secundárias ao grupo de disponibilidade primário  
Qualquer réplica secundária deve ser unida ao grupo de disponibilidade com **ALTER AVAILABILITY GROUP** usando a opção **JOIN** . Como a propagação automática é usada neste exemplo, você também deve chamar **ALTER AVAILABILITY GROUP** com a opção **GRANT CREATE ANY DATABASE**. Essa configuração permite que o grupo de disponibilidade crie o banco de dados e comece propagá-lo automaticamente da réplica primária.  
  
Neste exemplo, os seguintes comandos são executados na réplica secundária, `server2`, para unir o grupo de disponibilidade `ag1` . O grupo de disponibilidade então pode criar bancos de dados na réplica secundária.  
  
```sql  
ALTER AVAILABILITY GROUP [ag1] JOIN   
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE  
GO  
```  

>[!NOTE]
>Quando o grupo de disponibilidade cria um banco de dados em uma réplica secundária, ele define o proprietário do banco de dados como a conta que executou a instrução `ALTER AVAILABILITY GROUP` para conceder permissão para criar qualquer banco de dados. Para obter mais informações, consulte [Conceder permissão para criar banco de dados na réplica secundária do grupo de disponibilidade](automatic-seeding-secondary-replicas.md#grantCreate).
  
### <a name="create-a-listener-for-the-primary-availability-group"></a>Criar um ouvinte para o grupo de disponibilidade primário  

Em seguida, crie um ouvinte para o grupo de disponibilidade primário no primeiro WSFC. Neste exemplo, o ouvinte é denominado `ag1-listener`. Para obter instruções detalhadas sobre como criar um ouvinte, veja [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).  
  
```sql
ALTER AVAILABILITY GROUP [ag1]    
    ADD LISTENER 'ag1-listener' ( 
        WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , 
        PORT = 60173);    
GO  
```  
  

## <a name="create-second-availability-group"></a>Criar o segundo grupo de disponibilidade  
 Em seguida, no segundo WSFC, crie um segundo grupo de disponibilidade, `ag2`. Neste caso, o banco de dados não é especificado, pois ele é propagado automaticamente do grupo de disponibilidade primário.  A réplica primária do grupo de disponibilidade secundário é conhecida como o **encaminhador** em um grupo de disponibilidade distribuído. Neste exemplo, o servidor3 é o encaminhador. 
  
```sql  
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
> O grupo de disponibilidade secundário deve usar o mesmo ponto de extremidade de espelhamento do banco de dados (no exemplo, a porta 5022). Caso contrário, a replicação será interrompida após um failover local.  
  
### <a name="join-the-secondary-replicas-to-the-secondary-availability-group"></a>Unir as réplicas secundárias ao grupo de disponibilidade secundário  
 Neste exemplo, os seguintes comandos são executados na réplica secundária, `server4`, para unir o grupo de disponibilidade `ag2` . O grupo de disponibilidade então pode criar bancos de dados na réplica secundária para oferecer suporte à propagação automática.  
  
```sql  
ALTER AVAILABILITY GROUP [ag2] JOIN   
ALTER AVAILABILITY GROUP [ag2] GRANT CREATE ANY DATABASE  
GO  
```  
  
### <a name="create-a-listener-for--the-secondary-availability-group"></a>Criar um ouvinte para o grupo de disponibilidade secundário  
 Em seguida, crie um ouvinte para o grupo de disponibilidade secundário no segundo WSFC. Neste exemplo, o ouvinte é denominado `ag2-listener`. Para obter instruções detalhadas sobre como criar um ouvinte, veja [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).  
  
```  
ALTER AVAILABILITY GROUP [ag2]    
    ADD LISTENER 'ag2-listener' ( WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , PORT = 60173);    
GO  
```  
  
## <a name="create-distributed-availability-group-on-first-cluster"></a>Criar um grupo de disponibilidade distribuído no primeiro cluster  
 No primeiro WSFC, crie um grupo de disponibilidade distribuído (denominado `distributedag` neste exemplo). Use o comando **CREATE AVAILABILITY GROUP** com a opção **DISTRIBUTED** . O parâmetro **AVAILABILITY GROUP ON** especifica os grupos de disponibilidade membros, `ag1` e `ag2`.  
  
```sql  
CREATE AVAILABILITY GROUP [distributedag]  
   WITH (DISTRIBUTED)   
   AVAILABILITY GROUP ON  
      'ag1' WITH    
      (   
         LISTENER_URL = 'tcp://ag1-listener.contoso.com:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      ),   
      'ag2' WITH    
      (   
         LISTENER_URL = 'tcp://ag2-listener.contoso.com:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      );    
GO   
```  
  
> [!NOTE]  
>  O **LISTENER_URL** especifica o ouvinte para cada grupo de disponibilidade, juntamente com o ponto de extremidade de espelhamento de banco de dados do grupo de disponibilidade. Neste exemplo, esse ponto de extremidade é a porta `5022` (não a porta `60173` usada para criar o ouvinte). Se você estiver usando um balanceador de carga, por exemplo, no Azure, [adicione uma regra de balanceamento de carga à porta do grupo de disponibilidade distribuído](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener#add-load-balancing-rule-for-distributed-availability-group). Adicione a regra à porta do ouvinte, além da porta da instância do SQL Server. 

### <a name="cancel-automatic-seeding-to-forwarder"></a>Cancelar a propagação automática para o encaminhador

Se, por qualquer motivo, for necessário cancelar a inicialização do encaminhador _antes_ de os dois grupos de disponibilidade serem sincronizados, ALTERE o grupo de disponibilidade distribuído definindo o parâmetro SEEDING_MODE do encaminhador como MANUAL e cancele imediatamente a propagação. Execute o comando no primário global: 

```sql
-- Cancel automatic seeding.  Connect to global primary but specify DAG AG2
ALTER AVAILABILITY GROUP [distributedag]   
   MODIFY  
   AVAILABILITY GROUP ON  
   'ag2' WITH  
   (  SEEDING_MODE = MANUAL  );   
```

  
## <a name="join-distributed-availability-group-on-second-cluster"></a>Ingressar o grupo de disponibilidade distribuído no segundo cluster  
 Em seguida, una o grupo de disponibilidade distribuída no segundo WSFC.  
  
```sql  
ALTER AVAILABILITY GROUP [distributedag]   
   JOIN   
   AVAILABILITY GROUP ON  
      'ag1' WITH    
      (   
         LISTENER_URL = 'tcp://ag1-listener.contoso.com:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      ),   
      'ag2' WITH    
      (   
         LISTENER_URL = 'tcp://ag2-listener.contoso.com:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      );    
GO  
```  

## <a name="failover"></a> Ingressar no banco de dados no secundário do segundo grupo de disponibilidade
Depois que o banco de dados na réplica secundária do segundo grupo de disponibilidade tiver entrado em um estado de repouso, será necessário uni-o manualmente ao grupo de disponibilidade.

```sql  
ALTER DATABASE [db1] SET HADR AVAILABILITY GROUP = [ag2];   
```
  
## <a name="failover"></a> Fazer failover em um grupo de disponibilidade secundário  

No momento, apenas o failover manual é permitido. Para fazer failover manual de um grupo de disponibilidade distribuído:

1. Para garantir que nenhum dado seja perdido, defina o grupo de disponibilidade distribuído para confirmação síncrona.
1. Aguarde até que o grupo de disponibilidade distribuído esteja sincronizado.
1. Na réplica primária global, defina a função do grupo de disponibilidade distribuído como `SECONDARY`.
1. Teste a prontidão de failover.
1. Faça failover do grupo de disponibilidade para o site primário.

Os exemplos de Transact-SQL a seguir demonstram as etapas detalhadas para fazer failover do grupo de disponibilidade distribuído denominado `distributedag`:

1. Defina o grupo de disponibilidade distribuído como confirmação síncrona executando o seguinte código em *ambos*, na primária global e no encaminhador.   
    
      ```sql  
      -- sets the distributed availability group to synchronous commit 
       ALTER AVAILABILITY GROUP [distributedag] 
       MODIFY 
       AVAILABILITY GROUP ON
       'ag1' WITH 
        ( 
        AVAILABILITY_MODE = SYNCHRONOUS_COMMIT 
        ), 
        'ag2' WITH  
        ( 
        AVAILABILITY_MODE = SYNCHRONOUS_COMMIT 
        );
       
       -- verifies the commit state of the distributed availability group
       select ag.name, ag.is_distributed, ar.replica_server_name, ar.availability_mode_desc, ars.connected_state_desc, ars.role_desc, 
       ars.operational_state_desc, ars.synchronization_health_desc from sys.availability_groups ag  
       join sys.availability_replicas ar on ag.group_id=ar.group_id
       left join sys.dm_hadr_availability_replica_states ars
       on ars.replica_id=ar.replica_id
       where ag.is_distributed=1
       GO

      ```  
   >[!NOTE]
   >Em um grupo de disponibilidade distribuído, o status de sincronização entre os dois grupos de disponibilidade depende do modo de disponibilidade de ambas as réplicas. Para o modo de confirmação síncrona, tanto o grupo de disponibilidade primária quanto o grupo de disponibilidade secundária atuais precisam ter o modo de disponibilidade `SYNCHRONOUS_COMMIT`. Por esse motivo, você precisa executar o script acima, tanto na réplica primária global quanto no encaminhador.

1. Aguarde até que o status do grupo de disponibilidade distribuído seja alterado para `SYNCHRONIZED`. Execute a consulta a seguir na primária global que é a réplica primária do grupo de disponibilidade primário. 
    
      ```sql  
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

    Continuar depois que o grupo de disponibilidade **synchronization_state_desc** for `SYNCHRONIZED`. Se **synchronization_state_desc** não for `SYNCHRONIZED`, execute o comando a cada cinco segundos até que ele seja alterado. Não continue até que **synchronization_state_desc** =  seja `SYNCHRONIZED`. 

1. Na primária global, defina a função do grupo de disponibilidade distribuído como `SECONDARY`. 

    ```sql
    ALTER AVAILABILITY GROUP distributedag SET (ROLE = SECONDARY); 
    ```  

    Neste ponto, o grupo de disponibilidade distribuído não está disponível.

1. Teste a prontidão de failover. Execute a seguinte consulta:

    ```sql
    SELECT ag.name, 
        drs.database_id, 
        drs.group_id, 
        drs.replica_id, 
        drs.synchronization_state_desc, 
        drs.end_of_log_lsn 
    FROM sys.dm_hadr_database_replica_states drs, sys.availability_groups ag
    WHERE drs.group_id = ag.group_id; 
    ```  
    O grupo de disponibilidade estará pronto para failover quando **synchronization_state_desc** for `SYNCHRONIZED` e **end_of_log_lsn** for igual para ambos os grupos de disponibilidade. 

1. Faça failover do grupo de disponibilidade primário para o grupo de disponibilidade secundário. Execute o comando a seguir no SQL Server que hospeda a réplica primária do grupo de disponibilidade secundário. 

    ```sql
    ALTER AVAILABILITY GROUP distributedag FORCE_FAILOVER_ALLOW_DATA_LOSS; 
    ```  

    Após esta etapa, o grupo de disponibilidade distribuído estará disponível.
      
Depois de concluir as etapas acima, será executado failover do grupo de disponibilidade distribuído sem perda de dados. Se os grupos de disponibilidade estiverem em uma distância geográfica que causa latência, altere o modo de disponibilidade de volta para ASYNCHRONOUS_COMMIT. 
  
## <a name="remove-a-distributed-availability-group"></a>Remover um grupo de disponibilidade distribuída  
 A seguinte instrução Transact-SQL remove um grupo de disponibilidade distribuído denominado `distributedag`:  
  
```sql  
DROP AVAILABILITY GROUP [distributedag]  
```  

## <a name="create-distributed-availability-group-on-failover-cluster-instances"></a>Criar um grupo de disponibilidade distribuído com instâncias de cluster de failover

Você pode criar um grupo de disponibilidade distribuído usando um grupo de disponibilidade em uma FCI (instância de cluster de failover). Nesse caso, não é necessário um ouvinte do grupo de disponibilidade. Use o VNN (nome de rede virtual) para a réplica primária da instância FCI. O exemplo a seguir mostra um grupo de disponibilidade distribuído chamado SQLFCIDAG. Um grupo de disponibilidade é SQLFCIAG. SQLFCIAG tem duas réplicas FCI. O VNN da réplica FCI primária é SQLFCIAG-1, e o VNN da réplica FCI secundária é SQLFCIAG-2. O grupo de disponibilidade distribuído também inclui o SQLAG-DR, para a recuperação de desastre.

![Grupo de Disponibilidade AlwaysOn distribuído](../../../database-engine/availability-groups/windows/media/always-on-availability-group-distributed.png)

 
 
 A DDL a seguir cria esse grupo de disponibilidade distribuído. 

```sql  
CREATE AVAILABILITY GROUP [SQLFCIDAG]  
   WITH (DISTRIBUTED)   
   AVAILABILITY GROUP ON  
  'SQLFCIAG' WITH    
    (   
        LISTENER_URL = 'tcp://SQLFCIAG-1.contoso.com:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC
      ),   
  'SQLAG-DR' WITH    
       (   
         LISTENER_URL = 'tcp://SQLAG-DR.contoso.com:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC
      );   
```  

A URL do ouvinte é o VNN da instância da FCI primária.

## <a name="manually-fail-over-fci-in-distributed-availability-group"></a>Fazer failover manual da FCI no grupo de disponibilidade distribuído

Para fazer failover manual do grupo de disponibilidade da FCI, atualize o grupo de disponibilidade distribuído para que ele reflita a alteração da URL do ouvinte. Por exemplo, execute a seguinte DDL nos AGs primário e secundário de SQLFCIAG:

```sql  
ALTER AVAILABILITY GROUP [SQLFCIDAG]  
   MODIFY AVAILABILITY GROUP ON  
 'SQLFCIAG' WITH    
    (   
        LISTENER_URL = 'tcp://SQLFCIAG-2.contoso.com:5022'
    )
```  
  
## <a name="next-steps"></a>Próximas etapas

 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  
