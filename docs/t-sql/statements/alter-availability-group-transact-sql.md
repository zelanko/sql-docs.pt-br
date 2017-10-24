---
title: ALTERAR o grupo de disponibilidade (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_AVAILABILITY_GROUP_TSQL
- ALTER_AVAILABILITY_TSQL
- ALTER AVAILABILITY GROUP
- ALTER AVAILABILITY
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- ALTER AVAILABILITY GROUP statement
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], Transact-SQL statements
ms.assetid: f039d0de-ade7-4aaf-8b7b-d207deb3371a
caps.latest.revision: 152
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ef1d68317c2e288a13d7b07d559b5de45e29cd28
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="alter-availability-group-transact-sql"></a>ALTER AVAILABILITY GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Altera um sempre no grupo de disponibilidade em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A maioria dos argumentos ALTER AVAILABILITY GROUP só têm suporte na réplica primária atual. Entretanto, os argumentos JOIN, FAILOVER e FORCE_FAILOVER_ALLOW_DATA_LOSS só têm suporte na réplica secundária.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ALTER AVAILABILITY GROUP group_name   
  {  
     SET ( <set_option_spec> )   
   | ADD DATABASE database_name   
   | REMOVE DATABASE database_name  
   | ADD REPLICA ON <add_replica_spec>   
   | MODIFY REPLICA ON <modify_replica_spec>  
   | REMOVE REPLICA ON <server_instance>  
   | JOIN  
   | JOIN AVAILABILITY GROUP ON <add_availability_group_spec> [ ,...2 ]  
   | MODIFY AVAILABILITY GROUP ON <modify_availability_group_spec> [ ,...2 ]  
   | GRANT CREATE ANY DATABASE  
   | DENY CREATE ANY DATABASE  
   | FAILOVER  
   | FORCE_FAILOVER_ALLOW_DATA_LOSS   | ADD LISTENER ‘dns_name’ ( <add_listener_option> )  
   | MODIFY LISTENER ‘dns_name’ ( <modify_listener_option> )  
   | RESTART LISTENER ‘dns_name’  
   | REMOVE LISTENER ‘dns_name’  
   | OFFLINE  
  }  
[ ; ]  
  
<set_option_spec> ::=   
    AUTOMATED_BACKUP_PREFERENCE = { PRIMARY | SECONDARY_ONLY| SECONDARY | NONE }  
  | FAILURE_CONDITION_LEVEL  = { 1 | 2 | 3 | 4 | 5 }   
  | HEALTH_CHECK_TIMEOUT = milliseconds  
  | DB_FAILOVER  = { ON | OFF }   
  | REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT = { integer }
  
<server_instance> ::=   
 { 'system_name[\instance_name]' | 'FCI_network_name[\instance_name]' }  
  
<add_replica_spec>::=  
  <server_instance> WITH  
    (  
       ENDPOINT_URL = 'TCP://system-address:port',  
       AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT },  
       FAILOVER_MODE = { AUTOMATIC | MANUAL }   
       [ , <add_replica_option> [ ,...n ] ]  
    )   
  
  <add_replica_option>::=  
       SEEDING_MODE = { AUTOMATIC | MANUAL }   
     | BACKUP_PRIORITY = n  
     | SECONDARY_ROLE ( {   
          ALLOW_CONNECTIONS = { NO | READ_ONLY | ALL }   
        | READ_ONLY_ROUTING_URL = 'TCP://system-address:port'   
          } )  
     | PRIMARY_ROLE ( {   
          ALLOW_CONNECTIONS = { READ_WRITE | ALL }   
        | READ_ONLY_ROUTING_LIST = { ( ‘<server_instance>’ [ ,...n ] ) | NONE }   
          } )  
     | SESSION_TIMEOUT = seconds  
  
<modify_replica_spec>::=  
  <server_instance> WITH  
    (    
       ENDPOINT_URL = 'TCP://system-address:port'   
     | AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT }   
     | FAILOVER_MODE = { AUTOMATIC | MANUAL }   
     | SEEDING_MODE = { AUTOMATIC | MANUAL }   
     | BACKUP_PRIORITY = n  
     | SECONDARY_ROLE ( {   
          ALLOW_CONNECTIONS = { NO | READ_ONLY | ALL }   
        | READ_ONLY_ROUTING_URL = 'TCP://system-address:port'   
          } )  
     | PRIMARY_ROLE ( {   
          ALLOW_CONNECTIONS = { READ_WRITE | ALL }   
        | READ_ONLY_ROUTING_LIST = { ( ‘<server_instance>’ [ ,...n ] ) | NONE }   
          } )  
     | SESSION_TIMEOUT = seconds  
    )   
  
<add_availability_group_spec>::=  
 <ag_name> WITH  
    (  
       LISTENER_URL = 'TCP://system-address:port',  
       AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT },  
       FAILOVER_MODE = MANUAL,  
       SEEDING_MODE = { AUTOMATIC | MANUAL }  
    )  
  
<modify_availability_group_spec>::=  
 <ag_name> WITH  
    (  
       LISTENER = 'TCP://system-address:port'  
       | AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT }  
       | SEEDING_MODE = { AUTOMATIC | MANUAL }  
    )  
  
<add_listener_option> ::=  
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
  
