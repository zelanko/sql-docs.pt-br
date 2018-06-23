---
title: Ingressar um banco de dados secundário em um grupo de disponibilidade (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.availabilitygroup.joindbs.f1
helpviewer_keywords:
- secondary databases [SQL Server], in availability group
- secondary databases [SQL Server]
- Availability Groups [SQL Server], joining
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], databases
ms.assetid: fd7efe79-c1f9-497d-bfe7-b2a2b2321cf5
caps.latest.revision: 37
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: 63a6421ede7afbae66b80fda01e50223e732a27a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018973"
---
# <a name="join-a-secondary-database-to-an-availability-group-sql-server"></a>Unir um banco de dados secundário a um grupo de disponibilidade (SQL Server)
  Este tópico explica como unir um banco de dados secundário a um grupo de disponibilidade AlwaysOn usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)], ou o PowerShell no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Após preparar um banco de dados secundário para uma réplica secundária, você precisará unir o banco de dados ao grupo de disponibilidade o quanto antes. Isso iniciará a movimentação de dados do banco de dados primário correspondente para o banco de dados secundário.  
  
-   **Antes de começar:**  
  
     [Pré-requisitos](#Prerequisites)  
  
     [Segurança](#Security)  
  
-   **Para preparar um banco de dados secundário, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
> [!NOTE]  
>  Para obter informações sobre o que acontece depois que um banco de dados secundário se une ao grupo, consulte [visão geral dos grupos de disponibilidade do AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md).  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
  
-   Você deve estar conectado à instância de servidor que hospeda a réplica secundária.  
  
-   A réplica secundária já deve estar unida ao grupo de disponibilidade. Para obter mais informações, veja [Unir uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md).  
  
-   O banco de dados secundário deve ter sido preparado recentemente. Para obter mais informações, veja [Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para unir um banco de dados secundário a um grupo de disponibilidade**  
  
1.  No Pesquisador de Objetos, conecte-se à instância de servidor que hospeda a réplica secundária e expanda a árvore de servidores.  
  
2.  Expanda os nós **Alta Disponibilidade AlwaysOn** e **Grupos de Disponibilidade** .  
  
3.  Expanda o grupo de disponibilidade a ser alterado e expanda o nó **Bancos de Dados de Disponibilidade** .  
  
4.  Clique com o botão direito do mouse no banco de dados e clique em **Unir a um Grupo de Disponibilidade**.  
  
5.  Isso abre a caixa de diálogo **Unir Bancos de Dados a Grupo de Disponibilidade** . Verifique o nome do grupo de disponibilidade que é exibido na barra de título e os nomes de banco de dados exibidos na grade. Clique em **OK**ou em **Cancelar**.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para unir um banco de dados secundário a um grupo de disponibilidade**  
  
1.  Conecte-se à instância de servidor que hospeda a réplica secundária.  
  
2.  Use a [cláusula SET HADR da instrução ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-hadr) , da seguinte maneira:  
  
     ALTER DATABASE *database_name* SET HADR AVAILABILITY GROUP = *group_name*  
  
     em que *database_name* é o nome de um banco de dados a ser associado e *group_name* é o nome do grupo de disponibilidade.  
  
     O exemplo a seguir une o banco de dados secundário `Db1` à réplica secundária local do grupo de disponibilidade `MyAG`.  
  
    ```  
    ALTER DATABASE Db1 SET HADR AVAILABILITY GROUP = MyAG;  
    ```  
  
    > [!NOTE]  
    >  Para ver esta instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] usada no contexto, veja [Criar um grupo de disponibilidade &#40;Transact-SQL&#41;](create-an-availability-group-transact-sql.md).  
  
##  <a name="PowerShellProcedure"></a> Usando o PowerShell  
 **Para unir um banco de dados secundário a um grupo de disponibilidade**  
  
1.  Altere o diretório (`cd`) para a instância do servidor que hospeda a réplica secundária.  
  
2.  Use o `Add-SqlAvailabilityDatabase` cmdlet para unir um ou mais bancos de dados secundários ao grupo de disponibilidade.  
  
     Por exemplo, o comando a seguir une um banco de dados secundário, `Db1`, ao grupo de disponibilidade `MyAG` em uma das instâncias de servidor que hospeda uma réplica secundária.  
  
    ```  
    Add-SqlAvailabilityDatabase `   
    -Path SQLSERVER:\SQL\SecondaryServer\InstanceName\AvailabilityGroups\MyAG `   
    -Database "Db1"  
    ```  
  
    > [!NOTE]  
    >  Para exibir a sintaxe de um cmdlet, use o `Get-Help` cmdlet o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ambiente do PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Para configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Unir uma réplica secundária a um grupo de disponibilidade &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Preparar um banco de dados secundário manualmente para um grupo de disponibilidade &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>Consulte também  
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-availability-group-transact-sql)   
 [Visão geral dos grupos de disponibilidade do AlwaysOn &#40;do SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Solucionar problemas de configuração de grupos de disponibilidade do AlwaysOn &#40;SQL Server&#41;excluído](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
  
