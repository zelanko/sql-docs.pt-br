---
title: CREATE AVAILABILITY GROUP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- AVAILABILITY GROUP
- CREATE_AVAILABILITY_TSQL
- CREATE_AVAILABILITY_GROUP_TSQL
- CREATE AVAILABILITY GROUP
- CREATE AVAILABILITY
- AVAILABILITY_GROUP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
- CREATE AVAILABILITY GROUP statement
- Availability Groups [SQL Server], creating
- Availability Groups [SQL Server], Transact-SQL statements
ms.assetid: a3d55df7-b4e4-43f3-a14b-056cba36ab98
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b52f9aa0131639bdfe68222bba42eae774d2b18f
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51698325"
---
# <a name="create-availability-group-transact-sql"></a>CREATE AVAILABILITY GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Cria um novo grupo de disponibilidade, se a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for habilitada para o recurso [!INCLUDE[ssHADR](../../includes/sshadr-md.md)].  
  
> [!IMPORTANT]  
>  Execute CREATE AVAILABILITY GROUP na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que você pretende usar como a réplica primária inicial de seu novo grupo de disponibilidade. Essa instância de servidor deve residir em um nó WSFC (Windows Server Failover Clustering).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```SQL  
  
CREATE AVAILABILITY GROUP group_name  
   WITH (<with_option_spec> [ ,...n ] )  
   FOR [ DATABASE database_name [ ,...n ] ]  
   REPLICA ON <add_replica_spec> [ ,...n ]  
   AVAILABILITY GROUP ON <add_availability_group_spec> [ ,...2 ]  
   [ LISTENER ‘dns_name’ ( <listener_option> ) ]  
[ ; ]  
  
<with_option_spec>::=   
    AUTOMATED_BACKUP_PREFERENCE = { PRIMARY | SECONDARY_ONLY| SECONDARY | NONE }  
  | FAILURE_CONDITION_LEVEL  = { 1 | 2 | 3 | 4 | 5 }   
  | HEALTH_CHECK_TIMEOUT = milliseconds  
  | DB_FAILOVER  = { ON | OFF }   
  | DTC_SUPPORT  = { PER_DB | NONE }  
  | BASIC  
  | DISTRIBUTED
  | REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT = { integer }
  | CLUSTER_TYPE = { WSFC | EXTERNAL | NONE } 
  
<add_replica_spec>::=  
  <server_instance> WITH  
    (  
       ENDPOINT_URL = 'TCP://system-address:port',  
       AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT | CONFIGURATION_ONLY },  
       FAILOVER_MODE = { AUTOMATIC | MANUAL | EXTERNAL }  
       [ , <add_replica_option> [ ,...n ] ]  
    )   
  
  <add_replica_option>::=  
       SEEDING_MODE = { AUTOMATIC | MANUAL }  
     | BACKUP_PRIORITY = n  
     | SECONDARY_ROLE ( {   
            [ ALLOW_CONNECTIONS = { NO | READ_ONLY | ALL } ]   
        [,] [ READ_ONLY_ROUTING_URL = 'TCP://system-address:port' ]  
     } )  
     | PRIMARY_ROLE ( {   
            [ ALLOW_CONNECTIONS = { READ_WRITE | ALL } ]   
        [,] [ READ_ONLY_ROUTING_LIST = { ( ‘<server_instance>’ [ ,...n ] ) | NONE } ]  
        [,] [ READ_WRITE_ROUTING_URL = { ( ‘<server_instance>’ ) ] 
     } )  
     | SESSION_TIMEOUT = integer  
  
<add_availability_group_spec>::=  
 <ag_name> WITH  
    (  
       LISTENER_URL = 'TCP://system-address:port',  
       AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT },  
       FAILOVER_MODE = MANUAL,  
       SEEDING_MODE = { AUTOMATIC | MANUAL }  
    )  
  
<listener_option> ::=  
   {  
      WITH DHCP [ ON ( <network_subnet_option> ) ]  
    | WITH IP ( { ( <ip_address_option> ) } [ , ...n ] ) [ , PORT = listener_port ]  
   }  
  
  <network_subnet_option> ::=  
     ‘four_part_ipv4_address’, ‘four_part_ipv4_mask’    
  
  <ip_address_option> ::=  
     {   
        ‘four_part_ipv4_address’, ‘four_part_ipv4_mask’  
      | ‘ipv6_address’  
     }  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *group_name*  
 Especifica o nome do novo grupo de disponibilidade. *group_name* deve ser um [identificador](../../relational-databases/databases/database-identifiers.md) válido do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e deve ser exclusivo em todos os grupos de disponibilidade no cluster WSFC. O tamanho máximo de um nome de grupo de disponibilidade é 128 caracteres.  
  
 AUTOMATED_BACKUP_PREFERENCE **=** { PRIMARY | SECONDARY_ONLY| SECONDARY | NONE }  
 Especifica uma preferência sobre como um trabalho de backup deve avaliar a réplica primária ao escolher onde executar backups. Você pode criar um script de um determinado trabalho de backup para considerar a preferência de backup automatizada. É importante entender que a preferência não é imposta pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], portanto, não tem nenhum impacto em backups ad hoc.  
  
 Os valores com suporte são os seguintes:  
  
 PRIMARY  
 Especifica que os backups sempre devem ocorrer na réplica primária. Essa opção será útil se você precisar de recursos de backup, como a criação de backups diferenciais, que não têm suporte quando o backup é executado em uma réplica secundária.  
  
> [!IMPORTANT]  
>  Se você pretende usar o envio de logs para preparar qualquer banco de dados secundário para um grupo de disponibilidade, defina a preferência de backup automatizada como **Primário** até que todos os bancos de dados secundários estejam preparados e associados ao grupo de disponibilidade.  
  
 SECONDARY_ONLY  
 Especifica que os backups nunca devem ser executados na réplica primária. Se a réplica primária for a única réplica online, o backup não deveria ocorrer.  
  
 SECONDARY  
 Especifica que os backups devem ocorrer em uma réplica secundária, exceto quando a réplica primária for a única réplica online. Nesse caso, o backup deve ocorrer na réplica primária. Esse é o comportamento padrão.  
  
 Nenhuma  
 Especifica que você prefere que trabalhos de backup ignorem a função das réplicas de disponibilidade ao escolher a réplica para executar backups. Observe que os trabalhos de backup podem avaliar outros fatores, como prioridade de backup de cada réplica de disponibilidade em combinação com seu estado operacional e estado conectado.  
  
> [!IMPORTANT]  
>  Não há nenhuma imposição da configuração AUTOMATED_BACKUP_PREFERENCE. A interpretação dessa preferência depende da lógica, se houver, que você usa para o script em trabalhos de backup para os bancos de dados em um determinado grupo de disponibilidade. A configuração de preferência de backup automatizado não tem efeito sobre backups ad hoc. Para obter mais informações, consulte [Configurar o backup em réplicas de disponibilidade &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md).  
  
> [!NOTE]  
>  Para exibir a preferência de backup automatizada de um grupo de disponibilidade existente, selecione a coluna **automated_backup_preference** ou **automated_backup_preference_desc** da exibição do catálogo [sys.availability_groups](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md). Além disso, [sys.fn_hadr_backup_is_preferred_replica &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md) pode ser usado para determinar a réplica de backup preferencial.  Essa função sempre retorna 1 para, pelo menos, uma das réplicas, mesmo quando `AUTOMATED_BACKUP_PREFERENCE = NONE`.  
  
 FAILURE_CONDITION_LEVEL **=** { 1 | 2 | **3** | 4 | 5 }  
 Especifica quais condições de falha disparam um failover automático para esse grupo de disponibilidade. FAILURE_CONDITION_LEVEL é definido no nível do grupo, mas só é relevante em réplicas de disponibilidade configuradas para o modo de disponibilidade de confirmação síncrona (AVAILIBILITY_MODE **=** SYNCHRONOUS_COMMIT). Além disso, as condições de falha apenas poderão disparar um failover automático se as réplicas primária e secundária estiverem configuradas para o modo de failover automático (FAILOVER_MODE **=** AUTOMATIC) e a réplica secundária estiver sincronizada com a réplica primária no momento.  
  
 Os níveis da condição de falha (1 a 5) variam do menos restritivo, nível 1, até o mais restritivo, nível 5. Um determinado nível de condição abrange todos os níveis menos restritivos. Assim, o nível de condição mais rígido, 5, inclui os quatro níveis de condição menos restritivos (1 a 4), o nível 4 inclui os níveis 1 a 3 e assim sucessivamente. A tabela a seguir descreve a condição de falha que corresponde a cada nível.  
  
|Nível|Condição de falha|  
|-----------|-----------------------|  
|1|Especifica que um failover automático deverá ser iniciado quando uma destas condições ocorrer:<br /><br /> - O serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está inativo.<br /><br /> - A concessão do grupo de disponibilidade para conexão com o cluster WSFC expira porque nenhum ACK foi recebido da instância de servidor. Para obter mais informações, veja [Como funciona o tempo limite de concessão de AlwaysOn do SQL Server](https://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-AlwaysOn-lease-timeout.aspx).|  
|2|Especifica que um failover automático deverá ser iniciado quando uma destas condições ocorrer:<br /><br /> - A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não se conecta ao cluster e o limite de HEALTH_CHECK_TIMEOUT especificado pelo usuário do grupo de disponibilidade é excedido.<br /><br /> - A réplica de disponibilidade está em um estado com falha.|  
|3|Especifica que um failover automático deve ser iniciado em erros internos críticos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como spinlocks órfãos, violações do acesso de gravação graves ou muito descarte.<br /><br /> Esse é o comportamento padrão.|  
|4|Especifica que um failover automático deve ser iniciado em caso de erros internos moderados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como uma condição de memória insuficiente persistente no pool de recursos interno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|5|Especifica que um failover automático deve ser iniciado em qualquer condição de falha qualificada, incluindo:<br /><br /> - Esgotamento dos threads de trabalho do SQL Engine.<br /><br /> - Detecção de um deadlock insolúvel.|  
  
> [!NOTE]  
>  A falta de resposta por uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para solicitações cliente não é relevante para grupos de disponibilidade.  
  
 Os valores FAILURE_CONDITION_LEVEL e HEALTH_CHECK_TIMEOUT definem uma *política de failover flexível* para determinado grupo. Essa política de failover flexível permite a você um controle granular sobre quais condições devem causar um failover automático. Para obter mais informações, consulte [Política de failover flexível para failover automático de um grupo de disponibilidade &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/flexible-automatic-failover-policy-availability-group.md).  
  
 HEALTH_CHECK_TIMEOUT **=** *milissegundos*  
 Especifica o tempo de espera (em milissegundos) para que o procedimento armazenado do sistema [sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) retorne informações da integridade do servidor antes de o cluster WSFC supor que a instância do servidor está lenta ou travou. HEALTH_CHECK_TIMEOUT é definido no nível do grupo, mas é apenas relevante em réplicas de disponibilidade configuradas para o modo de disponibilidade de confirmação síncrona com failover automático (AVAILIBILITY_MODE **=** SYNCHRONOUS_COMMIT).  Além disso, o tempo limite da verificação de integridade apenas poderá disparar um failover automático se as réplicas primárias e secundárias estiverem configuradas para o modo de failover automático (FAILOVER_MODE **=** AUTOMATIC) e a réplica secundária estiver sincronizada com a réplica primária no momento.  
  
 O valor HEALTH_CHECK_TIMEOUT padrão é 30.000 milissegundos (30 segundos). O valor mínimo é 15000 milissegundos (15 segundos) e o máximo é 4294967295 milissegundos.  
  
> [!IMPORTANT]  
>  **sp_server_diagnostics** não realiza verificações de integridade no nível de banco de dados.  
  
 DB_FAILOVER **=** { ON | OFF }  
 Especifica a resposta a ser usada quando um banco de dados na réplica primária estiver offline. Quando estiver definida como ON, qualquer status diferente de ONLINE para um banco de dados no grupo de disponibilidade disparará um failover automático. Quando essa opção estiver definida como OFF, somente a integridade da instância será usada para disparar um failover automático.  
  
  Para obter mais informações sobre essa configuração, consulte [Opção de detecção de integridade no nível do banco de dados](../../database-engine/availability-groups/windows/sql-server-always-on-database-health-detection-failover-option.md) 
  
 DTC_SUPPORT **=** { PER_DB | NONE }  
 Especifica se há compatibilidade com transações entre bancos de dados por meio do DTC (coordenador de transações distribuídas). Há compatibilidade com transações entre bancos de dados apenas começando pelo [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. PER_DB cria o grupo de disponibilidade com suporte para essas transações. Para obter mais informações, consulte [Transações entre bancos de dados e transações distribuídas para espelhamento de banco de dados e grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md).  
  
 BÁSICA  
 Usado para criar um grupo de disponibilidade básico. Grupos de disponibilidade básicos são limitados a um banco de dados e duas réplicas: uma réplica primária e uma réplica secundária. Essa opção é uma substituição para o recurso de espelhamento de banco de dados preterido no SQL Server Standard Edition. Para obter mais informações, consulte [Grupos de disponibilidade básicos &#40;Grupos de Disponibilidade AlwaysOn&#41;](../../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md). Há compatibilidade com grupos de disponibilidade básicos do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] em diante.  

 DISTRIBUTED  
 Usado para criar um grupo de disponibilidade distribuído. Essa opção é usada com o parâmetro AVAILABILITY GROUP ON para conectar dois grupos de disponibilidade em Clusters de Failover do Windows Server separados.  Para obter mais informações, veja [Grupos de disponibilidade distribuídos e &#40;Grupos de disponibilidade AlwaysOn&#41;](../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md). Há compatibilidade com grupos de disponibilidade distribuídos do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] em diante. 

 REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT   
 Introduzida no SQL Server 2017. Usada para definir um número mínimo de réplicas secundárias síncronas que devem ser confirmadas antes que o primário confirme uma transação. Garante que a transação do SQL Server aguarde até que os logs de transações sejam atualizados no número mínimo de réplicas secundárias. O padrão é 0, que fornece o mesmo comportamento que o SQL Server 2016. O valor mínimo é 0. O valor máximo é o número de réplicas menos 1. Essa opção está relacionada com as réplicas no modo de confirmação síncrona. Quando as réplicas estão no modo de confirmação síncrona, as gravações na réplica primária aguardam até que as gravações nas réplicas síncronas secundárias sejam confirmadas no log de transações do banco de dados de réplica. Se um SQL Server que hospeda uma réplica síncrona secundária parar de responder, o SQL Server que hospeda a réplica primária marcará essa réplica secundária como NOT SYNCHRONIZED e continuará. Quando o banco de dados que não estava respondendo volta a ficar online, ele fica em um estado "não sincronizado" e a réplica é marcada como não íntegra até que o primário possa torná-la síncrona novamente. Essa configuração garante que a réplica primária aguarda até que o número mínimo de réplicas confirme cada transação. Se o número mínimo de réplicas não estiver disponível, as confirmações no primário falharão. Para o tipo de cluster `EXTERNAL`, a configuração é alterada quando o grupo de disponibilidade é adicionado a um recurso de cluster. Consulte [Alta disponibilidade e proteção de dados para as configurações de grupo de disponibilidade](../../linux/sql-server-linux-availability-group-ha.md).

 CLUSTER_TYPE  
 Introduzida no SQL Server 2017. Usado para identificar se o grupo de disponibilidade está em um WSFC (Cluster de Failover do Windows Server).  Definido como WSFC quando o grupo de disponibilidade está em uma instância de cluster de failover em um cluster de failover do Windows Server. Definido como EXTERNAL quando o cluster é gerenciado por um gerenciador de cluster que não é um cluster de failover do Windows Server, como o Linux Pacemaker. Definido como NONE quando o grupo de disponibilidade não usa o WSFC para a coordenação de cluster. Por exemplo, quando um grupo de disponibilidade inclui servidores Linux sem nenhum gerenciador de cluster. 

 DATABASE *database_name*  
 Especifica uma lista de um ou mais bancos de dados de usuário na instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (isto é, a instância de servidor na qual você está criando o grupo de disponibilidade). É possível especificar vários bancos de dados para um grupo de disponibilidade, mas cada banco de dados pode pertencer a apenas um grupo de disponibilidade. Para obter informações sobre os tipos de bancos de dados compatíveis com um grupo de disponibilidade, consulte [Pré-requisitos, restrições e recomendações para Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md). Para descobrir quais bancos de dados locais já pertencem a um grupo de disponibilidade, consulte a coluna **replica_id** na exibição do catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  
  
 A cláusula DATABASE é opcional. Se você a omitir, o novo grupo de disponibilidade estará vazio.  
  
 Depois de criar o grupo de disponibilidade, conecte-se a cada instância de servidor que hospeda uma réplica secundária e, em seguida, preparar cada banco de dados secundário e ingressá-lo ao grupo de disponibilidade. Para obter mais informações, veja [Iniciar movimentação de dados em um banco de dados secundário &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md).  
  
> [!NOTE]  
>  Posteriormente, você pode adicionar bancos de dados qualificados na instância do servidor que hospedam a réplica primária atual em um grupo de disponibilidade. Você também pode remover um banco de dados de um grupo de disponibilidade. Para obter mais informações, consulte [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md).  
  
 REPLICA ON  
 Especifica de uma a cinco instâncias do SQL Server para hospedar réplicas de disponibilidade no novo grupo de disponibilidade.  Cada réplica é especificada por seu endereço de instância de servidor seguido por uma cláusula WITH (...). No mínimo, é necessário especificar a instância de servidor local, que se torna a réplica primária inicial. Opcionalmente, você também pode especificar até quatro réplicas secundárias.  
  
 É necessário unir cada réplica secundária ao grupo de disponibilidade. Para obter mais informações, consulte [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md).  
  
> [!NOTE]  
>  Se você especificar menos de quatro réplicas secundárias ao criar um grupo de disponibilidade, poderá criar uma réplica secundária adicional a qualquer momento por meio da instrução [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)]. Também é possível usar essa instrução para remover qualquer réplica secundária de um grupo de disponibilidade existente.  
  
 \<server_instance> Especifica o endereço da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que é o host de uma réplica. O formato de endereço depende se a instância é a instância padrão ou uma instância nomeada, e se é uma instância autônoma ou uma instância de cluster de failover (FCI), da seguinte maneira:  
  
 { '*system_name*[\\*instance_name*]' | '*FCI_network_name*[\\*instance_name*]' }  
  
 Os componentes desse endereço são os seguintes:  
  
 *system_name*  
 É o nome NetBIOS do computador do sistema no qual reside uma instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esse computador deve ser um nó WSFC.  
  
 *FCI_network_name*  
 É o nome da rede usada para acessar um cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Use-o se a instância de servidor participar como um parceiro de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Executar SELECT [@@SERVERNAME](../../t-sql/functions/servername-transact-sql.md) em uma instância de servidor FCI retorna a cadeia de caracteres '*FCI_network_name*[\\*instance_name*]' inteira (que é o nome completo da réplica).  
  
 *instance_name*  
 É o nome de uma instância de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que é hospedada por *system_name* ou *FCI_network_name* e que tem o serviço HADR habilitado. Para uma instância de servidor padrão, *instance_name* é opcional. O nome da instância não diferencia maiúsculas de minúsculas. Em uma instância de servidor autônomo, esse nome de valor é igual ao valor retornado pela execução de SELECT [@@SERVERNAME](../../t-sql/functions/servername-transact-sql.md).  
  
 \  
 É um separador usado apenas ao especificar *instance_name* para separá-lo de *system_name* ou de *FCI_network_name*.  
  
 Para obter informações sobre os pré-requisitos para nós WSFC e instâncias de servidor, consulte [Pré-requisitos, restrições e recomendações para Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
 ENDPOINT_URL **='** TCP **://**_system-address_**:**_port_**'**  
 Especifica o caminho da URL para o [ponto de extremidade de espelhamento de banco de dados](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md) na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda a réplica de disponibilidade que está sendo definida na cláusula REPLICA ON atual.  
  
 A cláusula ENDPOINT_URL é necessária. Para obter mais informações, consulte [Especificar a URL do ponto de extremidade ao adicionar ou modificar uma réplica de disponibilidade &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md).  
  
 **'** TCP **://**_system-address_**:**_port_**'**  
 Especifica uma URL para especificar uma URL de ponto de extremidade ou URL de roteamento somente leitura. Os parâmetros de URL são os seguintes:  
  
 *system-address*  
 É uma cadeia de caracteres, como um nome de sistema, um nome de domínio totalmente qualificado ou um endereço IP, que identifica de forma exclusiva o sistema do computador de destino.  
  
 *port*  
 É um número da porta associado ao ponto de extremidade de espelhamento da instância do servidor parceiro (para a opção ENDPOINT_URL) ou o número da porta usado pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)] da instância de servidor (para a opção READ_ONLY_ROUTING_URL).  
  
 AVAILABILITY_MODE **=** { {SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT | CONFIGURATION_ONLY }  
 SYNCHRONOUS_COMMIT ou ASYNCHRONOUS_COMMIT especifica se a réplica primária precisa aguardar a réplica secundária confirmar a proteção (gravação) dos registros de log em disco antes que a réplica primária possa confirmar a transação em determinado banco de dados primário. As transações em bancos de dados diferentes na mesma réplica primária podem ser confirmadas independentemente. O SQL Server 2017 CU 1 introduz CONFIGURATION_ONLY. A réplica de CONFIGURATION_ONLY apenas se aplica a grupos de disponibilidade com CLUSTER_TYPE = EXTERNAL ou CLUSTER_TYPE = NONE. 
  
 SYNCHRONOUS_COMMIT  
 Especifica que a réplica primária aguardará para confirmar as transações até que elas tenham sido protegidas nessa réplica secundária (modo de confirmação síncrona). Você pode especificar SYNCHRONOUS_COMMIT para até três réplicas, inclusive a réplica primária.  
  
 ASYNCHRONOUS_COMMIT  
 Especifica se a réplica primária confirma transações sem esperar que essa réplica secundária fortaleça o log (modo de disponibilidade de confirmação síncrona). Você pode especificar ASYNCHRONOUS_COMMIT para até cinco réplicas de disponibilidade, inclusive a réplica primária.  

 CONFIGURATION_ONLY Especifica que a réplica primária confirma de forma síncrona os metadados de configuração do grupo de disponibilidade no banco de dados mestre dessa réplica. A réplica não conterá dados de usuário. Essa opção:

- Pode ser hospedada em qualquer edição do SQL Server, inclusive a Express Edition.
- Requer que o ponto de extremidade de espelhamento de dados da réplica de CONFIGURATION_ONLY seja do tipo `WITNESS`.
- Não pode ser alterada.
- É inválida quando `CLUSTER_TYPE = WSFC`. 

   Para obter mais informações, consulte [Réplica somente configuração](../../linux/sql-server-linux-availability-group-ha.md).
  
 A cláusula AVAILABILITY_MODE é necessária. Para obter mais informações, consulte [Modos de disponibilidade &#40;Grupos de disponibilidade AlwaysOn&#41;](../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md).  
  
 FAILOVER_MODE **=** { AUTOMATIC | MANUAL }  
 Especifica o modo de disponibilidade da réplica de disponibilidade que você está definindo.  
  
 AUTOMATIC  
 Permite o failover automático. Esta opção só terá suporte se você também especificar AVAILABILITY_MODE = SYNCHRONOUS_COMMIT. Você pode especificar AUTOMATIC para duas réplicas de disponibilidade, inclusive a réplica primária.  
  
> [!NOTE]  
>  As FCIs (Instâncias de cluster de failover) do SQL Server não dão suporte ao failover automático por grupos de disponibilidade, de modo que qualquer réplica de disponibilidade que esteja hospedado por um FCI só pode ser configurada para failover manual.  
  
 MANUAL  
 Habilita o failover manual planejado ou o failover manual forçado (em geral, chamado *failover forçado*) pelo administrador de banco de dados.  
  
 A cláusula FAILOVER_MODE é necessária. Os dois tipos de failover manual - failover manual sem perda de dados e failover forçado (com possível perda de dados) - têm suporte em condições diferentes. Para obter mais informações, consulte [Failover e modos de failover &#40;grupos de disponibilidade AlwaysOn&#41;](../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md).  
  
 SEEDING_MODE **=** { AUTOMATIC | MANUAL }  
 Especifica como a réplica secundária é inicialmente propagada.  
  
 AUTOMATIC  
 Habilita a propagação direta. Esse método propaga a réplica secundária na rede. Esse método não exige que você faça backup e restauração de uma cópia do banco de dados primário na réplica.  
  
> [!NOTE]  
>  Para a propagação direta, é necessário permitir a criação de banco de dados em cada réplica secundária chamando **ALTER AVAILABILITY GROUP** com a opção **GRANT CREATE ANY DATABASE**.  
  
 MANUAL  
 Especifica a propagação manual (padrão). Esse método requer que você crie um backup do banco de dados na réplica primária e restaure manualmente esse backup na réplica secundária.  
  
 BACKUP_PRIORITY **=** *n*  
 Especifica sua prioridade para executar backups nesta réplica em relação às outras réplicas no mesmo grupo de disponibilidade. O valor é um número inteiro no intervalo de 0..100. Esses valores têm estes significados:  
  
-   1..100 indica que a réplica de disponibilidade pode ser escolhida para executar backups. 1 indica a prioridade mais baixa, e 100 indica a prioridade mais alta. Se BACKUP_PRIORITY = 1, a réplica de disponibilidade será escolhida para só executar backups se nenhuma réplica de disponibilidade de prioridade mais alta estiver atualmente disponível.  
  
-   0 indica que essa réplica de disponibilidade não se destina a executar backups. Isso é útil, por exemplo, para uma réplica de disponibilidade remota para a qual você nunca deseja que ocorra o failover de backups.  
  
 Para obter mais informações, consulte [Secundárias ativas: backup em réplicas secundárias &#40;Grupos de Disponibilidade AlwaysOn&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md).  
  
 SECONDARY_ROLE **(**… **)**  
 Especifica as configurações específicas à função que terão efeito se, atualmente, essa réplica de disponibilidade for o proprietário da função secundária (ou seja, sempre que ela for uma réplica secundária). Dentro dos parênteses, especifique uma ou ambas as opções de função secundária. Se você especificar ambas, use uma lista separada por vírgulas.  
  
 As opções de função secundária são as seguintes:  
  
 ALLOW_CONNECTIONS **=** { NO | READ_ONLY | ALL }  
 Especifica se os bancos de dados de uma determinada réplica de disponibilidade que está executando a função primária (isto é, está atuando como uma réplica secundária) podem aceitar conexões de clientes. Pode ser:  
  
 NO  
 Nenhuma conexão de usuário é permitida para bancos de dados secundários desta réplica. Eles não estão disponíveis para acesso de leitura. Esse é o comportamento padrão.  
  
 READ_ONLY  
 Apenas conexões são permitidas com os bancos de dados na réplica secundária em que a propriedade Application Intent está definida como **ReadOnly**. Para obter mais informações sobre essa propriedade, consulte [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 ALL  
 Todas as conexões são permitidas com os bancos de dados na réplica secundária para acesso somente leitura.  
  
 Para obter mais informações, consulte [Secundárias ativas: réplicas secundárias legíveis &#40;Grupos de Disponibilidade AlwaysOn&#41;](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).  
  
 READ_ONLY_ROUTING_URL **='** TCP **://**_system-address_**:**_port_**'**  
 Especifica a URL a ser usada para rotear solicitações de conexão de intenção de leitura para esta réplica de disponibilidade. Esta é a URL na qual o Mecanismo de Banco de Dados do SQL Server escuta. Normalmente, a instância padrão do Mecanismo de Banco de Dados do SQL Server escuta na porta TCP 1433.  
  
 Para uma instância nomeada, você pode obter o número da porta consultando as colunas **port** e **type_desc** da exibição de gerenciamento dinâmico [sys.dm_tcp_listener_states](../../relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql.md). A instância do servidor usa o ouvinte Transact-SQL (**type_desc='TSQL'**).  
  
 Para obter mais informações sobre como calcular a URL de roteamento somente leitura de uma réplica, consulte [Calculando read_only_routing_url para o Always On](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-AlwaysOn.aspx).  
  
> [!NOTE]  
>  Para uma instância nomeada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o ouvinte do Transact-SQL deve ser configurado para usar uma porta específica. Para obter mais informações, veja [Configurar um servidor para escuta em uma porta TCP específica &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md).  
  
 PRIMARY_ROLE **(** … **)**  
 Especifica as configurações específicas à função que terão efeito se, atualmente, essa réplica de disponibilidade for o proprietário da função primária (ou seja, sempre que ela for a réplica primária). Dentro dos parênteses, especifique uma ou ambas as opções de função primária. Se você especificar ambas, use uma lista separada por vírgulas.  
  
 As opções de função primária são as seguintes:  
  
 ALLOW_CONNECTIONS **=** { READ_WRITE | ALL }  
 Especifica o tipo de conexão que os bancos de dados de uma determinada réplica de disponibilidade que está executando a função primária (isto é, está atuando como uma réplica primária) podem aceitar de clientes. O tipo pode ser:  
  
 READ_WRITE  
 Conexões em que a propriedade de conexão Application Intent é definida como **ReadOnly** não são permitidas.  Quando a propriedade Application Intent está definida como **ReadWrite** ou não está definida, a conexão é permitida. Para obter mais informações sobre a propriedade de conexão Tentativa de Aplicativo, consulte [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 ALL  
 Todas as conexões são permitidas com os bancos de dados na réplica primária. Esse é o comportamento padrão.  
  
 READ_ONLY_ROUTING_LIST **=** { **(‘**\<server_instance>**’** [ **,**...*n* ] **)** | NONE } Especifica uma lista separada por vírgula de instâncias de servidor que hospedam réplicas de disponibilidade para esse grupo de disponibilidade que atendem aos seguintes requisitos ao serem executadas na função secundária:  
  
-   Ser configurado para permitir todas as conexões ou conexões somente leitura (veja o argumento ALLOW_CONNECTIONS da opção SECONDARY_ROLE acima).  
  
-   Ter a URL de roteamento somente leitura definida (veja o argumento READ_ONLY_ROUTING_URL da opção SECONDARY_ROLE acima).  
  
 Os valores READ_ONLY_ROUTING_LIST são os seguintes:  
  
 \<server_instance> Especifica o endereço da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que é o host de uma réplica que é uma réplica secundária legível quando é executada na função secundária.  
  
 Use uma lista separada por vírgulas para especificar todas as instâncias de servidor que podem hospedar uma réplica secundária legível. O roteamento somente leitura segue a ordem na qual as instâncias de servidor são especificadas na lista. Se você incluir uma instância de servidor de host de uma réplica na lista de roteamento somente leitura da réplica, colocar esta instância de servidor no final da lista geralmente é uma boa prática, de forma que as conexões de intenção de leitura vão para uma réplica secundária, se houver.  
  
 Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], você pode balancear a carga de solicitações de tentativa de leitura entre réplicas secundárias legíveis. Especifique isso colocando as réplicas em um conjunto aninhado de parênteses na lista de roteamento somente leitura. Para obter mais informações e exemplos, consulte [Configurar o balanceamento de carga entre réplicas somente leitura](../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md#loadbalancing).  
  
 Nenhuma  
 Especifica que, quando esta réplica de disponibilidade for a réplica primária, o roteamento somente leitura não será compatível. Esse é o comportamento padrão.  
  
 SESSION_TIMEOUT **=** *integer*  
 Especifica o tempo limite da sessão, em segundos. Se você não especificar essa opção, por padrão, o período de tempo será de 10 segundos. O valor mínimo é 5 segundos.  
  
> [!IMPORTANT]  
>  Recomendamos que você mantenha o tempo limite em 10 segundos ou mais.  
  
 Para obter mais informações sobre o período de tempo limite da sessão, consulte [Visão geral dos Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).  
  
 AVAILABILITY GROUP ON  
 Especifica dois grupos de disponibilidade que constituem um *grupo de disponibilidade distribuído*. Cada grupo de disponibilidade faz parte de seu próprio WSFC (Cluster de Failover do Windows Server). Quando você cria um grupo de disponibilidade distribuído, o grupo de disponibilidade na instância atual do SQL Server se torna o grupo de disponibilidade primário. O segundo grupo de disponibilidade se torna o grupo de disponibilidade secundário.  
  
 Você precisa unir o grupo de disponibilidade secundário ao grupo de disponibilidade distribuído. Para obter mais informações, consulte [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md).  
  
 \<ag_name> Especifica o nome do grupo de disponibilidade que constitui uma metade do grupo de disponibilidade distribuído.  
  
 LISTENER **='** TCP **://**_system-address_**:**_port_**'**  
 Especifica o caminho da URL para o ouvinte associado ao grupo de disponibilidade.  
  
 A cláusula LISTENER é obrigatória.  
  
 **'** TCP **://**_system-address_**:**_port_**'**  
 Especifica uma URL para o ouvinte associado ao grupo de disponibilidade. Os parâmetros de URL são os seguintes:  
  
 *system-address*  
 É uma cadeia de caracteres, como um nome do sistema, um nome de domínio totalmente qualificado ou um endereço IP, que identifica o ouvinte de forma não ambígua.  
  
 *port*  
 É um número da porta associado ao ponto de extremidade de espelhamento do grupo de disponibilidade. Observe que essa não é a porta do ouvinte.  
  
 AVAILABILITY_MODE **=** { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT | CONFIGURATION_ONLY }  
 Especifica se a réplica primária precisa aguardar o grupo de disponibilidade secundário confirmar a proteção (gravação) dos registros de log em disco, antes que a réplica primária possa confirmar a transação em determinado banco de dados primário.  
  
 SYNCHRONOUS_COMMIT  
 Especifica que a réplica primária aguarda para confirmar as transações até que elas tenham sido protegidas no grupo de disponibilidade secundário. Você pode especificar SYNCHRONOUS_COMMIT para até dois grupos de disponibilidade, incluindo o grupo de disponibilidade primário.  
  
 ASYNCHRONOUS_COMMIT  
 Especifica que a réplica primária confirma as transações sem aguardar esse grupo de disponibilidade secundário proteger o log. Você pode especificar ASYNCHRONOUS_COMMIT para até dois grupos de disponibilidade, incluindo o grupo de disponibilidade primário.  
  
 A cláusula AVAILABILITY_MODE é necessária.  
  
 FAILOVER_MODE **=** { MANUAL }  
 Especifica o modo de failover do grupo de disponibilidade distribuído.  
  
 MANUAL  
 Habilita o failover manual planejado ou o failover manual forçado (em geral, chamado *failover forçado*) pelo administrador de banco de dados.  
  
 A cláusula FAILOVER_MODE é obrigatória e a única opção é MANUAL. Não há suporte para failover automático para o grupo de disponibilidade secundário.  
  
 SEEDING_MODE **=** { AUTOMATIC | MANUAL }  
 Especifica como o grupo de disponibilidade secundário é inicialmente propagado.  
  
 AUTOMATIC  
 Habilita a propagação direta. Esse método propaga o grupo de disponibilidade secundário na rede. Este método não exige que você faça o backup e a restauração de uma cópia do banco de dados primário nas réplicas do grupo de disponibilidade secundário.  
  
 MANUAL  
 Especifica a propagação manual (padrão). Esse método exige que você crie um backup do banco de dados na réplica primária e restaure manualmente esse backup nas réplicas do grupo de disponibilidade secundário.  
  
 LISTENER **‘**_dns\_name_**’(** \<listener_option\> **)** Define um novo ouvinte do grupo de disponibilidade para esse grupo de disponibilidade. LISTENER é um argumento opcional.  
  
> [!IMPORTANT]  
>  Antes de criar seu primeiro ouvinte, é altamente recomendável que você leia [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).  
>   
>  Depois que você criar um ouvinte para um determinado grupo de disponibilidade, será altamente recomendável fazer o seguinte:  
>   
>  -   Peça ao administrador da rede para reservar o endereço IP do ouvinte para seu uso exclusivo.  
> -   Informe o nome do host DNS do ouvinte aos desenvolvedores de aplicativos para uso em cadeias de conexão ao pedir conexões cliente com esse grupo de disponibilidade.  
  
 *dns_name*  
 Especifica o nome de host DNS do ouvinte de grupo de disponibilidade. O nome DNS do ouvinte deve ser exclusivo no domínio e no NetBIOS.  
  
 *dns_name* é um valor de cadeia de caracteres. Este nome pode conter somente caracteres alfanuméricos, traços (-) e hífens (_), em qualquer ordem. Os nomes de host DNS diferenciam maiúsculas de minúsculas. O tamanho máximo é de 63 caracteres.  
  
 Nós recomendamos que você especifique uma cadeia de caracteres significativa. Por exemplo, para um grupo de disponibilidade denominado `AG1`, um nome de host de DNS significativo seria `ag1-listener`.  
  
> [!IMPORTANT]  
>  O NetBIOS reconhece somente os primeiros 15 caracteres no dns_name. Se você tiver dois clusters WSFC que sejam controlados pelo mesmo Active Directory e tentar criar ouvintes do grupo de disponibilidade nos dois clusters usando nomes com mais de 15 caracteres e um prefixo idêntico de 15 caracteres, ocorrerá um erro relatando que o recurso de nome de rede virtual não pôde ser colocado online. Para obter informações sobre regras da nomenclatura de prefixos para nomes DNS, consulte [Atribuindo nomes de domínio](https://technet.microsoft.com/library/cc731265\(WS.10\).aspx).  
  
 \<listener_option> LISTENER usa uma das seguintes opções de \<listener_option>: 
  
 WITH DHCP [ ON { **(‘**_four\_part\_ipv4\_address_**’,‘**_four\_part\_ipv4\_mask_**’)** } ]  
 Especifica que o ouvinte do grupo de disponibilidade usa o protocolo DHCP.  Opcionalmente, use a cláusula ON para identificar a rede na qual esse ouvinte foi criado. DHCP é limitado a uma única sub-rede que é usada para toda instância de servidor que hospeda uma réplica no grupo de disponibilidade.  
  
> [!IMPORTANT]  
>  Nós não recomendamos o DHCP em ambiente de produção. Se houver um tempo de inatividade e a concessão do IP do DHCP expirar, a hora adicional deverá registrar o novo endereço IP da rede DHCP que está associado ao nome DNS do ouvinte e afetará a conectividade do cliente. No entanto, o DHCP é bom para configurar seu ambiente de desenvolvimento e teste para verificar as funções básicas de grupos de disponibilidade e para integração com seus aplicativos.  
  
 Por exemplo:  
  
 `WITH DHCP ON ('10.120.19.0','255.255.254.0')`  
  
 WITH IP **(** { **(‘**_four\_part\_ipv4\_address_**’,‘**_four\_part\_ipv4\_mask_**’)** | **(‘**_ipv6\_address_**’)** } [ **,** ...*n* ] **)** [ **,** PORT **=**_listener\_port_ ]  
 Especifica que, em vez de usar o DHCP, o ouvinte do grupo de disponibilidade usa um ou mais endereços IP estáticos. Para criar um grupo de disponibilidade em várias sub-redes, cada sub-rede exige um endereço IP estático na configuração de ouvinte. Para determinada sub-rede, o endereço IP estático pode ser um endereço IPv4 ou um endereço IPv6. Contate o administrador de rede para obter um endereço IP estático para cada sub-rede que hospeda uma réplica para o novo grupo de disponibilidade.  
  
 Por exemplo:  
  
 `WITH IP ( ('10.120.19.155','255.255.254.0') )`  
  
 *four_part_ipv4_address*  
 Especifica um endereço IPv4 de quatro partes para um ouvinte de grupo de disponibilidade. Por exemplo, `10.120.19.155`.  
  
 *four_part_ipv4_mask*  
 Especifica uma máscara IPv4 de quatro partes para um ouvinte de grupo de disponibilidade. Por exemplo, `255.255.254.0`.  
  
 *ipv6_address*  
 Especifica um endereço IPv6 de quatro partes para um ouvinte de grupo de disponibilidade. Por exemplo, `2001::4898:23:1002:20f:1fff:feff:b3a3`.  
  
 PORT **=** *listener_port*  
 Especifica o número da porta, *listener_port*, a ser usado por um ouvinte do grupo de disponibilidade especificado por uma cláusula WITH IP. PORT é opcional.  
  
 Não há suporte para o número da porta padrão 1433. No entanto, se você estiver preocupado com a segurança, nós recomendaremos usar um número de porta diferente.  
  
 Por exemplo: `WITH IP ( ('2001::4898:23:1002:20f:1fff:feff:b3a3') ) , PORT = 7777`  
  
## <a name="prerequisites-and-restrictions"></a>Pré-requisitos e restrições  
 Para obter informações sobre os pré-requisitos para criar um grupo de disponibilidade, consulte [Pré-requisitos, restrições e recomendações para Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
 Para obter informações sobre as restrições nas instruções Transact-SQL AVAILABILITY GROUP, consulte [Visão geral de instruções Transact-SQL para Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/transact-sql-statements-for-always-on-availability-groups.md).  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer a associação na função de servidor fixa **sysadmin** e a permissão de servidor CREATE AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-configuring-backup-on-secondary-replicas-flexible-failover-policy-and-connection-access"></a>A. Configurando backup em réplicas secundárias, política de failover flexível e acesso de conexão  
 O exemplo a seguir cria um grupo de disponibilidade denominado `MyAg` para dois bancos de dados de usuários, `ThisDatabase` e `ThatDatabase`. A tabela a seguir resume os valores especificados para as opções que são definidas como um todo para o grupo de disponibilidade.  
  
|Opção de grupo|Configuração|Descrição|  
|------------------|-------------|-----------------|  
|AUTOMATED_BACKUP_PREFERENCE|SECONDARY|Essa preferência de backup automatizado indica que os backups devem ocorrer em uma réplica secundária, exceto quando a réplica primária for a única réplica online (comportamento padrão). Para que a configuração AUTOMATED_BACKUP_PREFERENCE tenha efeito, é preciso executar o script dos trabalhos de backup nos bancos de dados de disponibilidade para levar em conta a preferência de backup automatizado.|  
|FAILURE_CONDITION_LEVEL|3|Essa configuração de nível de condição de falha especifica que um failover automático deve ser iniciado em erros internos críticos do SQL Server, como spinlocks órfãos, violações do acesso de gravação graves ou muito descarte.|  
|HEALTH_CHECK_TIMEOUT|600000|Esse valor de tempo limite de verificação da integridade, 60 segundos, especifica que o cluster WSFC aguarda 60.000 milissegundos para o procedimento armazenado do sistema [sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) retornar as informações de integridade do servidor de uma instância de servidor que hospeda uma réplica de confirmação síncrona com backup automático antes de o cluster considerar que a instância de servidor host está lenta ou travada. (O valor padrão é 30000 milissegundos.)|  
  
 Três réplicas de disponibilidade devem ser hospedadas pelas instâncias de servidor padrão nos computadores denominados `COMPUTER01`, `COMPUTER02`e `COMPUTER03`. A tabela a seguir resume os valores especificados para as opções de réplica de cada réplica.  
  
|Opção de réplica|Configuração no `COMPUTER01`|Configuração no `COMPUTER02`|Configuração no `COMPUTER03`|Descrição|  
|--------------------|-----------------------------|-----------------------------|-----------------------------|-----------------|  
|ENDPOINT_URL|TCP://*COMPUTER01:5022*|TCP://*COMPUTER02:5022*|TCP://*COMPUTER03:5022*|Neste exemplo, os sistemas estão no mesmo domínio e, portanto, as URLs de pontos de extremidade podem usar o nome do sistema de computador como endereço do sistema.|  
|AVAILABILITY_MODE|SYNCHRONOUS_COMMIT|SYNCHRONOUS_COMMIT|ASYNCHRONOUS_COMMIT|Duas das réplicas usam o modo de confirmação síncrona. Quando sincronizadas, elas oferecem suporte ao failover sem perda de dados. A terceira réplica, que usa o modo de disponibilidade de confirmação assíncrona.|  
|FAILOVER_MODE|AUTOMATIC|AUTOMATIC|MANUAL|As réplicas da confirmação síncrona oferecem suporte ao failover automático e manual planejado. A réplica em modo de disponibilidade de confirmação síncrona oferece suporte somente ao failover manual forçado.|  
|BACKUP_PRIORITY|30|30|90|Uma prioridade mais alta, 90, é atribuída à réplica de confirmação assíncrona, que para as réplicas de confirmação síncrona. Os backups tendem a ocorrer na instância de servidor que hospeda a réplica de confirmação assíncrona.|  
|SECONDARY_ROLE|( ALLOW_CONNECTIONS = NO,<br /><br /> READ_ONLY_ROUTING_URL = 'TCP://COMPUTER01:1433' )|( ALLOW_CONNECTIONS = NO,<br /><br /> READ_ONLY_ROUTING_URL = 'TCP://COMPUTER02:1433' )|( ALLOW_CONNECTIONS = READ_ONLY, <br />READ_ONLY_ROUTING_URL = 'TCP://COMPUTER03:1433' )|Somente a réplica de confirmação assíncrona serve como réplica secundária legível.<br /><br /> Especifica o nome de computador e o número de porta do Mecanismo de Banco de Dados padrão (1433).<br /><br /> Esse argumento é opcional.|  
|PRIMARY_ROLE|( ALLOW_CONNECTIONS = READ_WRITE, <br />READ_ONLY_ROUTING_LIST = (COMPUTER03) )|( ALLOW_CONNECTIONS = READ_WRITE, <br />READ_ONLY_ROUTING_LIST = (COMPUTER03) )|( ALLOW_CONNECTIONS = READ_WRITE, <br />READ_ONLY_ROUTING_LIST = NONE )|Na função primária, todas as réplicas rejeitam tentativas de conexão de intenção de leitura.<br /><br /> As solicitações de conexão de intenção de leitura são encaminhadas para COMPUTER03 se a réplica local está sendo executada na função secundária. Quando essa réplica é executada na função primária, o roteamento somente leitura é desabilitado.<br /><br /> Esse argumento é opcional.|  
|SESSION_TIMEOUT|10|10|10|Este exemplo especifica o valor do tempo limite de sessão padrão (10). Esse argumento é opcional.|  
  
 Finalmente, o exemplo especifica a cláusula LISTENER opcional para criar um ouvinte de grupo de disponibilidade para o novo grupo de disponibilidade. Um nome DNS exclusivo, `MyAgListenerIvP6`, é especificado para esse ouvinte. As duas réplicas estão em sub-redes diferentes e, portanto, o ouvinte deve usar endereços IP estáticos. Para cada uma das duas réplicas de disponibilidade, a cláusula WITH IP especifica um endereço IP estático, `2001:4898:f0:f00f::cf3c` e `2001:4898:e0:f213::4ce2`, que usam o formato IPv6. Este exemplo também especifica o uso do argumento PORT opcional para especificar a porta `60173` como a porta do ouvinte.  
  
```SQL
CREATE AVAILABILITY GROUP MyAg   
   WITH (  
      AUTOMATED_BACKUP_PREFERENCE = SECONDARY,  
      FAILURE_CONDITION_LEVEL  =  3,   
      HEALTH_CHECK_TIMEOUT = 600000  
       )  
  
   FOR   
      DATABASE  ThisDatabase, ThatDatabase   
   REPLICA ON   
      'COMPUTER01' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER01:5022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = AUTOMATIC,  
         BACKUP_PRIORITY = 30,  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = NO,   
            READ_ONLY_ROUTING_URL = 'TCP://COMPUTER01:1433' ),
         PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE,   
            READ_ONLY_ROUTING_LIST = (COMPUTER03) ),  
         SESSION_TIMEOUT = 10  
         ),   
  
      'COMPUTER02' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER02:5022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = AUTOMATIC,  
         BACKUP_PRIORITY = 30,  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = NO,   
            READ_ONLY_ROUTING_URL = 'TCP://COMPUTER02:1433' ),  
         PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE,   
            READ_ONLY_ROUTING_LIST = (COMPUTER03) ),  
         SESSION_TIMEOUT = 10  
         ),   
  
      'COMPUTER03' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER03:5022',  
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,  
         FAILOVER_MODE =  MANUAL,  
         BACKUP_PRIORITY = 90,  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY,   
            READ_ONLY_ROUTING_URL = 'TCP://COMPUTER03:1433' ),  
         PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE,   
            READ_ONLY_ROUTING_LIST = NONE ),  
         SESSION_TIMEOUT = 10  
         );
GO  
ALTER AVAILABILITY GROUP [MyAg]
  ADD LISTENER ‘MyAgListenerIvP6’ ( WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , PORT = 60173 );   
GO  
```  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Criar um grupo de disponibilidade &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)  
  
-   [Usar o Assistente de Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar a caixa de diálogo Novo Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Usar o Assistente de Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [ALTER DATABASE SET HADR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)   
 [DROP AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-availability-group-transact-sql.md)   
 [Solucionar problemas de configuração de Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)   
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativo &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)  
  
  

