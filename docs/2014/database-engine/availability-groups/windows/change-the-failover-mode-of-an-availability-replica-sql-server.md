---
title: Alterar o modo de failover de uma réplica de disponibilidade (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- failover modes [SQL Server]
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], failover modes
- Availability Groups [SQL Server], configuring
ms.assetid: 619a826f-8e65-48eb-8c34-39497d238279
caps.latest.revision: 26
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fa3771b373292278ac3131dfd7f8484b6f4b8601
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37304246"
---
# <a name="change-the-failover-mode-of-an-availability-replica-sql-server"></a>Alterar o modo de failover de uma réplica de disponibilidade (SQL Server)
  Este tópico descreve como alterar o modo de failover de uma réplica de disponibilidade em um grupo de disponibilidade AlwaysOn no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../../includes/tsql-md.md)]ou o PowerShell. O modo de failover é uma propriedade de réplica que determina o modo de failover para réplicas que executam sob modo de disponibilidade de confirmação síncrona. Para obter mais informações, consulte [Failover e modos de failover &#40;Grupos de disponibilidade AlwaysOn&#41;](failover-and-failover-modes-always-on-availability-groups.md) e [Modos de disponibilidade &#40;Grupos de disponibilidade AlwaysOn&#41;](availability-modes-always-on-availability-groups.md).  
  

  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos e restrições  
  
-   Esta tarefa tem suporte apenas em réplicas primárias. Você deve estar conectado à instância do servidor que hospeda a réplica primária.  
  
-   As FCIs (Instâncias de cluster de failover) do SQL Server não dão suporte ao failover automático por grupos de disponibilidade, de modo que qualquer réplica de disponibilidade que esteja hospedado por um FCI só pode ser configurada para failover manual.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para alterar o modo de failover de uma réplica de disponibilidade**  
  
1.  No Pesquisador de Objetos, conecte-se à instância de servidor que hospeda a réplica primária e expanda a árvore de servidores.  
  
2.  Expanda os nós **Alta Disponibilidade AlwaysOn** e **Grupos de Disponibilidade** .  
  
3.  Clique no grupo de disponibilidade cuja réplica você deseja alterar.  
  
4.  Clique com o botão direito do mouse na réplica e clique em **Propriedades**.  
  
5.  Na caixa de diálogo **Propriedades da Réplica de Disponibilidade** , use a lista suspensa **Modo de failover** para alterar o modo de failover desta réplica.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para alterar o modo de failover de uma réplica de disponibilidade**  
  
1.  Conecte-se à instância de servidor que hospeda a réplica primária.  
  
2.  Use a instrução [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) , da seguinte maneira:  
  
     ALTER AVAILABILITY GROUP *group_name* MODIFY REPLICA ON '*server_name*'  
  
     WITH ( {  
  
     AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT }  
  
     | FAILOVER_MODE = { AUTOMATIC | MANUAL }  
  
     }  )  
  
     onde  
  
    -   *group_name* é o nome do grupo de disponibilidade.  
  
    -   { '*system_name*[\\*instance_name*]' | '*FCI_network_name*[\\*instance_name*]' }  
  
         Especifica o endereço da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda a réplica de disponibilidade a ser alterada. Os componentes desse endereço são os seguintes:  
  
         *system_name*  
         É o nome do NetBIOS do sistema de computador no qual reside uma instância autônoma do servidor.  
  
         *FCI_network_name*  
         É o nome de rede usado para acessar um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no qual uma instância de servidor de destino é um parceiro de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (um FCI).  
  
         *instance_name*  
         É o nome da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda a réplica de disponibilidade de destino. Para uma instância de servidor padrão, *instance_name* é opcional.  
  
     Para obter mais informações sobre esses parâmetros, veja [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-availability-group-transact-sql).  
  
     O exemplo a seguir, inserido na réplica primária do grupo de disponibilidade *MyAG* , altera o modo de failover para failover automático na réplica de disponibilidade localizada na instância de servidor padrão em um computador denominado *COMPUTER01*.  
  
    ```  
    ALTER AVAILABILITY GROUP MyAG MODIFY REPLICA ON 'COMPUTER01' WITH  
       (FAILOVER_MODE = AUTOMATIC);  
    ```  
  
##  <a name="PowerShellProcedure"></a> Usando o PowerShell  
 **Para alterar o modo de failover de uma réplica de disponibilidade**  
  
1.  Altere o diretório (`cd`) para a instância do servidor que hospeda a réplica primária.  
  
2.  Use o `Set-SqlAvailabilityReplica` cmdlet com o `FailoverMode` parâmetro. Ao definir uma réplica como failover automático, você talvez precise usar o `AvailabilityMode` parâmetro para alterar a réplica para o modo de disponibilidade de confirmação síncrona.  
  
     Por exemplo, o comando a seguir modifica a réplica `MyReplica` no grupo de disponibilidade `MyAg` para usar o modo de disponibilidade de confirmação síncrona e para oferecer suporte ao failover automático.  
  
    ```  
    Set-SqlAvailabilityReplica -AvailabilityMode "SynchronousCommit" -FailoverMode "Automatic" `   
    -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\Replicas\MyReplica  
    ```  
  
    > [!NOTE]  
    >  Para exibir a sintaxe de um cmdlet, use o `Get-Help` cmdlet no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ambiente do PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Para configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../../powershell/sql-server-powershell-provider.md)  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)  
 [Modos de disponibilidade &#40;grupos de disponibilidade AlwaysOn&#41;](availability-modes-always-on-availability-groups.md)   
 [Failover e modos de Failover &#40;grupos de disponibilidade AlwaysOn&#41;](failover-and-failover-modes-always-on-availability-groups.md) 
  
  
