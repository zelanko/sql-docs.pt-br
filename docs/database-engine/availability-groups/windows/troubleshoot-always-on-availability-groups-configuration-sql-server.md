---
title: "Solução de problemas de configuração de Grupos de Disponibilidade AlwaysOn (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- troubleshooting [SQL Server], deploying
- Availability Groups [SQL Server], troubleshooting
- Availability Groups [SQL Server], configuring
ms.assetid: 8c222f98-7392-4faf-b7ad-5fb60ffa237e
caps.latest.revision: 39
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 7e05564a4ccd20258f656fae1cbb627aa1255e60
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="troubleshoot-always-on-availability-groups-configuration-sql-server"></a>Solucionar problemas de configuração de grupos de disponibilidade AlwaysOn (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Este tópico fornece informações para ajudar a solucionar problemas típicos ao configurar instâncias de servidor para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Os problemas de configuração típicos incluem: o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] está desabilitado, as contas estão configuradas incorretamente, o ponto de extremidade de espelhamento de banco de dados não existe, o ponto de extremidade está inacessível (Erro 1418 do SQL Server), o acesso à rede não existe e falha no comando de junção de banco de dados (Erro 35250 do SQL Server).  
  
> [!NOTE]  
>  Verifique se você está atendendo aos pré-requisitos do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] . Para obter mais informações, consulte [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
 **Neste tópico:**  
  
|Seção|Descrição|  
|-------------|-----------------|  
|[Os grupos de disponibilidade AlwaysOn não estão habilitados](#IsHadrEnabled)|Se uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não estiver habilitada para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], a instância não dará suporte à criação de grupo de disponibilidade e não poderá hospedar nenhuma réplica de disponibilidade.|  
|[Contas](#Accounts)|Discute os requisitos para configurar corretamente as contas nas quais o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] será executado.|  
|[Pontos de extremidade](#Endpoints)|Discute como diagnosticar problemas com o ponto de extremidade de espelhamento de banco de dados de uma instância de servidor.|  
|[Nome do sistema](#SystemName)|Resume as alternativas para especificar o nome do sistema de uma instância do servidor em uma URL de ponto de extremidade.|  
|[Acesso de rede](#NetworkAccess)|Documenta o requisito de que cada instância do servidor que está hospedando uma réplica de disponibilidade deve poder acessar a porta de cada uma das instâncias do servidor sobre TCP.|  
|[Acesso ao ponto de extremidade (erro 1418 do SQL Server)](#Msg1418)|Contém informações sobre essa mensagem de erro do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|[Falha ao unir bancos de dados (erro 35250 do SQL Server)](#JoinDbFails)|Discute as possíveis causas e resolução de uma falha ao unir bancos de dados secundários a um grupo de disponibilidade porque a conexão com a réplica primária não está ativa.|  
|[O roteamento somente leitura não está funcionando corretamente](#ROR)||  
|[Tarefas relacionadas](#RelatedTasks)|Contém uma lista de tópicos orientados para tarefas nos Manuais Online do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] que são particularmente relevantes para solucionar problemas de configuração de grupos de disponibilidade.|  
|[Conteúdo relacionado](#RelatedContent)|Contém uma lista de recursos relevantes que são externos aos Manuais Online do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
  
##  <a name="IsHadrEnabled"></a> Os grupos de disponibilidade AlwaysOn não estão habilitados  
 O recurso do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] deve estar habilitado em cada uma das instâncias do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Para obter mais informações, consulte [Habilitar e desabilitar Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md).  
  
##  <a name="Accounts"></a> Contas  
 As contas nas quais o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está sendo executado devem ser configuradas corretamente.  
  
1.  As contas têm as permissões corretas?  
  
    1.  Se os parceiros forem executados como a mesma conta de usuário do domínio, os logons de usuário corretos existirão automaticamente em ambos os bancos de dados **master** . Isso simplifica a configuração de segurança do banco de dados e é recomendado.  
  
    2.  Se duas instâncias do servidor forem executadas como contas diferentes, o logon de cada conta deverá ser criado no banco de dados **master** na instância do servidor remoto e esse logon deverá receber permissões CONNECT para se conectar ao ponto de extremidade de espelhamento do banco de dados dessa instância do servidor. Para obter mais informações, veja [Configurar contas de logon para espelhamento de banco de dados ou para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/database-mirroring/set-up-login-accounts-database-mirroring-always-on-availability.md).  
  
2.  Se o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] estiver sendo executado como uma conta interna, como Sistema Local, Serviço Local ou Serviço de Rede ou uma conta que não pertença ao domínio, você deverá usar certificados para autenticação de ponto de extremidade. Se suas contas de serviço estiverem usando contas de domínio no mesmo domínio, você poderá escolher conceder acesso de CONNECT a cada conta de serviço em todos os locais de réplica ou usar certificados. Para obter mais informações, veja [Usar certificados para um ponto de extremidade do espelhamento de banco de dados &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md).  
  
##  <a name="Endpoints"></a> Pontos de extremidade  
 Os pontos de extremidade devem ser configurados corretamente.  
  
1.  Verifique se cada instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que vai hospedar uma réplica de disponibilidade (cada *local de réplica*) tem um ponto de extremidade de espelhamento de banco de dados. Para determinar se existe um ponto de extremidade de espelhamento do banco de dados em determinada instância do servidor, use a exibição de catálogo [sys.database_mirroring_endpoints](../../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md). Para obter mais informações, veja [Criar um ponto de extremidade de espelhamento de banco de dados para a Autenticação do Windows &#40;SQL Server&#41;](../../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md) ou [Permitir que um ponto de extremidade de espelhamento de banco de dados use certificados para conexões de saída &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md).  
  
2.  Verifique se os números da porta estão corretos.  
  
     Para identificar a porta associada atualmente com o ponto de extremidade de espelhamento de banco de dados de uma instância de servidor, use a seguinte instrução do [!INCLUDE[tsql](../../../includes/tsql-md.md)] :  
  
    ```  
    SELECT type_desc, port FROM sys.tcp_endpoints;  
    GO  
    ```  
  
3.  Para os problemas da configuração do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] que forem difíceis de explicar, recomendamos que você inspecione cada instância do servidor para determinar se ela está escutando nas portas corretas.  
  
4.  Verifique se os pontos de extremidade foram iniciados (STATE=STARTED). Em cada instância do servidor, use a seguinte instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)]:  
  
    ```  
    SELECT state_desc FROM sys.database_mirroring_endpoints  
    ```  
  
     Para obter mais informações sobre a coluna **state_desc**, veja [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md).  
  
     Para iniciar um ponto de extremidade, use a seguinte instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)]:  
  
    ```  
    ALTER ENDPOINT Endpoint_Mirroring   
    STATE = STARTED   
    AS TCP (LISTENER_PORT = <port_number>)  
    FOR database_mirroring (ROLE = ALL);  
    GO  
    ```  
  
     Para obter mais informações, veja [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-endpoint-transact-sql.md).  
  
5.  Verifique se o logon do outro servidor tem permissão CONNECT. Para determinar quem tem permissão CONNECT para um ponto de extremidade, em cada instância do servidor, use a seguinte instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] :  
  
    ```  
    SELECT 'Metadata Check';  
    SELECT EP.name, SP.STATE,   
       CONVERT(nvarchar(38), suser_name(SP.grantor_principal_id))   
          AS GRANTOR,   
       SP.TYPE AS PERMISSION,  
       CONVERT(nvarchar(46),suser_name(SP.grantee_principal_id))   
          AS GRANTEE   
       FROM sys.server_permissions SP , sys.endpoints EP  
       WHERE SP.major_id = EP.endpoint_id  
       ORDER BY Permission,grantor, grantee;   
    GO  
  
    ```  
  
##  <a name="SystemName"></a> System Name  
 Para o nome de sistema de uma instância do servidor em uma URL de ponto de extremidade, você pode usar qualquer nome que identifique o sistema inequivocamente. O endereço de servidor pode ser um nome de sistema (se os sistemas estiverem no mesmo domínio), um nome de domínio totalmente qualificado ou um endereço de IP (preferivelmente, um endereço de IP estático). Usando o nome de domínio totalmente qualificado o funcionamento é garantido. Para obter mais informações, consulte [Especificar a URL do ponto de extremidade ao adicionar ou modificar uma réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md).  
  
##  <a name="NetworkAccess"></a> Network Access  
 Cada instância do servidor que esteja hospedando uma réplica de disponibilidade deve poder acessar a porta de cada uma das instâncias do servidor sobre TCP. Isso será especialmente importante se as instâncias do servidor estiverem em domínios diferentes que não confiam um no outro (domínios não confiáveis).  
  
##  <a name="Msg1418"></a> Acesso ao ponto de extremidade (erro 1418 do SQL Server)  
 Essa mensagem do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] indica que o endereço de rede do servidor especificado na URL do ponto de extremidade não pode ser atingido ou não existe e sugere que você verifique o nome do endereço de rede e emita o comando novamente.  
  
##  <a name="JoinDbFails"></a> Falha ao unir bancos de dados (erro 35250 do SQL Server)  
 Discute as possíveis causas e resolução de uma falha ao unir bancos de dados secundários a um grupo de disponibilidade porque a conexão com a réplica primária não está ativa.  
  
 **Resolução:**  
  
1.  Verifique a configuração do firewall para confirmar se ele permite comunicação da porta do ponto de extremidade entre as instâncias do servidor que hospedam a réplica primária e a réplica secundária (por padrão, a porta 5022).  
  
2.  Verifique se a conta de serviço de rede tem permissão para conectar-se ao ponto de extremidade.  
  
##  <a name="ROR"></a> O roteamento somente leitura não está funcionando corretamente  
 Verifique as configurações de valores a seguir e corrija-as se necessário.  
  
||Em...|Ação|Comentários|Link|  
|------|---------|------------|--------------|----------|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Réplica primária atual|Verifique se o ouvinte do grupo de disponibilidade está online.|**Para verificar se o ouvinte está online:**<br /><br /> `SELECT * FROM sys.dm_tcp_listener_states;`<br /><br /> **Para reiniciar um ouvinte offline:**<br /><br /> `ALTER AVAILABILITY GROUP myAG RESTART LISTENER 'myAG_Listener';`|[sys.dm_tcp_listener_states &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql.md)<br /><br /> [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Réplica primária atual|Verifique se READ_ONLY_ROUTING_LIST contém somente instâncias de servidor que hospedem uma réplica secundária legível.|**Para identificar réplicas secundárias legíveis:** sys.availability_replicas (coluna**secondary_role_allow_connections_desc** )<br /><br /> **Para exibir uma lista de roteamento somente leitura:** sys.availability_read_only_routing_lists<br /><br /> **Para alterar uma lista de roteamento somente leitura:** ALTER AVAILABILITY GROUP|[sys.availability_replicas &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)<br /><br /> [sys.availability_read_only_routing_lists &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-availability-read-only-routing-lists-transact-sql.md)<br /><br /> [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Cada réplica em read_only_routing_list|Verifique se o firewall do Windows não está bloqueando a porta READ_ONLY_ROUTING_URL.|—|[Configurar um Firewall do Windows para acesso ao Mecanismo de Banco de Dados](../../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Cada réplica em read_only_routing_list|No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager, verifique se:<br /><br /> A conectividade remota do SQL Server está habilitada.<br /><br /> TCP/IP está habilitado.<br /><br /> Os endereços IP estão configurados corretamente.|—|[Exibir ou alterar as propriedades de servidor &#40;SQL Server&#41;](../../../database-engine/configure-windows/view-or-change-server-properties-sql-server.md)<br /><br /> [Configurar um servidor para escuta em uma porta TCP específica &#40;SQL Server Configuration Manager&#41;](../../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Cada réplica em read_only_routing_list|Verifique se READ_ONLY_ROUTING_URL (TCP**://***system-address***:***port*) contém o FQDN (nome de domínio totalmente qualificado) e o número da porta corretos.|—|[Calculando read_only_routing_url do AlwaysOn](http://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-Always%20On.aspx)<br /><br /> [sys.availability_replicas &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)<br /><br /> [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)|  
|![Caixa de seleção](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Sistema cliente|Verifique se o driver cliente dá suporte a roteamento somente leitura.|—|[Conectividade de cliente AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md)|  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Criação e configuração de grupos de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)  
  
-   [Criar um ponto de extremidade de espelhamento de banco de dados para a Autenticação do Windows &#40;SQL Server&#41;](../../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Especificar a URL do ponto de extremidade ao adicionar ou modificar uma réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
-   [Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [Solução de problemas de uma operação de adição de arquivos com falha &#40;Grupos de disponibilidade de AlwaysOn&#41;](../../../database-engine/availability-groups/windows/troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
-   [Gerenciamento de logons e trabalhos para os bancos de dados de um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/logins-and-jobs-for-availability-group-databases.md)  
  
-   [Gerenciar metadados ao disponibilizar um banco de dados em outra instância do servidor &#40;SQL Server&#41;](../../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)  
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
  
-   [Exibir eventos e logs de um cluster de failover](http://technet.microsoft.com/library/cc772342\(WS.10\).aspx)  
  
-   [Cluster de failover Get-ClusterLog do cmdlet](http://technet.microsoft.com/library/ee461045.aspx)  
  
-   [Blog da equipe do AlwaysOn do SQL Server: o blog oficial da equipe do AlwaysOn do SQL Server](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
## <a name="see-also"></a>Consulte também  
 [Segurança de transporte para espelhamento de banco de dados e grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [Configuração de rede do cliente](../../../database-engine/configure-windows/client-network-configuration.md)   
 [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)  
  
  

