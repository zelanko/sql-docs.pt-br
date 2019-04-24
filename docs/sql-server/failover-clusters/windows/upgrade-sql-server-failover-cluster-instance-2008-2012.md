---
title: Fazer upgrade das instâncias do SQL Server em execução em clusters do Windows Server 2008/2008 R2/2012 | Microsoft Docs
ms.date: 01/25/2018
ms.prod: sql
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- upgrading failover clusters
- clusters [SQL Server], upgrading
- failover clustering [SQL Server], upgrading
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a73eda4fbb3898846894a4cf35de4253cffedbc3
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2019
ms.locfileid: "58872246"
---
# <a name="upgrade-sql-server-instances-running-on-windows-server-20082008-r22012-clusters"></a>Fazer upgrade das instâncias do SQL Server em execução em clusters do Windows Server 2008/2008 R2/2012

O [!INCLUDE[nextref-longhorn-md](../../../includes/nextref-longhorn-md.md)], [!INCLUDE[winserver2008r2-md](../../../includes/winserver2008r2-md.md)] e [!INCLUDE[win8srv-md](../../../includes/win8srv-md.md)] impedem que os clusters de failover do Windows Server executem upgrades do sistema operacional in-loco, limitando a versão permitida do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de um cluster. Depois que o cluster é atualizado para, no mínimo, o [!INCLUDE[winblue-server-2-md](../../../includes/winblue-server-2-md.md)], ele pode permanecer atualizado.

## <a name="prerequisites"></a>Prerequisites

-   Antes de executar uma das estratégias de migração, é necessário preparar um cluster de failover paralelo do Windows Server com o Windows Server 2016/2012 R2. Todos os nós que incluem FCIs (instâncias de cluster de failover) do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] devem ser ingressados no cluster do Windows com as FCIs paralelas instaladas. Os computadores autônomos **não devem** ser ingressados no cluster de failover do Windows Server antes da migração. Os bancos de dados de usuário devem ser sincronizados no novo ambiente antes da migração.
-   Todas as instâncias de destino devem executar a mesma versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de sua instância paralela no ambiente original, com os mesmos nomes e IDs de instância e devem ser instaladas com os mesmos recursos. Os caminhos de instalação e a estrutura de diretórios devem ser idênticos nos computadores de destino. Isso não inclui os nomes da rede virtual da FCI, que devem ser diferentes antes da migração. Todos os recursos habilitados pela instância original (Always On, FILESTREAM, etc.) devem ser habilitados na instância de destino.

-   O cluster paralelo não deve ter nenhum [!INCLUDE[sshadrc-md](../../../includes/sshadrc-md.md)] instalado antes da migração.

-   O tempo de inatividade durante a migração de um cluster que usa estritamente Grupos de Disponibilidade (com ou sem FCIs do SQL) pode ser bastante limitado com Grupos de Disponibilidade Distribuídos, mas isso exige que todas as instâncias executem as versões [!INCLUDE[sssql15-md](../../../includes/sssql15-md.md)] RTM (ou superior).

-   Todas as estratégias de migração exigem a função sysadmin do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Todos os usuários do Windows usados pelos serviços do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (ou seja, a conta do Windows que executa os agentes de replicação) devem ter as permissões no nível do sistema operacional em cada computador no novo ambiente.

-   Os compartilhamentos de arquivos da rede e as unidades mapeadas da rede usados no ambiente de cluster original do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ainda devem existir e permanecer acessíveis pelo cluster de destino com as mesmas permissões das instâncias originais.

-   Todas as portas TCP/IP escutadas pela instância original do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não devem estar sendo utilizadas e devem permitir o tráfego de entrada no computador de destino.
-   Todos os serviços relacionados ao SQL devem ser instalados e executados pelo mesmo usuário do Windows.

-   As instâncias de destino devem ser instaladas com a mesma localidade das instâncias originais.

## <a name="migration-scenarios"></a>Cenários de migração

A estratégia de migração adequada depende de determinados parâmetros da topologia de cluster original do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], ou seja, do uso do [!INCLUDE[sshadrc-md](../../../includes/sshadrc-md.md)] e das instâncias de cluster de failover do SQL. A estratégia escolhida depende também dos requisitos do ambiente de destino. Se o novo ambiente exigir que cada computador ou FCI do SQL mantenha o VNN (nome da rede virtual) original ou se a topologia do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] depender da herança pelas novas instâncias de todos os objetos do sistema das instâncias originais, deveremos escolher uma estratégia que migre-os.

