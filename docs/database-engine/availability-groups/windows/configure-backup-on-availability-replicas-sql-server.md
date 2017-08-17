---
title: "Configurar o backup em réplicas de disponibilidade (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- backup priority
- backup on secondary replicas
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], backup on secondary replicas
- active secondary replicas [SQL Server], backup on
- automated backup preference
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: 74bc40bb-9f57-44e4-8988-1d69c0585eb6
caps.latest.revision: 32
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6e4b5b176c1974dd0bfe628b1fde91913dcd0309
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="configure-backup-on-availability-replicas-sql-server"></a>Configurar backup em réplicas de disponibilidade (SQL Server)
  Este tópico descreve como configurar o backup em réplicas secundárias de um grupo de disponibilidade AlwaysOn usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../../includes/tsql-md.md)]ou o PowerShell no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
> [!NOTE]  
>  Para obter uma introdução ao backup em réplicas secundárias, veja [Secundárias ativas: backup em réplicas secundárias &#40;Grupos de Disponibilidade AlwaysOn&#41;](../../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md).  
  
-   **Antes de começar:**  
  
     [Pré-requisitos](#Prerequisites)  
  
     [Segurança](#Security)  
  
-   **Para configurar o backup em réplicas secundárias, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **Acompanhamento:**  [Após configurar o backup em réplicas secundárias](#FollowUp)  
  
-   [Para obter informações sobre configurações de preferência de backup](#ForInfoAboutBuPref)  
  
-   [Conteúdo relacionado](#RelatedContent)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Você deve estar conectado à instância do servidor que hospeda a réplica primária.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
  
|Tarefa|Permissões|  
|----------|-----------------|  
|Para configurar o backup em réplicas secundárias ao criar um grupo de disponibilidade|Requer associação na função de servidor fixa **sysadmin** e a permissão de servidor CREATE AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou CONTROL SERVER.|  
|Para modificar um grupo de disponibilidade ou uma réplica de disponibilidade|Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.|  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para configurar o backup em réplicas secundárias**  
  
1.  No Pesquisador de Objetos, conecte-se à instância do servidor que hospeda a réplica primária e clique no nome do servidor para expandir a árvore de servidores.  
  
2.  Expanda os nós **Alta Disponibilidade AlwaysOn** e **Grupos de Disponibilidade** .  
  
3.  Clique no grupo de disponibilidade cujas preferências de backup você deseja configurar e selecione o comando **Propriedades** .  
  
4.  Na caixa de diálogo **Propriedades de Grupo de Disponibilidade** , selecione a página **Preferências de Backup** .  
  
5.  No painel **Onde devem ocorrer os backups?** , selecione uma destas preferências de backup automatizada para o grupo de disponibilidade:  
  
     **Preferir Secundário**  
     Especifica que os backups devem ocorrer em uma réplica secundária, exceto quando a réplica primária for a única réplica online. Nesse caso, o backup deve ocorrer na réplica primária. Essa é a opção padrão.  
  
     **Somente Secundário**  
     Especifica que os backups nunca devem ser executados na réplica primária. Se a réplica primária for a única réplica online, o backup não deveria ocorrer.  
  
     **Primária**  
     Especifica que os backups sempre devem ocorrer na réplica primária. Essa opção será útil se você precisar de recursos de backup, como a criação de backups diferenciais, que não têm suporte quando o backup é executado em uma réplica secundária.  
  
    > [!IMPORTANT]  
    >  Se você pretende usar o envio de logs para preparar qualquer banco de dados secundário para um grupo de disponibilidade, defina a preferência de backup automatizada como **Primário** até que todos os bancos de dados secundários estejam preparados e associados ao grupo de disponibilidade.  
  
     **Qualquer Réplica**  
     Especifica que você prefere que trabalhos de backup ignorem a função das réplicas de disponibilidade ao escolher a réplica para executar backups. Observe que os trabalhos de backup podem avaliar outros fatores, como prioridade de backup de cada réplica de disponibilidade em combinação com seu estado operacional e estado conectado.  
  
    > [!IMPORTANT]  
    >  Não há nenhuma imposição da configuração de preferência de backup automatizado. A interpretação dessa preferência depende da lógica, se houver, que você usa para o script em trabalhos de backup para os bancos de dados em um determinado grupo de disponibilidade. A configuração de preferência de backup automatizado não tem efeito sobre backups ad hoc. Para obter mais informações, consulte [Acompanhamento: Após configurar o backup em réplicas secundárias](#FollowUp) , posteriormente neste tópico.  
  
6.  Use a grade **Prioridades de backup de réplica** para alterar a prioridade de backup das réplicas de disponibilidade. Esta grade exibe a prioridade de backup atual de cada instância de servidor que hospeda uma réplica para o grupo de disponibilidade. As colunas da grade são as seguintes:  
  
     **Instância do Servidor**  
     O nome da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda a réplica de disponibilidade.  
  
     **Prioridade de Backup (Mais Baixa = 1, Mais Alta = 100)**  
     Especifica sua prioridade para executar backups nesta réplica em relação às outras réplicas no mesmo grupo de disponibilidade. O valor é um número inteiro no intervalo de 0..100. 1 indica a prioridade mais baixa, e 100 indica a prioridade mais alta. Se **Prioridade de Backup** = 1, a réplica de disponibilidade será escolhida para execução de backups apenas se nenhuma réplica de disponibilidade de prioridade mais alta estiver disponível atualmente.  
  
     **Excluir Réplica**  
     Selecione se desejar que esta réplica de disponibilidade nunca seja escolhida para executar backups. Isso é útil, por exemplo, para uma réplica de disponibilidade remota para a qual você nunca deseja que ocorra o failover de backups.  
  
7.  Para confirmar suas alterações, clique em **OK**.  
  
 **Modos alternativos de acessar a página Preferências de Backup**  
  
-   [Usar a caixa de diálogo Novo Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Usar o Assistente para Adicionar Réplica ao Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar a caixa de diálogo Novo Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 **Para configurar o backup em réplicas secundárias**  
  
1.  Conecte-se à instância de servidor que hospeda a réplica primária.  
  
2.  Para um novo grupo de disponibilidade, use a instrução [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md). Se você estiver modificando um grupo de disponibilidade existente, use a instrução [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md).  
  
##  <a name="PowerShellProcedure"></a> Usando o PowerShell  
 **Para configurar o backup em réplicas secundárias**  
  
1.  Defina o padrão (**cd**) como a instância de servidor que hospeda a réplica primária.  
  
2.  Opcionalmente, configure a prioridade de backup de cada réplica de disponibilidade que você está adicionando ou modificando. Esta prioridade é usada pela instância de servidor que hospeda a réplica primária para decidir qual réplica deve atender uma solicitação de backup automatizado em um banco de dados no grupo de disponibilidade (a réplica com prioridade mais alta é escolhida). Essa prioridade pode ser qualquer número entre 0 e 100, inclusive. Uma prioridade de 0 indica que a réplica não deve ser considerada como candidata para atender solicitações de backup.  A configuração padrão é 50.  
  
     Ao adicionar uma réplica de disponibilidade a um grupo de disponibilidade, use o cmdlet **New-SqlAvailabilityReplica** . Ao modificar uma réplica de disponibilidade existente, use o cmdlet **Set-SqlAvailabilityReplica** . Nos dois casos, especifique o parâmetro **BackupPriority***n* , onde *n* é um valor de 0 a 100.  
  
     Por exemplo, o comando a seguir define a prioridade de backup da réplica de disponibilidade `MyReplica` como **60**.  
  
    ```  
    Set-SqlAvailabilityReplica -BackupPriority 60 `  
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
3.  Outra opção é configurar a preferência de backup automatizada para o grupo de disponibilidade que você está criando ou modificando. Esta preferência indica como um trabalho de backup deve avaliar a réplica primária ao escolher onde executar backups. A configuração padrão é preferir réplicas secundárias.  
  
     Ao criar um grupo de disponibilidade, use o cmdlet **New-SqlAvailabilityGroup** . Ao modificar um grupo de disponibilidade existente, use o cmdlet **Set-SqlAvailabilityGroup** . Nos dois casos, especifique o parâmetro **AutomatedBackupPreference** .  
  
     onde:  
  
     **Primária**  
     Especifica que os backups sempre devem ocorrer na réplica primária. Essa opção será útil se você precisar de recursos de backup, como a criação de backups diferenciais, que não têm suporte quando o backup é executado em uma réplica secundária.  
  
    > [!IMPORTANT]  
    >  Se você pretende usar o envio de logs para preparar qualquer banco de dados secundário para um grupo de disponibilidade, defina a preferência de backup automatizada como **Primário** até que todos os bancos de dados secundários estejam preparados e associados ao grupo de disponibilidade.  
  
     **SecondaryOnly**  
     Especifica que os backups nunca devem ser executados na réplica primária. Se a réplica primária for a única réplica online, o backup não deveria ocorrer.  
  
     **Secundário**  
     Especifica que os backups devem ocorrer em uma réplica secundária, exceto quando a réplica primária for a única réplica online. Nesse caso, o backup deve ocorrer na réplica primária. Esse é o comportamento padrão.  
  
     **Nenhuma**  
     Especifica que você prefere que trabalhos de backup ignorem a função das réplicas de disponibilidade ao escolher a réplica para executar backups. Observe que os trabalhos de backup podem avaliar outros fatores, como prioridade de backup de cada réplica de disponibilidade em combinação com seu estado operacional e estado conectado.  
  
    > [!IMPORTANT]  
    >  Não há nenhuma imposição de **AutomatedBackupPreference**. A interpretação dessa preferência depende da lógica, se houver, que você usa para o script em trabalhos de backup para os bancos de dados em um determinado grupo de disponibilidade. A configuração de preferência de backup automatizado não tem efeito sobre backups ad hoc. Para obter mais informações, consulte [Acompanhamento: Após configurar o backup em réplicas secundárias](#FollowUp) , posteriormente neste tópico.  
  
     Por exemplo, o comando a seguir define a propriedade **AutomatedBackupPreference** no grupo de disponibilidade `MyAg` como **SecondaryOnly**. Backups automatizados de bancos de dados neste grupo de disponibilidade nunca ocorrerão na réplica primária, mas serão redirecionados à réplica secundária com a configuração de prioridade de backup mais alta.  
  
    ```  
    Set-SqlAvailabilityGroup `  
    -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg `  
    -AutomatedBackupPreference SecondaryOnly  
    ```  
  
> [!NOTE]  
>  Para exibir a sintaxe de um cmdlet, use o cmdlet **Get-Help** no ambiente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Para configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
-   [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)  
  
##  <a name="FollowUp"></a> Acompanhamento: Após configurar o backup em réplicas secundárias  
 Para levar em conta a preferência de backup automatizada para um determinado grupo de disponibilidade, em cada instância de servidor que hospeda uma réplica de disponibilidade cuja prioridade de backup for maior que zero (>0), gere trabalhos de backup de script para os bancos de dados no grupo de disponibilidade. Para determinar se a réplica atual é a réplica de backup preferencial, use a função [sys.fn_hadr_backup_is_preferred_replica](../../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md) no script de backup. Se a réplica de disponibilidade que está hospedada pela instância de servidor atual for a réplica de backup preferida, esta função retornará 1. Se não, a função retornará 0. Ao executar um script simples em cada réplica de disponibilidade que consulte essa função, você poderá determinar qual réplica deve executar um determinado trabalho de backup. Por exemplo, um trecho típico de um script de trabalho de backup teria a seguinte aparência:  
  
```  
IF (NOT sys.fn_hadr_backup_is_preferred_replica(@DBNAME))  
BEGIN  
      Select ‘This is not the preferred replica, exiting with success’;  
      RETURN 0 – This is a normal, expected condition, so the script returns success  
END  
BACKUP DATABASE @DBNAME TO DISK=<disk>  
   WITH COPY_ONLY;  
```  
  
 O script de um trabalho de backup com essa lógica permite agendar o trabalho para execução em cada réplica de disponibilidade na mesma agenda. Cada um desses trabalhos examina os mesmos dados para determinar qual trabalho deve ser executado, portanto, somente um dos trabalhos agendados realmente continuará para o estágio de backup.  No caso de um failover, nenhum dos scripts ou trabalhos precisa ser modificado. Além disso, se você reconfigurar um grupo de disponibilidade para adicionar uma réplica de disponibilidade, o gerenciamento do trabalho de backup exigirá simplesmente copiar ou agendar o trabalho de backup. Se você remover uma réplica de disponibilidade, simplesmente exclua o trabalho de backup da instância de servidor que hospeda essa réplica.  
  
> [!TIP]  
>  Se você usar o[Assistente de Plano de Manutenção](../../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)para criar determinado trabalho de backup, o trabalho incluirá automaticamente a lógica de script que chama e verifica a função **sys.fn_hadr_backup_is_preferred_replica** . No entanto, o trabalho de backup não retornará a mensagem "Esta não é a réplica mensagem. Crie um trabalho para cada banco de dados de disponibilidade em cada instância de servidor que hospeda uma réplica de disponibilidade para o grupo de disponibilidade.  
  
##  <a name="ForInfoAboutBuPref"></a> Para obter informações sobre configurações de preferência de backup  
 Os seguintes são úteis para obter informações relevantes para backup em secundário.  
  
|Exibição|Informações|Colunas relevantes|  
|----------|-----------------|----------------------|  
|[sys.fn_hadr_backup_is_preferred_replica](../../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md)|A réplica atual é a réplica de backup preferencial?|Não aplicável.|  
|[sys.availability_groups](../../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)|preferência de backup automatizada|**automated_backup_preference**<br /><br /> **automated_backup_preference_desc**|  
|[sys.availability_replicas](../../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)|Prioridade de backup de determinada réplica de disponibilidade|**backup_priority**|  
|[sys.dm_hadr_availability_replica_states](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md)|A réplica é local para a instância de servidor?<br /><br /> Função atual<br /><br /> Estado operacional<br /><br /> Estado conectado<br /><br /> Integridade da sincronização de uma réplicas de disponibilidade|**is_local**<br /><br /> **role**, **role_desc**<br /><br /> **operational_state**, **operational_state_desc**<br /><br /> **connected_state**, **connected_state_desc**<br /><br /> **synchronization_health**, **synchronization_health_desc**|  
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
  
-   [Guia de soluções AlwaysOn do Microsoft SQL Server para alta disponibilidade e recuperação de desastre](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   [Blog da equipe do AlwaysOn do SQL Server: o blog oficial da equipe do AlwaysOn do SQL Server](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Secundárias ativas: backup em réplicas secundárias &#40;Grupos de Disponibilidade AlwaysOn&#41;](../../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)  
  
  

