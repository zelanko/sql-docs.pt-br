---
title: Remover um grupo de disponibilidade (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.deleteag.f1
helpviewer_keywords:
- Availability Groups [SQL Server], removing
- Availability Groups [SQL Server], dropping
ms.assetid: 4b7f7f62-43a3-49db-a72e-22d4d7c2ddbb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e4227b0af8453a40e9dd63b4aef170d52f8115b2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72782925"
---
# <a name="remove-an-availability-group-sql-server"></a>Remover um grupo de disponibilidade (SQL Server)
  Este tópico descreve como excluir (descartar) um grupo de disponibilidade AlwaysOn usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou o PowerShell no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Se uma instância de servidor que hospeda uma das réplicas de disponibilidade estiver offline quando você exclui um grupo de disponibilidade, ela removerá a réplica de disponibilidade local quando estiver online novamente. O descarte de um grupo de disponibilidade exclui qualquer ouvinte de grupo de disponibilidade associado.  
  
 Observe que, se for necessário, você pode remover um grupo de disponibilidade de qualquer nó WSFC (Windows Server Failover Clustering) que processa as credenciais de segurança corretas para o grupo de disponibilidade. Isso permite excluir um grupo de disponibilidade quando nenhuma de suas réplicas de disponibilidade permanece.  
  
> [!IMPORTANT]  
>  Se possível, remova o grupo de disponibilidade somente quando ele estiver conectado à instância do servidor que hospeda a réplica primária. Quando o grupo de disponibilidade é removido da réplica primária, são permitidas alterações nos bancos de dados primários antigos (sem proteção de alta disponibilidade). Quando um grupo de disponibilidade é excluído de uma réplica secundária, a réplica primária fica no estado RESTORING, e as alterações não são permitidas nos bancos de dados.  
  
-   **Antes de começar:**  
  
     [Limitações e recomendações](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para excluir um grupo de disponibilidade usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   [Conteúdo relacionado](#RelatedContent)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-recommendations"></a><a name="Restrictions"></a>Limitações e recomendações  
  
-   Quando o grupo de disponibilidade está online, excluí-lo de uma réplica secundária faz com que a réplica primária passe para o estado RESTORING. Portanto, se for possível, remova o grupo de disponibilidade somente da instância do servidor que hospeda a réplica principal.  
  
-   Se você excluir um grupo de disponibilidade de um computador que foi removido do cluster de failover WSFC, o grupo de disponibilidade só será excluído localmente.  
  
-   Evite remover um grupo de disponibilidade quando o cluster WSFC (Windows Server Failover Clustering) não tem quorum. Caso seja necessário remover um grupo de disponibilidade enquanto o cluster perde quorum, o grupo de disponibilidade de metadados armazenado no cluster não será removido. Depois que o cluster recuperar o quorum, será necessário remover novamente o grupo de disponibilidade para removê-lo do cluster WSFC.  
  
-   Em uma réplica secundária, DROP AVAILABILITY GROUP só deve ser usado para fins de emergência. Isso ocorre porque, ao remover um grupo de disponibilidade, você o coloca offline. Se você remover o grupo de disponibilidade de uma réplica secundária, a réplica primária não poderá determinar se o estado OFFLINE ocorreu devido à perda de quorum, a um failover forçado ou a um comando DROP AVAILABILITY GROUP. A réplica primária passa para o estado RESTORING para evitar uma possível situação de separação. Para obter mais informações, consulte [How It Works: DROP AVAILABILITY GROUP Behaviors](https://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) (Como funcionam os comportamentos de DROP AVAILABILITY GROUP) (blog CSS SQL Server Engineers).  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER. Para remover um grupo de disponibilidade que não é hospedado pela instância de servidor local, você precisará da permissão CONTROL SERVER ou CONTROL nesse grupo de disponibilidade.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para excluir um grupo de disponibilidade**  
  
1.  No Pesquisador de Objetos, conecte-se à instância de servidor que hospeda a réplica primária, se possível, ou conecte-se a outra instância de servidor que é habilitada para Grupos de Disponibilidade AlwaysOn em um nó WSFC que possuem as credenciais de segurança corretas para o grupo de disponibilidade. Expanda a árvore de servidor.  
  
2.  Expanda os nós **Alta Disponibilidade AlwaysOn** e **Grupos de Disponibilidade** .  
  
3.  Essa etapa depende de se você deseja excluir vários grupos de disponibilidade ou apenas um grupo de disponibilidade da seguinte maneira:  
  
    -   Para excluir vários grupos de disponibilidade (cujas réplicas primárias estão na instância de servidor conectada), use o painel **Detalhes do Pesquisador de Objetos** para exibir e selecionar todos os grupos de disponibilidade que você deseja excluir. Para obter mais informações, veja [Usar os detalhes do Pesquisador de Objetos para monitorar grupos de disponibilidade &#40;SQL Server Management Studio&#41;](use-object-explorer-details-to-monitor-availability-groups.md).  
  
    -   Para excluir um único grupo de disponibilidade, selecione-o no painel **Pesquisador de Objetos** ou no painel **Detalhes do Pesquisador de Objetos** .  
  
4.  Clique com o botão direito do mouse no grupo ou grupos de disponibilidade selecionados e selecione o comando **Excluir** .  
  
5.  Na caixa de diálogo **Remover Grupo de Disponibilidade** , para excluir todos os grupos de disponibilidade listados, clique em **OK**. Se você não desejar remover todos os grupos de disponibilidade listados, clique em **Cancelar**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para excluir um grupo de disponibilidade**  
  
1.  Conecte-se à instância de servidor que hospeda a réplica primária, se possível, ou conecte-se a outra instância de servidor que é habilitada para Grupos de Disponibilidade AlwaysOn em um nó WSFC que possuem as credenciais de segurança corretas para o grupo de disponibilidade.  
  
2.  Use a instrução [DROP AVAILABILITY GROUP](/sql/t-sql/statements/drop-availability-group-transact-sql) , da seguinte maneira  
  
     DROP AVAILABILITY GROUP *group_name*  
  
     em que *group_name* é o nome do grupo de disponibilidade a ser removido.  
  
     O exemplo a seguir exclui o grupo de disponibilidade `MyAG` .  
  
    ```sql
    DROP AVAILABILITY GROUP MyAG;  
    ```  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> Usando o PowerShell  
 **Para excluir um grupo de disponibilidade**  
  
 No provedor do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell:  
  
1.  Altere o diretório (`cd`) na instância de servidor que hospeda a réplica primária, se possível, ou conecte-se a outra instância de servidor que é habilitada para Grupos de Disponibilidade AlwaysOn em um nó WSFC que possuem as credenciais de segurança corretas para o grupo de disponibilidade.  
  
2.  Use o cmdlet **Remove-SqlAvailabilityGroup** .  
  
     Por exemplo, o comando a seguir remove o grupo de disponibilidade denominado `MyAg`. Este comando pode ser executado em qualquer instância de servidor que hospeda uma réplica de disponibilidade para o grupo de disponibilidade.  
  
    ```powershell
    Remove-SqlAvailabilityGroup -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg  
    ```  
  
    > [!NOTE]  
    >  Para exibir a sintaxe de um cmdlet, use o cmdlet `Get-Help` no ambiente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Para configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> Conteúdo relacionado  
  
-   [How It Works: DROP AVAILABILITY GROUP Behaviors](https://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) (Como funcionam os comportamentos de DROP AVAILABILITY GROUP) (blog CSS SQL Server Engineers)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Criação e configuração de grupos de disponibilidade &#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)  