|                                   | Exige todos os objetos de servidor e VNNS | Exige todos os objetos de servidor e VNNS | Não exige objetos de servidor/VNNS\* | Não exige objetos de servidor/VNNS\* |
|-----------------------------------|--------------------------------------|--------------------------------------------------------------------|------------|------------|
| **_Grupos de Disponibilidade? (S/N)_**                  | **_S_**                              | **_N_**                                                            | **_S_**    | **_N_**    |
| **O cluster usa somente FCI do SQL**         | [Cenário 3](#scenario-3-windows-cluster-has-both-sql-fcis-and-sql-server-availability-groups)                           | [Cenário 2](#scenario-2-windows-clusters-with-sql-server-failover-cluster-instances-fcis)                                                        | [Cenário 1](#scenario-1-windows-cluster-with-sql-server-availability-groups-and-no-failover-cluster-instances-fcis) | [Cenário 2](#scenario-2-windows-clusters-with-sql-server-failover-cluster-instances-fcis) |
| **O cluster usa instâncias autônomas** | [Cenário 5](#scenario-5-windows-cluster-with-standalone-sql-server-instances-and-availability-groups)                           | [Cenário 4](#scenario-4-windows-cluster-with-standalone-sql-server-instances-and-no-availability-groups)                                                         | [Cenário 1](#scenario-1-windows-cluster-with-sql-server-availability-groups-and-no-failover-cluster-instances-fcis) | [Cenário 4](#scenario-4-windows-cluster-with-standalone-sql-server-instances-and-no-availability-groups) |

\* Excluindo nomes do ouvinte do Grupo de Disponibilidade

## <a name="scenario-1-windows-cluster-with-sql-server-availability-groups-and-no-failover-cluster-instances-fcis"></a>Cenário 1: Cluster do Windows com Grupos de Disponibilidade do SQL Server e nenhuma FCI (Instância do Cluster de Failover)
Se você tiver uma instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que usa AGs (Grupos de Disponibilidade) e nenhuma instância de cluster de failover, poderá migrar para um novo cluster criando uma implantação paralela de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em um Cluster do Windows diferente com o Windows Server 2016/2012 R2. Depois disso, você poderá criar um AG distribuído em que o cluster de destino é o secundário para o cluster de produção atual. Isso exige que o usuário faça upgrade para o [!INCLUDE[sssql15-md](../../../includes/sssql15-md.md)] ou superior.

###  <a name="to-perform-the-upgrade"></a>Para fazer o upgrade

1.  Se necessário, faça upgrade de todas as instâncias para o [!INCLUDE[sssql15-md](../../../includes/sssql15-md.md)] ou superior. As instâncias paralelas devem executar a mesma versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].

2.  Crie um Grupo de Disponibilidade para o cluster de destino. Se o nó primário do cluster de destino não for uma FCI, crie um ouvinte.

3.  Forme um grupo de disponibilidade distribuído em que o cluster de destino é o Grupo de Disponibilidade secundário.

    >[!NOTE]
    >O parâmetro LISTENER\_URL da criação do T-SQL do AG distribuído se comporta de forma diferente para AGs com FCI do SQL como a instância primária. Se esse for o caso para o AG primário ou secundário, use o VNN da FCI de SQL primária como a URL do ouvinte no lugar do nome da rede do ouvinte, juntamente com a porta do ponto de extremidade do espelhamento de banco de dados.

4.  Ingresse o Grupo de Disponibilidade secundário no AG distribuído.

5.  Ingresse os bancos de dados secundários no AG secundário.

    >[!NOTE]
    >Isso será feito automaticamente se o Grupo de Disponibilidade de destino usar a propagação automática; isso só é possível se os caminhos de dados e de log são os mesmos em todas as réplicas.

6.  Corte todo o tráfego para o AG primário e permita que o secundário seja sincronizado.

7.  Altere a política de confirmação em ambos os Grupos de Disponibilidade para SYNCHRONOUS_COMMIT e faça failover para o cluster de destino depois que o status for SYNCHRONIZED.

8.  Exclua o AG distribuído.

9.  Exclua ou renomeie o ouvinte no AG original.

10. Renomeie ou crie o ouvinte do novo AG com o nome do ouvinte do AG original.

    >[!NOTE]
    >Embora o registro DNS do ouvinte do AG original exista, a tentativa de criar um ouvinte usando esse nome falhará.

11. Retome o tráfego em direção ao ouvinte.

## <a name="scenario-2-windows-clusters-with-sql-server-failover-cluster-instances-fcis"></a>Cenário 2: Clusters do Windows com FCIs (Instâncias de Cluster de Failover) do SQL Server

Se você tiver um ambiente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com apenas instâncias de FCI do SQL, poderá migrar para um novo cluster criando um ambiente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] paralelo em um Cluster do Windows diferente com o Windows Server 2016/2012 R2. Você migrará para o cluster de destino “roubando” os VNNs das FCIs antigas do SQL e adquirindo-as nos novos clusters. Isso criará um tempo de inatividade adicional que depende dos tempos de propagação de DNS.

