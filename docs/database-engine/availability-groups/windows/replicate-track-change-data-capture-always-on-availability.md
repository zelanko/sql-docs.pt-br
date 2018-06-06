---
title: Replicação, Controle de Alterações e Change Data Capture – grupos de disponibilidade | Microsoft Docs
ms.custom: ''
ms.date: 04/25/2018
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- change tracking [SQL Server], AlwaysOn Availability Groups
- change data capture [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
- replication [SQL Server], AlwaysOn Availability Groups
ms.assetid: e17a9ca9-dd96-4f84-a85d-60f590da96ad
caps.latest.revision: 37
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 37070e0b036d109624048603b24464a2019ec69d
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34769372"
---
# <a name="replication-change-tracking--change-data-capture---always-on-availability-groups"></a>Replicação, controle de alterações e Change Data Capture – grupos de disponibilidade AlwaysOn
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Há suporte para a replicação, a CDC (captura de dados de alteração) e o CT (controle de alterações) no [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] fornece alta disponibilidade e recursos adicionais de recuperação de banco de dados.  
  
##  <a name="Overview"></a> Visão geral da replicação com grupos de disponibilidade  
  
###  <a name="PublisherRedirect"></a> Redirecionamento do publicador  
 Quando um banco de dados publicado reconhecer o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], o distribuidor que fornece ao agente acesso a esse banco de dados será configurado com as entradas de redirected_publishers. Essas entradas redirecionam o par de publicador/banco de dados configurado originalmente, usando um nome do ouvinte do grupo de disponibilidade para conectar-se ao publicador e ao banco de dados de publicação. Haverá falha no failover das conexões estabelecidas pelo nome do ouvinte do grupo de disponibilidade. Quando o agente de replicação for reiniciado depois do failover, a conexão será automaticamente redirecionada para o novo primário.  
  
 Em um grupo de disponibilidade, um banco de dados secundário não pode ser um distribuidor. Há suporte para a republicação apenas quando a replicação transacional é combinada com o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)].  
  
 Se um banco de dados publicado for membro de um grupo de disponibilidade e o publicador for redirecionado, ele deverá ser redirecionado para um nome de ouvinte de grupo de disponibilidade associado ao grupo de disponibilidade. Ele não poderá ser redirecionado para um nó explícito.  
  
> [!NOTE]  
>  Após o failover em uma replica secundária, o Replication Monitor não poderá ajustar o nome da instância de publicação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e continuará exibindo informações de replicação abaixo do nome da instância primária original do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Depois do failover, um token de rastreamento não pode ser inserido usando o Replication Monitor; porém um token de rastreamento inserido no novo publicador usando [!INCLUDE[tsql](../../../includes/tsql-md.md)]é visível no Replication Monitor.  
  
