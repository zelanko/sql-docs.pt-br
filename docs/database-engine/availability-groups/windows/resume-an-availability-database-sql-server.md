---
title: Retomar um banco de dados de disponibilidade (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.availabilitygroup.resumedatamove.f1
helpviewer_keywords:
- Availability Groups [SQL Server], resuming a database
- secondary databases [SQL Server], in availability group
- primary databases [SQL Server], in availability group
- Availability Groups [SQL Server], databases
ms.assetid: 20e9147b-e985-4caa-910e-fc4b38dbf9a1
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: 5304bd107c5aa41a2c0be30d7576f4f782d19820
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66777780"
---
# <a name="resume-an-availability-database-sql-server"></a>Retomar um banco de dados de disponibilidade (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Você pode retomar um banco de dados de disponibilidade suspenso no [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]ou PowerShell no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. A retomada de um banco de dados suspenso coloca o banco de dados no estado SYNCHRONIZING. A retomada do banco de dados primário também retoma todos os bancos de dados secundários que foram suspensos devido à suspensão do banco de dados primário. Se um banco de dados secundário foi suspenso localmente, na instância de servidor que hospeda a réplica secundária, o banco de dados secundário deverá ser retomado localmente. Quando um determinado banco de dados secundário e o banco de dados primário correspondente estiverem no estado SYNCHRONIZING, a sincronização de dados é retomada no banco de dados secundário.  
  
> [!NOTE]  
>  Suspender e retomar um banco de dados secundário AlwaysOn não afetam diretamente a disponibilidade do banco de dados primário. Porém, suspender um banco de dados secundário pode afetar os recursos de redundância e failover para o banco de dados primário, até que o banco de dados secundário suspenso seja retomado. Isto está em contraste com o espelhamento de banco de dados, onde o estado de espelhamento é suspenso no banco de dados espelho e no banco de dados principal até que o espelhamento seja retomado. Suspender um banco de dados secundário AlwaysOn suspende o movimento de dados em todos os bancos de dados secundários correspondentes, e os recursos de failover e a redundância são eliminados para esse banco de dados até que o banco de dados primário seja retomado.  
  
  
  
## <a name="limitations-and-restrictions"></a>Limitações e Restrições  
 O comando RESUME retorna assim que é aceito pela réplica que hospeda o banco de dados de destino, mas, na verdade, a retomada do banco de dados ocorre de forma assíncrona.  
  
##  <a name="Prerequisites"></a> Pré-requisitos  
  
-   Você deve estar conectado à instância de servidor que hospeda o banco de dados a ser retomado.    
-   O grupo de disponibilidade deve estar online.    
-   O banco de dados primário deve estar online e disponível.  
  
  
##  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER no banco de dados.  
  
 Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para retomar um banco de dados secundário**  
  
1.  No Pesquisador de Objetos, conecte-se à instância de servidor que hospeda a réplica de disponibilidade na qual você deseja retomar o banco de dados e expanda a árvore de servidores.  
  
2.  Expanda os nós **Alta Disponibilidade AlwaysOn** e **Grupos de Disponibilidade**.  
  
3.  Expanda o grupo de disponibilidade.  
  
4.  Expanda o nó **Bancos de dados de Disponibilidade** , clique com o botão direito do mouse no banco de dados e clique em **Retomar a Movimentação de Dados**.  
  
5.  Na caixa de diálogo **Retomar a Movimentação de Dados** , clique em **OK**.  
  
> [!NOTE]  
>  Para retomar bancos de dados adicionais neste local de réplica, repita as etapas 4 e 5 para cada banco de dados.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para retomar um banco de dados secundário que foi suspenso localmente**  
  
1.  Conecte-se à instância do servidor que hospeda a réplica secundária, cujo banco de dados você deseja retomar.  
  
2.  Retome o banco de dados secundário usando a seguinte instrução [ALTER DATABASE](../../../t-sql/statements/alter-database-transact-sql-set-hadr.md):  
  
     ALTER DATABASE *database_name* SET HADR RESUME  
  
##  <a name="PowerShellProcedure"></a> Usando o PowerShell  
 **Para retomar um banco de dados secundário**  
  
1.  Altere o diretório (**cd**) para a instância de servidor que hospeda a réplica cujo banco de dados você deseja retomar. Para obter mais informações, consulte [Pré-requisitos](#Prerequisites)anteriormente neste tópico.  
  
2.  Use o cmdlet **Resume-SqlAvailabilityDatabase** para retomar o grupo de disponibilidade.  
  
     Por exemplo, o comando a seguir retoma a sincronização dos dados para o banco de dados de disponibilidade `MyDb3` no grupo de disponibilidade `MyAg`.  
  
    ```  
    Resume-SqlAvailabilityDatabase `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\Databases\MyDb3  
    ```  
  
    > [!NOTE]  
    >  Para exibir a sintaxe de um cmdlet, use o cmdlet **Get-Help** no ambiente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Para configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Suspender um banco de dados de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/suspend-an-availability-database-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