<modify_listener_option>::=  
    {  
       ADD IP ( <ip_address_option> )   
     | PORT = listener_port  
    }  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *nome_do_grupo*  
 Especifica o nome do novo grupo de disponibilidade. *group_name* deve ser um válido [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identificador e devem ser exclusivo em todos os grupos de disponibilidade no cluster WSFC.  
  
 AUTOMATED_BACKUP_PREFERENCE  **=**  {PRIMÁRIO | SECONDARY_ONLY | SECUNDÁRIO | NONE}  
 Especifica uma preferência sobre como um trabalho de backup deve avaliar a réplica primária ao escolher onde executar backups. Você pode criar um script de um determinado trabalho de backup para considerar a preferência de backup automatizada. É importante entender que a preferência não é imposta pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], portanto, não tem nenhum impacto em backups ad hoc.  
  
 Com suporte apenas na réplica principal.  
  
 Os valores são os seguintes:  
  
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
>  Não há nenhuma imposição da configuração AUTOMATED_BACKUP_PREFERENCE. A interpretação dessa preferência depende da lógica, se houver, que você usa para o script em trabalhos de backup para os bancos de dados em um determinado grupo de disponibilidade. A configuração de preferência de backup automatizado não tem efeito sobre backups ad hoc. Para obter mais informações, consulte [Configurar Backup em réplicas de disponibilidade &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md).  
  
