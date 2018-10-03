---
title: Configurar o roteamento somente leitura para um grupo de disponibilidade (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: cbe56ab8f9665535837a1f50147ec64222a51e58
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48049438"
---
# <a name="configure-read-only-routing-for-an-availability-group-sql-server"></a>Configurar o roteamento somente leitura para um grupo de disponibilidade (SQL Server)
  Para configurar um grupo de disponibilidade AlwaysOn para dar suporte ao roteamento somente leitura no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], você pode usar o [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou o PowerShell. *Roteamento somente leitura* refere-se à capacidade de o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] rotear solicitações de conexão somente leitura para uma [réplica secundária legível](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md) AlwaysOn disponível (ou seja, uma réplica que é configurada para permitir cargas de trabalho somente leitura ao ser executada sob a função secundária). Para dar suporte ao roteamento somente leitura, o grupo de disponibilidade deve ter um [ouvinte do grupo de disponibilidade](../../listeners-client-connectivity-application-failover.md). Clientes somente leitura devem direcionar suas solicitações de conexão para este ouvinte e as cadeias de conexão do cliente devem especificar a intenção do aplicativo como "somente leitura." Ou seja, elas devem ser *solicitações de conexão de intenção de leitura*.  
  
> [!NOTE]  
>  Para obter informações sobre como configurar uma réplica secundária legível, veja [Configurar o acesso somente leitura em uma réplica de disponibilidade &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md).  
  

  
    > [!NOTE]  
    >  Configuring read-only routing is not supported by [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  

  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
  
-   O grupo de disponibilidade deve possuir um ouvinte de grupo de disponibilidade. Para obter mais informações, consulte [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md).  
  
-   Uma ou mais réplicas de disponibilidade devem ser configuradas para aceitar somente leitura na função secundária (ou seja, para ser [réplicas secundárias legíveis](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)(AlwaysOn % 20Availability % 20Groups\). MD)). Para obter mais informações, consulte [Configurar o acesso somente leitura em uma réplica de disponibilidade &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md).  
  
-   Você deve estar conectado à instância do servidor que hospeda a réplica primária atual.  
  
###  <a name="RORReplicaProperties"></a> Quais as propriedades de réplica você precisa configurar para dar suporte a roteamento somente leitura?  
  
