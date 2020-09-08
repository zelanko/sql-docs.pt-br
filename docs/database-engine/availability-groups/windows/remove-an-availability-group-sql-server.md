---
title: Remover um grupo de disponibilidade
description: 'Descreve como remover um grupo de disponibilidade com SSMS (SQL Server Management Studio), T-SQL (Transact-SQL) ou SQL PowerShell. '
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.availabilitygroup.deleteag.f1
helpviewer_keywords:
- Availability Groups [SQL Server], removing
- Availability Groups [SQL Server], dropping
ms.assetid: 4b7f7f62-43a3-49db-a72e-22d4d7c2ddbb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d68a51bd65f7339b27e753c47585d85cf05002d2
ms.sourcegitcommit: 827ad02375793090fa8fee63cc372d130f11393f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2020
ms.locfileid: "89480715"
---
# <a name="remove-an-availability-group-sql-server"></a>Remover um grupo de disponibilidade (SQL Server)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Este artigo descreve como excluir (remover) um grupo de disponibilidade Always On usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou o PowerShell no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Se uma instância de servidor que hospeda uma das réplicas de disponibilidade estiver offline quando você exclui um grupo de disponibilidade, ela removerá a réplica de disponibilidade local quando estiver online novamente. O descarte de um grupo de disponibilidade exclui qualquer ouvinte de grupo de disponibilidade associado.  
  
 Observe que, se for necessário, você pode remover um grupo de disponibilidade de qualquer nó WSFC (Windows Server Failover Clustering) que processa as credenciais de segurança corretas para o grupo de disponibilidade. Isso permite excluir um grupo de disponibilidade quando nenhuma de suas réplicas de disponibilidade permanece.  
  
> [!IMPORTANT]  
>  Se possível, remova o grupo de disponibilidade somente quando ele estiver conectado à instância do servidor que hospeda a réplica primária. Quando o grupo de disponibilidade é removido da réplica primária, são permitidas alterações nos bancos de dados primários antigos (sem proteção de alta disponibilidade). Quando um grupo de disponibilidade é excluído de uma réplica secundária, a réplica primária fica no estado RESTORING, e as alterações não são permitidas nos bancos de dados.  

  
## <a name="limitations-and-recommendations"></a><a name="Restrictions"></a> Limitações e recomendações  
  
