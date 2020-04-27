---
title: Visão geral dos cmdlets do PowerShell para Grupos de Disponibilidade AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], PowerShell cmdlets
- Availability Groups [SQL Server], about
- PowerShell [SQL Server], cmdlets
ms.assetid: b3fef0d5-b6d7-4386-a0f0-d06c165ad4de
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4996a1026b4c85b105efc09b8381913f7a47942a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62789453"
---
# <a name="overview-of-powershell-cmdlets-for-alwayson-availability-groups-sql-server"></a>Visão geral de cmdlets do PowerShell para grupos de disponibilidade AlwaysOn (SQL Server)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] O PowerShell é um shell de linha de comando baseado em tarefa e linguagem de script criado especialmente para a administração do sistema. [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] fornece um conjunto de cmdlets do PowerShell no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] que permitem implantar, gerenciar e monitorar grupos de disponibilidade, réplicas de disponibilidade e bancos de dados de disponibilidade.  
  
> [!NOTE]  
>  Um cmdlet do PowerShell pode ser executado com o início bem-sucedido de uma ação. Isso não indica que o trabalho planejado, como o failover de um grupo de disponibilidade, foi concluído. Ao gerar o script de uma sequência de ações, talvez seja necessário verificar o status das ações e esperar que elas sejam concluídas.  
  
 Este tópico introduz os cmdlets para os seguintes conjuntos de tarefas:  
  