###  <a name="Changes"></a> Alterações gerais nos agentes de replicação para dar suporte a grupos de disponibilidade  
 Três agentes de replicação foram modificados para dar suporte ao [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. O Leitor de Log, o Instantâneo e os Agentes de mesclagem foram modificados para consultar o banco de dados de distribuição para o publicador redirecionado e para usar o nome do ouvinte do grupo de disponibilidade retornado, se um publicador redirecionado tiver sido declarado, para conectar-se ao publicador de banco de dados.  
  
 Por padrão, quando os agentes consultam o distribuidor para determinar se o publicador original foi redirecionado, é verificada a adequação do destino atual ou o redirecionamento antes de retornar o host redirecionado ao agente. Este é o comportamento recomendado. No entanto, se a inicialização do agente ocorrer com muita frequência, a sobrecarga associada com o procedimento armazenado de validação poderá ser considerada muito cara. Uma nova opção de linha de comando, *BypassPublisherValidation*, foi adicionada aos agentes de Leitor de Log, Instantâneo e Mesclagem. Quando o comutador é usado, o publicador redirecionado é retornado imediatamente ao agente e a execução do procedimento armazenado de validação é ignorada.  
  
 As falhas retornadas do procedimento armazenado de validação são registradas nos logs de histórico do agente. Esses erros com severidade maior que ou igual a 16 causarão a finalização dos agentes. Alguns recursos de tentar novamente foram embutidos para os agentes tratarem a desconexão esperada de um banco de dados publicado quando ocorrer failover para um novo primário.  
  
#### <a name="log-reader-agent-modifications"></a>Modificações do Agente de Leitor de Log  
 O Logreader Agent tem as seguintes alterações.  
  
-   **Consistência do banco de dados replicado**  
  
     Quando um banco de dados publicado é membro de um grupo de disponibilidade, por padrão, o leitor de log não processa registros de log que ainda não foram protegidos em todas as réplicas secundárias do grupo de disponibilidade. Isso garante que, durante um failover, todas as linhas replicadas para um assinante também estejam presentes no novo primário.  
  
     Quando o distribuidor tem só duas réplicas de disponibilidade (uma primária e uma secundária) e ocorre um failover, a réplica primária original permanece desativada porque o leitor de log não avança até que todos os bancos de dados secundários sejam colocados novamente online ou até que as réplicas secundárias com falha sejam removidas do grupo de disponibilidade. Agora o leitor de log, que está sendo executado no banco de dados secundário, não continuará porque o AlwaysOn não poderá proteger as alterações feitas nos bancos de dados secundários. Para permitir que o leitor de log continue e ainda tenha a capacidade de recuperação de desastres, remova a réplica primária original do grupo de disponibilidade usando ALTER AVAILABITY GROUP <nome_do_grupo> REMOVE REPLICA. Em seguida, adicione uma nova réplica secundária ao grupo de disponibilidade.  
  
-   **Sinalizador de rastreamento 1448**  
  
     O sinalizador de rastreamento 1448 permite que o leitor de log de replicação avance, mesmo se as réplicas secundárias assíncronas não tiverem confirmado a recepção de uma alteração. Mesmo com esse sinalizador de rastreamento habilitado, o leitor de log sempre aguardará as réplicas secundárias síncronas. O leitor de log não ultrapassará o reconhecimento mínimo das réplicas secundárias síncronas. Ele se aplica à instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], e não apenas a um grupo de disponibilidade, um banco de dados de disponibilidade ou uma instância do leitor de log. Esse sinalizador de rastreamento entrará em vigor imediatamente, sem reinicialização. Ele pode ser ativado antecipadamente ou quando uma réplica secundária assíncrona apresentar falha.  
  
###  <a name="StoredProcs"></a> Procedimentos armazenados que dão suporte a grupos de disponibilidade  
  
-   **sp_redirect_publisher**  
  
     O procedimento armazenado **sp_redirect_publisher** é usado para especificar um publicador redirecionado para um par de publicador/banco de dados existente. Se o banco de dados publicador pertencer a um grupo de disponibilidade, o publicador redirecionado será o nome do ouvinte do grupo de disponibilidade.  
  
-   **sp_get_redirected_publisher**  
  
     O procedimento armazenado **sp_get_redirected_publisher** é usado por agentes de replicação para consultar um distribuidor para determinar se um par de publicador/banco de dados tem um publicador redirecionado definido. Esse procedimento armazenado atende a dois objetivos. Primeiro, permite que o agente determine se o publicador original foi redirecionado. Em segundo lugar, também pode iniciar a execução de um procedimento armazenado de validação no distribuidor (**sp_validate_redirected_publisher**), que verifica a adequação do nó de destino do redirecionamento para servir como um publicador para o banco de dados nomeado.  
  
     Para executar esse procedimento armazenado, o chamador deve ser membro da função de servidor **sysadmin** , da função de banco de dados **db_owner** para o banco de dados de distribuição ou membro de uma **Lista de Acesso à Publicação** para uma publicação definida associada ao banco de dados publicador.  
  
-   **sp_validate_redirected_publisher**  
  
     Este procedimento armazenado tenta validar se o publicador atual pode hospedar o banco de dados publicado. Ele pode ser chamado a qualquer momento para verificar se o host atual do banco de dados publicado pode dar suporte à replicação.  
  
-   **sp_validate_replicate_hosts_as_publishers**  
  
     Embora seja útil para os agentes garantir que o primário atual possa funcionar como o distribuidor de replicação em um banco de dados distribuidor, é necessária uma funcionalidade de validação mais genérica para estabelecer a validade de uma topologia de replicação inteira no banco de dados de disponibilidade AlwaysOn. O procedimento armazenado **sp_validate_replica_hosts_as_publishers** foi criado para atender a essa necessidade.  
  
     Esse procedimento armazenado sempre é executado manualmente. O chamador deve ser **sysadmin** no distribuidor, **dbowner** do banco de dados de distribuição ou membro da **Lista de Acesso à Publicação** de uma publicação do banco de dados publicador. Além disso, o logon do chamador deve ser válido para todos os hosts de réplica de disponibilidade e ter privilégios selecionados no banco de dados de disponibilidade associado ao banco de dados publicador.  
  
