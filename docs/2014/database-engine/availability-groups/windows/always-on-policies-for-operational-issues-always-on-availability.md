---
title: Políticas AlwaysOn para problemas operacionais com grupos de disponibilidade (SQL Server) Always On | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], troubleshooting
- Availability Groups [SQL Server], policies
ms.assetid: afa5289c-641a-4c03-8749-44862384ec5f
caps.latest.revision: 19
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 44d086a00d2e18bfd87410848a5acd73461fac6d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37287912"
---
# <a name="always-on-policies-for-operational-issues-with-always-on-availability-groups-sql-server"></a>Políticas AlwaysOn para problemas operacionais com grupos de disponibilidade AlwaysOn (SQL Server)
  O modelo de integridade do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] avalia um conjunto de políticas predefinidas de gerenciamento baseado em políticas (PBM). Você pode usar essas políticas para visualizar a integridade de um grupo de disponibilidade e suas réplicas de disponibilidade e bancos de dados no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
 
  
##  <a name="TermsAndDefinitions"></a> Termos e definições  
 Políticas predefinidas AlwaysOn  
 Um conjunto de políticas internas que permitem que um administrador de banco de dados verifique um grupo de disponibilidade e suas réplicas de disponibilidade e bancos de dados quanto à conformidade com os estados definidos pelas políticas AlwaysOn.  
  
 [Grupos de disponibilidade AlwaysOn](always-on-availability-groups-sql-server.md) uma solução de alta disponibilidade e recuperação de desastres que fornece uma alternativa de nível corporativo para espelhamento de banco de dados.  
  
 grupo de disponibilidade  
 Um contêiner para um conjunto discreto de bancos de dados de usuário, conhecido como *bancos de dados de disponibilidade*, que executam failover juntos.  
  
 réplica de disponibilidade  
 Uma instanciação de um grupo de disponibilidade que é hospedado por uma instância específica do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e que mantém uma cópia local de cada banco de dados de disponibilidade pertencente ao grupo de disponibilidade. Existem dois tipos de réplica de disponibilidade: uma única *réplica primária* e uma a quatro *réplicas secundárias*. As instâncias do servidor que hospedam as réplicas de disponibilidade de um determinado grupo de disponibilidade residem em nós diferentes de um único cluster do WSFC (Windows Server Failover Clustering).  
  
 banco de dados de disponibilidade  
 Um banco de dados que pertence a um grupo de disponibilidade. Para cada banco de dados de disponibilidade, o grupo de disponibilidade mantém uma única cópia de leitura-gravação (o *banco de dados primário*) e uma a quatro cópias somente leitura (*bancos de dados secundários*).  
  
 Painel AlwaysOn  
 O painel do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] que fornece uma visão geral da integridade de um grupo de disponibilidade. Para obter mais informações, consulte [Painel AlwaysOn](#Dashboard)mais adiante neste tópico.  
  
##  <a name="AlwaysOnPBM"></a> Políticas predefinidas e problemas  
 A tabela a seguir resume as políticas predefinidas.  
  
|Nome de política|Problema|Categoria**<sup>*</sup>**|Faceta|  
|-----------------|-----------|------------------------------|-----------|  
|Estado do cluster WSFC|[WSFC cluster service is offline](wsfc-cluster-service-is-offline.md).|Crítico|Instância do SQL Server|  
|Estado Online do Grupo de Disponibilidade|[Availability group is offline](availability-group-is-offline.md).|Crítico|grupo de disponibilidade|  
|Prontidão para Failover Automático do Grupo de Disponibilidade|[Availability group is not ready for automatic failover](availability-group-is-not-ready-for-automatic-failover.md).|Crítico|grupo de disponibilidade|  
|Estado de Sincronização de Dados de Réplicas de Disponibilidade|[Some availability replicas are not synchronizing data](some-availability-replicas-are-not-synchronizing-data.md).|Aviso|grupo de disponibilidade|  
|Estado de sincronização de dados de réplicas síncronas|[Some synchronous replicas are not synchronized](some-synchronous-replicas-are-not-synchronized.md).|Aviso|grupo de disponibilidade|  
|Estado da Função das Réplica de Disponibilidade|[Some availability replicas do not have a healthy role](some-availability-replicas-do-not-have-a-healthy-role.md).|Aviso|grupo de disponibilidade|  
|Estado da conexão em réplicas de disponibilidade|[Some availability replicas are disconnected](some-availability-replicas-are-disconnected.md).|Aviso|grupo de disponibilidade|  
|Estado da função da réplica de disponibilidade|[Availability replica does not have a healthy role](availability-replica-does-not-have-a-healthy-role.md).|Crítico|réplica de disponibilidade|  
|Estado da Conexão da Réplica de Disponibilidade|[Availability replica is disconnected](availability-replica-is-disconnected.md).|Crítico|Réplica de disponibilidade|  
|Estado da junção da réplica de disponibilidade|[A réplica de disponibilidade não está unida](availability-replica-is-not-joined.md).|Aviso|Réplica de disponibilidade|  
|Estado de Sincronização de Dados de Réplicas de Disponibilidade|[Data synchronization state of some availability database is not healthy](data-synchronization-state-of-some-availability-database-is-not-healthy.md).|Aviso|Réplica de disponibilidade|  
|Estado de Suspensão do Banco de Dados de Disponibilidade|[Availability database is suspended](availability-database-is-suspended.md).|Aviso|Banco de dados de disponibilidade|  
|Estado de junção do banco de dados de disponibilidade|[Secondary database is not joined](secondary-database-is-not-joined.md).|Aviso|Banco de dados de disponibilidade|  
|Estado de Sincronização dos Dados do Banco de Dados de Disponibilidade|[Data synchronization state of availability database is not healthy](data-synchronization-state-of-availability-database-is-not-healthy.md).|Aviso|Banco de dados de disponibilidade|  
  
> [!IMPORTANT]  
>  **<sup>*</sup>**  Para políticas de AlwaysOn, os nomes das categorias são usados como IDs. A alteração do nome de uma categoria AlwaysOn interrompe sua funcionalidade de avaliação de integridade. Portanto, não modifique os nomes das categorias AlwaysOn.  
  
##  <a name="Dashboard"></a> Painel AlwaysOn  
 O Painel AlwaysOn apresenta uma visão geral da integridade de um grupo de disponibilidade. O Painel AlwaysOn inclui os seguintes recursos gerais:  
  
-   Permite que você exiba facilmente os detalhes sobre um determinado grupo de disponibilidade, suas réplicas de disponibilidade e seus bancos de dados.  
  
-   Exibe indicações visuais dos estados principais para ajudar os administradores de bancos de dados a tomarem decisões operacionais rápidas.  
  
-   Fornece pontos de lançamento para cenários de solução de problemas.  
  
-   Para um determinado problema operacional, preenche a caixa de diálogo **Resultado de Avaliação de Política** com informações sobre violações de política de integridade AlwaysOn específicas e com links para ajuda com a solução.  
  
-   Fornece um visualizador de eventos estendido de integridade para mostrar eventos anteriores para problemas específicos AlwaysOn.  
  
-   Se o failover do grupo de disponibilidade for uma solução possível para um problema, fornece um ponto de inicialização para os links[Assistente de Grupo de Disponibilidade de Failover](use-the-fail-over-availability-group-wizard-sql-server-management-studio.md). Esse assistente orienta um administrador de banco de dados durante o processo de failover manual.  
  
##  <a name="ExtendHealthModel"></a> Estendendo o modelo de integridade do AlwaysOn  
 Estender o modelo de integridade do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] é simplesmente uma questão de criar suas próprias políticas definidas pelo usuário e colocá-las em certas categorias com base no tipo de objeto que você está monitorando.  Depois que você alterar algumas configurações, o painel AlwaysOn avaliará automaticamente suas próprias políticas definidas pelo usuário, assim como as políticas predefinidas AlwaysOn.  
  
 Uma política definida pelo usuário pode usar qualquer uma das facetas de PBM disponíveis, inclusive as usadas pelas políticas predefinidas AlwaysOn (consulte [Políticas predefinidas e problemas](#AlwaysOnPBM), anteriormente neste tópico). A faceta do servidor fornece as seguintes propriedades para monitorar [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] integridade: (`IsHadrEnabled` e `HadrManagerStatus`). A faceta do Servidor também fornece às propriedades as políticas a seguir para monitorar a configuração do cluster WSFC: `ClusterQuorumType` e `ClusterQuorumState`.  
  
 Para obter mais informações, consulte [The AlwaysOn Health Model Part 2 -- Extending the Health Model](http://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/extending-the-alwayson-health-model.aspx) (O modelo de integridade AlwaysOn Parte 2 – Estendendo o modelo de integridade) (um blog da equipe do AlwaysOn do SQL Server).  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Use as políticas AlwaysOn para exibir a integridade de um grupo de disponibilidade &#40;SQL Server&#41;](use-always-on-policies-to-view-the-health-of-an-availability-group-sql-server.md)  
  
-   [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
-   [Recuperação de desastres do WSFC por meio de quorum forçado &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-disaster-recovery-through-forced-quorum-sql-server.md)  
  
-   [Forçar um cluster WSFC para iniciar sem um quorum](../../../sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum.md)  
  
-   [Executar um failover manual forçado de um grupo de disponibilidade &#40;SQL Server&#41;](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [Solucionar problemas de uma operação de adição de arquivos com falha &#40;grupos de disponibilidade AlwaysOn&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
  
-   [O modelo de integridade AlwaysOn parte 1 – arquitetura do modelo de integridade](http://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/extending-the-alwayson-health-model.aspx)  
  
-   [O modelo de integridade AlwaysOn parte 2 – Extending the Health Model](http://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/extending-the-alwayson-health-model.aspx)  
  
-   [Guia de soluções do Microsoft SQL Server AlwaysOn para alta disponibilidade e recuperação de desastres](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
## <a name="see-also"></a>Consulte também  
 [Grupos de disponibilidade AlwaysOn (SQL Server)](always-on-availability-groups-sql-server.md)   
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Administração de um grupo de disponibilidade &#40;SQL Server&#41;](administration-of-an-availability-group-sql-server.md)   
 [Monitoramento de grupos de disponibilidade &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)  
  
  
