---
title: "Usar as políticas AlwaysOn para exibir a integridade de um grupo de disponibilidade | Microsoft Docs"
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
- Availability Groups [SQL Server], policies
ms.assetid: 6f1bcbc3-1220-4071-8e53-4b957f5d3089
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 15ce6e641cf6c5e8f060910a6eb38aa0f2e97587
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="use-always-on-policies-to-view-the-health-of-an-availability-group-sql-server"></a>Usar as políticas AlwaysOn para exibir a integridade de um grupo de disponibilidade (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve como determinar a integridade operacional de um grupo de disponibilidade AlwaysOn usando a política AlwaysOn no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou PowerShell no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Para obter informações sobre o Gerenciamento Baseado em Políticas AlwaysOn, consulte [Políticas AlwaysOn para problemas operacionais com grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-policies-for-operational-issues-always-on-availability.md).  
  
> [!IMPORTANT]  
>  Para políticas AlwaysOn, os nomes das categorias são usados como IDs. A alteração do nome de uma categoria AlwaysOn interrompe sua funcionalidade de avaliação de integridade. Portanto, os nomes das categorias AlwaysOn nunca devem ser modificados.  
  
-   **Antes de começar:** [Segurança](#Security)  
  
-   **Use as políticas AlwaysOn para exibir a integridade de um grupo de disponibilidade, usando:**  
  
     [Painel AlwaysOn](#SSMSProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer as permissões CONNECT, VIEW SERVER STATE e VIEW ANY DEFINITION.  
  
##  <a name="SSMSProcedure"></a> Usando o Painel AlwaysOn  
 **Para abrir o Painel AlwaysOn**  
  
1.  No Pesquisador de Objetos, conecte-se à instância do servidor que hospeda uma das réplicas de disponibilidade. Para exibir informações sobre todas as réplicas de disponibilidade em um grupo de disponibilidade, use a instância do servidor que hospeda a réplica primária.  
  
2.  Clique no nome do servidor para expandir a arvore de servidores.  
  
3.  Expanda o nó **Alta Disponibilidade AlwaysOn** .  
  
     Clique com o botão direito do mouse no nó **Grupos de Disponibilidade** ou expanda esse nó e clique com o botão direito do mouse em um grupo de disponibilidade específico.  
  
4.  Selecione o comando **Mostrar Painel** .  
  
 Para obter informações sobre como usar o Painel AlwaysOn, veja [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](~/database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md).  
  
##  <a name="PowerShellProcedure"></a> Usando o PowerShell  
 **Use Always On policies to view the health of an availability group**  
  
1.  Defina o padrão (**cd**) como uma instância de servidor que hospeda uma das réplicas de disponibilidade. Para exibir informações sobre todas as réplicas de disponibilidade em um grupo de disponibilidade, use a instância do servidor que hospeda a réplica primária.  
  
2.  Use os seguintes cmdlets:  
  
     **Test-SqlAvailabilityGroup**  
     Avalia a integridade de um grupo de disponibilidade avaliando as políticas do PBM (gerenciamento baseado em políticas) do SQL Server. Você deve ter as permissões CONNECT, VIEW SERVER STATE e VIEW ANY DEFINITION para executar esse cmdlet.  
  
     Por exemplo, o comando a seguir mostra todos os grupos de disponibilidade com o estado de integridade "Error" na instância de servidor `Computer\Instance`.  
  
    ```  
    Get-ChildItem SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups `   
    | Test-SqlAvailabilityGroup | Where-Object { $_.HealthState -eq "Error" }  
    ```  
  
     **Test-SqlAvailabilityReplica**  
     Avalia a integridade de réplicas de disponibilidade avaliando as políticas do PBM (gerenciamento baseado em políticas) do SQL Server. Você deve ter as permissões CONNECT, VIEW SERVER STATE e VIEW ANY DEFINITION para executar esse cmdlet.  
  
     Por exemplo, o comando a seguir avalia a integridade da réplica de disponibilidade denominada `MyReplica` no grupo de disponibilidade `MyAg` e gera um breve resumo.  
  
    ```  
    Test-SqlAvailabilityReplica `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
     **Test-SqlDatabaseReplicaState**  
     Avalia a integridade de um banco de dados de disponibilidade em todas as réplicas de disponibilidade unidas avaliando as políticas do PBM (gerenciamento baseado em políticas) do SQL Server.  
  
     Por exemplo, o comando a seguir avalia a integridade de todos os bancos de dados de disponibilidade no grupo de disponibilidade `MyAg` e gera um breve resumo para cada banco de dados.  
  
    ```  
    Get-ChildItem SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\DatabaseReplicaStates `   
     | Test-SqlDatabaseReplicaState  
    ```  
  
     Esses cmdlets aceitam as seguintes opções:  
  
    |Opção|Description|  
    |------------|-----------------|  
    |**AllowUserPolicies**|Executa as políticas de usuário localizadas nas categorias de políticas AlwaysOn.|  
    |**InputObject**|Uma coleção de objetos que representam grupos de disponibilidade, réplicas de disponibilidade ou estados de bancos de dados de disponibilidade (dependendo de qual cmdlet que você está usando). O cmdlet computará a integridade dos objetos especificados.|  
    |**NoRefresh**|Quando esse parâmetro estiver definido, o cmdlet não atualizará manualmente os objetos especificados pelo parâmetro **-Path** ou **-InputObject** .|  
    |**Caminho**|O caminho para o grupo de disponibilidade, uma ou mais réplicas de disponibilidade ou o estado do cluster de réplicas do banco de dados de disponibilidade (dependendo do cmdlet que você está usando). Esse é um parâmetro opcional. Se não for especificado, o valor desse parâmetro será padronizado como o local de trabalho atual.|  
    |**ShowPolicyDetails**|Mostra o resultado de cada avaliação de política executada por esse cmdlet. O cmdlet produz um objeto por avaliação de política e esse objeto tem campos que descrevem os resultados da avaliação (se a política é aprovada ou não, o nome e a categoria da política e assim por diante).|  
  
     Por exemplo, o comando **Test-SqlAvailabilityGroup** a seguir especifica o parâmetro **-ShowPolicyDetails** para mostrar o resultado de cada avaliação de política executada por esse cmdlet para cada política PBM (gerenciamento baseada em políticas) que foi executada no grupo de disponibilidade denominado `MyAg`.  
  
    ```  
    Test-SqlAvailabilityGroup `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\AgName `  
    -ShowPolicyDetails  
  
    ```  
  
    > [!NOTE]  
    >  Para exibir a sintaxe de um cmdlet, use o cmdlet **Get-Help** no ambiente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Para configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
-   [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)  
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
 **Blogs da equipe de AlwaysOn do SQL Server – Monitorando a integridade de AlwaysOn com o PowerShell:**  
  
-   [Parte 1: Visão geral básica de cmdlet](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/13/monitoring-alwayson-health-with-powershell-part-1-basic-cmdlet-overview/)  
  
-   [Parte 2: Uso avançado de cmdlet](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/13/monitoring-alwayson-health-with-powershell-part-2-advanced-cmdlet-usage/)  
  
-   [Parte 3: Um simples aplicativo de monitoramento](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/14/monitoring-alwayson-health-with-powershell-part-3-a-simple-monitoring-application/)  
  
-   [Parte 4: Integração com o SQL Server Agent](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/15/monitoring-alwayson-health-with-powershell-part-4-integration-with-sql-server-agent/)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Administração de um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/administration-of-an-availability-group-sql-server.md)   
 [Monitoramento de grupos de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/monitoring-of-availability-groups-sql-server.md)   
 [Políticas AlwaysOn para problemas operacionais com grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-policies-for-operational-issues-always-on-availability.md)  
  
  


