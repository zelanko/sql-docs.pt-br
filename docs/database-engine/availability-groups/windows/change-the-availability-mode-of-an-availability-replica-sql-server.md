---
title: Alterar o modo de disponibilidade de uma réplica para um grupo de disponibilidade
description: Uma descrição de como alterar o modo de disponibilidade de uma réplica de disponibilidade dentro de um grupo de disponibilidade Always On usando o T-SQL (Transact-SQL), o PowerShell ou o SQL Server Management Studio.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], availability modes
ms.assetid: c4da8f25-fb1b-45a4-8bf2-195df6df634c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b1a3b5d1dfdf3a5e8556058cee750a4e2e08476a
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "74822448"
---
# <a name="change-availability-mode-of-a-replica-within-an-always-on-availability-group"></a>Alterar o modo de disponibilidade de uma réplica dentro de um grupo de disponibilidade Always On
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como alterar o modo de disponibilidade de uma réplica de disponibilidade em um grupo de disponibilidade AlwaysOn no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../../includes/tsql-md.md)]ou o PowerShell. O modo de disponibilidade é uma propriedade de réplica que controla se a réplica confirma de forma assíncrona ou síncrona. O*modo de confirmação assíncrona* maximiza o desempenho às custas da alta disponibilidade e dá suporte apenas ao failover manual forçado (com possível perda de dados), que costuma ser chamado de *failover forçado*. O*modo de confirmação síncrona* enfatiza a alta disponibilidade sobre o desempenho e, quando a réplica secundária é sincronizada, dá suporte ao failover manual e, opcionalmente, ao failover automático.  
    
##  <a name="prerequisites"></a><a name="Prerequisites"></a> Pré-requisitos  
  
Você deve estar conectado à instância do servidor que hospeda a réplica primária.  
  

##  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para alterar o modo de disponibilidade de um grupo de disponibilidade**  
  
1.  No Pesquisador de Objetos, conecte-se à instância de servidor que hospeda a réplica primária e expanda a árvore de servidores.  
  
2.  Expanda os nós **Alta Disponibilidade AlwaysOn** e **Grupos de Disponibilidade**.  
  
3.  Clique no grupo de disponibilidade cuja réplica você deseja alterar.  
  
4.  Clique com o botão direito do mouse na réplica e clique em **Propriedades**.  
  
5.  Na caixa de diálogo **Propriedades da Réplica de Disponibilidade** , use a lista suspensa **Modo de disponibilidade** para alterar o modo de disponibilidade desta réplica.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para alterar o modo de disponibilidade de um grupo de disponibilidade**  
  
1.  Conecte-se à instância de servidor que hospeda a réplica primária.  
  
2.  Use a instrução [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) , da seguinte maneira:  
  
     ALTER AVAILABILITY GROUP *group_name* MODIFY REPLICA ON '*server_name*'  
  
     WITH ( {  
  
     AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT }  
  
     | FAILOVER_MODE = { AUTOMATIC | MANUAL }  
  
     } )  
  
     em que *group_name* é o nome do grupo de disponibilidade e *server_name* é o nome da instância do servidor que hospeda a réplica a ser modificada.  
  
    > [!NOTE]  
    >  FAILOVER_MODE = AUTOMATIC terá suporte apenas se você também especificar AVAILABILITY_MODE = SYNCHRONOUS_COMMIT.  
  
     O exemplo a seguir, inserido na réplica primária do grupo de disponibilidade `AccountsAG` , altera os modos de disponibilidade e de failover para confirmação síncrona e failover automático, respectivamente, para a réplica hospedada pela instância de servidor `INSTANCE09` .  
  
    ```  
  
    ALTER AVAILABILITY GROUP AccountsAG MODIFY REPLICA ON 'INSTANCE09'  
       WITH (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);  
    ALTER AVAILABILITY GROUP AccountsAG MODIFY REPLICA ON 'INSTANCE09'  
       WITH (FAILOVER_MODE = AUTOMATIC);  
    ```  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> Usando o PowerShell  
 **Para alterar o modo de disponibilidade de um grupo de disponibilidade**  
  
1.  Altere o diretório (**cd**) para a instância de servidor que hospeda a réplica primária.  
  
2.  Use o cmdlet **Set-SqlAvailabilityReplica** com o parâmetro **AvailabilityMode** e, opcionalmente, o parâmetro **FailoverMode** .  
  
     Por exemplo, o comando a seguir modifica a réplica `MyReplica` no grupo de disponibilidade `MyAg` para usar o modo de disponibilidade de confirmação síncrona e para oferecer suporte ao failover automático.  
  
    ```  
    Set-SqlAvailabilityReplica -AvailabilityMode "SynchronousCommit" -FailoverMode "Automatic" `   
    -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
    > [!NOTE]  
    >  Para exibir a sintaxe de um cmdlet, use o cmdlet **Get-Help** no ambiente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Para configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Modos de disponibilidade &#40;Grupos de disponibilidade AlwaysOn&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)   
 [Failover e modos de failover &#40;Grupos de Disponibilidade AlwaysOn&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)  
  
  