-   [Configurando uma instância de servidor para Grupos de Disponibilidade AlwaysOn](#ConfiguringServerInstance)  
  
-   [Fazendo backup e restaurando bancos de dados e logs de transações](#BnRcmdlets)  
  
-   [Criando e gerenciando um grupo de disponibilidade](#DeployManageAGs)  
  
-   [Criando e gerenciando um ouvinte de grupo de disponibilidade](#AGlisteners)  
  
-   [Criando e gerenciando uma réplica de disponibilidade](#DeployManageARs)  
  
-   [Adicionando e gerenciando um banco de dados de disponibilidade](#DeployManageDbs)  
  
-   [Monitorando a integridade de grupos de disponibilidade](#MonitorTblshtAGs)  
  
> [!NOTE]  
>  Para obter uma lista de tópicos [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] nos manuais online do que descrevem como usar cmdlets para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] executar tarefas, consulte a seção "tarefas relacionadas" de [visão geral do grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md).  
  
##  <a name="configuring-a-server-instance-for-alwayson-availability-groups"></a><a name="ConfiguringServerInstance"></a>Configurando uma instância de servidor para Grupos de Disponibilidade AlwaysOn  
  
|Cmdlets|Descrição|Com suporte em|  
|-------------|-----------------|------------------|  
|`Disable-SqlAlwaysOn`|Desabilita o recurso [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] em uma instância de servidor.|A instância de servidor que é especificada pelo parâmetro `Path`, `InputObject` ou `Name`. (Deve ser uma edição do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que dê suporte ao [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)].)|  
|`Enable-SqlAlwaysOn`|Habilita o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] em uma instância do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] que dá suporte ao recurso [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] . Para obter informações sobre o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]suporte para o, consulte [pré-requisitos, restrições e recomendações para Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).|Qualquer edição do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que dê suporte ao [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)].|  
|`New-SqlHadrEndPoint`|Cria um novo ponto de extremidade de espelhamento de banco de dados em uma instância de servidor. Esse ponto de extremidade é necessário para a movimentação de dados entre os bancos de dados primário e secundário.|Qualquer instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|  
|`Set-SqlHadrEndpoint`|Altera as propriedades de um ponto de extremidade de espelhamento de banco de dados existente, como o nome, o estado ou as propriedades de autenticação.|Uma instância de servidor que dá suporte ao [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] e não tem um ponto de extremidade de espelhamento de banco de dados.|  
  
##  <a name="backing-up-and-restoring-databases-and-transaction-logs"></a><a name="BnRcmdlets"></a>Fazendo backup e restaurando bancos de dados e logs de transações  
  
|Cmdlets|Descrição|Com suporte em|  
|-------------|-----------------|------------------|  
|`Backup-SqlDatabase`|Cria um backup de dados ou de log.|Qualquer banco de dados online (para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], um banco de dados na instância do servidor que hospeda a réplica primária).|  
|`Restore-SqlDatabase`|Restaura um backup.|Qualquer instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], uma instância de servidor que hospeda uma réplica secundária)<br /><br /> **&#42;&#42; importantes &#42;&#42;** Ao preparar um banco de dados secundário, você deve `-NoRecovery` usar o parâmetro `Restore-SqlDatabase` em cada comando.|  
  
 Para obter informações sobre como usar esses cmdlets para preparar um banco de dados secundário, veja [Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
  
##  <a name="creating-and-managing-an-availability-group"></a><a name="DeployManageAGs"></a>Criando e gerenciando um grupo de disponibilidade  
  
|Cmdlets|Descrição|Com suporte em|  
|-------------|-----------------|------------------|  
|`New-SqlAvailabilityGroup`|Cria um novo grupo de disponibilidade.|Instância de servidor para hospedar a réplica primária|  
|`Remove-SqlAvailabilityGroup`|Exclui um grupo de disponibilidade.|Instância de servidor habilitada para HADR|  
|`Set-SqlAvailabilityGroup`|Define as propriedades de um grupo de disponibilidade; coloca um grupo de disponibilidade online/offline|Instância de servidor que hospeda a réplica primária|  
|`Switch-SqlAvailabilityGroup`|Inicia um dos seguintes formulários de failover:<br /><br /> Um failover forçado de um grupo de disponibilidade (com possível perda de dados).<br /><br /> Um failover manual de um grupo de disponibilidade.|Instância de servidor que hospeda a réplica secundária de destino|  
  
##  <a name="creating-and-managing-an-availability-group-listener"></a><a name="AGlisteners"></a>Criando e gerenciando um ouvinte de grupo de disponibilidade  
  
|Cmdlet|Descrição|Com suporte em|  
|------------|-----------------|------------------|  
|`New-SqlAvailabilityGroupListener`|Cria um novo ouvinte de grupo de disponibilidade e conecta-o a um grupo de disponibilidade existente.|Instância de servidor que hospeda a réplica primária|  
|`Set-SqlAvailabilityGroupListener`|Modifica a configuração de porta em um ouvinte de grupo de disponibilidade existente.|Instância de servidor que hospeda a réplica primária|  
|`Add-SqlAvailabilityGroupListenerStaticIp`|Adiciona um endereço IP estático à configuração de um ouvinte de grupo de disponibilidade existente. O endereço IP poderá ser um endereço IPv4 com sub-rede ou um endereço IPv6.|Instância de servidor que hospeda a réplica primária|  
  
##  <a name="creating-and-managing-an-availability-replica"></a><a name="DeployManageARs"></a>Criando e gerenciando uma réplica de disponibilidade  
  
|Cmdlets|Descrição|Com suporte em|  
|-------------|-----------------|------------------|  
|**New-SqlAvailabilityReplica**|Cria uma nova réplica de disponibilidade. Você pode usar o parâmetro `-AsTemplate` para criar um objeto de réplica de disponibilidade de memória para cada nova réplica de disponibilidade.|Instância de servidor que hospeda a réplica primária|  
|`Join-SqlAvailabilityGroup`|Une uma réplica secundária ao grupo de disponibilidade.|Instância de servidor que hospeda a réplica secundária|  
|**Remove-SqlAvailabilityReplica**|Exclui uma réplica de disponibilidade.|Instância de servidor que hospeda a réplica primária|  
|`Set-SqlAvailabilityReplica`|Define as propriedades de uma réplica de disponibilidade.|Instância de servidor que hospeda a réplica primária|  
  
##  <a name="adding-and-managing-an-availability-database"></a><a name="DeployManageDbs"></a>Adicionando e gerenciando um banco de dados de disponibilidade  
  
|Cmdlets|Descrição|Com suporte em|  
|-------------|-----------------|------------------|  
|**Add-SqlAvailabilityDatabase**|Na réplica primária, adiciona um banco de dados a um grupo de disponibilidade.<br /><br /> Em uma réplica secundária, une um banco de dados secundário a um grupo de disponibilidade.|Qualquer instância de servidor que hospeda uma réplica de disponibilidade (o comportamento difere para réplicas primárias e secundárias)|  
|**Remove-SqlAvailabilityDatabase**|Na réplica primária, remove o banco de dados do grupo de disponibilidade.<br /><br /> Em uma réplica secundária, remove o banco de dados secundário da réplica secundária local.|Qualquer instância de servidor que hospeda uma réplica de disponibilidade (o comportamento difere para réplicas primárias e secundárias)|  
|`Resume-SqlAvailabilityDatabase`|Retoma a movimentação de dados para um banco de dados de disponibilidade suspenso.|As instância do servidor na qual o banco de dados é suspenso.|  
|`Suspend-SqlAvailabilityDatabase`|Suspende a movimentação de dados para um banco de dados de disponibilidade.|Qualquer instância de servidor que hospeda uma réplica de disponibilidade.|  
  
##  <a name="monitoring-availability-group-health"></a><a name="MonitorTblshtAGs"></a>Integridade do Grupo de Disponibilidade de monitoramento  
 Os cmdlets [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a seguir permitem monitorar a integridade de um grupo de disponibilidade e de suas réplicas e bancos de dados.  
  
> [!IMPORTANT]  
>  Você deve ter as permissões CONNECT, VIEW SERVER STATE e VIEW ANY DEFINITION para executar esses cmdlets.  
  
|Cmdlet|Descrição|Com suporte em|  
|------------|-----------------|------------------|  
|`Test-SqlAvailabilityGroup`|Avalia a integridade de um grupo de disponibilidade avaliando as políticas do PBM (gerenciamento baseado em políticas) do SQL Server.|Qualquer instância de servidor que hospede uma réplica de disponibilidade.*|  
|`Test-SqlAvailabilityReplica`|Avalia a integridade de réplicas de disponibilidade avaliando as políticas do PBM (gerenciamento baseado em políticas) do SQL Server.|Qualquer instância de servidor que hospede uma réplica de disponibilidade.*|  
|`Test-SqlDatabaseReplicaState`|Avalia a integridade de um banco de dados de disponibilidade em todas as réplicas de disponibilidade unidas avaliando as políticas do PBM (gerenciamento baseado em políticas) do SQL Server.|Qualquer instância de servidor que hospede uma réplica de disponibilidade.*|  
  
 *Para exibir informações sobre todas as réplicas de disponibilidade em um grupo de disponibilidade, use a instância do servidor que hospeda a réplica primária.  
  
 Para obter mais informações, consulte [usar políticas AlwaysOn para exibir a integridade de um grupo de disponibilidade &#40;SQL Server&#41;](use-always-on-policies-to-view-the-health-of-an-availability-group-sql-server.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)  
  
  
