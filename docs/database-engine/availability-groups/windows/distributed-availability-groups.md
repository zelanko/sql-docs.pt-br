---
title: "Grupos de disponibilidade distribuídos (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 08/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], distributed
ms.assetid: 
caps.latest.revision: 
author: allanhirt
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 0463d237614b25667c8402da70b7c5e4217d4ef5
ms.openlocfilehash: ee06ae8d3a3a60d77e72ee9e55ee615a1bcf0cb9
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="distributed-availability-groups"></a>Grupos de disponibilidade distribuídos

Grupos de disponibilidade distribuídos são um novo recurso introduzido no SQL Server 2016, como uma variação do recurso existente grupos de disponibilidade AlwaysOn. Este artigo explica alguns aspectos dos grupos de disponibilidade distribuídos e complementa a [documentação existente do SQL Server](https://docs.microsoft.com/en-us/sql/sql-server/sql-server-technical-documentation).

> [!NOTE]
> “DAG” não é a abreviação oficial de *grupo de disponibilidade distribuído*, pois a abreviação já é usada para o recurso Grupo de Disponibilidade de Banco de Dados do Exchange. Esse recurso do Exchange não tem nenhuma relação com os grupos de disponibilidade do SQL Server nem com os grupos de disponibilidade distribuídos.

Para configurar um grupo de disponibilidade distribuído, consulte [Configurar grupos de disponibilidade distribuídos](configure-distributed-availability-groups.md).

## <a name="understand-distributed-availability-groups"></a>Noções básicas dos grupos de disponibilidade distribuídos

Um grupo de disponibilidade distribuído é um tipo especial de grupo de disponibilidade que abrange dois grupos de disponibilidade separados. Os grupos de disponibilidade subjacentes são configurados em dois clusters WSFC (Clustering de Failover do Windows Server) diferentes. Os grupos de disponibilidade que fazem parte de um grupo de disponibilidade distribuído não precisam estar no mesmo local. Eles podem ser físicos, virtuais, locais, estar na nuvem pública ou em qualquer lugar que dá suporte a uma implantação de grupo de disponibilidade. Contanto que dois grupos de disponibilidade possam se comunicar, você pode configurar um grupo de disponibilidade distribuído com eles.

Um grupo de disponibilidade tradicional tem recursos configurados em um cluster WSFC. Um grupo de disponibilidade distribuído não configura nada no cluster WSFC. Tudo sobre ele é mantido no SQL Server. Para saber como exibir informações de um grupo de disponibilidade distribuído, consulte [Exibindo informações do grupo de disponibilidade distribuído](#viewing-distributed-availability-group-information). 

Um grupo de disponibilidade distribuído exige que os grupos de disponibilidade subjacentes tenham um ouvinte. Em vez de fornecer o nome do servidor subjacente de uma instância autônoma (ou, no caso de uma instância de cluster de failover do SQL Server [FCI], o valor associado ao recurso de nome de rede) como você faria com um grupo de disponibilidade tradicional, especifique o ouvinte configurado para o grupo de disponibilidade distribuído com o parâmetro ENDPOINT_URL ao criá-lo. Embora cada grupo de disponibilidade subjacente do grupo de disponibilidade distribuído tenha um ouvinte, um grupo de disponibilidade distribuído não tem nenhum ouvinte.

A figura a seguir mostra uma exibição de alto nível de um grupo de disponibilidade distribuído que abrange dois grupos de disponibilidade (AG 1 e AG 2), cada um configurado em seu próprio cluster WSFC. O grupo de disponibilidade distribuído tem um total de quatro réplicas, com dois em cada grupo de disponibilidade. Cada grupo de disponibilidade pode dar suporte a até o número máximo de réplicas, então uma disponibilidade distribuída pode ter até um total de 18 réplicas.

<a name="fig1"></a>
![Exibição de alto nível de um grupo de disponibilidade distribuída][1]

Você pode configurar a movimentação de dados em grupos de disponibilidade distribuídos como síncrona ou assíncrona. No entanto, a movimentação de dados é ligeiramente diferente nos grupos de disponibilidade distribuídos comparado a um grupo de disponibilidade tradicional. Embora cada grupo de disponibilidade tenha uma réplica primária, há apenas uma cópia dos bancos de dados que fazem parte de um grupo de disponibilidade distribuído que pode aceitar inserções, atualizações e exclusões. Conforme mostrado na figura a seguir, o AG 1 é o grupo de disponibilidade primário. Sua réplica primária envia transações para as réplicas secundárias do AG 1 e a réplica primária do AG 2. A réplica primária do AG 2 também é conhecida como um *encaminhador*. Um encaminhador é uma réplica primária em um grupo de disponibilidade secundário em um grupo de disponibilidade distribuída. O encaminhador recebe as transações da réplica primária no grupo de disponibilidade primária e os encaminha para as réplicas secundárias em seu próprio grupo de disponibilidade.  O encaminhador mantém as réplicas secundárias do AG 2 atualizadas. 

![Grupo de disponibilidade distribuída e sua movimentação de dados][2]

A única maneira de fazer com que a réplica primária do AG 2 aceite inserções, atualizações e exclusões é fazer failover manual do grupo de disponibilidade distribuído do AG 1. Na figura anterior, como o AG 1 contém a cópia gravável do banco de dados, a emissão de um failover faz com que o grupo de disponibilidade AG 2 possa manipular inserções, atualizações e exclusões. Para obter informações sobre como fazer failover de um grupo de disponibilidade distribuído para outro, consulte [Failover para um grupo de disponibilidade secundário]( https://docs.microsoft.com/en-us/sql/database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups).

> [!NOTE]
> Os grupos de disponibilidade distribuídos do SQL Server 2016 dão suporte ao failover somente de um grupo de disponibilidade para outro usando a opção FORCE_FAILOVER_ALLOW_DATA_LOSS.

## <a name="sql-server-version-and-edition-requirements-for-distributed-availability-groups"></a>Requisitos de versão e edição do SQL Server para grupos de disponibilidade distribuídos

Atualmente, os grupos de disponibilidade distribuídos funcionam apenas com grupos de disponibilidade que são criados com a mesma versão principal do SQL Server. Por exemplo, todos os grupos de disponibilidade que fazem parte de um grupo de disponibilidade distribuído devem ser criados com o SQL Server 2016 atualmente. Como o recurso de grupos de disponibilidade distribuídos não existe no SQL Server 2012 ou 2014, os grupos de disponibilidade que foram criados com essas versões não podem fazer parte de grupos de disponibilidade distribuídos. 

> [!NOTE]
> Grupos de disponibilidade distribuída não podem ser configurados com a Standard edition ou uma combinação da Standard e da Enterprise edition.

Como há dois grupos de disponibilidade separados, o processo de instalação de um service pack ou de uma atualização cumulativa em uma réplica que faz parte de um grupo de disponibilidade distribuído é ligeiramente diferente do processo de um grupo de disponibilidade tradicional:

1. Comece atualizando as réplicas do segundo grupo de disponibilidade do grupo de disponibilidade distribuído.

2. Aplique patch às réplicas do grupo de disponibilidade primário do grupo de disponibilidade distribuído.

3. Assim como você faz com um grupo de disponibilidade padrão, faça failover do grupo de disponibilidade primário para uma de suas próprias réplicas (não para o primário do segundo grupo de disponibilidade) e aplique patch a ele. Se não houver nenhuma réplica que não seja o primário, um failover manual para o segundo grupo de disponibilidade será necessário.

> [!NOTE]
> Nenhum comunicado foi feito indicando se as versões futuras do SQL Server permitirão que versões anteriores façam parte do mesmo grupo de disponibilidade distribuído. Se esse cenário for permitido, ele possibilitará que grupos de disponibilidade distribuídos façam parte de um plano de upgrade de versão do SQL Server.

### <a name="windows-server-versions-and-distributed-availability-groups"></a>Versões do Windows Server e grupos de disponibilidade distribuídos

Um grupo de disponibilidade distribuído abrange vários grupos de disponibilidade, cada um em seu próprio cluster WSFC subjacente e um grupo de disponibilidade distribuído é um constructo somente do SQL Server.  Isso significa que os clusters WSFC que hospedam os grupos de disponibilidade individuais podem ter diferentes versões principais do Windows Server. As versões principais do SQL Server devem ser as mesmas, conforme abordado na seção anterior. Assim como mostrado [na figura inicial](#fig1), a figura a seguir mostra o AG 1 e o AG 2 fazendo parte de um grupo de disponibilidade distribuído, mas cada um dos clusters WSFC é uma versão diferente do Windows Server.


![Grupos de disponibilidade distribuída com clusters WSFC com versões diferentes do Windows Server][3]

Os clusters WSFC individuais e seus grupos de disponibilidade correspondentes seguem regras tradicionais. Ou seja, eles podem ser ingressados ou não em um domínio (Windows Server 2016 ou posterior). Quando dois grupos de disponibilidade diferentes são combinados em um único grupo de disponibilidade distribuído, há quatro cenários:

* Ambos os clusters WSFC são ingressados no mesmo domínio.
* Cada cluster WSFC é ingressado em um domínio diferente.
* Um cluster WSFC é ingressado em um domínio e o outro cluster WSFC não é ingressado em um domínio.
* Nenhum cluster WSFC é ingressado em um domínio.

Quando ambos os clusters WSFC são ingressados no mesmo domínio (domínios não confiáveis), você não precisa executar nenhuma ação especial ao criar o grupo de disponibilidade distribuído. Para grupos de disponibilidade e clusters WSFC que não são ingressados no mesmo domínio, use certificados para fazer com que o grupo de disponibilidade distribuído funcione, semelhante ao modo como você poderia criar um grupo de disponibilidade para um grupo de disponibilidade independente de domínio. Para saber como configurar certificados para um grupo de disponibilidade distribuído, siga as etapas 3 a 13 em [Criar um grupo de disponibilidade independente de domínio](domain-independent-availability-groups.md#create-a-domain-independent-availability-group).

Com um grupo de disponibilidade distribuído, as réplicas primárias de cada grupo de disponibilidade subjacente devem ter os certificados umas das outras. Se você já tiver pontos de extremidade que não usam certificados, reconfigure os pontos de extremidade usando [ALTER ENDPOINT](https://docs.microsoft.com/en-us/sql/t-sql/statements/alter-endpoint-transact-sql) para refletir o uso de certificados.

## <a name="distributed-availability-group-usage-scenarios"></a>Cenários de uso do grupo de disponibilidade distribuído

Estes são os três principais cenários de uso de um grupo de disponibilidade distribuído: 

* [Recuperação de desastre e configurações multissite mais fáceis](#disaster-recovery-and-multi-site-scenarios)
* [Migração para o novo hardware ou para as novas configurações, que podem incluir o uso do novo hardware ou a alteração dos sistemas operacionais subjacentes](#migration-using-a-distributed-availability-group)
* [Aumentar o número de réplicas legíveis além de oito em um único grupo de disponibilidade, abrangendo vários grupos de disponibilidade](#scaling-out-readable-replicas-with-distributed-accessibility-groups)

### <a name="disaster-recovery-and-multi-site-scenarios"></a>Cenários de recuperação de desastre e multissite

Um grupo de disponibilidade tradicional exige que todos os servidores façam parte do mesmo cluster WSFC, que pode tornar a abrangência de vários data centers um desafio. A figura a seguir mostra a aparência da arquitetura de um grupo de disponibilidade multissite tradicional, incluindo o fluxo de dados. Há uma réplica primária que envia transações para todas as réplicas secundárias. Essa configuração é menos flexível de algumas maneiras do que um grupo de disponibilidade distribuído. Por exemplo, você deve implementar itens como o Active Directory (se aplicável) e a testemunha para um quorum no cluster WSFC. Talvez você também precise levar em consideração outros aspectos de um cluster WSFC, como a alteração de votos de nó.

![Grupo de disponibilidade multissite tradicional][4]

Os grupos de disponibilidade distribuídos oferecem um cenário de implantação mais flexível para grupos de disponibilidade que abrangem vários data centers. Você pode usar até mesmo grupos de disponibilidade distribuídos nos quais recursos como o [envio de logs]( https://docs.microsoft.com/en-us/sql/database-engine/log-shipping/about-log-shipping-sql-server) foram usados no passado. No entanto, ao contrário dos grupos de disponibilidade tradicionais, os grupos de disponibilidade distribuídos não podem ter a aplicação atrasada de transações. Isso significa que os grupos de disponibilidade ou os grupos de disponibilidade distribuídos não podem ajudar, em caso de erro humano em que os dados são atualizados incorretamente ou excluídos.

Os grupos de disponibilidade distribuídos são acoplados de forma flexível, o que, nesse caso, significa que eles não exigem nenhum cluster WSFC e são mantidos pelo SQL Server. Como os clusters WSFC são mantidos individualmente e a sincronização é principalmente assíncrona entre os dois grupos de disponibilidade, é mais fácil configurar a recuperação de desastre em outro site. As réplicas primárias em cada grupo de disponibilidade sincronizam suas próprias réplicas secundárias.

* Apenas há suporte para o failover manual em um grupo de disponibilidade distribuído. Em uma situação de recuperação de desastre em que você está alternando data centers, você não deve configurar o failover automático (com raras exceções). 
* Provavelmente, você não precisará definir alguns dos itens ou parâmetros tradicionais para clusters WSFC multissite ou de sub-rede, como CrossSubnetThreshold, mas ainda precisa considerar a latência de rede em uma camada diferente para o transporte de dados. A diferença é que cada cluster WSFC mantém sua própria disponibilidade; o cluster não é uma entidade grande de quatro nós. Você tem dois clusters WSFC de dois nós separados, conforme mostrado na figura anterior.  
* Recomendamos a movimentação de dados assíncrona, porque essa abordagem será para fins de recuperação de desastre.
* Se você configurar a movimentação de dados síncrona entre a réplica primária e, pelo menos, uma réplica secundária do segundo grupo de disponibilidade e configurar a movimentação síncrona no grupo de disponibilidade distribuído, um grupo de disponibilidade distribuído aguardará até que todas as cópias síncronas reconheçam que contêm os dados.

### <a name="migrate-by-using-a-distributed-availability-group"></a>Migrar usando um grupo de disponibilidade distribuído

Como os grupos de disponibilidade distribuídos dão suporte a duas configurações de grupo de disponibilidade completamente diferentes, eles permitem não apenas cenários de recuperação de desastre e multissite mais fáceis, mas também cenários de migração. Se você estiver migrando para um novo hardware ou novas máquinas virtuais (IaaS na nuvem pública ou local), a configuração de um grupo de disponibilidade distribuído permitirá que uma migração ocorra, quando, no passado, você poderia ter usado o backup, a cópia e a restauração ou o envio de logs. 

A capacidade de migrar é especialmente útil em cenários em que você está alterando ou fazendo upgrade do sistema operacional subjacente, ao mesmo tempo que mantém a mesma versão do SQL Server. Embora o Windows Server 2016 permita uma atualização sem interrupção do Windows Server 2012 R2 no mesmo hardware, a maioria dos usuários opta por implantar um novo hardware ou novas máquinas virtuais. 

Para concluir a migração para a nova configuração, no final do processo, pare todo o tráfego de dados do grupo de disponibilidade original e altere o grupo de disponibilidade distribuído para a movimentação de dados síncrona. Essa ação garante que a réplica primária do segundo grupo de disponibilidade está totalmente sincronizada, de modo que não haja nenhuma perda de dados. Depois de verificar a sincronização, faça failover do grupo de disponibilidade distribuída para o grupo de disponibilidade secundária. Para obter mais informações, consulte [Fazer failover em um grupo de disponibilidade secundária](configure-distributed-availability-groups.md#failover).

Após a migração, na qual o segundo grupo de disponibilidade agora é o novo grupo de disponibilidade primário, talvez seja necessário fazer o seguinte:

* Renomeie o ouvinte no grupo de disponibilidade secundário (e possivelmente exclua ou renomeie o antigo no grupo de disponibilidade primário original) ou recrie-o com o ouvinte do grupo de disponibilidade primário original, para que os aplicativos e os usuários possam acessar a nova configuração.
* Se uma renomeação ou recriação não for possível, aponte os aplicativos e os usuários para o ouvinte no segundo grupo de disponibilidade.

### <a name="scale-out-readable-replicas-with-distributed-availability-groups"></a>Expandir réplicas legíveis com grupos de disponibilidade distribuídos

Um único grupo de disponibilidade distribuído pode ter até 16 réplicas secundárias, conforme necessário. Portanto, ele pode ter até 18 cópias para leitura, incluindo as duas réplicas primárias dos grupos de disponibilidade diferentes. Essa abordagem significa que mais de um site pode ter acesso quase em tempo real para relatar para vários aplicativos.

Os grupos de disponibilidade distribuídos podem ajudar você a expandir um farm somente leitura mais do que conseguirá com apenas um único grupo de disponibilidade. Um grupo de disponibilidade distribuído pode expandir réplicas legíveis de duas maneiras:

* Use a réplica primária do segundo grupo de disponibilidade em um grupo de disponibilidade distribuído para criar outro grupo de disponibilidade distribuído, mesmo que o banco de dados não esteja no estado RECOVERY.
* Você também pode usar a réplica primária do primeiro grupo de disponibilidade para criar outro grupo de disponibilidade distribuído.

Em outras palavras, uma réplica primária pode fazer parte de dois grupos de disponibilidade distribuídos diferentes. A figura a seguir mostra AG 1 e AG 2 fazendo parte do AG 1 Distribuído, enquanto AG 2 e AG 3 fazem parte do AG 2 Distribuído. A réplica primária (ou encaminhador) do AG 2 é uma réplica secundária para o AG 1 Distribuído e uma réplica primária do AG 2 Distribuído.

![Colocação em escala das leituras com grupos de disponibilidade distribuída][5]

A figura a seguir mostra o AG 1 como a réplica primária para dois grupos de disponibilidade distribuídos diferentes: AG 1 Distribuído (composto por AG 1 e AG 2) e AG 2 Distribuído (composto por AG 1 e AG 3).


![Outra colocação em escala das leituras usando o exemplo de grupos de disponibilidade distribuída][6]


Nos dois exemplos anteriores, pode haver até 27 réplicas no total nos três grupos de disponibilidade, que podem ser usados para consultas somente leitura. 

Atualmente, o [roteamento somente leitura]( https://docs.microsoft.com/en-us/sql/database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server) não funciona com grupos de disponibilidade distribuídos. Todas as consultas, caso usem o ouvinte para se conectar, vão para a réplica primária. Caso contrário, você precisará configurar cada réplica para permitir todas as conexões como uma réplica secundária e acessá-las diretamente. Esse comportamento pode ser alterado em uma atualização para o SQL Server 2016 ou em uma versão futura do SQL Server.

## <a name="initialize-secondary-availability-groups-in-a-distributed-availability-group"></a>Inicializar grupos de disponibilidade secundários em um grupo de disponibilidade distribuído

Os grupos de disponibilidade distribuídos foram criados com a [propagação automática]( https://docs.microsoft.com/en-us/sql/database-engine/availability-groups/windows/automatically-initialize-always-on-availability-group) como o principal método usado para inicializar a réplica primária no segundo grupo de disponibilidade. Uma restauração completa de banco de dados na réplica primária do segundo grupo de disponibilidade será possível se você fizer o seguinte:

1. Restaure o backup de banco de dados com WITH NORECOVERY.
2. Se necessário, restaure os backups de log de transações apropriados com WITH NORECOVERY.
3. Crie o segundo grupo de disponibilidade sem especificar um nome de banco de dados e com SEEDING_MODE definido como AUTOMATIC.
4. Crie o grupo de disponibilidade distribuído usando a propagação automática.

Quando você adicionar a réplica primária do segundo grupo de disponibilidade ao grupo de disponibilidade distribuído, a réplica será verificada nos bancos de dados primários do primeiro grupo de disponibilidade e a propagação atualizará o banco de dados com a origem. Há algumas advertências:

* A saída mostrada em `sys.dm_hadr_automatic_seeding` na réplica primária do segundo grupo de disponibilidade exibirá um `current_state` FAILED com o motivo “Tempo limite da mensagem de verificação da propagação”.

* O log atual do SQL Server na réplica primária do segundo grupo de disponibilidade mostrará que a propagação funcionou e que os [LSNs]( https://docs.microsoft.com/en-us/sql/relational-databases/sql-server-transaction-log-architecture-and-management-guide) foram sincronizados.

* A saída mostrada em `sys.dm_hadr_automatic_seeding` na réplica primária do primeiro grupo de disponibilidade mostrará um current_state COMPLETED. 

* A propagação também tem um comportamento diferente com grupos de disponibilidade distribuídos. Para que a propagação seja iniciada na segunda réplica, você deve emitir o comando `ALTER AVAILABILITY GROUP [AGName] GRANT CREATE ANY DATABASE` na réplica. Embora essa condição ainda seja verdadeira sobre qualquer réplica secundária que faz parte do grupo de disponibilidade subjacente, a réplica primária do segundo grupo de disponibilidade já tem as permissões corretas para permitir o início da propagação depois que ela é adicionada ao grupo de disponibilidade distribuído. 

### <a name="view-distributed-availability-group-information"></a>Exibir informações do grupo de disponibilidade distribuído 
    
Conforme mencionado anteriormente, um grupo de disponibilidade distribuído é um constructo somente do SQL Server e não é visto no cluster WSFC subjacente. A figura a seguir mostra dois clusters WSFC diferentes (CLUSTER_A e CLUSTER_B), cada um com seus próprios grupos de disponibilidade. Somente o AG1 no CLUSTER_A e o AG2 no CLUSTER_B são abordados aqui. 

<!-- ![Two WSFC clusters with multiple availability groups through PowerShell Get-ClusterGroup command][7]  -->
<a name="fig7"></a>

```
PS C:\> Get-ClusterGroup -Cluster CLUSTER_A

Name                            OwnerNode             State
----                            ---------             -----
AG1                             DENNIS                Online
Available Storage               GLEN                  Offline
Cluster Group                   JY                    Online
New_RoR                         DENNIS                Online
Old_RoR                         DENNIS                Online
SeedingAG                       DENNIS                Online


PS C:\> Get-ClusterGroup -Cluster CLUSTER_B

Name                            OwnerNode             State
----                            ---------             -----
AG2                             TOMMY                 Online
Available Storage               JC                    Offline
Cluster Group                   JC                    Online
```

Todas as informações detalhadas sobre um grupo de disponibilidade distribuída estão no SQL Server, especificamente nas exibições de gerenciamento dinâmico do grupo de disponibilidade. Atualmente, as únicas informações mostradas no SQL Server Management Studio para um grupo de disponibilidade distribuída estão na réplica primária para os grupos de disponibilidade. Conforme mostrado na figura a seguir, na pasta Grupos de Disponibilidade, o SQL Server Management Studio mostra que há um grupo de disponibilidade distribuída. A figura mostra AG1 como uma réplica primária para um grupo de disponibilidade individual que é local para essa instância, e não para um grupo de disponibilidade distribuída.

![Exibição no SQL Server Management Studio da réplica primária no primeiro cluster WSFC de um grupo de disponibilidade distribuída][8]


No entanto, se você clicar com o botão direito do mouse no grupo de disponibilidade distribuída, nenhuma opção estará disponível (consulte a figura a seguir) e as pastas expandidas Grupos de Disponibilidade, Ouvintes do Grupo de Disponibilidade e Réplicas de Disponibilidade estarão vazias. O SQL Server Management Studio 16 exibe esse resultado, mas ele poderá ser alterado em uma versão futura do SQL Server Management Studio.

![Não há opções disponíveis para a ação][9]

Conforme mostrado na figura a seguir, as réplicas secundárias não mostram nada no SQL Server Management Studio relacionado ao grupo de disponibilidade distribuída. Estes nomes de grupo de disponibilidade mapeiam as funções mostradas anteriormente na imagem [CLUSTER_A WSFC cluster](#fig7).

![Exibir uma réplica secundária no SQL Server Management Studio][10]

Os mesmos conceitos são verdadeiros quando você usa as exibições de gerenciamento dinâmico. Ao usar a consulta a seguir, você pode ver todos os grupos de disponibilidade (regulares e distribuídos) e os nós que participam deles. Esse resultado será exibido apenas se você consultar a réplica primária em um dos clusters de WSFC que estão participando do grupo de disponibilidade distribuída. Há uma nova coluna na exibição de gerenciamento dinâmico `sys.availability_groups` chamado `is_distributed`, que é 1 quando o grupo de disponibilidade é um grupo de disponibilidade distribuída. Para ver essa coluna:

```sql
SELECT ag.[name] as 'AG Name', 
    ag.Is_Distributed, 
    ar.replica_server_name as 'Replica Name'
FROM    sys.availability_groups ag, 
    sys.availability_replicas ar       
WHERE   ag.group_id = ar.group_id
```

Um exemplo de saída do segundo cluster WSFC que está participando de um grupo de disponibilidade distribuída é mostrado na figura a seguir. SPAG1 é composto de duas réplicas: DENNIS e JY. No entanto, o grupo de disponibilidade distribuída denominado SPDistAG tem os nomes dos dois grupos de disponibilidade participantes (SPAG1 e SPAG2) em vez dos nomes de instâncias, assim como acontece com um grupo de disponibilidade tradicional. 

![Exemplo de saída da consulta anterior][11]

No SQL Server Management Studio, qualquer status mostrado no painel e em outras áreas é destinado à sincronização local somente dentro desse grupo de disponibilidade. Para exibir a integridade de um grupo de disponibilidade distribuída, consulte as exibições de gerenciamento dinâmico. A consulta de exemplo a seguir amplia e aprimora a consulta anterior:

```sql
SELECT ag.[name] as 'AG Name', ag.is_distributed, ar.replica_server_name as 'Underlying AG', ars.role_desc as 'Role', ars.synchronization_health_desc as 'Sync Status'
FROM    sys.availability_groups ag, 
sys.availability_replicas ar,       
sys.dm_hadr_availability_replica_states ars       
WHERE   ar.replica_id = ars.replica_id
and     ag.group_id = ar.group_id 
and ag.is_distributed = 1
```
       
       
![Status do grupo de disponibilidade distribuída][12]


Para estender ainda mais a consulta anterior, você também pode ver o desempenho subjacente por meio de exibições de gerenciamento dinâmico ao adicionar em `sys.dm_hadr_database_replicas_states`. Atualmente, o modo de exibição de gerenciamento dinâmico armazena informações somente sobre o segundo grupo de disponibilidade. A consulta de exemplo a seguir, executada no grupo de disponibilidade primária, gera a saída de exemplo mostrada abaixo:

```
SELECT ag.[name] as 'Distributed AG Name', ar.replica_server_name as 'Underlying AG', dbs.[name] as 'DB', ars.role_desc as 'Role', drs.synchronization_health_desc as 'Sync Status', drs.log_send_queue_size, drs.log_send_rate, drs.redo_queue_size, drs.redo_rate
FROM    sys.databases dbs,
    sys.availability_groups ag,
    sys.availability_replicas ar,
    sys.dm_hadr_availability_replica_states ars,
    sys.dm_hadr_database_replica_states drs
WHERE   drs.group_id = ag.group_id
and ar.replica_id = ars.replica_id
and ars.replica_id = drs.replica_id
and dbs.database_id = drs.database_id
and ag.is_distributed = 1
```

![Informações de desempenho para um grupo de disponibilidade distribuída][13]


### <a name="next-steps"></a>Próximas etapas 

* [Usar a caixa de diálogo Assistente de Grupo de Disponibilidade (SQL Server Management Studio)](use-the-availability-group-wizard-sql-server-management-studio.md)

* [Usar a caixa de diálogo Novo Grupo de Disponibilidade (SQL Server Management Studio)](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)
 
* [Criar um grupo de disponibilidade com o Transact-SQL](create-an-availability-group-transact-sql.md)

<!--Image references-->
[1]: ./media/dag-01-high-level-view-distributed-ag.png
[2]: ./media/dag-02-distributed-ag-data-movement.png
[3]: ./media/dag-03-distributed-ags-wsfcs-different-versions-windows-server.png
[4]: ./media/dag-04-traditional-multi-site-ag.png
[5]: ./media/dag-05-scaling-out-reads-with-distributed-ags.png
[6]: ./media/dag-06-another-scaling-out-reads-using-distributed-ags-example.png
[7]: ./media/dag-07-two-wsfcs-multiple-ags-through-get-clustergroup-command.png
[8]: ./media/dag-08-view-smss-primary-replica-first-wsfc-distributed-ag.png
[9]: ./media/dag-09-no-options-available-action.png
[10]: ./media/dag-10-view-ssms-secondary-replica.png
[11]: ./media/dag-11-example-output-of-query-above.png
[12]: ./media/dag-12-distributed-ag-status.png
[13]: ./media/dag-13-performance-information-distributed-ag.png

 