###  <a name="to-perform-the-upgrade"></a>Para fazer o upgrade

1.  Faça um backup completo e pare o tráfego em direção ao cluster original do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].

2.  Faça um backup da parte final do log dos bancos de dados de usuário e restaure-os com a recuperação no novo ambiente.

3.  No cluster de destino no Gerenciador de Cluster de Failover, desative todas as funções clusterizadas da FCI do SQL.

4.  Ainda no Gerenciador de Cluster de Failover no cluster de destino, ative novamente os discos clusterizados usados por cada FCI do SQL.

5.  No cluster original no Gerenciador de Cluster de Failover, desative todas as funções clusterizadas da FCI do SQL.

6.  Ainda no Gerenciador de Cluster de Failover no cluster original, ative novamente os discos clusterizados usados por cada FCI do SQL.

7.  Copie os bancos de dados do sistema dos computadores originais para seu computador de destino paralelo.

8.  No ambiente original no Gerenciador de Cluster de Failover, altere o nome do recurso "Nome do Servidor" de cada função da FCI do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].

9.  Agora coloque online novamente apenas o recurso Nome do Servidor renomeado para cada uma das funções da FCI do SQL.

10. Agora no cluster de destino no Gerenciador de Cluster de Failover, renomeie o recurso "Nome do Servidor" de cada função da FCI do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com o nome usado anteriormente pelo cluster original.

    >[!NOTE]
    >Os erros resultantes do nome que já está sendo usado por outro computador serão interrompidos depois que os registros DNS do nome forem excluídos.

11. Depois que todas as FCIs forem renomeadas, reinicie cada um dos computadores no novo cluster.

12. Conforme os computadores voltam a ficar online após a reinicialização, inicie cada uma das funções da FCI do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Gerenciador de Cluster de Failover.

## <a name="scenario-3-windows-cluster-has-both-sql-fcis-and-sql-server-availability-groups"></a>Cenário 3: o Cluster do Windows tem FCIs do SQL e Grupos de Disponibilidade do SQL Server

Se você tiver uma instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que não usa nenhuma instância autônoma do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], apenas FCIs do SQL, que estão contidas em, pelo menos, um Grupo de Disponibilidade, poderá migrar isso para um novo cluster usando métodos semelhantes ao cenário "nenhum Grupo de Disponibilidade, nenhuma instância autônoma". Antes de copiar as tabelas do sistema para os discos compartilhados da FCI de destino, você deverá remover todos os Grupos de Disponibilidade do ambiente original. Depois que todos os bancos de dados forem migrados para os computadores de destino, você recriará os Grupos de Disponibilidade com os mesmos nomes de esquema e de ouvinte. Ao fazer isso, os recursos de cluster de failover do Windows Server serão formados corretamente e gerenciados no cluster de destino. **O Always On deve estar habilitado no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager em cada computador no ambiente de destino antes da migração.**

### <a name="to-perform-the-upgrade"></a>Para fazer o upgrade

1.  Pare o tráfego em direção ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].

2.  Faça um backup da parte final do log dos bancos de dados de usuário e restaure-os com a recuperação no primário pretendido do novo ambiente e com NORECOVERY em todos os secundários pretendidos.

3.  No cluster de destino no Gerenciador de Cluster de Failover, desative todas as funções clusterizadas da FCI do SQL.

4.  Ainda no Gerenciador de Cluster de Failover no cluster de destino, ative novamente os discos clusterizados usados por cada FCI do SQL.

5.  No cluster original, exclua o Grupo de Disponibilidade.