###  <a name="CDC"></a> Change Data Capture  
 Os bancos de dados habilitados para CDC (Change Data Capture) podem utilizar o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] para garantir não apenas que o banco de dados permaneça disponível em caso de falha, mas que as alterações nas tabelas de banco de dados continuem sendo monitoradas e depositadas nas tabelas de alterações de CDC. A ordem na qual o CDC e o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] são configurados não é importante. Os bancos de dados habilitados para CDC podem ser adicionados ao [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], e os bancos de dados que são membros de um grupo de disponibilidade AlwaysOn podem ser habilitados para CDC. Porém, nos dois casos, a configuração de CDC sempre é executada na réplica primária atual ou pretendida. O CDC usa o agente de leitor de log e tem as mesmas restrições descritas na seção **Modificações do Agente de Leitor de Log** , apresentada anteriormente neste tópico.  
  
-   **Colhendo alterações para o Change Data Capture sem replicação**  
  
     Se o CDC estiver habilitado para um banco de dados, mas a replicação não estiver, o processo de captura usado para coletar alterações do log e depositá-las nas tabelas de alteração do CDC é executado no host do CDC como seu próprio trabalho do SQL Agent.  
  
     Para retomar a coleta de alterações depois de um failover, o procedimento armazenado **sp_cdc_add_job** deve ser executado no novo primário para criar o trabalho de captura local.  
  
     No exemplo a seguir, é criado o trabalho de captura.  
  
    ```sql  
    EXEC sys.sp_cdc_add_job @job_type = 'capture';  
    ```  
  
-   **Colhendo alterações para o Change Data Capture com replicação**  
  
     Se o CDC e a replicação estiverem habilitados para um banco de dados, o leitor de log tratará da população das tabelas de alteração do CDC. Nesse caso, as técnicas usadas pela replicação para utilizar o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] garantirão que as alterações continuem sendo coletadas no log e depositadas nas tabelas de alteração de CDC após o failover. Não é necessário fazer nada mais para o CDC nesta configuração para garantir que as tabelas de alteração sejam populadas.  
  
-   **Limpeza do Change Data Capture**  
  
     Para garantir que a limpeza apropriada ocorra no novo banco de dados primário, um trabalho de limpeza local sempre deve ser criado. No exemplo a seguir, é criado o trabalho de limpeza.  
  
    ```sql  
    EXEC sys.sp_cdc_add_job @job_type = 'cleanup';  
    ```  
  
    > [!NOTE]  
    >  Você deve criar os trabalhos em todos os destinos de failover possíveis antes do failover e marcá-los como desabilitados até que a réplica de disponibilidade em um host se torne a nova réplica primária. Os trabalhos de CDC em execução no banco de dados primário antigo também devem ser desabilitados quando o banco de dados local se torna um banco de dados secundário. Para desabilitar e habilitar trabalhos, use a opção *@enabled* de [sp_update_job &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md). Para obter mais informações sobre como criar trabalhos de CDC, consulte [sys.sp_cdc_add_job &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md).  
  
-   **Adicionando funções de CDC a uma réplica de banco de dados primário AlwaysOn**  
  
     Quando uma tabela está habilitada para CDC, é possível associar uma função de banco de dados com a instância de captura. Se uma função for especificada, o usuário que quiser usar as funções com valor de tabela do CDC para acessar as alterações para a tabela não somente terá que ter acesso de seleção às colunas de tabela rastreadas, mas também deverá ser um membro da função nomeada. Se a função especificada ainda não existir, a função será criada. Quando as funções de banco de dados são automaticamente adicionadas a um banco de dados primário AlwaysOn, as funções também são propagadas para os bancos de dados secundários do grupo de disponibilidade.  
  
