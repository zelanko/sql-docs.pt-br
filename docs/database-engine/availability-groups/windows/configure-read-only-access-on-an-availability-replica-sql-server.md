---
title: Configurar o acesso somente leitura a uma réplica secundária de um grupo de disponibilidade
description: 'Configure a réplica secundária para permitir apenas acesso de leitura para o grupo de disponibilidade Always On. '
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
helpviewer_keywords:
- connection access to availability replicas
- Availability Groups [SQL Server], readable secondary replicas
- active secondary replicas [SQL Server], read-only access to
- Availability Groups [SQL Server], read-only routing
- Availability Groups [SQL Server], client connectivity
ms.assetid: 22387419-22c4-43fa-851c-5fecec4b049b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3cc8b9f310065c101d0c1d141389fe980cdb0654
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91113451"
---
# <a name="configure-read-only-access-to-a-secondary-replica-of-an-always-on-availability-group"></a>Configurar o acesso somente leitura a uma réplica secundária de um grupo de disponibilidade Always On
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Por padrão, tanto o acesso de leitura-gravação quanto o acesso de tentativa de leitura são permitidos para a réplica primária e nenhuma conexão direta é permitida com as réplicas secundárias de um grupo de disponibilidade AlwaysOn. Este tópico descreve como configurar o acesso de conexão em uma réplica de disponibilidade de um grupo de disponibilidade AlwaysOn no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]ou PowerShell.  
  
 Para obter informações sobre as implicações de permitir o acesso somente leitura para uma réplica secundária e uma introdução ao acesso de conexão, confira [Sobre o acesso de conexão de cliente a réplicas de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md) e [Secundárias ativas: Réplicas secundárias legíveis &#40;Grupos de Disponibilidade Always On&#41;](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).  
  
 
##  <a name="prerequisites-and-restrictions"></a><a name="Prerequisites"></a> Pré-requisitos e restrições  
  
-   Para configurar um acesso de conexão diferente, deverá estar conectado à instância de servidor que hospeda a réplica primária.  
  
##  <a name="permissions"></a><a name="Permissions"></a> Permissões  
  
|Tarefa|Permissões|  
|----------|-----------------|  
|Para configurar réplicas ao criar um grupo de disponibilidade|Requer a associação na função de servidor fixa **sysadmin** e a permissão de servidor CREATE AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.|  
|Para modificar uma réplica de disponibilidade|Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.|  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para configurar o acesso em uma réplica de disponibilidade**  
  
1.  No Pesquisador de Objetos, conecte-se à instância de servidor que hospeda a réplica primária e expanda a árvore de servidores.  
  
2.  Expanda os nós **Alta Disponibilidade AlwaysOn** e **Grupos de Disponibilidade**.  
  
3.  Clique no grupo de disponibilidade cuja réplica você deseja alterar.  
  
4.  Clique com o botão direito do mouse na réplica de disponibilidade e clique em **Propriedades**.  
  
5.  Na caixa de diálogo **Propriedades de Réplica de disponibilidade** , você pode alterar o acesso de conexão para as funções primária e secundária, da seguinte forma:  
  
    -   Para a função secundária, selecione um novo valor na lista suspensa **Secundária de Leitura** , da seguinte forma:  
  
         **Não**  
         Nenhuma conexão de usuário é permitida para bancos de dados secundários desta réplica. Eles não estão disponíveis para acesso de leitura. Essa é a configuração padrão.  
  
         **Tentativa de leitura somente**  
         Somente conexões somente leitura são permitidas para bancos de dados secundários desta réplica. Os bancos de dados secundários estão disponíveis para acesso de leitura.  
  
         **Sim**  
         Todas as conexões são permitidas para os bancos de dados secundários desta réplica, mas somente para acesso de leitura. Os bancos de dados secundários estão disponíveis para acesso de leitura.  
  
    -   Para a função primária, selecione um novo valor na lista suspensa **Conexões na função primária** , da seguinte forma:  
  
         **Permitir todas as conexões**  
         Todas as conexões são permitidas com os bancos de dados na réplica primária. Essa é a configuração padrão.  
  
         **Permitir conexões de leitura/gravação**  
         Quando a propriedade Application Intent está definida como **ReadWrite** ou não está definida, a conexão é permitida. Conexões em que a propriedade de conexão Application Intent é definida como **ReadOnly** não são permitidas. Isto pode ajudar a impedir os clientes de conectarem uma carga de trabalho com intenção de leitura à réplica primária por engano. Para obter mais informações sobre a propriedade de conexão Tentativa de Aplicativo, consulte [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para configurar o acesso em uma réplica de disponibilidade**  
  
> [!NOTE]  
>  Para obter um exemplo desse procedimento, veja [Exemplo (Transact-SQL)](#TsqlExample), mais adiante nesta seção.  
  
1.  Conecte-se à instância de servidor que hospeda a réplica primária.  
  
2.  Se você estiver especificando uma réplica para um novo grupo de disponibilidade, use a instrução [CREATE AVAILABILITY GROUP](../../../t-sql/statements/create-availability-group-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] . Se você estiver adicionando ou modificando uma réplica de um grupo de disponibilidade existente, use a instrução [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] .  
  
    -   Para configurar o acesso de conexão para a função secundária, na cláusula ADD REPLICA ou MODIFY REPLICA WITH, especifique a opção SECONDARY_ROLE, da seguinte forma:  
  
         SECONDARY_ROLE **(** ALLOW_CONNECTIONS **=** { NO | READ_ONLY | ALL } **)**  
  
         onde:  
  
         Não  
         Nenhuma conexão direta é permitida para bancos de dados secundários desta réplica. Eles não estão disponíveis para acesso de leitura. Essa é a configuração padrão.  
  
         READ_ONLY  
         Somente conexões somente leitura são permitidas para bancos de dados secundários desta réplica. Os bancos de dados secundários estão disponíveis para acesso de leitura.  
  
         ALL  
         Todas as conexões são permitidas para os bancos de dados secundários desta réplica, mas somente para acesso de leitura. Os bancos de dados secundários estão disponíveis para acesso de leitura.  
  
3.  Para configurar o acesso de conexão para a função primária, na cláusula ADD REPLICA ou MODIFY REPLICA WITH, especifique a opção PRIMARY_ROLE, da seguinte forma:  
  
     PRIMARY_ROLE **(** ALLOW_CONNECTIONS **=** { READ_WRITE | ALL } **)**  
  
     onde:  
  
     READ_WRITE  
     Conexões em que a propriedade de conexão Application Intent é definida como **ReadOnly** não são permitidas.  Quando a propriedade Application Intent está definida como **ReadWrite** ou não está definida, a conexão é permitida. Para obter mais informações sobre a propriedade de conexão Tentativa de Aplicativo, consulte [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
     ALL  
     Todas as conexões são permitidas com os bancos de dados na réplica primária. Essa é a configuração padrão.  
  
###  <a name="example-transact-sql"></a><a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 O exemplo a seguir adiciona uma réplica secundária a um grupo de disponibilidade denominado *AG2*. Uma instância de servidor autônoma *COMPUTER03\HADR_INSTANCE*, é especificada para hospedar a nova réplica de disponibilidade. Essa réplica foi configurada para permitir apenas conexões de leitura-gravação para a função primária e para permitir apenas conexões de tentativa de leitura para uma função secundária.  
  
```  
ALTER AVAILABILITY GROUP AG2   
   ADD REPLICA ON   
      'COMPUTER03\HADR_INSTANCE' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER03:7022',  
         PRIMARY_ROLE ( ALLOW_CONNECTIONS = READ_WRITE ),  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY )  
         );   
GO  
```  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> Usando o PowerShell  
 **Para configurar o acesso em uma réplica de disponibilidade**  
  
> [!NOTE]  
>  Para obter um exemplo de código, consulte [Exemplo (PowerShell)](#PSExample), posteriormente nesta seção.  
  
1.  Altere o diretório (**cd**) para a instância de servidor que hospeda a réplica primária.  
  
2.  Ao adicionar uma réplica de disponibilidade a um grupo de disponibilidade, use o cmdlet **New-SqlAvailabilityReplica** . Ao modificar uma réplica de disponibilidade existente, use o cmdlet **Set-SqlAvailabilityReplica** . Os parâmetros relevantes são os seguintes:  
  
    -   Para configurar o acesso de conexão para a função secundária, especifique o parâmetro **ConnectionModeInSecondaryRole**_secondary_role_keyword_ , em que *secondary_role_keyword* é igual a um dos seguintes valores:  
  
         **AllowNoConnections**  
         Nenhuma conexão direta é permitida com os bancos de dados na réplica secundária e os bancos de dados não estão disponíveis para acesso de leitura. Essa é a configuração padrão.  
  
         **AllowReadIntentConnectionsOnly**  
         Conexões são permitidas somente com os bancos de dados na réplica secundária em que a propriedade Application Intent está definida como **ReadOnly**. Para obter mais informações sobre essa propriedade, consulte [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
         **AllowAllConnections**  
         Todas as conexões são permitidas com os bancos de dados na réplica secundária para acesso somente leitura.  
  
    -   Para configurar o acesso de conexão para a função primária, especifique o **ConnectionModeInPrimaryRole**_primary_role_keyword_, em que *primary_role_keyword* é igual a um dos seguintes valores:  
  
         **AllowReadWriteConnections**  
         Conexões em que a propriedade de conexão Application Intent é definida como ReadOnly não são permitidas. Quando a propriedade Application Intent está definida como ReadWrite ou não está definida, a conexão é permitida. Para obter mais informações sobre a propriedade de conexão Tentativa de Aplicativo, consulte [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
         **AllowAllConnections**  
         Todas as conexões são permitidas com os bancos de dados na réplica primária. Essa é a configuração padrão.  
  
    > [!NOTE]  
    >  Para exibir a sintaxe de um cmdlet, use o cmdlet **Get-Help** no ambiente do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Para configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
###  <a name="example-powershell"></a><a name="PSExample"></a> Exemplo (PowerShell)  
 O exemplo a seguir define os parâmetros **ConnectionModeInSecondaryRole** e **ConnectionModeInPrimaryRole** para **AllowAllConnections**.  
  
```  
Set-Location SQLSERVER:\SQL\PrimaryServer\default\AvailabilityGroups\MyAg  
$primaryReplica = Get-Item "AvailabilityReplicas\PrimaryServer"  
Set-SqlAvailabilityReplica -ConnectionModeInSecondaryRole "AllowAllConnections" `   
-InputObject $primaryReplica  
Set-SqlAvailabilityReplica -ConnectionModeInPrimaryRole "AllowAllConnections" `   
-InputObject $primaryReplica  
  
```  
  
##  <a name="follow-up-after-configuring-read-only-access-for-an-availability-replica"></a><a name="FollowUp"></a> Acompanhamento: depois de configurar o acesso somente leitura para uma réplica de disponibilidade  
 **Acesso somente leitura para uma réplica secundária legível**  
  
-   Com o [Utilitário bcp](../../../tools/bcp-utility.md) ou o [Utilitário sqlcmd](../../../tools/sqlcmd-utility.md), você pode especificar o acesso somente leitura a qualquer réplica secundária habilitada para acesso somente leitura especificando a opção **-K ReadOnly** .  
  
-   Para permitir que aplicativos clientes conectem-se a réplicas secundárias legíveis:  
  
|Pré-requisito|Link|  
|------------------|----------|  
|Verifique se o grupo de disponibilidade tem um ouvinte.|[Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)|  
|Configurar o roteamento somente leitura para o grupo de disponibilidade.|[Configurar o roteamento somente leitura para um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)|  
  
 **Fatores que podem afetar gatilhos e trabalhos depois de um failover**  
  
 Se você tem gatilhos e trabalhos que podem falhar ao executar um banco de dados secundário não legível ou em um banco de dados secundário legível, você precisa executar o script dos gatilhos e dos trabalhos para verificar em uma réplica determinada se o banco de dados é primário ou secundário legível. Para obter estas informações, use a função [DATABASEPROPERTYEX](../../../t-sql/functions/databasepropertyex-transact-sql.md) para retornar a propriedade **Updatability** do banco de dados. Para identificar um banco de dados somente leitura, especifique READ_ONLY como o valor, da seguinte maneira:  
  
```  
DATABASEPROPERTYEX([db name],'UpdateAbility') = N'READ_ONLY'  
```  
  
 Para identificar um banco de dados leitura/gravação, especifique READ_WRITE como o valor.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Configurar o roteamento somente leitura para um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> Conteúdo relacionado  
  
-   [Always On: proposta de valor da secundária legível](https://docs.microsoft.com/archive/blogs/sqlserverstorageengine/alwayson-value-proposition-of-readable-secondary)  
  
-   [Always On: por que há duas opções para habilitar uma réplica secundária para a carga de trabalho de leitura?](https://docs.microsoft.com/archive/blogs/sqlserverstorageengine/alwayson-why-there-are-two-options-to-enable-a-secondary-replica-for-read-workload)  
  
-   [Always On: configurar uma réplica secundária legível](https://docs.microsoft.com/archive/blogs/sqlserverstorageengine/alwayson-setting-up-readable-seconary-replica)  
  
-   [Always On: acabei de habilitar a réplica secundária legível, mas minha consulta está bloqueada?](https://docs.microsoft.com/archive/blogs/sqlserverstorageengine/alwayson-i-just-enabled-readable-secondary-but-my-query-is-blocked)  
  
-   [Always On: disponibilizando as estatísticas mais recentes na réplica secundária legível, no banco de dados somente leitura e no instantâneo do banco de dados](https://docs.microsoft.com/archive/blogs/sqlserverstorageengine/alwayson-making-latest-statistics-available-on-readable-secondary-read-only-database-and-database-snapshot)  
  
-   [Always On: desafios das estatísticas no banco de dados somente leitura, no instantâneo do banco de dados e na réplica secundária](https://docs.microsoft.com/archive/blogs/sqlserverstorageengine/alwayson-challenges-with-statistics-on-readonly-database-database-snapshot-and-secondary-replica)  
  
-   [Always On: impacto na carga de trabalho primária ao executar a carga de trabalho de relatório na réplica secundária](https://docs.microsoft.com/archive/blogs/sqlserverstorageengine/alwayson-impact-on-the-primary-workload-when-you-run-reporting-workload-on-the-secondary-replica)  
  
-   [Always On: impacto do mapeamento da carga de trabalho de relatório na réplica secundária legível para o isolamento do instantâneo](https://docs.microsoft.com/archive/blogs/sqlserverstorageengine/alwayson-impact-of-mapping-reporting-workload-on-readable-secondary-to-snapshot-isolation)  
  
-   [Always On: minimizando o bloqueio do thread REDO ao executar a carga de trabalho de relatório na réplica secundária](https://docs.microsoft.com/archive/blogs/sqlserverstorageengine/alwayson-minimizing-blocking-of-redo-thread-when-running-reporting-workload-on-secondary-replica)  
  
-   [Always On: réplica secundária legível e latência de dados](https://docs.microsoft.com/archive/blogs/sqlserverstorageengine/alwayson-readable-secondary-and-data-latency)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Secundárias ativas: réplicas secundárias legíveis &#40;Grupos de Disponibilidade Always On&#41;](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [Sobre o acesso de conexão de cliente a réplicas de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)  
  
  