6.  No cluster original no Gerenciador de Cluster de Failover, desative todas as funções clusterizadas da FCI do SQL.

7.  Ainda no Gerenciador de Cluster de Failover no cluster original, ative novamente os discos clusterizados usados por cada FCI do SQL.

8.  Copie os bancos de dados do sistema dos computadores originais para seu computador de destino paralelo.

9.  No ambiente original no Gerenciador de Cluster de Failover, altere o nome do recurso "Nome do Servidor" de cada função da FCI do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].

10. Agora coloque online novamente apenas o recurso Nome do Servidor renomeado para cada uma das funções da FCI do SQL.

11. Agora no cluster de destino no Gerenciador de Cluster de Failover, renomeie o recurso "Nome do Servidor" de cada função da FCI do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com o nome usado anteriormente pelo cluster original.

12. Depois que todas as FCIs forem renomeadas, reinicie cada um dos computadores no novo cluster.

13. Conforme os computadores voltam a ficar online após a reinicialização, inicie cada uma das funções da FCI do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Gerenciador de Cluster de Failover.

14. Depois que todas as instâncias estiverem online, forme o Grupo de Disponibilidade na réplica em que os bancos de dados foram restaurados com a recuperação.

15. Ingresse todas as réplicas secundárias e todos os bancos de dados secundários no AG.

16. Crie um ouvinte no novo AG com o nome do ouvinte do Grupo de Disponibilidade original.

## <a name="scenario-4-windows-cluster-with-standalone-sql-server-instances-and-no-availability-groups"></a>Cenário 4: Cluster do Windows com Instâncias do SQL Server autônomas e nenhum Grupo de Disponibilidade

A migração de um cluster com instâncias autônomas é semelhante no processo de migração de um cluster do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com apenas FCIs. No entanto, em vez de alterar o VNN do recurso de cluster do nome da rede da FCI, altere o nome do computador autônomo original e “roube” o nome do computador antigo no computador de destino. Isso introduz um tempo de inatividade adicional em relação ao cenário “nenhuma instância autônoma”, pois não é possível ingressar o computador autônomo de destino no WSFC até que o nome da rede do computador antigo tenha sido adquirido.

###  <a name="to-perform-the-upgrade"></a>Para fazer o upgrade

1.  Pare o tráfego em direção ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].

2.  Faça um backup da parte final do log dos bancos de dados de usuário e restaure-os com a recuperação no novo ambiente em cada computador.

3.  No cluster de destino no Gerenciador de Cluster de Failover, desative todas as funções clusterizadas da FCI do SQL.

4.  Ainda no cluster de destino no Gerenciador de Cluster de Failover, ative novamente os discos clusterizados usados por cada FCI do SQL.

5.  No cluster original no Gerenciador de Cluster de Failover, desative cada função clusterizada da FCI do SQL e pare as instâncias autônomas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager.

6.  Para cada computador autônomo do cluster original, renomeie cada computador com um novo nome exclusivo de computador. Reinicie cada um desses computadores, conforme indicado.

7.  No cluster original no Gerenciador de Cluster de Failover, ative novamente os discos clusterizados usados por cada FCI do SQL.

8.  Copie os bancos de dados do sistema para os computadores de destino.

9.  No ambiente original no Gerenciador de Cluster de Failover, altere o recurso "Nome do Servidor" de cada função da FCI do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para um novo nome exclusivo.

10. Agora coloque online novamente apenas o recurso Nome do Servidor renomeado para cada uma das funções da FCI do SQL.

11. Agora nas instâncias autônomas paralelas, renomeie os computadores com os nomes dos computadores autônomos originais. (Remova o nome antigo do servidor e adicione o novo nome do servidor com o parâmetro local.) Reinicie os computadores, conforme indicado.

12. Após a reinicialização, ingresse cada um dos computadores autônomos no Cluster de Failover do Windows Server de destino.

13. Agora no cluster de destino no Gerenciador de Cluster de Failover, renomeie o recurso "Nome do Servidor" de cada função da FCI do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com o nome usado anteriormente pelo cluster original.

14. Depois que todas as FCIs forem renomeadas, reinicie cada um dos computadores no novo cluster.

15. Conforme os computadores voltam a ficar online após a reinicialização, inicie cada uma das funções da FCI do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Gerenciador de Cluster de Failover.

## <a name="scenario-5-windows-cluster-with-standalone-sql-server-instances-and-availability-groups"></a>Cenário 5: Cluster do Windows com Instâncias do SQL Server autônomas e Grupos de Disponibilidade