-   Quando o grupo de disponibilidade está online, excluí-lo de uma réplica secundária faz com que a réplica primária passe para o estado RESTORING. Portanto, se for possível, remova o grupo de disponibilidade somente da instância do servidor que hospeda a réplica principal.    
-   Se você excluir um grupo de disponibilidade de um computador que foi removido do cluster de failover WSFC, o grupo de disponibilidade só será excluído localmente. 
-   Evite remover um grupo de disponibilidade quando o cluster WSFC (Windows Server Failover Clustering) não tem quorum. Caso seja necessário remover um grupo de disponibilidade enquanto o cluster perde quorum, o grupo de disponibilidade de metadados armazenado no cluster não será removido. Depois que o cluster recuperar o quorum, será necessário remover novamente o grupo de disponibilidade para removê-lo do cluster WSFC.    
-   Em uma réplica secundária, DROP AVAILABILITY GROUP só deve ser usado para fins de emergência. Isso ocorre porque, ao remover um grupo de disponibilidade, você o coloca offline. Se você remover o grupo de disponibilidade de uma réplica secundária, a réplica primária não poderá determinar se o estado OFFLINE ocorreu devido à perda de quorum, a um failover forçado ou a um comando DROP AVAILABILITY GROUP. A réplica primária passa para o estado RESTORING para evitar uma possível situação de separação. Para obter mais informações, consulte [How It Works: DROP AVAILABILITY GROUP Behaviors](https://docs.microsoft.com/archive/blogs/psssql/how-it-works-drop-availability-group-behaviors) (Como funcionam os comportamentos de DROP AVAILABILITY GROUP) (blog CSS SQL Server Engineers).  
  
##  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER. Para remover um grupo de disponibilidade que não é hospedado pela instância de servidor local, você precisará da permissão CONTROL SERVER ou CONTROL nesse grupo de disponibilidade.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para excluir um grupo de disponibilidade**  
  
1.  No Pesquisador de Objetos, conecte-se à instância de servidor que hospeda a réplica primária, se possível, ou conecte-se a outra instância de servidor que é habilitada para Grupos de Disponibilidade AlwaysOn em um nó WSFC que possuem as credenciais de segurança corretas para o grupo de disponibilidade. Expanda a árvore de servidor.  
  
2.  Expanda os nós **Alta Disponibilidade AlwaysOn** e **Grupos de Disponibilidade**.  
  
3.  Essa etapa depende de se você deseja excluir vários grupos de disponibilidade ou apenas um grupo de disponibilidade da seguinte maneira:  
  
    -   Para excluir vários grupos de disponibilidade (cujas réplicas primárias estão na instância de servidor conectada), use o painel **Detalhes do Pesquisador de Objetos** para exibir e selecionar todos os grupos de disponibilidade que você deseja excluir. Para obter mais informações, veja [Usar os detalhes do Pesquisador de Objetos para monitorar grupos de disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-object-explorer-details-to-monitor-availability-groups.md).  
  
    -   Para excluir um único grupo de disponibilidade, selecione-o no painel **Pesquisador de Objetos** ou no painel **Detalhes do Pesquisador de Objetos** .  
  
4.  Clique com o botão direito do mouse no grupo ou grupos de disponibilidade selecionados e selecione o comando **Excluir** .  
  
5.  Na caixa de diálogo **Remover Grupo de Disponibilidade** , para excluir todos os grupos de disponibilidade listados, clique em **OK**. Se você não desejar remover todos os grupos de disponibilidade listados, clique em **Cancelar**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para excluir um grupo de disponibilidade**  
  
1.  Conecte-se à instância de servidor que hospeda a réplica primária, se possível, ou conecte-se a outra instância de servidor que é habilitada para Grupos de Disponibilidade AlwaysOn em um nó WSFC que possuem as credenciais de segurança corretas para o grupo de disponibilidade.  
  
2.  Use a instrução [DROP AVAILABILITY GROUP](../../../t-sql/statements/drop-availability-group-transact-sql.md) , da seguinte maneira  
  
     DROP AVAILABILITY GROUP *group_name*  
  
     em que *group_name* é o nome do grupo de disponibilidade a ser removido.  
  
     O exemplo a seguir exclui o grupo de disponibilidade `MyAG` .  
  
    ```  
    DROP AVAILABILITY GROUP MyAG;  
    ```  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> Usando o PowerShell  
 **Para excluir um grupo de disponibilidade**  
  
 No provedor do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell:  
  
1.  Altere o diretório (**cd**) na instância de servidor que hospeda a réplica primária, se possível, ou conecte-se a outra instância de servidor que esteja habilitada para Grupos de Disponibilidade AlwaysOn em um nó WSFC que possuam as credenciais de segurança corretas para o grupo de disponibilidade.  
  
2.  Use o cmdlet **Remove-SqlAvailabilityGroup** .  
  
     Por exemplo, o comando a seguir remove o grupo de disponibilidade denominado `MyAg`. Este comando pode ser executado em qualquer instância de servidor que hospeda uma réplica de disponibilidade para o grupo de disponibilidade.  
  
    ```  
    Remove-SqlAvailabilityGroup `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg  
    ```  
  
    > [!NOTE]  
    >  Para exibir a sintaxe de um cmdlet, use o cmdlet **Get-Help** no ambiente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Para configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> Conteúdo relacionado  
  
-   [How It Works: DROP AVAILABILITY GROUP Behaviors](https://docs.microsoft.com/archive/blogs/psssql/how-it-works-drop-availability-group-behaviors) (Como funcionam os comportamentos de DROP AVAILABILITY GROUP) (blog CSS SQL Server Engineers)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Criação e configuração de grupos de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)  
  
  
