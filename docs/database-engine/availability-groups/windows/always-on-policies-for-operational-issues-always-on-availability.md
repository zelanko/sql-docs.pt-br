---
title: "Políticas AlwaysOn para problemas operacionais – disponibilidade AlwaysOn | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], troubleshooting
- Availability Groups [SQL Server], policies
ms.assetid: afa5289c-641a-4c03-8749-44862384ec5f
caps.latest.revision: 19
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c8256ee37c22d96961c78b5c5a057c0e60b81269
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="always-on-policies-for-operational-issues---always-on-availability"></a>Políticas AlwaysOn para problemas operacionais – disponibilidade AlwaysOn
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  O modelo de integridade do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] avalia um conjunto de políticas predefinidas de gerenciamento baseado em políticas (PBM). Você pode usar essas políticas para visualizar a integridade de um grupo de disponibilidade e suas réplicas de disponibilidade e bancos de dados no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
 **Neste tópico:**  
  
-   [Termos e definições](#TermsAndDefinitions)  
  
-   [Políticas predefinidas e problemas](#Always OnPBM)  
  
-   [Painel AlwaysOn](#Dashboard)  
  
-   [Estendendo o modelo de integridade AlwaysOn](#ExtendHealthModel)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
-   [Conteúdo relacionado](#RelatedContent)  
  
##  <a name="TermsAndDefinitions"></a> Termos e definições  
 Políticas predefinidas AlwaysOn  
 Um conjunto de políticas internas que permitem que um administrador de banco de dados verifique um grupo de disponibilidade e suas réplicas de disponibilidade e bancos de dados quanto à conformidade com os estados definidos pelas políticas AlwaysOn.  
  
 [Grupos de Disponibilidade AlwaysOn](../../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
 Uma solução de alta disponibilidade e de recuperação de desastres que fornece uma alternativa em nível corporativo para espelhamento de banco de dados.  
  
 grupo de disponibilidade  
 Um contêiner para um conjunto discreto de bancos de dados de usuário, conhecido como *bancos de dados de disponibilidade*, que executam failover juntos.  
  
 réplica de disponibilidade  
 Uma instanciação de um grupo de disponibilidade que é hospedado por uma instância específica do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e que mantém uma cópia local de cada banco de dados de disponibilidade pertencente ao grupo de disponibilidade. Existem dois tipos de réplica de disponibilidade: uma única *réplica primária* e uma a quatro *réplicas secundárias*. As instâncias do servidor que hospedam as réplicas de disponibilidade de um determinado grupo de disponibilidade residem em nós diferentes de um único cluster do WSFC (Windows Server Failover Clustering).  
  
 banco de dados de disponibilidade  
 Um banco de dados que pertence a um grupo de disponibilidade. Para cada banco de dados de disponibilidade, o grupo de disponibilidade mantém uma única cópia de leitura-gravação (o *banco de dados primário*) e uma a quatro cópias somente leitura (*bancos de dados secundários*).  
  
 Painel AlwaysOn  
 O painel do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] que fornece uma visão geral da integridade de um grupo de disponibilidade. Para obter mais informações, veja [Painel AlwaysOn](#Dashboard), mais adiante neste tópico.  
  
##  <a name="Always OnPBM"></a> Políticas predefinidas e problemas  
 A tabela a seguir resume as políticas predefinidas.  
  
|Nome de política|Problema|Categoria**\***|Faceta|  
|-----------------|-----------|--------------------|-----------|  
|Estado do cluster WSFC|[O serviço de cluster WSFC está offline](../../../database-engine/availability-groups/windows/wsfc-cluster-service-is-offline.md).|Crítico|Instância do SQL Server|  
|Estado Online do Grupo de Disponibilidade|[O grupo de disponibilidade está offline](../../../database-engine/availability-groups/windows/availability-group-is-offline.md).|Crítico|grupo de disponibilidade|  
|Prontidão para Failover Automático do Grupo de Disponibilidade|[O grupo de disponibilidade não está pronto para o failover automático](../../../database-engine/availability-groups/windows/availability-group-is-not-ready-for-automatic-failover.md).|Crítico|grupo de disponibilidade|  
|Estado de Sincronização de Dados de Réplicas de Disponibilidade|[Algumas réplicas de disponibilidade não estão sincronizando dados](../../../database-engine/availability-groups/windows/some-availability-replicas-are-not-synchronizing-data.md).|Aviso|grupo de disponibilidade|  
|Estado de sincronização de dados de réplicas síncronas|[Algumas réplicas síncronas não estão sincronizadas](../../../database-engine/availability-groups/windows/some-synchronous-replicas-are-not-synchronized.md).|Aviso|grupo de disponibilidade|  
|Estado da Função das Réplica de Disponibilidade|[Algumas réplicas de disponibilidade não têm uma função íntegra](../../../database-engine/availability-groups/windows/some-availability-replicas-do-not-have-a-healthy-role.md).|Aviso|grupo de disponibilidade|  
|Estado da conexão em réplicas de disponibilidade|[Algumas réplicas de disponibilidade estão desconectadas](../../../database-engine/availability-groups/windows/some-availability-replicas-are-disconnected.md).|Aviso|grupo de disponibilidade|  
|Estado da função da réplica de disponibilidade|[A réplica de disponibilidade não tem uma função íntegra](../../../database-engine/availability-groups/windows/availability-replica-does-not-have-a-healthy-role.md).|Crítico|réplica de disponibilidade|  
|Estado da Conexão da Réplica de Disponibilidade|[A réplica de disponibilidade está desconectada](../../../database-engine/availability-groups/windows/availability-replica-is-disconnected.md).|Crítico|réplica de disponibilidade|  
|Estado da junção da réplica de disponibilidade|[A réplica de disponibilidade não está unida](../../../database-engine/availability-groups/windows/availability-replica-is-not-joined.md).|Aviso|réplica de disponibilidade|  
|Estado de Sincronização de Dados de Réplicas de Disponibilidade|[O estado de sincronização de dados de algum banco de dados de disponibilidade não está íntegro](../../../database-engine/availability-groups/windows/data-synchronization-state-of-some-availability-database-is-not-healthy.md).|Aviso|réplica de disponibilidade|  
|Estado de Suspensão do Banco de Dados de Disponibilidade|[Banco de dados de disponibilidade está suspenso](../../../database-engine/availability-groups/windows/availability-database-is-suspended.md).|Aviso|banco de dados de disponibilidade|  
|Estado de junção do banco de dados de disponibilidade|[O banco de dados secundário não está unido](../../../database-engine/availability-groups/windows/secondary-database-is-not-joined.md).|Aviso|banco de dados de disponibilidade|  
|Estado de Sincronização dos Dados do Banco de Dados de Disponibilidade|[O estado de sincronização de dados do banco de dados de disponibilidade não está íntegro](../../../database-engine/availability-groups/windows/data-synchronization-state-of-availability-database-is-not-healthy.md).|Aviso|banco de dados de disponibilidade|  
  
> [!IMPORTANT]  
>  **\*** Para as políticas AlwaysOn, os nomes das categorias são usados como IDs. A alteração do nome de uma categoria AlwaysOn interrompe sua funcionalidade de avaliação de integridade. Portanto, não modifique os nomes das categorias AlwaysOn.  
  
##  <a name="Dashboard"></a> Painel AlwaysOn  
 O Painel AlwaysOn apresenta uma visão geral da integridade de um grupo de disponibilidade. O Painel AlwaysOn inclui os seguintes recursos:  
  
-   Permite que você exiba facilmente os detalhes sobre um determinado grupo de disponibilidade, suas réplicas de disponibilidade e seus bancos de dados.  
  
-   Exibe indicações visuais dos estados principais para ajudar os administradores de bancos de dados a tomarem decisões operacionais rápidas.  
  
-   Fornece pontos de lançamento para cenários de solução de problemas.  
  
-   Para determinado problema operacional, popula a caixa de diálogo **Resultado de Avaliação de Política** com informações sobre violações de política de integridade AlwaysOn específicas e com links para ajuda com a solução.  
  
-   Fornece um visualizador de eventos estendido de integridade para mostrar eventos anteriores para problemas específicos AlwaysOn.  
  
-   Se o failover do grupo de disponibilidade for uma solução possível para um problema, fornece um ponto de inicialização para os links[Assistente de Grupo de Disponibilidade de Failover](../../../database-engine/availability-groups/windows/use-the-fail-over-availability-group-wizard-sql-server-management-studio.md). Esse assistente orienta um administrador de banco de dados durante o processo de failover manual.  
  
##  <a name="ExtendHealthModel"></a> Estendendo o modelo de integridade AlwaysOn  
 Estender o modelo de integridade do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] é simplesmente uma questão de criar suas próprias políticas definidas pelo usuário e colocá-las em certas categorias com base no tipo de objeto que você está monitorando.  Depois que você alterar algumas configurações, o painel AlwaysOn avaliará automaticamente suas próprias políticas definidas pelo usuário, assim como as políticas predefinidas AlwaysOn.  
  
 Uma política definida pelo usuário pode usar qualquer uma das facetas de PBM disponíveis, inclusive as usadas pelas políticas predefinidas AlwaysOn (veja [Políticas predefinidas e problemas](#Always OnPBM), acima neste tópico). A faceta do Servidor fornece as seguintes propriedades para monitorar a integridade do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] : (**IsHadrEnabled** e **HadrManagerStatus**). A faceta do Servidor também fornece às propriedades as políticas a seguir para monitorar a configuração do cluster WSFC: **ClusterQuorumType**e **ClusterQuorumState**.  
  
 Para obter mais informações, veja [The Always On Health Model Part 2 – Extending the Health Model](http://blogs.msdn.com/b/sqlAlways On/archive/2012/02/13/extending-the-Always On-health-model.aspx) (O modelo de integridade AlwaysOn Parte 2 – Arquitetura do modelo de integridade) (um blog da equipe AlwaysOn do SQL Server).  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Usar as políticas AlwaysOn para exibir a integridade de um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/use-always-on-policies-to-view-the-health-of-an-availability-group-sql-server.md)  
  
-   [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
-   [Recuperação de desastres do WSFC por meio de quorum forçado &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-disaster-recovery-through-forced-quorum-sql-server.md)  
  
-   [Forçar um cluster WSFC para iniciar sem um quorum](../../../sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum.md)  
  
-   [Executar um failover manual forçado de um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [Solução de problemas de uma operação de adição de arquivos com falha &#40;Grupos de disponibilidade de AlwaysOn&#41;](../../../database-engine/availability-groups/windows/troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
  
-   [The Always On Health Model Part 1 – Health Model Architecture (O modelo de integridade AlwaysOn Parte 1 – Arquitetura do modelo de integridade)](http://blogs.msdn.com/b/sqlAlways On/archive/2012/02/13/extending-the-Always On-health-model.aspx)  
  
-   [The Always On Health Model Part 2 – Extending the Health Model](http://blogs.msdn.com/b/sqlAlways On/archive/2012/02/13/extending-the-Always On-health-model.aspx)  
  
-   [Guia de soluções AlwaysOn do Microsoft SQL Server para alta disponibilidade e recuperação de desastre](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
## <a name="see-also"></a>Consulte também  
 [Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Administração de um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/administration-of-an-availability-group-sql-server.md)   
 [Monitoramento de grupos de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/monitoring-of-availability-groups-sql-server.md)  
  
  

