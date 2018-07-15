---
title: Introdução aos grupos de disponibilidade AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], about
ms.assetid: 33f2f2d0-79e0-4107-9902-d67019b826aa
caps.latest.revision: 51
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3700a2e2d7b96a572fd8c72210a5d287ca56cf6e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37237636"
---
# <a name="getting-started-with-alwayson-availability-groups-sql-server"></a>Introdução aos Grupos de Disponibilidade AlwaysOn (SQL Server)
  Este tópico apresenta as etapas para configurar instâncias do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] para dar suporte a [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] e para criar, gerenciar e monitorar um grupo de disponibilidade.  
  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="RecommendedReading"></a> Leitura recomendada  
 Antes de criar seu primeiro grupo de disponibilidade, recomendamos que você leia os seguintes tópicos:  
  
-   [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
-   [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)  
  
##  <a name="ConfigSI"></a> Configurando uma instância do SQL Server para dar suporte a grupos de disponibilidade AlwaysOn  
  
||Etapa|Links|  
|------|----------|-----------|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|**Habilitar [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)].** O recurso [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] deve estar habilitado em cada instância do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] que participará de um grupo de disponibilidade.<br /><br /> **Pré-requisitos:** o computador host deve ser um nó do WSFC (Clustering de Failover do Windows Server).<br /><br /> Para obter informações sobre outros pré-requisitos, consulte "Pré-requisitos e restrições da Instância do SQL Server"em [Pré-requisitos, restrições e recomendações para Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).|[Habilitar e desabilitar grupos de disponibilidade AlwaysOn](enable-and-disable-always-on-availability-groups-sql-server.md)|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|**Criar um ponto de extremidade de espelhamento de banco de dados (se não houver).** Verifique se cada instância de servidor tem um [ponto de extremidade de espelhamento de banco de dados](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md). A instância de servidor usa este ponto de extremidade para receber conexões de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] de outras instâncias de servidor.|Para determinar se um ponto de extremidade de espelhamento de banco de dados existe: [sys.database_mirroring_endpoints](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)<br /><br /> **Para a Autenticação do Windows:** Para criar um ponto de extremidade de espelhamento de banco de dados usando:<br /><br /> [Assistente de grupo de nova disponibilidade](use-the-availability-group-wizard-sql-server-management-studio.md)<br /><br /> [Transact-SQL](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)<br /><br /> [SQL Server PowerShell](database-mirroring-always-on-availability-groups-powershell.md)<br /><br /> **Para a autenticação de certificado:**  para criar um ponto de extremidade do espelhamento de banco de dados, usando <br />                    [Transact-SQL](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)|  
  
##  <a name="ConfigAG"></a> Creating and Configuring a New Availability Group  
  