-   Para cada réplica secundária legível que deve dar suporte a roteamento somente leitura, você precisa especificar uma *URL de roteamento somente leitura*. Esta URL só entra em vigor quando a réplica local estiver sendo executada sob a função secundária. A URL do roteamento somente leitura deve ser especificada réplica por réplica, quando necessário. Cada URL de roteamento somente leitura é usada para solicitações de conexão de intenção de leitura para uma réplica secundária legível específica. Normalmente, toda réplica secundária legível é atribuída uma URL de roteamento somente leitura.  
  
     Para obter informações sobre como calcular a URL de roteamento somente leitura de uma réplica de disponibilidade, consulte [Calculando read_only_routing_url de AlwaysOn](http://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-alwayson.aspx).  
  
-   Para cada réplica de disponibilidade que você quer dar suporte a roteamento somente leitura quando é a réplica primária, você precisará especificar uma *lista de roteamento somente leitura*. Uma determinada lista de roteamento somente leitura só entra em vigor quando a réplica local estiver sendo executada em uma função primária. Essa lista deve ser especificada réplica por réplica, quando necessário. Normalmente, cada lista de roteamento somente leitura deveria conter todas as URLs de roteamento somente leitura, com a URL da réplica local no final da lista.  
  
    > [!NOTE]  
    >  As solicitações e conexão de intenção de leitura são roteadas para a primeira réplica secundária legível disponível na lista de roteamento somente leitura da réplica primária atual. Não há nenhum balanceamento de carga.  
  
> [!NOTE]  
>  Para obter informações sobre ouvintes do grupo de disponibilidade e mais informações sobre roteamento somente leitura, veja [Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativo &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
  
|Tarefa|Permissões|  
|----------|-----------------|  
|Para configurar réplicas ao criar um grupo de disponibilidade|Requer a associação na função de servidor fixa **sysadmin** e a permissão de servidor CREATE AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.|  
|Para modificar uma réplica de disponibilidade|Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.|  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para configurar o roteamento somente leitura**  
  
> [!NOTE]  
>  Para obter um exemplo de código, veja [Exemplo (Transact-SQL)](#TsqlExample), mais adiante nesta seção.  
  
1.  Conecte-se à instância de servidor que hospeda a réplica primária.  
  
2.  Se você estiver especificando uma réplica para um novo grupo de disponibilidade, use a instrução [CREATE AVAILABILITY GROUP](/sql/t-sql/statements/create-availability-group-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] . Se você estiver adicionando ou modificando uma réplica para um grupo de disponibilidade existente, use a instrução [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] .  
  
    -   Para configurar o roteamento somente leitura para a função secundária, na cláusula ADD REPLICA ou MODIFY REPLICA WITH, especifique a opção SECONDARY_ROLE, da seguinte forma:  
  
         SECONDARY_ROLE **(** READ_ONLY_ROUTING_URL **='** TCP **://*`system-address`*:*`port`*')**  
  
         Os parâmetros da URL de roteamento somente leitura são os seguintes:  
  
         *system-address*  
         É uma cadeia de caracteres, como um nome de sistema, um nome de domínio totalmente qualificado ou um endereço IP, que identifica de forma exclusiva o sistema do computador de destino.  
  
         *port*  
         É um número de porta que é usado pelo mecanismo de banco de dados da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
         Por exemplo:   `SECONDARY_ROLE (READ_ONLY_ROUTING_URL = N'TCP://COMPUTER01.contoso.com:1433')`  
  
         Em uma cláusula MODIFY REPLICA, o ALLOW_CONNECTIONS será opcional se a réplica já estiver configurada para permitir conexões somente leitura.  
  
         Para obter mais informações, consulte [Calculando read_only_routing_url de AlwaysOn](http://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-alwayson.aspx).  
  
    -   Para configurar o roteamento somente leitura para a função primária, na cláusula ADD REPLICA ou MODIFY REPLICA WITH, especifique a opção PRIMARY_ROLE, da seguinte forma:  
  
         PRIMARY_ROLE **(** READ_ONLY_ROUTING_LIST **= ('*`server`*'** [ **,**... *n* ] **))**  
  
         em que *server* identifica uma instância de servidor que hospeda uma réplica secundária somente leitura em um grupo de disponibilidade.  
  
         Por exemplo:   `PRIMARY_ROLE (READ_ONLY_ROUTING_LIST=('Server1','Server2'))`  
  
        > [!NOTE]  
        >  Você precisa definir a URl de roteamento somente leitura antes de configurar a lista de roteamento somente leitura.  
  
###  <a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 O exemplo a seguir modifica duas réplicas de disponibilidade de um grupo de disponibilidade existente, `AG1` para oferecer suporte ao roteamento somente leitura quando uma dessas réplicas possui a função primária no momento. Para identificar as instâncias de servidor que hospedam a réplica de disponibilidade, este exemplo especifica os nomes da instância —`COMPUTER01` e `COMPUTER02`.  
  
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
 **Para configurar o roteamento somente leitura**  
  
> [!NOTE]  
>  Para obter um exemplo de código, consulte [Exemplo (PowerShell)](#PSExample), posteriormente nesta seção.  
  
1.  Defina o valor padrão (`cd`) para a instância de servidor que hospeda a réplica primária.  
  
2.  Ao adicionar uma réplica de disponibilidade a um grupo de disponibilidade, use o cmdlet `New-SqlAvailabilityReplica`. Ao modificar uma réplica de disponibilidade existente, use o cmdlet `Set-SqlAvailabilityReplica`. Os parâmetros relevantes são os seguintes:  
  
    -   Para configurar o roteamento somente leitura para a função secundária, especifique o **ReadonlyRoutingConnectionUrl "*`url`*"** parâmetro.  
  
         em que *url* é o FQDN (nome de domínio totalmente qualificado de conectividade) e a porta a ser usada no roteamento para a réplica em conexões somente leitura. Por exemplo:  `-ReadonlyRoutingConnectionUrl "TCP://DBSERVER8.manufacturing.Adventure-Works.com:7024"`  
  
         Para obter mais informações, consulte [Calculando read_only_routing_url de AlwaysOn](http://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-alwayson.aspx).  
  
    -   Para configurar o acesso de conexão para a função primária, especifique **ReadonlyRoutingList "*`server`*"** [ **,**... *n* ], onde *server* identifica uma instância de servidor que hospeda uma réplica secundária somente leitura no grupo de disponibilidade. Por exemplo:  `-ReadOnlyRoutingList "SecondaryServer","PrimaryServer"`  
  
        > [!NOTE]  
        >  Você precisa definir a URl de roteamento somente leitura de uma réplica antes de configurar sua lista de roteamento somente leitura.  
  
    > [!NOTE]  
    >  Para exibir a sintaxe de um cmdlet, use o `Get-Help` cmdlet no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ambiente do PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Para configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../../powershell/sql-server-powershell-provider.md)  
  
-   [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)  
  
###  <a name="PSExample"></a> Exemplo (PowerShell)  
 O exemplo a seguir configura a réplica primária e uma réplica secundária em um grupo de disponibilidade para o roteamento somente leitura. Primeiro, o exemplo atribui uma URL de roteamento somente leitura a cada réplica. Em seguida, ele define a lista de roteamento somente leitura na réplica primária. As conexões com o conjunto de propriedades "ReadOnly" na cadeia de conexão serão redirecionados à réplica secundária. Se a réplica secundária não estiver legível (conforme determinado pela configuração `ConnectionModeInSecondaryRole`), a conexão será direcionada de volta para a réplica primária.  
  
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
>  Ao usar o [utilitário bcp](../../../tools/bcp-utility.md) ou [utilitário sqlcmd](../../../tools/sqlcmd-utility.md), você pode especificar acesso somente leitura a qualquer réplica secundária que está habilitado para acesso somente leitura especificando a `-K ReadOnly` alternar.  
  
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
  
 Para obter mais informações sobre a intenção do aplicativo somente leitura e o roteamento somente leitura, veja [Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativo &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md).  
  
### <a name="if-read-only-routing-is-not-working-correctly"></a>Se o roteamento somente leitura não estiver funcionando corretamente  
 Para obter informações sobre como solucionar problemas de uma configuração de roteamento somente leitura, consulte [ roteamento somente leitura não está funcionando corretamente](troubleshoot-always-on-availability-groups-configuration-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para exibir configurações do roteamento somente leitura**  
  
-   [sys.availability_read_only_routing_lists &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-availability-read-only-routing-lists-transact-sql)  
  
-   [sys.availability_replicas &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-availability-replicas-transact-sql) (coluna **read_only_routing_url**)  
  
 **Para configurar o acesso de conexão de cliente**  
  
-   [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Configurar o acesso somente leitura em uma réplica de disponibilidade &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
 **Para usar cadeias de conexão em aplicativos**  
  
-   [Suporte do SQL Server Native Client à alta disponibilidade e recuperação de desastre](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
  
-   [Usando palavras-chave da cadeia de conexão com o SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
  
-   **Blogs:**  
  
     [Calculando read_only_routing_url de AlwaysOn](http://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-alwayson.aspx)  
  
     [Blogs da equipe do AlwaysOn do SQL Server: O SQL Server AlwaysOn Team Blog oficial](http://blogs.msdn.com/b/sqlalwayson/)  
  
     [Blogs dos engenheiros do CSS SQL Server](http://blogs.msdn.com/b/psssql/)  
  
-   **White papers:**  
  
     [White papers da Microsoft para SQL Server 2012](http://msdn.microsoft.com/library/hh403491.aspx)  
  
     [White papers da equipe de consultoria do cliente do SQL Server](http://sqlcat.com/)  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Secundárias ativas: Réplicas secundárias legíveis (grupos de disponibilidade AlwaysOn)](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [Sobre o acesso de conexão de cliente a réplicas de disponibilidade &#40;SQL Server&#41;](about-client-connection-access-to-availability-replicas-sql-server.md)   
 [Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativo &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)  
  
  