-   **Aplicativos cliente que acessam os dados de alteração do CDC e do AlwaysOn**  
  
     Aplicativos cliente que usam as TVFs (funções com valor de tabela) ou os servidores vinculados para acessar dados da tabela de alteração também precisam da capacidade de localizar um host de CDC apropriado depois do failover. O nome do ouvinte do grupo de disponibilidade é o mecanismo fornecido pelo [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] para permitir que uma conexão sempre seja redirecionada para um host diferente de modo transparente. Quando um nome do gruo de disponibilidade está associado a um grupo de disponibilidade, ele estará disponível para ser usado em cadeias de conexão TCP. Dois cenários de conexão diferentes têm suporte por meio do nome do ouvinte do grupo de disponibilidade.  
  
    -   Um garante que as solicitações de conexão sejam sempre direcionadas para a réplica primária atual.  
  
    -   O outro garante que as solicitações de conexão sejam direcionadas para uma réplica secundária somente leitura.  
  
     Se for usado para localizar uma réplica secundária somente leitura, uma lista de roteamento somente leitura também deverá ser definida para o grupo de disponibilidade. Para obter mais informações sobre roteamento do acesso a secundários legíveis, consulte [Para configurar réplicas de disponibilidade para roteamento somente leitura](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md#ConfigureARsForROR).  
  
    > [!NOTE]  
    >  Há algum atraso de propagação associado à criação de um nome do ouvinte do grupo de disponibilidade e seu uso por aplicativos cliente para acessar uma réplica de banco de dados do grupo de disponibilidade.  
  
     Use a consulta a seguir para determinar se um nome do ouvinte do grupo de disponibilidade foi definido para o grupo de disponibilidade que hospeda um banco de dados do CDC. A consulta retornará o nome do ouvinte do grupo de disponibilidade se ele tiver sido criado.  
  
    ```sql  
    SELECT dns_name   
    FROM sys.availability_group_listeners AS l  
    INNER JOIN sys.availability_databases_cluster AS d  
        ON l.group_id = d.group_id  
    WHERE d.database_name = N'MyCDCDB';  
    ```  
  
-   **Redirecionando a carga de consulta para uma réplica secundária legível**  
  
     Embora, em muitos casos, um aplicativo cliente sempre deseje se conectar à réplica primária atual, essa não é a única maneira de utilizar o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Se um grupo de disponibilidade for configurado para dar suporte a réplicas secundárias legíveis, os dados de alteração também poderão ser coletados a partir de nós secundários.  
  
     Quando um grupo de disponibilidade estiver configurado, o atributo ALLOW_CONNECTIONS associado à SECONDARY_ROLE será usado para especificar o tipo de acesso secundário com suporte. Se tiver sido configurado como ALL, todas as conexões à réplica secundária serão permitidas, mas somente as que exigirem acesso somente leitura terão sucesso. Se estiver configurado como READ_ONLY, será necessário especificar a intenção somente leitura ao estabelecer a conexão com o banco de dados secundário para que a conexão tenha sucesso. Para obter mais informações, consulte [Configurar o acesso somente leitura em uma réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md).  
  
     A consulta a seguir pode ser usada para determinar se a intenção somente leitura é necessária para estabelecer a conexão com uma réplica secundária legível.  
  
    ```sql  
    SELECT g.name AS AG, replica_server_name, secondary_role_allow_connections_desc  
    FROM sys.availability_replicas AS r  
    JOIN sys.availability_groups AS g  
        ON r.group_id = g.group_id  
    WHERE g.name = N'MY_AG_NAME;  
    ```  
  
     O nome do ouvinte do grupo de disponibilidade ou o nome de nó explícito pode ser usado para localizar a réplica secundária. Se o nome do ouvinte do grupo de disponibilidade for usado, o acesso será direcionado a qualquer réplica secundária adequada.  
  
     Quando **sp_addlinkedserver** é usado para criar um servidor vinculado para acessar o secundário, o parâmetro *@datasrc* é usado para o nome do ouvinte do grupo de disponibilidade ou o nome do servidor explícito e o parâmetro *@provstr* é usado para especificar intenção somente leitura.  
  
    ```sql  
    EXEC sp_addlinkedserver   
    @server = N'linked_svr',   
    @srvproduct=N'SqlServer',  
    @provider=N'SQLNCLI11',   
    @datasrc=N'AG_Listener_Name',   
    @provstr=N'ApplicationIntent=ReadOnly',   
    @catalog=N'MY_DB_NAME';  
    ```  
  
-   **Acesso de cliente aos dados de alteração do CDC e logons de domínio**  
  
     Em geral, você deve usar logons de domínio para acesso de cliente para dados de alteração que residem em bancos de dados que são membros de grupos de disponibilidade AlwaysOn. Para garantir o acesso continuado aos dados de alteração após o failover, o usuário de domínio precisará ter privilégios de acesso em todos os hosts que dão suporte a réplicas do grupo de disponibilidade. Se um usuário de banco de dados for adicionado a um banco de dados em uma réplica primária, e o usuário estiver associado com um logon de domínio, o usuário de banco de dados será propagado para bancos de dados secundários e continua sendo associado com o logon de domínio especificado. Se o novo usuário de banco de dados estiver associado com um logon de autenticação do SQL Server, o usuário nos bancos de dados secundários será propagado sem um logon. Embora o logon de autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] associado pudesse ser usado para acessar dados de alteração no primário onde o usuário de banco de dados foi definido originalmente, esse nó é o único em que o acesso seria possível. O logon de autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não poderia acessar dados de qualquer banco de dados secundário, nem de nenhum novo banco de dados primário além do banco de dados original onde o usuário de banco de dados foi definido.  
     