A migração de um cluster que usa Grupos de Disponibilidade com réplicas autônomas é semelhante ao processo de migração de um cluster com o uso de FCIs que usam Grupos de Disponibilidade. Ainda é necessário excluir os Grupos de Disponibilidade originais e reconstruí-los no cluster de destino; no entanto, um tempo de inatividade adicional é introduzido devido aos custos adicionais das migração de instâncias autônomas. **O Always On deve estar habilitado em cada FCI no ambiente de destino antes da migração.**

###  <a name="to-perform-the-upgrade"></a>Para fazer o upgrade

1.  Pare o tráfego em direção ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].

2.  Faça um backup da parte final do log dos bancos de dados de usuário e restaure-os com a recuperação no novo ambiente no primário pretendido e com NORECOVERY em cada secundário pretendido.

3.  Exclua o Grupo de Disponibilidade do cluster original.

4.  No cluster de destino no Gerenciador de Cluster de Failover, desative todas as funções clusterizadas da FCI do SQL.

5.  Ainda no cluster de destino no Gerenciador de Cluster de Failover, ative novamente os discos clusterizados usados por cada FCI do SQL.

6.  No cluster original no Gerenciador de Cluster de Failover, desative cada função clusterizada da FCI do SQL e pare as instâncias autônomas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager.

7.  Para cada computador autônomo do cluster original, renomeie cada computador com um novo nome exclusivo de computador. Reinicie cada um desses computadores, conforme indicado.

8.  No cluster original no Gerenciador de Cluster de Failover, ative novamente os discos clusterizados usados por cada FCI do SQL.

9.  Copie os bancos de dados do sistema para os computadores de destino.

10. No ambiente original no Gerenciador de Cluster de Failover, altere o recurso "Nome do Servidor" de cada função da FCI do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para um novo nome exclusivo.

11. Agora coloque online novamente apenas o recurso Nome do Servidor renomeado para cada uma das funções da FCI do SQL.

12. Agora nas instâncias autônomas paralelas, renomeie os computadores com os nomes dos computadores autônomos originais. (Remova e adicione o nome do servidor no SQL.) Reinicie os computadores, conforme indicado.

13. Após a reinicialização, ingresse cada um dos computadores autônomos no cluster de failover do Windows Server de destino.

14. Agora no cluster de destino no Gerenciador de Cluster de Failover, renomeie o recurso "Nome do Servidor" de cada função da FCI do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com o nome usado anteriormente pelo cluster original.

15. Depois que todas as FCIs forem renomeadas, reinicie cada um dos computadores no novo cluster.

16. Conforme os computadores voltam a ficar online após a reinicialização, inicie cada uma das funções da FCI do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Gerenciador de Cluster de Failover.

17. Depois que todas as instâncias estiverem online, recrie o Grupo de Disponibilidade no primário pretendido.

18. Ingresse cada réplica Secundária e banco de dados secundário.

19. Recrie o ouvinte do Grupo de Disponibilidade com o mesmo nome do original.

## <a name="specific-concerns-for-individual-features"></a>Preocupações específicas para recursos individuais

### [!INCLUDE[sshadrc-md](../../../includes/sshadrc-md.md)]

-   **Ponto de extremidade de espelhamento de banco de dados**

    De uma perspectiva do SQL, o ponto de extremidade de espelhamento de banco de dados será migrado para a nova instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] junto com as tabelas do sistema. Antes da migração, verifique se as regras apropriadas estão aplicadas em firewalls e se nenhum outro processo está escutando na mesma porta.

-   **Grupos de Disponibilidade**

    Os Grupos de Disponibilidade e seus ouvintes não podem ser migrados entre instâncias. Os recursos de cluster de failover do Windows Server criados pelo Grupo de Disponibilidade não podem ser recriados no ambiente de destino com facilidade. Em vez de tentar migrar Grupos de Disponibilidade, buscamos remover e recriar os Grupos de Disponibilidade no cluster de destino.

-   **Ouvintes do Grupo de Disponibilidade**

    Como os próprios Grupos de Disponibilidade, removemos e recriamos ouvintes em vez de migrá-los diretamente.

### <a name="replication"></a>Replicação

