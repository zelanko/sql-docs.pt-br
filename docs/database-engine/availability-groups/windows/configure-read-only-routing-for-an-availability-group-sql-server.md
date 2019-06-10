---
title: Configurar o roteamento somente leitura para um grupo de disponibilidade
description: Roteie automaticamente todo o tráfego somente leitura para uma réplica secundária usando o roteamento somente leitura para o grupo de disponibilidade Always On – usando o T-SQL (Transact-SQL) ou o PowerShell.
ms.custom: seodec18
ms.date: 02/25/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- read-only routing
- Availability Groups [SQL Server], readable secondary replicas
- Availability Groups [SQL Server], read-only routing
- readable secondary replicas
- Availability Groups [SQL Server], client connectivity
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: 7bd89ddd-0403-4930-a5eb-3c78718533d4
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: 405a8d9d63db1f295e4a4fd95ede4c5ff1950877
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66793661"
---
# <a name="configure-read-only-routing-for-an-always-on-availability-group"></a>Configurar o roteamento somente leitura para um grupo de disponibilidade Always On
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Para configurar um grupo de disponibilidade AlwaysOn para oferecer suporte ao roteamento somente leitura no [!INCLUDE[ssnoversion](../../../includes/ssnoversion-md.md)], você pode usar o [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou o PowerShell. *Roteamento somente leitura* refere-se à capacidade do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de encaminhar solicitações de conexão somente leitura para uma [réplica secundária legível](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md) AlwaysOn disponível (ou seja, uma réplica que é configurada para permitir cargas de trabalho somente leitura ao ser executada sob a função secundária). Para dar suporte ao roteamento somente leitura, o grupo de disponibilidade deve ter um [ouvinte do grupo de disponibilidade](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md). Clientes somente leitura devem direcionar suas solicitações de conexão para este ouvinte e as cadeias de conexão do cliente devem especificar a intenção do aplicativo como "somente leitura." Ou seja, elas devem ser *solicitações de conexão de intenção de leitura*.  

O roteamento somente leitura está disponível no [!INCLUDE[sssql15](../../../includes/sssql15-md.md)] e posterior.

> [!NOTE]  
>  Para obter informações sobre como configurar uma réplica secundária legível, veja [Configurar o acesso somente leitura em uma réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md).  

  
##  <a name="Prerequisites"></a> Pré-requisitos  
  
-   O grupo de disponibilidade deve possuir um ouvinte de grupo de disponibilidade. Para obter mais informações, veja [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).  
  
-   Uma ou mais réplicas de disponibilidade devem estar configuradas para aceitar somente leitura na função secundária (ou seja, para serem [réplicas secundárias legíveis](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)). Para obter mais informações, veja [Configure Read-Only Access on an Availability Replica &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md).  
  
-   Você deve estar conectado à instância do servidor que hospeda a réplica primária atual.  

-   Se estiver usando um Logon do SQL, verifique se a conta está configurada corretamente. Para obter mais informações, confira[Gerenciamento de logons e trabalhos para os bancos de dados de um grupo de disponibilidade (SQL Server)](logins-and-jobs-for-availability-group-databases.md).
  
##  <a name="RORReplicaProperties"></a> Quais as propriedades de réplica você precisa configurar para dar suporte a roteamento somente leitura?  
  
-   Para cada réplica secundária legível que deve dar suporte a roteamento somente leitura, você precisa especificar uma *URL de roteamento somente leitura*. Esta URL só entra em vigor quando a réplica local estiver sendo executada sob a função secundária. A URL do roteamento somente leitura deve ser especificada réplica por réplica, quando necessário. Cada URL de roteamento somente leitura é usada para solicitações de conexão de intenção de leitura para uma réplica secundária legível específica. Normalmente, toda réplica secundária legível é atribuída uma URL de roteamento somente leitura.  
  
     Para obter informações sobre como calcular a URL de roteamento somente leitura de uma réplica de disponibilidade, veja [Calculando read_only_routing_url de AlwaysOn](https://web.archive.org/web/20170512023255/https://blogs.msdn.microsoft.com/mattn/2012/04/25/calculating-read_only_routing_url-for-alwayson/)
  
-   Para cada réplica de disponibilidade que você quer dar suporte a roteamento somente leitura quando é a réplica primária, você precisará especificar uma *lista de roteamento somente leitura*. Uma determinada lista de roteamento somente leitura só entra em vigor quando a réplica local estiver sendo executada em uma função primária. Essa lista deve ser especificada réplica por réplica, quando necessário. Normalmente, cada lista de roteamento somente leitura deveria conter todas as URLs de roteamento somente leitura, com a URL da réplica local no final da lista.  
  
    > [!NOTE]  
    >  As solicitações de conexão de intenção de leitura são roteadas para a primeira entrada disponível na lista de roteamento somente leitura da réplica primária atual. No entanto, o balanceamento de carga entre réplicas somente leitura é suportado. Para obter mais informações, veja [Configurar o balanceamento de carga entre réplicas somente leitura](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md#loadbalancing).  
  
> [!NOTE]  
>  Para obter informações sobre ouvintes do grupo de disponibilidade e mais informações sobre roteamento somente leitura, veja [Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativo &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md).  
  
##  <a name="Permissions"></a> Permissões  
  
|Tarefa|Permissões|  
|----------|-----------------|  
|Para configurar réplicas ao criar um grupo de disponibilidade|Requer a associação na função de servidor fixa **sysadmin** e a permissão de servidor CREATE AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.|  
|Para modificar uma réplica de disponibilidade|Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.|  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
### <a name="configure-a-read-only-routing-list"></a>Configurar uma lista de roteamento somente leitura  
 Use as etapas a seguir para configurar o roteamento somente leitura usando o Transact-SQL. Para obter um exemplo de código, veja [Exemplo (Transact-SQL)](#TsqlExample), mais adiante nesta seção.  
  
1.  Conecte-se à instância de servidor que hospeda a réplica primária.  
  
2.  Se você estiver especificando uma réplica para um novo grupo de disponibilidade, use a instrução [CREATE AVAILABILITY GROUP](../../../t-sql/statements/create-availability-group-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] . Se você estiver adicionando ou modificando uma réplica para um grupo de disponibilidade existente, use a instrução [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] .  
  
    -   Para configurar o roteamento somente leitura para a função secundária, na cláusula ADD REPLICA ou MODIFY REPLICA WITH, especifique a opção SECONDARY_ROLE, da seguinte forma:  
  
         SECONDARY_ROLE **(** READ_ONLY_ROUTING_URL **='** TCP **://** _system-address_ **:** _port_ **')**  
  
         Os parâmetros da URL de roteamento somente leitura são os seguintes:  
  
         *system-address*  
         É uma cadeia de caracteres, como um nome de sistema, um nome de domínio totalmente qualificado ou um endereço IP, que identifica de forma exclusiva o sistema do computador de destino.  
  
         *port*  
         É um número de porta que é usado pelo mecanismo de banco de dados da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
         Por exemplo:   `SECONDARY_ROLE (READ_ONLY_ROUTING_URL = N'TCP://COMPUTER01.contoso.com:1433')`  
  
         Em uma cláusula MODIFY REPLICA, o ALLOW_CONNECTIONS será opcional se a réplica já estiver configurada para permitir conexões somente leitura.  
  
         Para obter mais informações, veja [Calculando read_only_routing_url do Always On](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-Always%20On.aspx).  
  
    -   Para configurar o roteamento somente leitura para a função primária, na cláusula ADD REPLICA ou MODIFY REPLICA WITH, especifique a opção PRIMARY_ROLE, da seguinte forma:  
  
         PRIMARY_ROLE **(** READ_ONLY_ROUTING_LIST **=('** _server_ **'** [ **,** ...*n* ] **))**  
  
         em que *server* identifica uma instância de servidor que hospeda uma réplica secundária somente leitura em um grupo de disponibilidade.  
  
         Por exemplo:   `PRIMARY_ROLE (READ_ONLY_ROUTING_LIST=('Server1','Server2'))`  
  
        > [!NOTE]  
        >  Você precisa definir a URl de roteamento somente leitura antes de configurar a lista de roteamento somente leitura.  
  
###  <a name="loadbalancing"></a> Configurar o balanceamento de carga entre réplicas somente leitura  
 A partir do [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)], é possível configurar o balanceamento de carga em um conjunto de réplicas somente leitura. Anteriormente, o roteamento somente leitura sempre direcionava o tráfego para a primeira réplica disponível na lista de roteamento. Para tirar proveito desse recurso, use um nível de parênteses aninhados em torno das instâncias de servidor **READ_ONLY_ROUTING_LIST** nos comandos **CREATE AVAILABILITY GROUP** ou **ALTER AVAILABILITY GROUP** .  
  
 Por exemplo, a lista de roteamento a seguir balanceia a carga da solicitação de conexão de intenção de leitura entre duas réplicas somente leitura, `Server1` e `Server2`. Os parênteses aninhados que envolvem esses servidores identificam o conjunto de balanceamento de carga. Se nenhuma das réplicas estiver disponível neste conjunto, ele continuará a tentar se conectar consecutivamente a outras réplicas, `Server3` e `Server4`, na lista de roteamento somente leitura.  
  
```sql  
READ_ONLY_ROUTING_LIST = (('Server1','Server2'), 'Server3', 'Server4')  
```  
  
 Observe que cada entrada na lista de roteamento pode ser, por si só, um conjunto de réplicas somente leitura com balanceamento de carga. O exemplo a seguir demonstra isso.  
  
```sql  
READ_ONLY_ROUTING_LIST = (('Server1','Server2'), ('Server3', 'Server4', 'Server5'), 'Server6')  
```  
  
 Há suporte para apenas um nível de parênteses aninhados.  
  
###  <a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 O exemplo a seguir modifica duas réplicas de disponibilidade de um grupo de disponibilidade existente, `AG1` para oferecer suporte ao roteamento somente leitura quando uma dessas réplicas possui a função primária no momento. Para identificar as instâncias de servidor que hospedam a réplica de disponibilidade, este exemplo especifica os nomes da instância –`COMPUTER01` e `COMPUTER02`.  
  
```  
ALTER AVAILABILITY GROUP [AG1]  
 MODIFY REPLICA ON  
N'COMPUTER01' WITH   
(SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY));  
ALTER AVAILABILITY GROUP [AG1]  
 MODIFY REPLICA ON  
N'COMPUTER01' WITH   
(SECONDARY_ROLE (READ_ONLY_ROUTING_URL = N'TCP://COMPUTER01.contoso.com:1433'));  
  
ALTER AVAILABILITY GROUP [AG1]  
 MODIFY REPLICA ON  
N'COMPUTER02' WITH   
(SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY));  
ALTER AVAILABILITY GROUP [AG1]  
 MODIFY REPLICA ON  
N'COMPUTER02' WITH   
(SECONDARY_ROLE (READ_ONLY_ROUTING_URL = N'TCP://COMPUTER02.contoso.com:1433'));  
  
ALTER AVAILABILITY GROUP [AG1]   
MODIFY REPLICA ON  
N'COMPUTER01' WITH   
(PRIMARY_ROLE (READ_ONLY_ROUTING_LIST=('COMPUTER02','COMPUTER01')));  
  
ALTER AVAILABILITY GROUP [AG1]   
MODIFY REPLICA ON  
N'COMPUTER02' WITH   
(PRIMARY_ROLE (READ_ONLY_ROUTING_LIST=('COMPUTER01','COMPUTER02')));  
GO  
  
```  
  
##  <a name="PowerShellProcedure"></a> Usando o PowerShell  
  
### <a name="configure-a-read-only-routing-list"></a>Configurar uma lista de roteamento somente leitura  
 Use as etapas a seguir para configurar o roteamento somente leitura usando o PowerShell. Para obter um exemplo de código, consulte [Exemplo (PowerShell)](#PSExample), posteriormente nesta seção.  
  
1.  Defina o padrão (**cd**) como a instância de servidor que hospeda a réplica primária.  
  
2.  Ao adicionar uma réplica de disponibilidade a um grupo de disponibilidade, use o cmdlet **New-SqlAvailabilityReplica** . Ao modificar uma réplica de disponibilidade existente, use o cmdlet **Set-SqlAvailabilityReplica** . Os parâmetros relevantes são os seguintes:  
  
    -   Para configurar o roteamento somente leitura para a função secundária, especifique o parâmetro **ReadonlyRoutingConnectionUrl"** _url_ **"** .  
  
         em que *url* é o FQDN (nome de domínio totalmente qualificado de conectividade) e a porta a ser usada no roteamento para a réplica em conexões somente leitura. Por exemplo:  `-ReadonlyRoutingConnectionUrl "TCP://DBSERVER8.manufacturing.Adventure-Works.com:7024"`  
  
         Para obter mais informações, veja [Calculando read_only_routing_url do Always On](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-Always%20On.aspx).  
  
    -   Para configurar o acesso de conexão para a função primária, especifique **ReadonlyRoutingList"** _server_ **"** [ **,** ...*n* ], em que *server* identifica uma instância de servidor que hospeda uma réplica secundária somente leitura no grupo de disponibilidade. Por exemplo:  `-ReadOnlyRoutingList "SecondaryServer","PrimaryServer"`  
  
        > [!NOTE]  
        >  Você precisa definir a URl de roteamento somente leitura de uma réplica antes de configurar sua lista de roteamento somente leitura.  
  
    > [!NOTE]  
    >  Para exibir a sintaxe de um cmdlet, use o cmdlet **Get-Help** no ambiente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
### <a name="set-up-and-use-the-sql-server-powershell-provider"></a>Configurar e usar o provedor do SQL Server PowerShell  
  
-   [Provedor do SQL Server PowerShell](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
-   [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)  
  
###  <a name="PSExample"></a> Exemplo (PowerShell)  
 O exemplo a seguir configura a réplica primária e uma réplica secundária em um grupo de disponibilidade para o roteamento somente leitura. Primeiro, o exemplo atribui uma URL de roteamento somente leitura a cada réplica. Em seguida, ele define a lista de roteamento somente leitura na réplica primária. As conexões com o conjunto de propriedades "ReadOnly" na cadeia de conexão serão redirecionados à réplica secundária. Se a réplica secundária não estiver legível (conforme determinado pela configuração **ConnectionModeInSecondaryRole** ), a conexão será direcionada de volta para a réplica primária.  
  
```  
Set-Location SQLSERVER:\SQL\PrimaryServer\default\AvailabilityGroups\MyAg  
$primaryReplica = Get-Item "AvailabilityReplicas\PrimaryServer"  
$secondaryReplica = Get-Item "AvailabilityReplicas\SecondaryServer"  
  
Set-SqlAvailabilityReplica -ReadOnlyRoutingConnectionUrl "TCP://PrimaryServer.domain.com:1433" -InputObject $primaryReplica  
Set-SqlAvailabilityReplica -ReadOnlyRoutingConnectionUrl "TCP://SecondaryServer.domain.com:1433" -InputObject $secondaryReplica  
Set-SqlAvailabilityReplica -ReadOnlyRoutingList "SecondaryServer","PrimaryServer" -InputObject $primaryReplica  
```  
  
##  <a name="FollowUp"></a> Acompanhamento: Depois de configurar o roteamento somente leitura  
 Quando a réplica primária atual e as réplicas secundárias legíveis são configuradas para oferecer suporte ao roteamento somente leitura em ambas as funções, as réplicas secundárias legíveis podem receber solicitações de conexão com intenção de leitura de clientes que se conectam pelo ouvinte de grupo de disponibilidade.  
  
> [!TIP]  
>  Com o [Utilitário bcp](../../../tools/bcp-utility.md) ou o [Utilitário sqlcmd](../../../tools/sqlcmd-utility.md), você pode especificar o acesso somente leitura a qualquer réplica secundária habilitada para acesso somente leitura especificando a opção **-K ReadOnly** .  
  
###  <a name="ConnStringReqsRecs"></a> Requisitos e recomendações para cadeias de conexão de cliente  
 Para que um aplicativo cliente use o roteamento somente leitura, sua cadeia de conexão deve atender aos seguintes requisitos:  
  
-   Usar o protocolo TCP.  
  
-   Definir o atributo/propriedade de intenção do aplicativo como readonly.  
  
-   Referenciar o ouvinte de um grupo de disponibilidade que está configurado para oferecer suporte ao roteamento somente leitura.  
  
-   Referenciar um banco de dados nesse grupo de disponibilidade.  
  
 Além disso, é recomendável que cadeias de conexão habilitem o failover de várias sub-redes, oferecendo suporte a um thread de cliente paralelo para cada réplica em cada sub-rede. Isso minimiza o tempo de reconexão do cliente após um failover.  
  
 A sintaxe de uma cadeia de conexão depende do provedor SQL Server que um aplicativo está usando. A cadeia de conexão de exemplo a seguir para o provedor de dados .NET Framework 4.0.2 para SQL Server ilustra as partes de uma cadeia de conexão que são necessárias e recomendadas no roteamento somente leitura.  
  
```  
Server=tcp:MyAgListener,1433;Database=Db1;IntegratedSecurity=SSPI;ApplicationIntent=ReadOnly;MultiSubnetFailover=True  
```  
  
 Para obter mais informações sobre a intenção do aplicativo somente leitura e o roteamento somente leitura, veja [Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativo &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md).  
  
### <a name="if-read-only-routing-is-not-working-correctly"></a>Se o roteamento somente leitura não estiver funcionando corretamente  
 Para obter informações sobre como solucionar problemas de uma configuração de roteamento somente leitura, veja [O roteamento somente leitura não está funcionando corretamente](../../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md#ROR).  
  
##  <a name="RelatedTasks"></a> Próximas etapas 
**Para exibir configurações do roteamento somente leitura**  
  
-   [sys.availability_read_only_routing_lists &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-availability-read-only-routing-lists-transact-sql.md)  
  
-   [sys.availability_replicas &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md) (coluna **read_only_routing_url**)  
  
**Para configurar o acesso de conexão de cliente**  
  
-   [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Configurar o acesso somente leitura em uma réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
**Para usar cadeias de conexão em aplicativos**  
  
-   [Suporte do SQL Server Native Client à alta disponibilidade e recuperação de desastre](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
  
-   [Usando palavras-chave da cadeia de conexão com o SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
  
**Blogs:**  
  
-    [Calculando read_only_routing_url de AlwaysOn](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-Always%20On.aspx)  
  
-    [Blogs da equipe do Always On do SQL Server: o blog oficial da equipe do Always On do SQL Server](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
-    [Blogs dos engenheiros do CSS SQL Server](https://blogs.msdn.com/b/psssql/)  
  
**White papers:**  
  
-    [White papers da Microsoft para SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
-    [White papers da equipe de consultoria do cliente do SQL Server](https://techcommunity.microsoft.com/t5/DataCAT/bg-p/DataCAT/)  

**Conteúdo adicional**

- [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   

- [Secundárias ativas: réplicas secundárias legíveis &#40;Grupos de Disponibilidade Always On&#41;](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   

- [Sobre o acesso de conexão de cliente a réplicas de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)   
 
- [Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativo &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)  
