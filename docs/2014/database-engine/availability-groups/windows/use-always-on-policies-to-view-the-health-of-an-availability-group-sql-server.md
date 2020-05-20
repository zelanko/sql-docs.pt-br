---
title: Usar políticas AlwaysOn para exibir a integridade de um grupo de disponibilidade (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 6f1bcbc3-1220-4071-8e53-4b957f5d3089
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 090c6fb7e19099ed5ad2650a99aa12f9ae3d5033
ms.sourcegitcommit: 37a3e2c022c578fc3a54ebee66d9957ff7476922
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82921970"
---
# <a name="use-alwayson-policies-to-view-the-health-of-an-availability-group-sql-server"></a>Use as políticas AlwaysOn para exibir a integridade de um grupo de disponibilidade (SQL Server)
  Este tópico descreve como determinar a integridade operacional de um grupo de disponibilidade AlwaysOn usando a política AlwaysOn no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou PowerShell no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Para obter informações sobre o gerenciamento baseado em políticas AlwaysOn, consulte [políticas AlwaysOn para problemas operacionais com o grupos de disponibilidade AlwaysOn (SQL Server)](always-on-policies-for-operational-issues-always-on-availability.md).  
  
> [!IMPORTANT]  
>  Para políticas de AlwaysOn, os nomes das categorias são usados como IDs. A alteração do nome de uma categoria AlwaysOn interrompe sua funcionalidade de avaliação de integridade. Portanto, os nomes das categorias AlwaysOn nunca devem ser modificados.  
  

  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer as permissões CONNECT, VIEW SERVER STATE e VIEW ANY DEFINITION.  
  
##  <a name="using-the-alwayson-dashboard"></a><a name="SSMSProcedure"></a>Usando o painel AlwaysOn  
 **Para abrir o Painel de AlwaysOn**  
  
1.  No Pesquisador de Objetos, conecte-se à instância do servidor que hospeda uma das réplicas de disponibilidade. Para exibir informações sobre todas as réplicas de disponibilidade em um grupo de disponibilidade, use a instância do servidor que hospeda a réplica primária.  
  
2.  Clique no nome do servidor para expandir a arvore de servidores.  
  
3.  Expanda o nó **Alta Disponibilidade AlwaysOn** .  
  
     Clique com o botão direito do mouse no nó **Grupos de Disponibilidade** ou expanda esse nó e clique com o botão direito do mouse em um grupo de disponibilidade específico.  
  
4.  Selecione o comando **Mostrar Painel** .  
  
 Para obter informações sobre como usar o Painel AlwaysOn, consulte [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md).  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> Usando o PowerShell  
 **Usar políticas AlwaysOn para exibir a integridade de um grupo de disponibilidade**  
  
1.  Defina o padrão (`cd`) como uma instância de servidor que hospeda uma das réplicas de disponibilidade. Para exibir informações sobre todas as réplicas de disponibilidade em um grupo de disponibilidade, use a instância do servidor que hospeda a réplica primária.  
  
2.  Use os seguintes cmdlets:  
  
     `Test-SqlAvailabilityGroup`  
     Avalia a integridade de um grupo de disponibilidade avaliando as políticas do PBM (gerenciamento baseado em políticas) do SQL Server. Você deve ter as permissões CONNECT, VIEW SERVER STATE e VIEW ANY DEFINITION para executar esse cmdlet.  
  
     Por exemplo, o comando a seguir mostra todos os grupos de disponibilidade com o estado de integridade "Error" na instância de servidor `Computer\Instance`.  
  
    ```powershell
    Get-ChildItem SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups |
        Test-SqlAvailabilityGroup |
        Where-Object { $_.HealthState -eq "Error" }  
    ```  
  
     `Test-SqlAvailabilityReplica`  
     Avalia a integridade de réplicas de disponibilidade avaliando as políticas do PBM (gerenciamento baseado em políticas) do SQL Server. Você deve ter as permissões CONNECT, VIEW SERVER STATE e VIEW ANY DEFINITION para executar esse cmdlet.  
  
     Por exemplo, o comando a seguir avalia a integridade da réplica de disponibilidade denominada `MyReplica` no grupo de disponibilidade `MyAg` e gera um breve resumo.  
  
    ```powershell
    Test-SqlAvailabilityReplica -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
     `Test-SqlDatabaseReplicaState`  
     Avalia a integridade de um banco de dados de disponibilidade em todas as réplicas de disponibilidade unidas avaliando as políticas do PBM (gerenciamento baseado em políticas) do SQL Server.  
  
     Por exemplo, o comando a seguir avalia a integridade de todos os bancos de dados de disponibilidade no grupo de disponibilidade `MyAg` e gera um breve resumo para cada banco de dados.  
  
    ```powershell
    Get-ChildItem SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\DatabaseReplicaStates |
        Test-SqlDatabaseReplicaState  
    ```  
  
     Esses cmdlets aceitam as seguintes opções:  
  
    |Opção|Descrição|  
    |------------|-----------------|  
    |`AllowUserPolicies`|Executa as políticas de usuário localizadas nas categorias de políticas AlwaysOn.|  
    |`InputObject`|Uma coleção de objetos que representam grupos de disponibilidade, réplicas de disponibilidade ou estados de bancos de dados de disponibilidade (dependendo de qual cmdlet que você está usando). O cmdlet computará a integridade dos objetos especificados.|  
    |`NoRefresh`|Quando esse parâmetro estiver definido, o cmdlet não atualizará manualmente os objetos especificados pelo parâmetro `-Path` ou `-InputObject`.|  
    |`Path`|O caminho para o grupo de disponibilidade, uma ou mais réplicas de disponibilidade ou o estado do cluster de réplicas do banco de dados de disponibilidade (dependendo do cmdlet que você está usando). Esse é um parâmetro opcional. Se não for especificado, o valor desse parâmetro será padronizado como o local de trabalho atual.|  
    |`ShowPolicyDetails`|Mostra o resultado de cada avaliação de política executada por esse cmdlet. O cmdlet produz um objeto por avaliação de política e esse objeto tem campos que descrevem os resultados da avaliação (se a política é aprovada ou não, o nome e a categoria da política e assim por diante).|  
  
     Por exemplo, o comando `Test-SqlAvailabilityGroup` a seguir especifica o parâmetro `-ShowPolicyDetails` para mostrar o resultado de cada avaliação de política executada por esse cmdlet para cada política de gerenciamento baseada em políticas (PBM) que foi executada no grupo de disponibilidade denominado `MyAg`.  
  
    ```powershell
    Test-SqlAvailabilityGroup -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\AgName -ShowPolicyDetails  
    ```  
  
    > [!NOTE]  
    >  Para exibir a sintaxe de um cmdlet, use o cmdlet `Get-Help` no ambiente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Para configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../../powershell/sql-server-powershell-provider.md)  
  
-   [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> Conteúdo relacionado  
 **SQL Server Blogs da equipe AlwaysOn – monitorando a integridade do AlwaysOn com o PowerShell:**  
  
-   [Parte 1: Visão geral básica de cmdlet](https://docs.microsoft.com/archive/blogs/sqlalwayson/monitoring-alwayson-health-with-powershell-part-1-basic-cmdlet-overview)  
  
-   [Parte 2: Uso avançado de cmdlet](https://docs.microsoft.com/archive/blogs/sqlalwayson/the-alwayson-health-model-part-2-extending-the-health-model)  
  
-   [Parte 3: Um simples aplicativo de monitoramento](https://docs.microsoft.com/archive/blogs/sqlalwayson/monitoring-alwayson-health-with-powershell-part-3-a-simple-monitoring-application)  
  
-   [Parte 4: Integração com o SQL Server Agent](https://docs.microsoft.com/archive/blogs/sqlalwayson/monitoring-alwayson-health-with-powershell-part-4-integration-with-sql-server-agent)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Administração de um grupo de disponibilidade &#40;SQL Server&#41;](administration-of-an-availability-group-sql-server.md)   
 [Monitoramento de grupos de disponibilidade &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)   
 [Políticas AlwaysOn para problemas operacionais com grupos de disponibilidade AlwaysOn (SQL Server)](always-on-policies-for-operational-issues-always-on-availability.md) 
