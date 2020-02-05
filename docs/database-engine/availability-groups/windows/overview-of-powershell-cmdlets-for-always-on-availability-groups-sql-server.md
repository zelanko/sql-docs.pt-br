---
title: Cmdlets do PowerShell para grupos de disponibilidade
description: 'Uma referência para os diferentes cmdlets do PowerShell disponíveis para gerenciar Grupos de Disponibilidade AlwaysOn. '
ms.custom: seo-lt-2019
ms.date: 08/30/2017
ms.prod: sql
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
ms.openlocfilehash: 8aac669c8e7b2f43666a43c26a8040c3658c560c
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75236093"
---
# <a name="overview-of-powershell-cmdlets-for-always-on-availability-groups"></a>Visão geral de cmdlets do PowerShell para grupos de disponibilidade AlwaysOn
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] O PowerShell é um shell de linha de comando baseado em tarefa e linguagem de script criado especialmente para a administração do sistema. [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] fornece um conjunto de cmdlets do PowerShell no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] que permitem implantar, gerenciar e monitorar grupos de disponibilidade, réplicas de disponibilidade e bancos de dados de disponibilidade.  
  
> [!NOTE]  
>  Um cmdlet do PowerShell pode ser executado com o início bem-sucedido de uma ação. Isso não indica que o trabalho planejado, como o failover de um grupo de disponibilidade, foi concluído. Ao gerar o script de uma sequência de ações, talvez seja necessário verificar o status das ações e esperar que elas sejam concluídas.  
  
> [!NOTE]  
>  Para obter uma lista de tópicos nos Manuais Online do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] que descrevem como usar os cmdlets para executar tarefas do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] , confira a seção “Tarefas relacionadas” de [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).  
  
##  <a name="ConfiguringServerInstance"></a> Configurando uma instância de servidor para o grupos de disponibilidade AlwaysOn  
  
|Cmdlets|DESCRIÇÃO|Com suporte em|  
|-------------|-----------------|------------------|
|[**Disable-SqlAlwaysOn**](/powershell/module/sqlserver/disable-sqlalwayson)|Desabilita o recurso [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] em uma instância de servidor.|A instância de servidor especificada pelo parâmetro **Path**, **InputObject**ou **Name** . (Deve ser uma edição do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que dê suporte ao [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)].)|  
|[**Enable-SqlAlwaysOn**](/powershell/module/sqlserver/enable-sqlalwayson)|Habilita o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] em uma instância do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] que dá suporte ao recurso [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] . Para obter informações sobre suporte para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], veja [Pré-requisitos, restrições e recomendações para os grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).|Qualquer edição do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que dê suporte ao [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)].|  
|[**New-SqlHadrEndPoint**](/powershell/module/sqlserver/new-sqlhadrendpoint)|Cria um novo ponto de extremidade de espelhamento de banco de dados em uma instância de servidor. Esse ponto de extremidade é necessário para a movimentação de dados entre os bancos de dados primário e secundário.|Qualquer instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|  
|[**Set-SqlHadrEndpoint**](/powershell/module/sqlserver/set-sqlhadrendpoint)|Altera as propriedades de um ponto de extremidade de espelhamento de banco de dados existente, como o nome, o estado ou as propriedades de autenticação.|Uma instância de servidor que dá suporte ao [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] e não tem um ponto de extremidade de espelhamento de banco de dados.|  

  
##  <a name="BnRcmdlets"></a> Backing Up and Restoring Databases and Transaction Logs  
  