||Etapa|Links|  
|------|----------|-----------|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|**Crie o grupo de disponibilidade.** Crie o grupo de disponibilidade na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda os bancos de dados a serem adicionados ao grupo de disponibilidade.<br /><br /> Minimamente, crie a réplica primária inicial na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] onde você cria o grupo de disponibilidade. Você também pode especificar de um a quatro réplicas secundárias. Para obter informações sobre grupos de disponibilidade e propriedades da réplica, consulte [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-availability-group-transact-sql).<br /><br /> Recomendamos expressamente criar um [ouvinte de grupos de disponibilidade](../../listeners-client-connectivity-application-failover.md).<br /><br /> **Pré-requisitos:**  as instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospedam réplicas de disponibilidade de determinado grupo de disponibilidade devem residir em nós separados de um único cluster WSFC. A única exceção é que, embora tenha sido migrado para outro cluster WSFC, um grupo de disponibilidade pode temporariamente abranger dois clusters.<br /><br /> Para obter informações sobre outros pré-requisitos, consulte "Pré-requisitos e restrições de grupos de disponibilidade", "Pré-requisitos e restrições de bancos de dados de disponibilidade" e "Pré-requisitos e restrições de instâncias do SQL Server" em [Pré-requisitos, restrições e recomendações para Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).|Para criar um grupo de disponibilidade, você poderá usar qualquer uma das ferramentas a seguir:<br /><br /> [Assistente de grupo de nova disponibilidade](use-the-availability-group-wizard-sql-server-management-studio.md)<br /><br /> [Transact-SQL](create-an-availability-group-transact-sql.md)<br /><br /> [SQL Server PowerShell](create-an-availability-group-transact-sql.md)|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|**Unir réplicas secundárias ao grupo de disponibilidade.** Conecte a cada instância do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] que está hospedando uma réplica secundária e una a réplica secundária local ao grupo de disponibilidade.|[Unir uma réplica secundária a um grupo de disponibilidade](join-a-secondary-replica-to-an-availability-group-sql-server.md)<br /><br /> Dica: se você usar o assistente de Novo Grupo de Disponibilidade, esta etapa será automatizada.|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|**Preparar bancos de dados secundários.** Em cada instância de servidor que está hospedando uma réplica secundária, restaure os backups dos bancos de dados primários usando RESTORE WITH NORECOVERY.|[Prepare manualmente um banco de dados secundário](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)<br /><br /> Dica: o Assistente de Novo Grupo de Disponibilidade pode preparar os bancos de dados secundários para você. Para obter mais informações, consulte "Pré-requisitos para usar a sincronização de dados inicial total" em [Selecionar página de sincronização de dados inicial &#40;Assistentes do Grupo de Disponibilidade AlwaysOn&#41;](select-initial-data-synchronization-page-always-on-availability-group-wizards.md).|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|**Unir bancos de dados secundários ao grupo de disponibilidade.** Em cada instância de servidor que está hospedando uma réplica secundária, una cada banco de dados secundário local ao grupo de disponibilidade. Ao unir o grupo de disponibilidade, um determinado banco de dados secundário inicia a sincronização de dados com o banco de dados primário correspondente.|[Unir um banco de dados secundário a um grupo de disponibilidade](join-a-secondary-database-to-an-availability-group-sql-server.md)<br /><br /> Dica: o Assistente de Novo Grupo de Disponibilidade poderá executar esta etapa se cada banco de dados secundário existir em cada réplica secundária.|  
||**Criar um ouvinte de grupo de disponibilidade.**  Esta etapa é necessária a menos que você já tenha criado o ouvinte do grupo de disponibilidade enquanto criou o grupo de disponibilidade.|[Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|**Dê o nome de host DNS do ouvinte aos desenvolvedores de aplicativos.**  Desenvolvedores precisam especificar esse nome de DNS nas cadeias de conexão para direcionar solicitações de conexão para o ouvinte do grupo de disponibilidade. Para obter mais informações, consulte [Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativo &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md).|"Acompanhamento: depois de criar um ouvinte de grupo de disponibilidade" em [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)|  
|![Caixa de seleção](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|**Configurar onde estão os trabalhos de backup.**  Para executar backups em bancos de dados secundários, você deverá criar um script de trabalho de backup que leva em conta a preferência de backup automatizado. Criar um script para cada banco de dados no grupo de disponibilidade em cada instância de servidor que hospeda uma réplica de disponibilidade para o grupo de disponibilidade.|“Acompanhamento: depois de configurar o backup em réplicas secundárias” em [Configurar backup em réplicas de disponibilidade &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)|  
  
##  <a name="ManageAGsEtc"></a> Managing Availability Groups, Replicas, and Databases  
  
> [!NOTE]  
>  Para obter informações sobre grupos de disponibilidade e propriedades da réplica, consulte [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-availability-group-transact-sql).  
  
 O gerenciamento de grupos de disponibilidade existente envolve uma ou mais das seguintes tarefas:  
  
|Tarefa|Link|  
|----------|----------|  
|Modificar a [política de failover flexível](flexible-automatic-failover-policy-availability-group.md) do grupo de disponibilidade para controlar as condições que causam um failover automático. Essa política só será pertinente quando o failover automático for possível.|[Configurar a política de failover flexível de um grupo de disponibilidade](configure-flexible-automatic-failover-policy.md)|  
|Executar um failover manual planejado ou um failover manual forçado (com possível perda de dados), geralmente chamado *failover forçado*. Para obter mais informações, consulte [Failover e modos de failover &#40;Grupos de Disponibilidade AlwaysOn&#41;](failover-and-failover-modes-always-on-availability-groups.md).|[Executar um failover manual planejado](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)<br /><br /> [Executar um failover manual forçado](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)|  
|Usar um conjunto de políticas predefinidas para exibir da integridade de um grupo de disponibilidade e suas réplicas e bancos de dados.|[Usar o gerenciamento baseado em políticas para exibir a integridade de um grupo de disponibilidade](use-always-on-policies-to-view-the-health-of-an-availability-group-sql-server.md)<br /><br /> [Use o painel grupo AlwaysOn](use-the-always-on-dashboard-sql-server-management-studio.md)|  
|Adicionar ou remover uma réplica secundária.|[Adicionar uma réplica secundária](add-a-secondary-replica-to-an-availability-group-sql-server.md)<br /><br /> [Remover uma réplica secundária](remove-a-secondary-replica-from-an-availability-group-sql-server.md)|  
|Suspender ou retomar um banco de dados de disponibilidade. Suspender um banco de dados secundário mantém-no em seu ponto atual no tempo até que você o continue.|[Suspender um banco de dados](suspend-an-availability-database-sql-server.md)<br /><br /> [Retomar um banco de dados](resume-an-availability-database-sql-server.md)|  
|Adicionar ou remover um banco de dados.|[Adicionar um banco de dados](availability-group-add-a-database.md)<br /><br /> [Remover um banco de dados secundário](remove-a-secondary-database-from-an-availability-group-sql-server.md)<br /><br /> [Remover um banco de dados primário](remove-a-primary-database-from-an-availability-group-sql-server.md)|  
|Reconfigurar ou criar um ouvinte de grupo de disponibilidade.|[Criar ou configurar um ouvinte de grupo de disponibilidade](create-or-configure-an-availability-group-listener-sql-server.md)|  
|Excluir um grupo de disponibilidade.|[Excluir um grupo de disponibilidade](remove-an-availability-group-sql-server.md)|  
|Solucionar problemas de operações de adicionar arquivo. Isto pode ser necessário se o banco de dados primário e um banco de dados secundário tiverem caminhos de arquivos diferentes.|[Solucionar problemas de operações de adicionar arquivo com falha](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)|  
|Alterar as propriedades da réplica de disponibilidade.|[Alterar o modo de disponibilidade](change-the-availability-mode-of-an-availability-replica-sql-server.md)<br /><br /> [Alterar o modo de failover](change-the-failover-mode-of-an-availability-replica-sql-server.md)<br /><br /> [Configurar prioridade de backup (e preferência de backup automatizado)](configure-backup-on-availability-replicas-sql-server.md)<br /><br /> [Configurar acesso somente leitura](configure-read-only-access-on-an-availability-replica-sql-server.md)<br /><br /> [Configurar roteamento somente leitura](configure-read-only-routing-for-an-availability-group-sql-server.md)<br /><br /> [Alterar o período do tempo limite de sessão](change-the-session-timeout-period-for-an-availability-replica-sql-server.md)|  
  
##  <a name="MonitorAGsEtc"></a> Monitorando grupos de disponibilidade  
 Para monitorar as propriedades e o estado de um grupo de disponibilidade AlwaysOn, você pode usar as seguintes ferramentas.  
  
|Ferramenta|Descrição breve|Links|  
|----------|-----------------------|-----------|  
|Pacote de monitoramento do System Center para SQL Server|O pacote de Monitoramento para SQL Server (SQLMP) é a solução indicada para monitorar grupos de disponibilidade, réplica de disponibilidade e bancos de dados de disponibilidade para administradores de TI. Os recursos de monitoramento que são de particular relevância para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] incluem o seguinte:<br /><br /> Capacidade de descoberta automática de grupos de disponibilidade, réplicas de disponibilidade e banco de dados de disponibilidade dentre centenas de computadores. Isto permite que você mantenha o controle de seu inventário de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] .<br /><br /> Alertas e tickets totalmente capazes do System Center Operations Manager (SCOM). Estes recursos fornecem um conhecimento detalhado que permite uma resolução mais rápida para um problema.<br /><br /> Uma extensão personalizada para o monitoramento de integridade AlwaysOn usando um gerenciamento baseado em políticas (PBM).<br /><br /> Acúmulos de integridade de bancos de dados de disponibilidade para réplicas de disponibilidade.<br /><br /> Tarefas personalizadas que gerenciam o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] do console do System Center Operations Manager.|Para baixar o pacote de monitoramento (SQLServerMP.msi) e o *Guia do Pacote de Gerenciamento do SQL Server para System Center Operations Manager* (SQLServerMPGuide.doc), consulte:<br /><br /> [Pacote de monitoramento do System Center para SQL Server](http://www.microsoft.com/download/details.aspx?displaylang=en&id=10631)|  
|[!INCLUDE[tsql](../../../includes/tsql-md.md)]|[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] e as exibições de gerenciamento dinâmico fornecem informações preciosas sobre seus grupos de disponibilidade e suas réplicas, bancos de dados, ouvintes e ambiente de cluster WSFC.|[Monitorar grupos de disponibilidade &#40;Transact-SQL&#41;](monitor-availability-groups-transact-sql.md)|  
|[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|O painel **Detalhes do Pesquisador de Objetos** exibe informações básicas sobre os grupos de disponibilidade hospedados na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] à qual você está conectado.<br /><br /> Dica: use esse painel para selecionar vários grupos de disponibilidade, réplicas ou bancos de dados e executar tarefas administrativas rotineiras nos objetos selecionados; por exemplo, remover várias réplicas ou bancos de dados de disponibilidade de um grupo de disponibilidade.|[Use os Detalhes do Pesquisador de Objetos para monitorar grupos de disponibilidade](use-object-explorer-details-to-monitor-availability-groups.md)|  
|[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|As caixas de diálogo de**Propriedades** permitem que você exiba as propriedades dos grupos de disponibilidade, réplicas ou ouvintes e, em alguns casos, alterar os seus valores.|[Propriedades do grupo de disponibilidade](view-availability-group-properties-sql-server.md)<br /><br /> [Propriedades da réplica de disponibilidade](view-availability-replica-properties-sql-server.md)<br /><br /> [Propriedades do ouvinte do grupo de disponibilidade](view-availability-group-listener-properties-sql-server.md)|  
|Monitor do Sistema|O objeto de desempenho **SQLServer:Availability Replica** contém contadores de desempenho que relatam informações sobre réplicas de disponibilidade.|[SQL Server, Réplica de Disponibilidade](../../../relational-databases/performance-monitor/sql-server-availability-replica.md)|  
|Monitor do Sistema|O objeto de desempenho **SQLServer:Database Replica** contém contadores de desempenho que relatam informações sobre os bancos de dados secundários em uma determinada réplica secundária.<br /><br /> O objeto **SQLServer:Databases** no SQL Server contém contadores de desempenho que monitoram atividades do log de transações, entre outras coisas. Os contadores a seguir são particularmente relevantes para o monitoramento de atividades do log de transações em bancos de dados de disponibilidade: **Tempo de Gravação de Liberação de Log (ms)**, **Liberações de log/s**, **Erros de Cache do Pool de Logs/s**, **Leituras de Disco do Pool de Logs/s**e **Solicitações do Pool de Logs/s**.|[SQL Server, Réplica de banco de dados](../../../relational-databases/performance-monitor/sql-server-database-replica.md)<br /><br /> [SQL Server, objeto Databases](../../../relational-databases/performance-monitor/sql-server-databases-object.md)|  
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
  
-   **Vídeo — Introdução ao AlwaysOn:**  [Microsoft SQL Server codinome "Denali" Série AlwaysOn, Parte 1: Introduzindo a próxima geração de solução de alta disponibilidade](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
-   **Vídeo — um mergulho no AlwaysOn:**  [Microsoft SQL Server codinome "Denali" Série AlwaysOn, Parte 2: Criando uma solução de disponibilidade de missão crítica usando AlwaysOn](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **White paper:**  [Guia de soluções AlwaysOn do Microsoft SQL Server para alta disponibilidade e recuperação de desastre](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   **Blogs:**  [Blog da equipe do AlwaysOn do SQL Server: o blog oficial da equipe do AlwaysOn do SQL Server](http://blogs.msdn.com/b/sqlalwayson/)  
  
## <a name="see-also"></a>Consulte também  
 [Grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](always-on-availability-groups-sql-server.md)   
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Configuração de uma instância de servidor para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](configuration-of-a-server-instance-for-always-on-availability-groups-sql-server.md)   
 [Criação e configuração de grupos de disponibilidade &#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)   
 [Monitoramento de grupos de disponibilidade &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)   
 [Visão geral de instruções Transact-SQL para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](transact-sql-statements-for-always-on-availability-groups.md)   
 [Visão geral dos Cmdlets do PowerShell para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md)  
  
  