-   **Desabilitando o Change Data Capture**  
Se o Change Data Capture precisar ser desabilitado em um banco de dados que faz parte de um Grupo de Disponibilidade AlwaysOn, você precisará realizar etapas adicionais para garantir que o truncamento de log não seja afetado. Você precisará implementar uma das seguintes etapas para evitar que o Change Data Capture bloqueie o truncamento de log depois de desabilitar o Change Data Capture:
    - Reiniciar o serviço SQL Server em cada instância da réplica secundária
    - OU remover o banco de dados de todas as instâncias da réplica secundária do Grupo de Disponibilidade e adicioná-lo às instâncias da réplica do Grupo de Disponibilidade usando a propagação automática ou manual
  
###  <a name="CT"></a> Controle de alterações  
 Um banco de dados habilitado para CT (controle de alterações) pode fazer parte de um grupo de disponibilidade AlwaysOn. Nenhuma configuração adicional é necessária. Os aplicativos cliente de controle de alterações que usam as TVFs (funções com valor de tabela) de CDC para acessar dados de alteração também precisarão localizar a réplica primária após o failover. Se o aplicativo cliente é conectado por meio do nome do ouvinte do grupo de disponibilidade, as solicitações de conexão serão sempre direcionadas corretamente para a réplica primária atual.  
  
> [!NOTE]  
>  Os dados de controle de alterações sempre devem ser obtidos da réplica primária. Uma tentativa para acessar dados de alteração de uma réplica secundária resultará no seguinte erro:  
>   
>  Msg 22117, Nível 16, Estado 1, Linha 1  
>   
>  Não há suporte para o controle de alterações nos bancos de dados que são membros de uma réplica secundária (ou seja, para bancos de dados secundários). Execute consultas de controle de alterações nos bancos de dados na réplica primária.  
  
##  <a name="Prereqs"></a> Pré-requisitos, restrições e considerações para usar replicação  
 Esta seção descreve as considerações para implantar a replicação com o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], incluindo pré-requisitos, restrições e recomendações.  
  
### <a name="prerequisites"></a>Prerequisites  
  
-   Ao usar a replicação transacional e o banco de dados de publicação estiver em um grupo de disponibilidade, o publicador e o distribuidor devem executar pelo menos o [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]. O assinante pode usar um nível inferior do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Ao usar a replicação de mesclagem e o banco de dados de publicação estiver em um grupo de disponibilidade:  
  
    -   Assinatura push: o publicador e o distribuidor devem executar pelo menos o [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
    -   Assinatura pull: o publicador, o distribuidor e os bancos de dados do assinante devem estar pelo menos no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]. Isso ocorre porque o agente de mesclagem no assinante deve entender como um grupo de disponibilidade pode fazer failover para seu secundário.  
  