> [!NOTE]  
>  Para exibir a preferência de backup automatizada de um grupo de disponibilidade existente, selecione o **automated_backup_preference** ou **automated_backup_preference_desc** coluna o [ sys. availability_groups](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md) exibição do catálogo. Além disso, [sys. fn_hadr_backup_is_preferred_replica &#40; Transact-SQL &#41; ](../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md) pode ser usado para determinar a réplica de backup preferencial.  Esta função sempre retornará 1 para pelo menos uma das réplicas, mesmo quando `AUTOMATED_BACKUP_PREFERENCE = NONE`.  
  
 FAILURE_CONDITION_LEVEL  **=**  {1 | 2 | **3** | 4 | 5}  
 Especifica quais condições de falha que dispararão um failover automático para esse grupo de disponibilidade. FAILURE_CONDITION_LEVEL é definido no nível do grupo, mas é só relevante em réplicas de disponibilidade que estão configuradas para modo de disponibilidade de confirmação síncrona (AVAILIBILITY_MODE  **=**  SYNCHRONOUS_COMMIT). Além disso, condições de falha poderá disparar um failover automático apenas se as réplicas primárias e secundárias estiverem configuradas para modo de failover automático (FAILOVER_MODE  **=**  automático) e a réplica secundária sincronizada atualmente com a réplica primária.  
  
 Com suporte apenas na réplica principal.  
  
 Os níveis da condição de falha (1 a 5) variam do menos restritivo, nível 1, até o mais restritivo, nível 5. Um determinado nível de condição abrange todos os níveis menos restritivos. Assim, o nível de condição mais rígido, 5, inclui os quatro níveis de condição menos restritivos (1 a 4), o nível 4 inclui os níveis 1 a 3 e assim sucessivamente. A tabela a seguir descreve a condição de falha que corresponde a cada nível.  
  
|Nível|Condição de falha|  
|-----------|-----------------------|  
|1|Especifica que um failover automático deverá ser iniciado quando uma destas condições ocorrer:<br /><br /> O serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está inativo.<br /><br /> A concessão do grupo de disponibilidade para conexão com o cluster WSFC expira porque nenhum ACK foi recebido da instância de servidor. Para obter mais informações, veja [Como funciona o tempo limite de concessão de AlwaysOn do SQL Server](http://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx).|  
|2|Especifica que um failover automático deverá ser iniciado quando uma destas condições ocorrer:<br /><br /> A instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não se conecta ao cluster e o limite de HEALTH_CHECK_TIMEOUT especificado pelo usuário do grupo de disponibilidade é excedido.<br /><br /> A réplica de disponibilidade está em estado de falha.|  
|3|Especifica que um failover automático deve ser iniciado em erros internos críticos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como spinlocks órfãos, violações do acesso de gravação graves ou muito descarte.<br /><br /> Esse é o comportamento padrão.|  
|4|Especifica que um failover automático deve ser iniciado em caso de erros internos moderados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como uma condição de memória insuficiente persistente no pool de recursos interno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|5|Especifica que um failover automático deve ser iniciado em qualquer condição de falha qualificada, incluindo:<br /><br /> Esgotamento dos threads de trabalho do SQL Engine.<br /><br /> Detecção de um deadlock insolúvel.|  
  
> [!NOTE]  
>  A falta de resposta por uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para solicitações cliente não é relevante para grupos de disponibilidade.  
  
 Os valores FAILURE_CONDITION_LEVEL e HEALTH_CHECK_TIMEOUT, definem um *política de failover flexível* para um determinado grupo. Essa política de failover flexível permite a você um controle granular sobre quais condições devem causar um failover automático. Para obter mais informações, consulte [política de Failover flexível para Failover automático de um grupo de disponibilidade &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/flexible-automatic-failover-policy-availability-group.md).  
  
 HEALTH_CHECK_TIMEOUT  **=**  *milissegundos*  
 Especifica o tempo de espera (em milissegundos) para o [sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) sistema de procedimento armazenado para retornar informações de integridade do servidor antes de cluster WSFC assume que a instância do servidor está lenta ou suspenso. HEALTH_CHECK_TIMEOUT é definido no nível do grupo, mas é só relevante em réplicas de disponibilidade que estão configuradas para modo de disponibilidade de confirmação síncrona com failover automático (AVAILIBILITY_MODE  **=**  SÍNCRONA COMMIT).  Além disso, um tempo limite de verificação de integridade poderá disparar um failover automático apenas se as réplicas primárias e secundárias estiverem configuradas para modo de failover automático (FAILOVER_MODE  **=**  automática) e o secundário Atualmente, a réplica é sincronizada com a réplica primária.  
  
 O valor HEALTH_CHECK_TIMEOUT padrão é 30.000 milissegundos (30 segundos). O valor mínimo é 15000 milissegundos (15 segundos) e o máximo é 4294967295 milissegundos.  
  
 Com suporte apenas na réplica principal.  
  
> [!IMPORTANT]  
>  **sp_server_diagnostics** não realiza verificações de integridade no nível de banco de dados.  
  
 DB_FAILOVER  **=**  {ON | OFF}  
 Especifica a resposta a ser tomada quando um banco de dados na réplica primária estiver offline. Quando definida como ON, qualquer status diferente de ONLINE para um banco de dados no grupo de disponibilidade dispara um failover automático. Quando essa opção é definida como OFF, somente a integridade da instância é usada para disparar um failover automático.  
 
 Para obter mais informações sobre essa configuração, consulte [opção de detecção de integridade de nível de banco de dados](../../database-engine/availability-groups/windows/sql-server-always-on-database-health-detection-failover-option.md) 

 
 REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT   
 Introduzido no SQL Server de 2017 CTP 2.2. Usado para definir um número mínimo de réplicas secundárias síncronas necessário para confirmar antes que o primário confirma uma transação. Garante que as transações do SQL Server aguardará até que os logs de transação são atualizados durante o número mínimo de réplicas secundárias. O padrão é 0, que fornece o mesmo comportamento que o SQL Server 2016. O valor mínimo é 0. O valor máximo é o número de réplicas menos 1. Essa opção se relaciona com réplicas no modo de confirmação síncrona. Quando réplicas estão no modo de confirmação síncrona, gravações na réplica primária espera até que as gravações nas réplicas secundárias síncronas são confirmadas para o log de transações do banco de dados de réplica. Se um SQL Server que hospeda uma réplica de síncrona secundária para de responder, o SQL Server que hospeda a réplica primária marcará essa réplica secundária não SINCRONIZADA e continuar. Quando o banco de dados não responder volta a ficar online ficará em um estado "não sincronizado" e a réplica será marcada como não íntegro até que o primário pode torná-la síncrona novamente. Essa configuração garante que a réplica primária não continuará até que o número mínimo de réplicas que foram confirmadas cada transação. Se o número mínimo de réplicas não estiver disponível, confirmações no primário falhará. Essa configuração se aplica a grupos de disponibilidade com o tipo de cluster `WSFC` e `EXTERNAL`. Para o tipo de cluster `EXTERNAL` a configuração é alterada quando o grupo de disponibilidade é adicionado a um recurso de cluster. Consulte [alta disponibilidade e proteção de dados para as configurações de grupo de disponibilidade](../../linux/sql-server-linux-availability-group-ha.md).
  
 Adicionar banco de dados *database_name*  
 Especifica uma lista de um ou mais bancos de dados do usuário que você deseja acrescentar ao grupo de disponibilidade. Esses bancos de dados devem residir na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda a réplica primária atual. É possível especificar vários bancos de dados para um grupo de disponibilidade, mas cada banco de dados pode pertencer a apenas um grupo de disponibilidade. Para obter informações sobre o tipo de bancos de dados que pode dar suporte a um grupo de disponibilidade, consulte [pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md). Para descobrir quais bancos de dados locais já pertencem a um grupo de disponibilidade, consulte o **replica_id** coluna o [sys. Databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) exibição do catálogo.  
  
 Com suporte apenas na réplica principal.  
  
> [!NOTE]  
>  Depois de criar o grupo de disponibilidade, você precisará conectar cada instância de servidor que hospeda uma réplica secundária, preparar cada banco de dados secundário e adicioná-lo ao grupo de disponibilidade. Para obter mais informações, veja [Iniciar movimentação de dados em um banco de dados secundário &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md).  
  
 Remover banco de dados *database_name*  
 Remove o banco de dados primário especificado e os bancos de dados secundários correspondentes do grupo de disponibilidade. Com suporte apenas na réplica principal.  
  
 Para obter informações sobre o acompanhamento recomendado depois de remover um banco de dados de disponibilidade de um grupo de disponibilidade, consulte [remover um banco de dados primário de um grupo de disponibilidade &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md).  
  
 ADD REPLICA ON  
 Especifica de uma a oito instâncias do SQL Server para hospedar réplicas secundárias em um grupo de disponibilidade.  Cada réplica é especificada por seu endereço de instância de servidor seguido por uma cláusula WITH (...).  
  
 Com suporte apenas na réplica principal.  
  
 É necessário unir cada réplica secundária nova ao grupo de disponibilidade. Para obter mais informações, consulte a descrição da opção JOIN, posteriormente nesta seção.  
  
 \<instância do servidor >  
 Especifica o endereço da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que é o host para uma réplica. O formato de endereço depende se a instância é a instância padrão ou uma instância nomeada, e se é uma instância autônoma ou uma instância de cluster de failover (FCI). A sintaxe é a seguinte:  
  
 { '*system_name*[\\*instance_name*]' | '*FCI_network_name*[\\*instance_name*]' }  
  
 Os componentes desse endereço são os seguintes:  
  
 *system_name*  
 É o nome NetBIOS do computador do sistema no qual reside uma instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esse computador deve ser um nó WSFC.  
  
 *FCI_network_name*  
 É o nome da rede usada para acessar um cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Use-o se a instância de servidor participar como um parceiro de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Execução de SELECT [@@SERVERNAME ](../../t-sql/functions/servername-transact-sql.md) em uma FCI instância de servidor retorna o inteiro '*FCI_network_name*[\\*instance_name*]' cadeia de caracteres (que é o nome da réplica completa).  
  
 *instance_name*  
 É o nome de uma instância de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que é hospedada por *system_name* ou *FCI_network_name* e que tem Always On habilitado. Para uma instância de servidor padrão, *instance_name* é opcional. O nome da instância não diferencia maiúsculas de minúsculas. Em uma instância de servidor autônomo, esse nome de valor é o mesmo que o valor retornado pela execução de SELECT [@@SERVERNAME](../../t-sql/functions/servername-transact-sql.md).  
  
 \  
 É um separador usado apenas ao especificar *instance_name*para separá-lo do *system_name* ou *FCI_network_name*.  
  
 Para obter informações sobre os pré-requisitos para nós WSFC e instâncias de servidor, consulte [pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
 ENDPOINT_URL ='TCP: / /*system-address*:*porta*'  
 Especifica o caminho da URL para o [ponto de extremidade de espelhamento de banco de dados](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md) na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospedará a réplica de disponibilidade que você está adicionando ou modificando.  
  
 ENDPOINT_URL é necessário na cláusula ADD REPLICA ON e opcional na cláusula MODIFY REPLICA ON.  Para obter mais informações, consulte [Especificar a URL do ponto de extremidade ao adicionar ou modificar uma réplica de disponibilidade &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md).  
  
 **'**TCP**://***system-address***:***porta***'**  
 Especifica uma URL para especificar uma URL de ponto de extremidade ou URL de roteamento somente leitura. Os parâmetros de URL são os seguintes:  
  
 *system-address*  
 É uma cadeia de caracteres, como um nome de sistema, um nome de domínio totalmente qualificado ou um endereço IP, que identifica de forma exclusiva o sistema do computador de destino.  
  
 *port*  
 É um número de porta que está associado ao ponto de extremidade de espelhamento da instância do servidor parceiro (para a opção ENDPOINT_URL) ou o número de porta usado pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)] da instância de servidor (para a opção READ_ONLY_ROUTING_URL).  
  
 AVAILABILITY_MODE  **=**  {SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT}  
 Especifica se a réplica primária tem que esperar a réplica secundária confirmar o fortalecimento (gravação) dos registros de log no disco, antes de a réplica primária poder confirmar a transação em um determinado banco de dados primário. As transações em bancos de dados diferentes na mesma réplica primária podem ser confirmadas independentemente.  
  
 SYNCHRONOUS_COMMIT  
 Especifica se a réplica primária esperará para confirmar transações até que eles tenham sido fortalecidas nessa réplica secundária (modo de confirmação síncrona). Você pode especificar SYNCHRONOUS_COMMIT para até três réplicas, inclusive a réplica primária.  
  
 ASYNCHRONOUS_COMMIT  
 Especifica se a réplica primária confirma transações sem esperar que essa réplica secundária fortaleça o log (modo de disponibilidade de confirmação síncrona). Você pode especificar ASYNCHRONOUS_COMMIT para até cinco réplicas de disponibilidade, inclusive a réplica primária.  
  
 AVAILABILITY_MODE é necessário na cláusula ADD REPLICA ON e opcional na cláusula MODIFY REPLICA ON. Para obter mais informações, veja [Modos de disponibilidade &#40;Grupos de Disponibilidade AlwaysOn&#41;](../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md).  
  
 FAILOVER_MODE  **=**  {AUTOMÁTICA | MANUAL}  
 Especifica o modo de disponibilidade da réplica de disponibilidade que você está definindo.  
  
 AUTOMATIC  
 Permite o failover automático. AUTOMATIC só terá suporte se você também especificar AVAILABILITY_MODE = SYNCHRONOUS_COMMIT. Você pode especificar AUTOMATIC para duas réplicas de disponibilidade, inclusive a réplica primária.  
  
> [!NOTE]  
>  As FCIs (Instâncias de cluster de failover) do SQL Server não dão suporte ao failover automático por grupos de disponibilidade, de modo que qualquer réplica de disponibilidade que esteja hospedado por um FCI só pode ser configurada para failover manual.  
  
 MANUAL  
 Habilita o failover manual ou failover manual forçado (*failover forçado*) pelo administrador do banco de dados.  
  
 FAILOVER_MODE é necessário na cláusula ADD REPLICA ON e opcional na cláusula MODIFY REPLICA ON. Existem dois tipos de failover manual: failover manual sem perda de dados e failover forçado (com possível perda de dados), que têm suporte em condições diferentes.  Para obter mais informações, consulte [Failover e modos de failover &#40;grupos de disponibilidade AlwaysOn&#41;](../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md).  
  
 SEEDING_MODE  **=**  {AUTOMÁTICA | MANUAL}  
 Especifica como a réplica secundária será propagada inicialmente.  
  
 AUTOMATIC  
 Habilita a propagação direta. Este método fará a propagação da réplica secundária na rede. Este método não exige que você fazer backup e restaurar uma cópia do banco de dados primário na réplica.  
  
> [!NOTE]  
>  Para a propagação direta, você deve permitir a criação de banco de dados em cada réplica secundária chamando **ALTER AVAILABILITY GROUP** com o **GRANT CREATE ANY DATABASE** opção.  
  
 MANUAL  
 Especifica a propagação manual (padrão). Esse método requer que você criar um backup do banco de dados na réplica primária e restaure manualmente esse backup na réplica secundária.  
  
 BACKUP_PRIORITY**=***n*  
 Especifica sua prioridade para executar backups nesta réplica em relação às outras réplicas no mesmo grupo de disponibilidade. O valor é um número inteiro no intervalo de 0..100. Esses valores têm estes significados:  
  
-   1..100 indica que a réplica de disponibilidade pode ser escolhida para executar backups. 1 indica a prioridade mais baixa, e 100 indica a prioridade mais alta. Se BACKUP_PRIORITY = 1, a réplica de disponibilidade será escolhida para só executar backups se nenhuma réplica de disponibilidade de prioridade mais alta estiver atualmente disponível.  
  
-   0 indica que essa réplica de disponibilidade nunca será escolhida para executar backups. Isso é útil, por exemplo, para uma réplica de disponibilidade remota para a qual você nunca deseja que ocorra o failover de backups.  
  
 Para obter mais informações, consulte [Secundárias ativas: backup em réplicas secundárias &#40;Grupos de Disponibilidade AlwaysOn&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md).  
  
 SECONDARY_ROLE **(** ... **)**  
 Especifica configurações específicas de papel que terão efeito se essa réplica de disponibilidade tiver a função secundária (ou seja, sempre que for uma réplica secundária) no momento. Dentro dos parênteses, especifique uma ou ambas as opções de função secundária. Se você especificar ambas, use uma lista separada por vírgulas.  
  
 As opções de função secundária são as seguintes:  
  
 ALLOW_CONNECTIONS  **=**  {NENHUM | READ_ONLY | ALL}  
 Especifica se os bancos de dados de uma determinada réplica de disponibilidade que está executando a função primária (isto é, está atuando como uma réplica secundária) podem aceitar conexões de clientes. Pode ser:  
  
 NO  
 Nenhuma conexão de usuário é permitida para bancos de dados secundários desta réplica. Eles não estão disponíveis para acesso de leitura. Esse é o comportamento padrão.  
  
 READ_ONLY  
 Apenas conexões são permitidas para os bancos de dados na réplica secundária em que a propriedade Application Intent é definida como **ReadOnly**. Para obter mais informações sobre essa propriedade, consulte [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 ALL  
 Todas as conexões são permitidas com os bancos de dados na réplica secundária para acesso somente leitura.  
  
 Para obter mais informações, veja [Secundárias ativas: réplicas secundárias legíveis &#40;Grupos de Disponibilidade AlwaysOn&#41;](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).  
  
 READ_ONLY_ROUTING_URL **='**TCP**://***system-address***:***porta***'**  
 Especifica a URL a ser usada para rotear solicitações de conexão de intenção de leitura para esta réplica de disponibilidade. Esta é a URL na qual o Mecanismo de Banco de Dados do SQL Server escuta. Normalmente, a instância padrão do Mecanismo de Banco de Dados do SQL Server escuta na porta TCP 1433.  
  
 Para uma instância nomeada, você pode obter o número da porta consultando o **porta** e **type_desc** colunas do [sys.DM tcp_listener_states](../../relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql.md) exibição de gerenciamento dinâmico. A instância de servidor usa o ouvinte do Transact-SQL (**type_desc = 'TSQL'**).  
  
 Para obter mais informações sobre como calcular a URL de roteamento somente leitura para uma réplica de disponibilidade, consulte [Calculando read_only_routing_url de AlwaysOn](http://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-Always%20On.aspx).  
  
> [!NOTE]  
>  Para uma instância nomeada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o ouvinte do Transact-SQL deve ser configurado para usar uma porta específica. Para obter mais informações, veja [Configurar um servidor para escuta em uma porta TCP específica &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md).  
  
 PRIMARY_ROLE **(** ... **)**  
 Especifica configurações específicas de papel que terão efeito se essa réplica de disponibilidade tiver a função primária (ou seja, sempre que for uma réplica primária) no momento. Dentro dos parênteses, especifique uma ou ambas as opções de função primária. Se você especificar ambas, use uma lista separada por vírgulas.  
  
 As opções de função primária são as seguintes:  
  
 ALLOW_CONNECTIONS  **=**  {READ_WRITE | ALL}  
 Especifica o tipo de conexão que os bancos de dados de uma determinada réplica de disponibilidade que está executando a função primária (isto é, está atuando como uma réplica primária) podem aceitar de clientes. O tipo pode ser:  
  
 READ_WRITE  
 Conexões em que a propriedade de conexão Application Intent é definida como **ReadOnly** não são permitidas.  Quando a propriedade Application Intent está definida como **ReadWrite** ou não está definida, a conexão é permitida. Para obter mais informações sobre a propriedade de conexão Tentativa de Aplicativo, consulte [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 ALL  
 Todas as conexões são permitidas com os bancos de dados na réplica primária. Esse é o comportamento padrão.  
  
 READ_ONLY_ROUTING_LIST  **=**  { **('**\<instância do servidor >**'** [ **,**... *n* ] **)** | NONE}  
 Especifica uma lista separada por vírgulas de instâncias de servidor que hospedam réplicas para este grupo de disponibilidade que atendem aos seguintes requisitos ao serem executados na função secundária:  
  
-   Ser configurado para permitir todas as conexões ou conexões somente leitura (veja o argumento ALLOW_CONNECTIONS da opção SECONDARY_ROLE acima).  
  
-   Ter a URL de roteamento somente leitura definida (veja o argumento READ_ONLY_ROUTING_URL da opção SECONDARY_ROLE acima).  
  
 Os valores READ_ONLY_ROUTING_LIST são os seguintes:  
  
 \<instância do servidor >  
 Especifica o endereço da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que é o host para uma réplica de disponibilidade que é uma réplica secundária legível ao ser executada na função secundária.  
  
 Use uma lista separada por vírgulas para especificar todas as instâncias de servidor que podem hospedar uma réplica secundária legível. O roteamento somente leitura seguirá a ordem na qual as instâncias de servidor são especificadas na lista. Se você incluir uma instância de servidor de host de uma réplica na lista de roteamento somente leitura da réplica, colocar esta instância de servidor no final da lista geralmente é uma boa prática, de forma que as conexões de intenção de leitura vão para uma réplica secundária, se houver.  
  
 Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], você pode solicitações de tentativa de leitura de balanceamento de carga entre réplicas secundárias legíveis. Você pode especificar isso colocando as réplicas em um conjunto aninhado de parênteses na lista de roteamento somente leitura. Para obter mais informações e exemplos, consulte [configurar o balanceamento de carga entre réplicas somente leitura](../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md#loadbalancing).  
  
 Nenhuma  
 Especifica que, quando esta réplica de disponibilidade for a réplica primária, o roteamento somente leitura não terá suporte. Esse é o comportamento padrão. Quando usado com MODIFY REPLICA ON, este valor desabilita uma lista existente, se houver.  
  
 SESSION_TIMEOUT  **=**  *segundos*  
 Especifica o tempo limite da sessão, em segundos. Se você não especificar essa opção, por padrão, o período de tempo será de 10 segundos. O valor mínimo é 5 segundos.  
  
> [!IMPORTANT]  
>  Recomendamos que você mantenha o tempo limite em 10 segundos ou mais.  
  
 Para obter mais informações sobre o período de tempo limite da sessão, consulte [visão geral dos grupos de disponibilidade AlwaysOn &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).  
  
 MODIFY REPLICA ON  
 Modifica qualquer uma das réplicas do grupo de disponibilidade. A lista de réplicas a ser modificada contém o endereço de instância de servidor e uma cláusula WITH (...) para cada réplica.  
  
 Com suporte apenas na réplica principal.  
  
 REMOVE REPLICA ON  
 Remove a réplica secundária especificada do grupo de disponibilidade. A réplica primária atual não pode ser removida de um grupo de disponibilidade. Ao ser removida, a réplica deixa de receber dados. Seus bancos de dados secundários são removidos do grupo de disponibilidade e inserem o estado RESTORING.  
  
 Com suporte apenas na réplica principal.  
  
> [!NOTE]  
>  Se você remover uma réplica enquanto ela estiver indisponível ou com falha, quando ficar online novamente, ela descobrirá que já não pertence ao grupo de disponibilidade.  
  
 JOIN  
 Faz com que a instância de servidor local hospede a réplica secundária no grupo de disponibilidade.  
  
 Com suporte apenas na réplica secundária que ainda não foi unida ao grupo de disponibilidade.  
  
 Para obter mais informações, veja [Unir uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md).  
  
 FAILOVER  
 Inicia um failover manual do grupo de disponibilidade sem perda de dados para a réplica secundária à qual você está conectado. A réplica em que você insere um comando de failover de destino de failover é conhecida como o.  O destino de failover assumirá a função primária, recuperará sua cópia de cada banco de dados e as colocará online como os novos bancos de dados primários. A réplica principal antiga faz a transição concorrente para a função secundária, seus bancos de dados se tornam bancos de dados secundários e são imediatamente suspensos. Potencialmente, estas funções podem ser alternadas de um lado para outro por uma série de falhas.  
  
 Com suporte apenas em uma réplica secundária de confirmação síncrona que esteja sincronizada com a réplica principal. Observe que para que a réplica secundária seja sincronizada, a réplica principal também precisará estar sendo executada em modo de confirmação síncrona.  
  
> [!NOTE]  
>  Um comando de failover é retornado assim que o destino de failover aceita o comando. No entanto, a recuperação de banco de dados ocorre de forma assíncrona depois que o grupo de disponibilidade terminar o failover.  
  
 Para obter informações sobre as limitações, pré-requisitos e as recomendações para executar um failover manual planejado, consulte [realizar um Failover Manual planejado de um grupo de disponibilidade &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server.md).  
  
 FORCE_FAILOVER_ALLOW_DATA_LOSS  
 > [!CAUTION]  
>  Forçar o failover, o que pode envolver alguma perda de dados, é estritamente um método de recuperação de desastre. Portanto, é altamente recomendável forçar failover apenas se a réplica primária ainda não estiver em execução, se estiver disposto a arriscar a perda de dados, e você deve restaurar o serviço para o grupo de disponibilidade imediatamente.  
  
 Tem suporte apenas em uma réplica cuja função está no estado SECONDARY ou RESOLVING. -- A réplica em que você insere um comando de failover é conhecida como o *destino de failover*.  
  
 Força o failover do grupo de disponibilidade, com possível perda de dados, para o destino de failover. O destino de failover assumirá a função primária, recuperará sua cópia de cada banco de dados e as colocará online como os novos bancos de dados primários. Em qualquer réplica secundária restante, todo banco de dados secundário ficará suspenso até que seja retomado manualmente. Quando a réplica primária antiga ficar disponível, ela assumirá a função secundária e seus bancos de dados se tornarão bancos de dados secundários suspensos.  
  
> [!NOTE]  
>  Um comando de failover é retornado assim que o destino de failover aceita o comando. No entanto, a recuperação de banco de dados ocorre de forma assíncrona depois que o grupo de disponibilidade terminar o failover.  
  
 Para obter informações sobre as limitações, pré-requisitos e recomendações para forçar o failover e o efeito de um failover forçado nos bancos de dados primários antigos no grupo de disponibilidade, consulte [executar um Failover de Manual forçado de um de disponibilidade Grupo &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md).  
  
 ADD LISTENER **'***dns_name***' (** \<add_listener_option > **)**  
 Define um novo ouvinte de grupo de disponibilidade para esse grupo de disponibilidade. Com suporte apenas na réplica principal.  
  
> [!IMPORTANT]  
>  Antes de criar seu primeiro ouvinte, é altamente recomendável que você leia [criar ou configurar um ouvinte de grupo de disponibilidade &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).  
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
>  O NetBIOS reconhece somente os primeiros 15 caracteres no dns_name. Se você tiver dois clusters do WSFC que sejam controlados pelo mesmo Active Directory e tentar criar ouvintes de grupo de disponibilidade nos dois clusters usando nomes com mais de 15 caracteres e um prefixo idêntico de 15 caracteres, você obterá um erro relatando que o recurso Nome de Rede virtual não pôde ser colocado online. Para obter informações sobre regras da nomenclatura de prefixos para nomes DNS, consulte [Atribuindo nomes de domínio](http://technet.microsoft.com/library/cc731265\(WS.10\).aspx).  
  
 ASSOCIAÇÃO DE GRUPO DE DISPONIBILIDADE EM  
 Une a um *grupo de disponibilidade distribuída*. Quando você cria um grupo de disponibilidade distribuída, o grupo de disponibilidade no cluster do qual ele é criado é o grupo de disponibilidade primária. O grupo de disponibilidade que se une ao grupo de disponibilidade distribuída é o grupo de disponibilidade secundária.  
  
 \<ag_name >  
 Especifica o nome do grupo de disponibilidade, o que constitui uma metade de um grupo de disponibilidade distribuída.  
  
 OUVINTE **='**TCP**://***system-address***:***porta***'**  
 Especifica o caminho da URL para o ouvinte associado ao grupo de disponibilidade.  
  
 A cláusula de OUVINTE é necessária.  
  
 **'**TCP**://***system-address***:***porta***'**  
 Especifica uma URL para o ouvinte associado ao grupo de disponibilidade. Os parâmetros de URL são os seguintes:  
  
 *system-address*  
 É uma cadeia de caracteres, como um nome de sistema, um nome de domínio totalmente qualificado ou um endereço IP, que identifica inequivocamente o ouvinte.  
  
 *port*  
 É um número de porta que está associado com o ponto de extremidade do grupo de disponibilidade. Observe que isso não é a porta do ouvinte.  
  
 AVAILABILITY_MODE  **=**  {SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT}  
 Especifica se a réplica primária precisa aguardar o grupo de disponibilidade secundária confirmar o fortalecimento (gravação) dos registros de log no disco antes da réplica primária pode confirmar a transação em um determinado banco de dados primário.  
  
 SYNCHRONOUS_COMMIT  
 Especifica que a réplica primária esperará para confirmar transações até que eles tenham sido fortalecidas no grupo de disponibilidade secundária. Você pode especificar SYNCHRONOUS_COMMIT para até dois grupos de disponibilidade, inclusive o grupo de disponibilidade primária.  
  
 ASYNCHRONOUS_COMMIT  
 Especifica que a réplica primária confirma transações sem esperar que esse grupo de disponibilidade secundária Proteja o log. Você pode especificar ASYNCHRONOUS_COMMIT para até dois grupos de disponibilidade, inclusive o grupo de disponibilidade primária.  
  
 A cláusula AVAILABILITY_MODE é necessária.  
  
 FAILOVER_MODE  **=**  {MANUAL}  
 Especifica o modo de failover do grupo de disponibilidade distribuída.  
  
 MANUAL  
 Habilita o failover manual planejado ou failover manual forçado (geralmente chamado *failover forçado*) pelo administrador do banco de dados.  
  
 Não há suporte para failover automático para o grupo de disponibilidade secundário.  
  
 SEEDING_MODE **=**  {AUTOMÁTICA | MANUAL}  
 Especifica como o grupo de disponibilidade secundário será propagado inicialmente.  
  
 AUTOMATIC  
 Permite que a propagação automática. Este método fará a propagação do grupo de disponibilidade secundário pela rede. Este método não exige que você fazer backup e restaurar uma cópia do banco de dados primário nas réplicas do grupo de disponibilidade secundária.  
  
 MANUAL  
 Especifica a propagação manual. Esse método requer que você criar um backup do banco de dados na réplica primária e restaure manualmente esse backup em réplicas do grupo de disponibilidade secundária.  
  
 MODIFICAR GRUPO DE DISPONIBILIDADE EM  
 Modifica as configurações de grupo de disponibilidade de um grupo de disponibilidade distribuída. A lista de grupos de disponibilidade a ser modificada contém o nome do grupo de disponibilidade e um com a cláusula (...) para cada grupo de disponibilidade.  
  
> [!IMPORTANT]  
>  Este comando deve ser repetido no grupo de disponibilidade primário e instâncias de grupo de disponibilidade secundária.  
  
 CONCESSÃO DE CRIAR QUALQUER BANCO DE DADOS  
 Permite que o grupo de disponibilidade para criar bancos de dados na réplica primária, que oferece suporte à propagação direta (SEEDING_MODE = AUTOMATIC). Esse parâmetro deve ser executado em cada réplica secundária que oferece suporte à propagação direta depois que secundário se une ao grupo de disponibilidade.  Requer a permissão CREATE ANY DATABASE.  
  
 NEGAR CRIAR QUALQUER BANCO DE DADOS  
 Remove a capacidade de criar bancos de dados a réplica primária do grupo de disponibilidade.  
  
 \<add_listener_option >  
 ADD LISTENER escolhe uma das seguintes opções:  
  
 COM o DHCP [ON { **('***four_part_ipv4_address***','***four_part_ipv4_mask***')** }]  
 Especifica que o ouvinte de grupo de disponibilidade usará o protocolo DHCP.  Opcionalmente, use a cláusula ON para identificar a rede na qual este ouvinte será criado. DHCP é limitado a uma única sub-rede que é usada para toda instância de servidor que hospeda uma réplica de disponibilidade no grupo de disponibilidade.  
  
> [!IMPORTANT]  
>  Nós não recomendamos o DHCP em ambiente de produção. Se houver um tempo de inatividade e a concessão do IP do DHCP expirar, a hora adicional deverá registrar o novo endereço IP da rede DHCP que está associado ao nome DNS do ouvinte e afetará a conectividade do cliente. No entanto, o DHCP é bom para configurar seu ambiente de desenvolvimento e teste para verificar as funções básicas de grupos de disponibilidade e para integração com seus aplicativos.  
  
 Por exemplo:  
  
 `WITH DHCP ON ('10.120.19.0','255.255.254.0')`  
  
 COM o IP **(** { **('***four_part_ipv4_address***','***four_part_ipv4_mask* **')** | **('***ipv6_address***')** } [ **,** ...  *n*  ] **)** [ **,** Porta  **=**  *listener_port* ]  
 Especifica que, em vez de usar o DHCP, o ouvinte do grupo de disponibilidade usará um ou mais endereços IP estáticos. Para criar um grupo de disponibilidade em várias sub-redes, cada sub-rede exige um endereço IP estático na configuração de ouvinte. Para determinada sub-rede, o endereço IP estático pode ser um endereço IPv4 ou um endereço IPv6. Contate o administrador da rede para obter um endereço IP estático para cada sub-rede que hospedará uma réplica de disponibilidade para o novo grupo de disponibilidade.  
  
 Por exemplo:  
  
 `WITH IP ( ('10.120.19.155','255.255.254.0') )`  
  
 *four_part_ipv4_address*  
 Especifica um endereço IPv4 de quatro partes para um ouvinte de grupo de disponibilidade. Por exemplo, `10.120.19.155`.  
  
 *four_part_ipv4_mask*  
 Especifica uma máscara IPv4 de quatro partes para um ouvinte de grupo de disponibilidade. Por exemplo, `255.255.254.0`.  
  
 *ipv6_address*  
 Especifica um endereço IPv6 de quatro partes para um ouvinte de grupo de disponibilidade. Por exemplo, `2001::4898:23:1002:20f:1fff:feff:b3a3`.  
  
 PORTA  **=**  *listener_port*  
 Especifica o número de porta —*listener_port*— a ser usado por um ouvinte de grupo de disponibilidade especificado por uma cláusula WITH IP. PORT é opcional.  
  
 Não há suporte para o número da porta padrão 1433. No entanto, se você estiver preocupado com a segurança, nós recomendaremos usar um número de porta diferente.  
  
 Por exemplo: `WITH IP ( ('2001::4898:23:1002:20f:1fff:feff:b3a3') ) , PORT = 7777`  
  
 MODIFY LISTENER **'***dns_name***' (** \<modify_listener_option > **)**  
 Modifica um ouvinte de grupo de disponibilidade existente para esse grupo de disponibilidade. Com suporte apenas na réplica principal.  
  
 \<modify_listener_option >  
 MODIFY LISTENER escolhe uma das seguintes opções:  
  
 Adicionar IP { **('***four_part_ipv4_address***','***four_part_ipv4_mask***')**  |  **('**dns_name*ipv6_address***')** }  
 Adiciona o endereço IP especificado para o ouvinte do grupo de disponibilidade especificado por *dns_name*.  
  
 PORTA  **=**  *listener_port*  
 Veja a descrição desse argumento anteriormente nesta seção.  
  
 Reinicie o OUVINTE **'***dns_name***'**  
 Reinicia o ouvinte que está associado ao nome DNS especificado. Com suporte apenas na réplica principal.  
  
 Remover OUVINTE **'***dns_name***'**  
 Remove o ouvinte que está associado ao nome DNS especificado. Com suporte apenas na réplica principal.  
  
 OFFLINE  
 Leva um grupo de disponibilidade online a se tornar offline Não há perda de dados para bancos de dados de confirmação síncrona.  
  
 Depois que um grupo de disponibilidade se torna offline, seus bancos de dados ficam indisponíveis para os clientes e você não pode recolocar o grupo de disponibilidade online. Portanto, use a opção OFFLINE somente durante uma migração entre clusters de [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], ao migrar recursos do grupo de disponibilidade para um novo cluster WSFC.  
  
 Para obter mais informações, consulte [colocar um grupo de disponibilidade Offline &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/take-an-availability-group-offline-sql-server.md).  
  
## <a name="prerequisites-and-restrictions"></a>Pré-requisitos e restrições  
 Para obter informações sobre os pré-requisitos e restrições em réplicas de disponibilidade e suas instâncias de servidor de host e computadores, consulte [pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
 Para obter informações sobre as restrições nas instruções Transact-SQL AVAILABILITY GROUP, consulte [visão geral de instruções Transact-SQL para grupos de disponibilidade AlwaysOn &#40; SQL Server &#41; ](../../database-engine/availability-groups/windows/transact-sql-statements-for-always-on-availability-groups.md).  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.  
  
## <a name="examples"></a>Exemplos  
  
###  <a name="Join_Secondary_Replica"></a> A. Unindo uma réplica secundária a um grupo de disponibilidade  
 O exemplo a seguir une a réplica secundária à qual você está conectado para o `AccountsAG` grupo de disponibilidade.  
  
```  
ALTER AVAILABILITY GROUP AccountsAG JOIN;  
GO  
```  
  
###  <a name="Force_Failover"></a> B. Forçando failover de um grupo de disponibilidade  
 O exemplo a seguir força o failover do grupo de disponibilidade `AccountsAG` para a réplica secundária à qual você está conectado.  
  
```  
ALTER AVAILABILITY GROUP AccountsAG FORCE_FAILOVER_ALLOW_DATA_LOSS;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER DATABASE SET HADR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)   
 [DESCARTE o grupo de disponibilidade &#40; Transact-SQL &#41;](../../t-sql/statements/drop-availability-group-transact-sql.md)   
 [sys. availability_replicas &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [sys. availability_groups &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [Solucionar problemas de sempre configuração de grupos de disponibilidade &#40; SQL Server &#41;](../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)   
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativo &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)  
  
  

