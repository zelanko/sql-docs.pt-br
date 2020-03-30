---
title: Configurar uma política de failover automático flexível para um grupo de disponibilidade
description: Descreve como configurar uma política de failover flexível para um Grupo de Disponibilidade AlwaysOn usando o T-SQL (Transact-SQL), o PowerShell ou o SQL Server Management Studio.
ms.date: 11/05/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], flexible failover policy
- Availability Groups [SQL Server], failover
- failover [SQL Server], AlwaysOn Availability Groups
ms.assetid: 1ed564b4-9835-4245-ae35-9ba67419a4ce
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.custom: seo-lt-2019
ms.openlocfilehash: 39e6e14700fe7ad9d9c1c3ba71eca82b3855beb2
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "74056679"
---
# <a name="configure-a-flexible-automatic-failover-policy-for-an-always-on-availability-group"></a>Configurar uma política de failover automático flexível para um grupo de disponibilidade Always On

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Este tópico descreve como configurar a política de failover flexível para um grupo de disponibilidade Always On usando o [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou o PowerShell no SQL Server. Uma política de failover flexível fornece um controle granular das condições que causam um [failover automático](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md) de um grupo de disponibilidade. Ao alterar as condições de falha que disparam um failover automático e a frequência de verificações de integridade, você pode aumentar ou diminuir a probabilidade de um failover automático para oferecer suporte ao seu SLA para alta disponibilidade.  

   A política de failover flexível de um grupo de disponibilidade é definida por seu nível da condição de falha e pelo limite de tempo limite da verificação de integridade. Ao detectar que um grupo de disponibilidade excedeu seu nível de condição de falha ou seu limite de tempo limite da verificação de integridade, a DLL de recurso do grupo de disponibilidade responde ao cluster WSFC (Windows Server Failover Clustering). O cluster WSFC inicia um failover automático para a réplica secundária.  
 
  > [!NOTE]  
  > A política de failover flexível de um grupo de disponibilidade não pode ser configurada usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
 
## <a name="limitations-on-automatic-failovers"></a><a name="Limitations"></a> Limitações sobre failovers automáticos  
  
-   Para que um failover automático ocorra, a réplica primária e uma réplica secundária deverão ser configuradas para o modo de disponibilidade de confirmação síncrona com failover automático e a réplica secundária deverá ser sincronizada com a réplica primária.  
  
-   Apenas três réplicas têm suporte para o failover automático.  
  
-   Se um grupo de disponibilidade exceder seu limite de falha do WSFC, o cluster do WSFC não tentará um failover automático para o grupo de disponibilidade. Além disso, o grupo de recursos do WSFC do grupo de disponibilidade permanece em um estado com falha até o administrador de cluster manualmente colocar online o grupo de recursos com falha ou o administrador de banco de dados executar um failover manual do grupo de disponibilidade. O *limite de falha do WSFC* é definido como o número máximo de falhas com suporte para o grupo de disponibilidade durante um determinado período de tempo. O período padrão é de seis horas e o valor padrão para o número máximo de falhas durante este período é *n*-1, em que *n* é o número de nós do WSFC. Para alterar os valores do limite de failover para um determinado grupo de disponibilidade, use o Console de Gerenciador de Failover WSFC.  
  
##  <a name="prerequisites"></a><a name="Prerequisites"></a> Pré-requisitos  
  
-   Você deve estar conectado à instância do servidor que hospeda a réplica primária.  
   
##  <a name="permissions"></a><a name="Permissions"></a> Permissões  
  
|Tarefa|Permissões|  
|----------|-----------------|  
|Para configurar a política de failover flexível para um novo grupo de disponibilidade|Requer a associação na função de servidor fixa **sysadmin** e a permissão de servidor CREATE AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.|  
|Para modificar a política de um grupo de disponibilidade existente|Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.|  

##  <a name="health-check-timeout-threshold"></a><a name="HCtimeout"></a> Limite do tempo limite da verificação de integridade  
 A DLL de recurso do WSFC do grupo de disponibilidade executa uma *verificação de integridade* da réplica primária, chamando o procedimento armazenado [sp_server_diagnostics](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) na instância do SQL Server que hospeda a réplica primária. **sp_server_diagnostics** retorna resultados em um intervalo 1/3 em relação ao limite do tempo limite da verificação de integridade para o grupo de disponibilidade. O limite do tempo limite da verificação de integridade padrão é de 30 segundos, levando **sp_server_diagnostics** a retornar em um intervalo de 10 segundos. Se **sp_server_diagnostics** for lento ou não estiver retornando informações, a DLL de recurso aguardará o intervalo completo do limite de tempo limite da verificação de integridade antes de determinar que a réplica primária não está respondendo. Se a réplica primária não estiver respondendo, um failover automático será iniciado, se tiver suporte no momento.  
  
> [!IMPORTANT]  
>  **sp_server_diagnostics** não realiza verificações de integridade no nível de banco de dados.  
  
##  <a name="failure-condition-level"></a><a name="FClevel"></a> Nível da condição de falha  
 O nível da condição de falha do grupo de disponibilidade determina se os dados de diagnóstico e as informações de integridade retornadas por **sp_server_diagnostics** garantem um failover automático. O *nível de condição de falha* especifica as condições de falha que disparam um failover automático. Há cinco níveis da condição de falha que variam do menos restritivo (nível 1) até o mais restritivo (nível 5). Um nível específico abrange todos os níveis menos restritivos. Portanto, o nível mais rígido, cinco, inclui os quatro níveis de condições menos restritivos e assim por diante.  
  
> [!IMPORTANT]  
>  Bancos de dados danificados e bancos de dados suspeitos não são detectados por nenhum nível de condição de falha. Portanto, um banco de dados que esteja danificado ou suspeito (seja devido a um problema de hardware, corrupção de dados ou outro problema) nunca dispara um failover automático.  
  
 A tabela a seguir descreve as condições de falha que correspondem a cada nível.  
  
|Nível|Condição de falha|[!INCLUDE[tsql](../../../includes/tsql-md.md)] Valor|Valor de PowerShell|  
|-----------|-----------------------|------------------------------|----------------------|  
|Um|Em servidor inativo. Especifica que um failover automático é iniciado quando uma destas condições ocorre:<br /><br /> O serviço [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está inativo.<br /><br /> A concessão do grupo de disponibilidade para conexão com o cluster WSFC expira porque nenhum ACK foi recebido da instância de servidor. Para obter mais informações, veja [Como funciona o tempo limite de concessão de AlwaysOn do SQL Server](https://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx).<br /><br /> <br /><br /> Este é o nível menos restritivo.|1|**OnServerDown**|  
|Dois|Em servidor sem resposta. Especifica que um failover automático é iniciado quando uma destas condições ocorre:<br /><br /> A instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não se conecta ao cluster e o limite de tempo limite especificado pelo usuário do grupo de disponibilidade é excedido.<br /><br /> A réplica de disponibilidade está em estado de falha.|2|**OnServerUnresponsive**|  
|Três|Em erros críticos do servidor. Especifica que um failover automático é iniciado em erros internos críticos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , como spinlocks órfãos, violações do acesso de gravação graves ou muito despejo.<br /><br /> Este é o nível padrão.|3|**OnCriticalServerError**|  
|Quatro|Em erros moderados do servidor. Especifica que um failover automático é iniciado em caso de erros internos moderados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , como uma condição de memória insuficiente persistente no pool de recursos interno do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|4|**OnModerateServerError**|  
|Cinco|Em qualquer condição de falha qualificada. Especifica que um failover automático é iniciado em qualquer condição de falha qualificada, incluindo:<br /><br /> Detecção de deadlock do Agendador.<br /><br /> Detecção de um deadlock insolúvel.<br /><br /> <br /><br /> Este é o nível mais restritivo.|5|**OnAnyQualifiedFailureConditions**|  
  
> [!NOTE]  
>  A falta de resposta de uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para solicitações do cliente é irrelevante para grupos de disponibilidade.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para configurar a política de failover flexível**  
  
1.  Conecte-se à instância de servidor que hospeda a réplica primária.  
  
2.  Para um novo grupo de disponibilidade, use a instrução [CREATE AVAILABILITY GROUP](../../../t-sql/statements/create-availability-group-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] . Se você estiver modificando um grupo de disponibilidade existente, use a instrução [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] .  
  
    -   Para definir o nível de condição de failover, use a opção FAILURE_CONDITION_LEVEL = *n* , em que *n* é um número inteiro de 1 a 5.  
  
         Por exemplo, a instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] a seguir altera o nível da condição de falha de um grupo de disponibilidade existente, `AG1`, para o nível um:  
  
        ```  
  
        ALTER AVAILABILITY GROUP AG1 SET (FAILURE_CONDITION_LEVEL = 1);  
        ```  
  
         A relação destes valores inteiros para os níveis de condição de falha é a seguinte:  
  
        |[!INCLUDE[tsql](../../../includes/tsql-md.md)] Valor|Nível|Automático é o failover iniciado em caso de...|  
        |------------------------------|-----------|-------------------------------------------|  
        |1|Um|Em servidor inativo. O serviço SQL Server é interrompido devido a um failover ou a uma reinicialização.|  
        |2|Dois|Em servidor sem resposta. Qualquer condição de valor inferior é atendida, o serviço SQL Server está conectado ao cluster e o tempo limite de verificação de integridade é excedido, ou a réplica primária atual está em um estado de falha.|  
        |3|Três|Em erros críticos do servidor. Qualquer condição de valor inferior é atendida ou há um erro crítico de servidor interno.<br /><br /> Este é o nível padrão.|  
        |4|Quatro|Em erros moderados do servidor. Qualquer condição de valor inferior é atendida ou há um erro moderado de servidor.|  
        |5|Cinco|Em qualquer condição de falha qualificada. Qualquer condição de valor inferior é atendida ou há uma condição de falha qualificada.|  
  
         Para obter mais informações sobre os níveis de condição de failover, consulte [Política de failover flexível para failover automático de um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/flexible-automatic-failover-policy-availability-group.md).  
  
    -   Para configurar o tempo limite de verificação de integridade, use a opção HEALTH_CHECK_TIMEOUT = *n* , em que *n* é um número inteiro de 15000 milissegundos (15 segundos) a 4294967295 milissegundos. O valor padrão é 30000 milissegundos (30 segundos).  
  
         Por exemplo, a instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] a seguir altera o limite de tempo limite de verificação de integridade de um grupo de disponibilidade existente, `AG1`, para 60.000 milissegundos (um minuto).  
  
        ```  
  
        ALTER AVAILABILITY GROUP AG1 SET (HEALTH_CHECK_TIMEOUT = 60000);  
        ```  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> Usando o PowerShell  
 **Para configurar a política de failover flexível**  
  
1.  Defina o padrão (**cd**) como a instância de servidor que hospeda a réplica primária.  
  
2.  Ao adicionar uma réplica de disponibilidade a um grupo de disponibilidade, use o cmdlet **New-SqlAvailabilityGroup** . Ao modificar uma réplica de disponibilidade existente, use o cmdlet **Set-SqlAvailabilityGroup** .  
  
    -   Para definir o nível de condição de failover, use o parâmetro **FailureConditionLevel**_level_ , onde *level* é um dos seguintes valores:  
  
        |Valor|Nível|Automático é o failover iniciado em caso de...|  
        |-----------|-----------|-------------------------------------------|  
        |**OnServerDown**|Um|Em servidor inativo. O serviço SQL Server é interrompido devido a um failover ou a uma reinicialização.|  
        |**OnServerUnresponsive**|Dois|Em servidor sem resposta. Qualquer condição de valor inferior é atendida, o serviço SQL Server está conectado ao cluster e o tempo limite de verificação de integridade é excedido, ou a réplica primária atual está em um estado de falha.|  
        |**OnCriticalServerError**|Três|Em erros críticos do servidor. Qualquer condição de valor inferior é atendida ou há um erro crítico de servidor interno.<br /><br /> Este é o nível padrão.|  
        |**OnModerateServerError**|Quatro|Em erros moderados do servidor. Qualquer condição de valor inferior é atendida ou há um erro moderado de servidor.|  
        |**OnAnyQualifiedFailureConditions**|Cinco|Em qualquer condição de falha qualificada. Qualquer condição de valor inferior é atendida ou há uma condição de falha qualificada.|  
  
         Para obter mais informações sobre os níveis de condição de failover, consulte [Política de failover flexível para failover automático de um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/flexible-automatic-failover-policy-availability-group.md).  
  
         Por exemplo, o comando a seguir altera o nível da condição de falha de um grupo de disponibilidade existente, `AG1`, para o nível um.  
  
        ```  
        Set-SqlAvailabilityGroup `   
        -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg `   
        -FailureConditionLevel OnServerDown  
        ```  
  
    -   Para definir o tempo limite de verificação de integridade, use o parâmetro **HealthCheckTimeout**_n_ , em que *n* é um número inteiro de 15000 milissegundos (15 segundos) a 4294967295 milissegundos. O valor padrão é 30000 milissegundos (30 segundos).  
  
         Por exemplo, o comando a seguir altera o tempo limite de verificação de integridade de um grupo de disponibilidade existente, `AG1`, para 120.000 milissegundos (dois minutos).  
  
        ```  
        Set-SqlAvailabilityGroup `   
        -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAG `   
        -HealthCheckTimeout 120000  
        ```  
  
> [!NOTE]  
>  Para exibir a sintaxe de um cmdlet, use o cmdlet **Get-Help** no ambiente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Para configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
-   [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)  

##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
 **To configure automatic failover**  
  
-   [Alterar o modo de disponibilidade de uma réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md) (o failover automático exige o modo de disponibilidade de confirmação síncrona)  
  
-   [Alterar o modo de failover de uma réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [Configurar a política de failover flexível para controlar condições de failover automático &#40;Grupos de disponibilidade AlwaysOn&#41;](../../../database-engine/availability-groups/windows/configure-flexible-automatic-failover-policy.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> Conteúdo relacionado  
  
-   [Como funciona o tempo limite de concessão de AlwaysOn do SQL Server](https://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Modos de disponibilidade &#40;Grupos de disponibilidade AlwaysOn&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)   
 [Failover e modos de failover &#40;Grupos de Disponibilidade AlwaysOn&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)   
 [WSFC &#40;Windows Server Failover Clustering&#41; com o SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [Política de failover para instâncias de cluster de failover](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)   
 [sp_server_diagnostics &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md)  
  
  