|Cmdlets|DESCRIÇÃO|Com suporte em|  
|-------------|-----------------|------------------|  
|[**Backup-SqlDatabase**](/powershell/module/sqlserver/backup-sqldatabase)|Cria um backup de dados ou de log.|Qualquer banco de dados online (para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], um banco de dados na instância do servidor que hospeda a réplica primária).|  
|[**Restore-SqlDatabase**](/powershell/module/sqlserver/restore-sqldatabase)|Restaura um backup.|Qualquer instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], uma instância de servidor que hospeda uma réplica secundária)<br /><br />

  >[!Important]
  >Ao preparar um banco de dados secundário, é necessário usar o parâmetro **-NoRecovery** em cada comando **Restore-SqlDatabase**. 
  
 Para obter informações sobre como usar esses cmdlets para preparar um banco de dados secundário, veja [Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
  
##  <a name="DeployManageAGs"></a> Criando e gerenciando um grupo de disponibilidade  
  
|Cmdlets|DESCRIÇÃO|Com suporte em|  
|-------------|-----------------|------------------|  
|[**New-SqlAvailabilityGroup**](/powershell/module/sqlserver/new-sqlavailabilitygroup)|Cria um novo grupo de disponibilidade.|Instância de servidor para hospedar a réplica primária|  
|[**Remove-SqlAvailabilityGroup**](/powershell/module/sqlserver/remove-sqlavailabilitygroup)|Exclui um grupo de disponibilidade.|Instância de servidor habilitada para HADR|  
|[**Set-SqlAvailabilityGroup**](/powershell/module/sqlserver/set-sqlavailabilitygroup)|Define as propriedades de um grupo de disponibilidade; coloca um grupo de disponibilidade online/offline|Instância de servidor que hospeda a réplica primária|  
|[**Switch-SqlAvailabilityGroup**](/powershell/module/sqlserver/switch-sqlavailabilitygroup)|Inicia um dos seguintes formulários de failover:<br /><br /> Um failover forçado de um grupo de disponibilidade (com possível perda de dados).<br /><br /> Um failover manual de um grupo de disponibilidade.|Instância de servidor que hospeda a réplica secundária de destino|  
  
##  <a name="AGlisteners"></a> Criando e gerenciando um ouvinte de grupo de disponibilidade  
  
|Cmdlet|DESCRIÇÃO|Com suporte em|  
|------------|-----------------|------------------|  
|[**New-SqlAvailabilityGroupListener**](/powershell/module/sqlserver/new-sqlavailabilitygrouplistener)|Cria um novo ouvinte de grupo de disponibilidade e conecta-o a um grupo de disponibilidade existente.|Instância de servidor que hospeda a réplica primária|  
|[**Set-SqlAvailabilityGroupListener**](/powershell/module/sqlserver/set-sqlavailabilitygrouplistener)|Modifica a configuração de porta em um ouvinte de grupo de disponibilidade existente.|Instância de servidor que hospeda a réplica primária|  
|[**Add-SqlAvailabilityGroupListenerStaticIp**](/powershell/module/sqlserver/add-sqlavailabilitygrouplistenerstaticip)|Adiciona um endereço IP estático à configuração de um ouvinte de grupo de disponibilidade existente. O endereço IP poderá ser um endereço IPv4 com sub-rede ou um endereço IPv6.|Instância de servidor que hospeda a réplica primária|  
  
##  <a name="DeployManageARs"></a> Creating and Managing an Availability Replica  
  
|Cmdlets|DESCRIÇÃO|Com suporte em|  
|-------------|-----------------|------------------|  
|[**New-SqlAvailabilityReplica**](/powershell/module/sqlserver/new-sqlavailabilityreplica)|Cria uma nova réplica de disponibilidade. Você pode usar o parâmetro **-AsTemplate** para criar um objeto de réplica de disponibilidade de memória para cada nova réplica de disponibilidade.|Instância de servidor que hospeda a réplica primária|  
|[**Join-SqlAvailabilityGroup**](/powershell/module/sqlserver/join-sqlavailabilitygroup)|Une uma réplica secundária ao grupo de disponibilidade.|Instância de servidor que hospeda a réplica secundária|  
|[**Remove-SqlAvailabilityReplica**](/powershell/module/sqlserver/remove-sqlavailabilityreplica)|Exclui uma réplica de disponibilidade.|Instância de servidor que hospeda a réplica primária|  
|[**Set-SqlAvailabilityReplica**](/powershell/module/sqlserver/set-sqlavailabilityreplica)|Define as propriedades de uma réplica de disponibilidade.|Instância de servidor que hospeda a réplica primária|  
  
##  <a name="DeployManageDbs"></a> Adicionando e gerenciando um banco de dados de disponibilidade  
  
|Cmdlets|DESCRIÇÃO|Com suporte em|  
|-------------|-----------------|------------------|  
|[**Add-SqlAvailabilityDatabase**](/powershell/module/sqlserver/add-sqlavailabilitydatabase)|Na réplica primária, adiciona um banco de dados a um grupo de disponibilidade.<br /><br /> Em uma réplica secundária, une um banco de dados secundário a um grupo de disponibilidade.|Qualquer instância de servidor que hospeda uma réplica de disponibilidade (o comportamento difere para réplicas primárias e secundárias)|  
|[**Remove-SqlAvailabilityDatabase**](/powershell/module/sqlserver/remove-sqlavailabilitydatabase)|Na réplica primária, remove o banco de dados do grupo de disponibilidade.<br /><br /> Em uma réplica secundária, remove o banco de dados secundário da réplica secundária local.|Qualquer instância de servidor que hospeda uma réplica de disponibilidade (o comportamento difere para réplicas primárias e secundárias)|  
|[**Resume-SqlAvailabilityDatabase**](/powershell/module/sqlserver/resume-sqlavailabilitydatabase)|Retoma a movimentação de dados para um banco de dados de disponibilidade suspenso.|As instância do servidor na qual o banco de dados é suspenso.|  
|[**Suspend-SqlAvailabilityDatabase**](/powershell/module/sqlserver/suspend-sqlavailabilitydatabase)|Suspende a movimentação de dados para um banco de dados de disponibilidade.|Qualquer instância de servidor que hospeda uma réplica de disponibilidade.|  
  
##  <a name="MonitorTblshtAGs"></a> Monitorando a integridade do grupo de disponibilidade  
 Os cmdlets [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a seguir permitem monitorar a integridade de um grupo de disponibilidade e de suas réplicas e bancos de dados.  
  
> [!IMPORTANT]  
>  Você deve ter as permissões CONNECT, VIEW SERVER STATE e VIEW ANY DEFINITION para executar esses cmdlets.  
  
|Cmdlet|DESCRIÇÃO|Com suporte em|  
|------------|-----------------|------------------|  
|[**Test-SqlAvailabilityGroup**](/powershell/module/sqlserver/test-sqlavailabilitygroup)|Avalia a integridade de um grupo de disponibilidade avaliando as políticas do PBM (gerenciamento baseado em políticas) do SQL Server.|Qualquer instância de servidor que hospede uma réplica de disponibilidade.*|  
|[**Test-SqlAvailabilityReplica**](/powershell/module/sqlserver/test-sqlavailabilityreplica)|Avalia a integridade de réplicas de disponibilidade avaliando as políticas do PBM (gerenciamento baseado em políticas) do SQL Server.|Qualquer instância de servidor que hospede uma réplica de disponibilidade.*|  
|[**Test-SqlDatabaseReplicaState**](/powershell/module/sqlserver/test-sqldatabasereplicastate)|Avalia a integridade de um banco de dados de disponibilidade em todas as réplicas de disponibilidade unidas avaliando as políticas do PBM (gerenciamento baseado em políticas) do SQL Server.|Qualquer instância de servidor que hospede uma réplica de disponibilidade.*|  
  
 *Para exibir informações sobre todas as réplicas de disponibilidade em um grupo de disponibilidade, use a instância do servidor que hospeda a réplica primária.  
  
 Para obter mais informações, veja [Usar as políticas AlwaysOn para exibir a integridade de um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/use-always-on-policies-to-view-the-health-of-an-availability-group-sql-server.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)  
  
  