-   **Distribuidores, publicadores e assinantes remotos**

    A relação entre um distribuidor e um publicador depende apenas do VNN dos computadores que hospedam os dois, que será resolvido corretamente no novo computador. Os trabalhos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent também serão migrados corretamente com as tabelas do sistema, de modo que os vários agentes de replicação possam continuar a execução como de costume. É necessário que, antes da migração, todas as contas do Windows que executam o próprio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent ou qualquer trabalho do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent tenham as mesmas permissões no ambiente de destino. A comunicação com o publicador e os assinantes será executada como de costume.

-   **Pasta do instantâneo**

    Antes da migração, é necessário que todos os compartilhamentos de rede usados pelos recursos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sejam acessíveis pelos computadores no ambiente de destino com as mesmas permissões do ambiente original. Você precisará garantir que isso ocorra antes da migração.

### <a name="service-broker"></a>Service Broker

-   **Ponto de extremidade do Service Broker**

    De uma perspectiva do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], não há nenhuma preocupação com o ponto de extremidade. Antes da migração, você precisará garantir que nenhum processo já esteja escutando na mesma porta e que nenhuma regra de firewall esteja bloqueando essa porta ou que exista uma regra de firewall permitindo especificamente a porta.

-   **Certificados**

    Os certificados também devem ser copiados em backup e restaurados para os computadores de destino, caso o certificado precise ser restaurado para um novo computador.

-   **Rotas**

    As rotas dependem do nome da rede virtual do destino, que será resolvido corretamente para os computadores corretos no novo ambiente para os nomes dos computadores e os nomes da rede da FCI do SQL. Qualquer outro VNN referenciado também deverá ser redirecionado para o novo computador.

-   **Associações de serviço remoto**

    As associações de serviço remoto funcionarão conforme esperado após a migração, já que qualquer usuário que usa a associação de serviço remoto será migrado corretamente.

### <a name="includessnoversionincludesssnoversion-mdmd-agent"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent

-   **Trabalhos**

    Os trabalhos serão migrados corretamente junto com os bancos de dados do sistema. Qualquer usuário que executa um trabalho do SQL Agent ou o próprio SQL Agent terá as mesmas permissões no computador de destino, conforme especificado nos pré-requisitos.

-   **Alertas e operadores**

    Os alertas e operadores serão migrados corretamente com os bancos de dados do sistema.

### <a name="filestream"></a>FILESTREAM

-   **Portas de compartilhamento de arquivos do Windows**

    As portas de compartilhamento de arquivos 139 e 445 do Windows devem ter regras que permitam o uso do FILESTREAM pelo tráfego de entrada

-   **Compartilhamento do Windows**

    O caminho do compartilhamento do Windows depende do recurso do nome da FCI do SQL, pois ele é acessado pelo `\\ServerName\ShareName`. A migração do FILESTREAM exige que todos os nós em uma FCI de destino habilitem o FILESTREAM e, caso um compartilhamento do Windows seja usado, que esses nós sejam configurados para usar o mesmo nome do compartilhamento do Windows do computador original. Depois que a FCI de Destino obtiver o nome do servidor correto, ela hospedará o compartilhamento do Windows usando o caminho desejado.

-   **Dados do FILESTREAM**

    Os dados do FILESTREAM estão incluídos no backup.

### <a name="integration-services"></a>Integration Services

-   **Projetos do SSIS**

    Os projetos do SSIS são migrados junto com o banco de dados do SSIS. Depois que o banco de dados do SSIS é movido, os pacotes são executáveis imediatamente antes da movimentação das tabelas do sistema.

-   **Fontes de dados baseadas em arquivo**

    Arquivos simples, arquivos do Excel, fontes de XML e outros devem ser acessíveis no mesmo local especificado pelo pacote do SSIS.

## <a name="next-steps"></a>Próximas etapas
- [Concluir a atualização do mecanismo de banco de dados](../../../database-engine/install-windows/complete-the-database-engine-upgrade.md)
- [Alterar o modo de compatibilidade do banco de dados e usar o repositório de consultas](../../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)
- [Aproveitar os Novos Recursos do SQL Server 2016](https://msdn.microsoft.com/library/d8879659-8efa-4442-bcbb-91272647ae16)
- [Atualizar uma instância de cluster de failover do SQL Server](upgrade-a-sql-server-failover-cluster-instance.md)
- [Exibir e ler arquivos de log da Instalação do SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)
- [Adicionar recursos a uma instância do SQL Server 2016 (instalação)](../../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)