-   As instâncias do Publicador satisfazem todos os pré-requisitos necessários para participar de um grupo de disponibilidade AlwaysOn. Para obter mais informações consulte [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
### <a name="restrictions"></a>Restrictions  
 Combinações de replicação com suporte no [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]:  
  
|||||  
|-|-|-|-|  
||**Publicador**|**Distribuidor***\*|**Assinante**|  
|**Transacional.**|Sim<br /><br /> Observação: não inclui suporte para replicação transacional bidirecional e recíproca.|não|Sim|  
|**P2P**|não|não|não|  
|**Mesclagem**|Sim|não|Sim*|  
|**Instantâneo**|Sim|não|Sim*|  
  
 *O failover no banco de dados de réplica é um procedimento manual. O failover automático não é fornecido.  
  
 **Não há suporte para o uso do banco de dados de distribuidor com espelhamento de banco de dados.  
  
### <a name="considerations"></a>Considerações  
  
-   Não há suporte para o uso do banco de dados de distribuição com o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] ou espelhamento de banco de dados. A configuração da replicação é acoplada à instância do SQL Server onde o Distribuidor é configurado. Portanto, o banco de dados de distribuição não pode ser espelhado ou replicado. Para fornecer alta disponibilidade para o Distribuidor, use um cluster de failover do SQL Server. Para obter mais informações, consulte [Instâncias do cluster de failover do AlwaysOn &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).  
  
-   Embora haja suporte para o failover do assinante em um banco de dados secundário, esse é um procedimento manual para assinantes de replicação de mesclagem. O procedimento é essencialmente idêntico ao método usado para failover de um banco de dados de assinante espelhado. Assinantes de replicação transacional não precisam de tratamento especial durante a participação no [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Os assinantes devem estar executando o [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] ou posterior para participar de um grupo de disponibilidade.  Para obter mais informações, consulte [Assinantes de replicação e Grupos de Disponibilidade AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/replication-subscribers-and-always-on-availability-groups-sql-server.md)
  
-   Os metadados e os objetos que existem fora do banco de dados não são propagados para as réplicas secundárias, inclusive logons, trabalhos, servidores vinculados. Se você precisar dos metadados e dos objetos no novo banco de dados primário após o failover, copie-os manualmente. Para obter mais informações, consulte [Gerenciamento de logons e trabalhos para os bancos de dados de um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/logins-and-jobs-for-availability-group-databases.md).  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Replicação**  
  
-   [Configurar a replicação para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-replication-for-always-on-availability-groups-sql-server.md)  
  
-   [Mantendo um banco de dados de publicação AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/maintaining-an-always-on-publication-database-sql-server.md)  
  
-   [Administração &#40;Replicação&#41;](../../../relational-databases/replication/administration/administration-replication.md)  
  
 **Change data capture**  
  
-   [Habilitar e desabilitar a captura de dados de alterações &#40;SQL Server&#41;](../../../relational-databases/track-changes/enable-and-disable-change-data-capture-sql-server.md)  
  
-   [Administrar e monitorar a captura de dados de alteração &#40;SQL Server&#41;](../../../relational-databases/track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
-   [Trabalhar com dados de alterações &#40;SQL Server&#41;](../../../relational-databases/track-changes/work-with-change-data-sql-server.md)  
  
 **Change tracking**  
  
-   [Habilitar e desabilitar o controle de alterações &#40;SQL Server&#41;](../../../relational-databases/track-changes/enable-and-disable-change-tracking-sql-server.md)  
  
-   [Gerenciar o controle de alterações &#40;SQL Server&#41;](../../../relational-databases/track-changes/manage-change-tracking-sql-server.md)  
  
-   [Trabalhar com o controle de alterações &#40;SQL Server&#41;](../../../relational-databases/track-changes/work-with-change-tracking-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Assinantes de replicação e grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/replication-subscribers-and-always-on-availability-groups-sql-server.md)   
 [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)   
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Grupos de Disponibilidade AlwaysOn: Interoperabilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)   
 [Instâncias de cluster de failover do AlwaysOn &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)   
 [Sobre a captura de dados de alterações &#40;SQL Server&#41;](../../../relational-databases/track-changes/about-change-data-capture-sql-server.md)   
 [Sobre o controle de alterações &#40;SQL Server&#41;](../../../relational-databases/track-changes/about-change-tracking-sql-server.md)   
 [Replicação do SQL Server](../../../relational-databases/replication/sql-server-replication.md)   
 [Controle de alterações de dados &#40;SQL Server&#41;](../../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [sys.sp_cdc_add_job &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)  
  
  
