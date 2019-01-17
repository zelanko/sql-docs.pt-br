---
title: Combinar o clustering de failover com grupos de disponibilidade
description: Aprimore sua alta disponibilidade e capacidade de recuperação de desastre combinando os recursos de uma instância de cluster de failover do SQL Server e um grupo de disponibilidade Always On.
ms.custom: seodec18
ms.date: 07/02/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- clustering [SQL Server]
- Availability Groups [SQL Server], WSFC clusters
- Failover Cluster Instances [SQL Server], see failover clustering [SQL Server]
- quorum [SQL Server]
- failover clustering [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], Failover Cluster Instances
ms.assetid: 613bfbf1-9958-477b-a6be-c6d4f18785c3
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 0db7b259158d9d7404230405c3e72bf78e93b822
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53213035"
---
# <a name="failover-clustering-and-always-on-availability-groups-sql-server"></a>Clustering de failover e Grupos de Disponibilidade AlwaysOn (SQL Server)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

   O [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], a solução de alta disponibilidade e recuperação de desastre incorporada no [!INCLUDE[sssql11](../../../includes/sssql11-md.md)], requer o WSFC (Windows Server Failover Clustering). Além disso, embora o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] não seja dependente do clustering de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , você pode usar uma FCI (instância de clustering de failover) para hospedar uma réplica de disponibilidade para um grupo de disponibilidade. É importante saber a função de cada tecnologia de clustering e quais considerações precisam ser observadas ao criar o ambiente do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] .  
  
> [!NOTE]  
>  Para obter informações sobre os conceitos do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] , confira [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).  
  
  
##  <a name="WSFC"></a> Windows Server Failover Clustering e grupos de disponibilidade  
 A implantação do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] exige um cluster do WSFC (Windows Server Failover Clustering). Para ser habilitado para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve residir em um nó WSFC, e o nó e o cluster WSFC devem estar online. Além do mais, cada réplica de disponibilidade de um determinado grupo de disponibilidade deve residir em um nó diferente do mesmo cluster do WSFC. A única exceção é que, embora tenha sido migrado para outro cluster WSFC, um grupo de disponibilidade pode temporariamente abranger dois clusters.  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] conta com o cluster WSFC (Windows Failover Clustering) para monitorar e gerenciar as funções atuais das réplicas de disponibilidade que pertencem a determinado grupo de disponibilidade e especificar como um evento de failover afeta as réplicas de disponibilidade. Um grupo de recursos do WSFC é criado para cada grupo de disponibilidade que você cria. O cluster WSFC monitora este grupo de recursos para avaliar a integridade da réplica primária.  
  
 O quorum para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] é baseado em todos os nós no cluster WSFC independentemente de se um determinado nó de cluster hospeda qualquer réplica de disponibilidade. Ao contrário do espelhamento do banco de dados, não há nenhuma função de testemunha no [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)].  
  
 A integridade geral de um cluster WSFC é determinada pelos votos do quorum de nós no cluster. Se o cluster WSFC for colocado offline devido a um desastre não planejado ou devido a um hardware ou uma falha de comunicação persistente, será necessária intervenção administrativa manual. Um administrador do Windows Server ou do cluster WSFC precisará forçar um quorum e colocar os nós de cluster de sobrevivência novamente online em uma configuração não tolerante a falhas.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] são subchaves do cluster WSFC. Se você excluir e recriar um cluster WSFC, deverá desabilitar e reabilitar o recurso [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] em cada instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospedava uma réplica de disponibilidade no cluster WSFC original.  
  
 Para obter informações sobre como executar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em nós de cluster WSFC (Clustering de Failover do Windows Server) e sobre o quorum do WSFC, veja [Clustering de Failover do Windows Server &#40;WSFC&#41; com SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md).  
  
##  <a name="SQLServerFC"></a> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCIs (Instâncias de Cluster de Failover) e grupos de disponibilidade  
 Você pode configurar uma segunda camada de failover no nível da instância do servidor implementando o clustering de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] junto com o cluster WSFC. Uma réplica de disponibilidade pode ser hospedada por ou uma instância autônoma do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou uma instância FCI. Somente um parceiro FCI pode hospedar uma réplica para um determinado grupo de disponibilidade. Quando uma réplica de disponibilidade estiver sendo executada em um FCI, a lista de proprietários possíveis para o grupo de disponibilidade conterá apenas o nó de FCI ativo.  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] não depende de nenhuma forma de armazenamento compartilhado. No entanto, se você usar uma FCI (instância de cluster de failover) do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para hospedar uma ou mais réplicas de disponibilidade, cada uma dessas FCIs exigirá armazenamento compartilhado para cada instalação de instância de cluster de failover padrão do SQL Server.  
  
 Para obter mais informações sobre os pré-requisitos adicionais, veja a seção “Pré-requisitos e restrições do uso de uma FCI (Instância de Cluster de Failover) do SQL Server para hospedar uma réplica de disponibilidade” de [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
### <a name="comparison-of-failover-cluster-instances-and-availability-groups"></a>Comparação de instâncias de cluster de failover e grupos de disponibilidade  
 Independentemente do número de nós na FCI, uma FCI inteira hospeda uma única réplica dentro de um grupo de disponibilidade. A tabela a seguir descreve as distinções em conceitos entre nós em uma FCI e réplicas dentro de um grupo de disponibilidade.  
  
||Nós dentro de uma FCI|Réplicas dentro de um grupo de disponibilidade|  
|-|-------------------------|-------------------------------------------|  
|**Usa cluster WSFC**|Sim|Sim|  
|**Nível de proteção**|Instância|banco de dados|  
|**Tipo de armazenamento**|Compartilhado|Não compartilhado<br /><br /> Embora as réplicas de um grupo de disponibilidade não compartilhem armazenamento, uma réplica hospedada por uma FCI usa uma solução de armazenamento compartilhado conforme exigido por essa FCI. A solução de armazenamento é compartilhada somente pelos nós dentro da FCI e não entre as réplicas do grupo de disponibilidade.|  
|**Soluções de armazenamento**|Conexão direta, rede SAN, pontos de montagem, SMB|Depende do tipo de nó|  
|**Secundários legíveis**|Não*|Sim|  
|**Configurações de política de failover aplicáveis**|Quorum WSFC<br /><br /> Específica da FCI<br /><br /> Configurações de grupo de disponibilidade**|Quorum WSFC<br /><br /> Configurações de grupo de disponibilidade|  
|**Recursos que recebem failover**|Servidor, instância e banco de dados|Somente banco de dados|  
  
 *Enquanto as réplicas secundárias síncronas em um grupo de disponibilidade sempre estão em execução em suas respectivas instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , os nós secundários em uma FCI não iniciaram suas respectivas instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de fato e, portanto, não são legíveis. Em uma FCI, um nó secundário inicia sua instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] somente quando a propriedade do grupo de recursos é transferida a ele durante um failover de FCI. No entanto, no nó FCI ativo, quando um banco de dados hospedado por FCI pertence a um grupo de disponibilidade, se a réplica de disponibilidade local estiver em execução como réplica secundária legível, o banco de dados será legível.  
  
 **As configurações de política de failover do grupo de disponibilidade se aplicam a todas as réplicas, sejam elas armazenadas em uma instância autônoma ou em uma instância FCI.  
  
> [!NOTE]  
>  Para obter mais informações sobre o **Número de nós** no Clustering de Failover e nos **Grupos de Disponibilidade Always On** para edições diferentes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473) (https://go.microsoft.com/fwlink/?linkid=232473)).  
  
### <a name="considerations-for-hosting-an-availability-replica-on-an-fci"></a>Considerações para hospedar uma réplica de disponibilidade em uma FCI  
  
> [!IMPORTANT]  
>  Se você planeja hospedar uma réplica de disponibilidade em uma FCI (Instância de Cluster de Failover) do SQL Server, é preciso garantir que os nós host do Windows Server 2008 atendem aos pré-requisitos e às restrições do AlwaysOn para FCIs (Instâncias de Cluster de Failover). Para obter mais informações, veja [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] As FCIs (Instâncias de Cluster de Failover) não dão suporte ao failover automático por grupos de disponibilidade, de modo que qualquer réplica de disponibilidade que esteja hospedado por um FCI só pode ser configurada para failover manual.  
  
 Talvez seja necessário configurar um cluster WSFC (Windows Server Failover Clustering) para incluir discos compartilhados que não estão disponíveis em todos os nós. Por exemplo, considere um cluster WSFC em dois centros de dados com três nós. Dois dos nós hospedam uma FCI (instância de clustering de failover) do SQL Server no data center primário e têm acesso aos mesmos discos compartilhados. O terceiro nó hospeda uma instância autônoma do SQL Server em um data center diferente e não tem acesso aos discos compartilhados do data center primário. Essa configuração de cluster WSFC oferece suporte à implantação de um grupo de disponibilidade se a FCI hospeda a réplica primária e a instância autônoma hospeda a réplica secundária.  
  
 Quando for escolher uma FCI para hospedar uma réplica de disponibilidade para determinado grupo de disponibilidade, assegure-se de que um failover da FCI não tenha a possibilidade de fazer com que um nó WSFC tente hospedar duas réplicas de disponibilidade para o mesmo grupo de disponibilidade.  
  
 O exemplo de cenário a seguir ilustra como esta configuração pode resultar em problemas:  
  
 Marcel configura um cluster WSFC com dois nós, `NODE01` e `NODE02`. Ele instala uma instância de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , `fciInstance1`, em `NODE01` e `NODE02` onde `NODE01` é o proprietário atual de `fciInstance1`.  
 Em `NODE02`, Marcel instala outra instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], `Instance3`, que é uma instância autônoma.  
 Em `NODE01`, Marcel habilita a fciInstance1 para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Em `NODE02`, ele habilita a `Instance3` para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Depois, ele configura um grupo de disponibilidade para qual a `fciInstance1` hospeda a réplica primária e `Instance3` hospeda a réplica secundária.  
 Em determinado momento, a `fciInstance1` torna-se disponível em `NODE01`e o cluster WSFC provoca o failover da `fciInstance1` em `NODE02`. Após o failover, `fciInstance1` torna-se uma instância habilitada para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]executada sob a função primária em `NODE02`. No entanto, agora a `Instance3` reside no mesmo nó WSFC da `fciInstance1`. Isso violará a restrição do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] .  
 Para resolver o problema apresentado por este cenário, a instância autônoma, `Instance3`, deve residir em outro nó no mesmo cluster WSFC de `NODE01` e `NODE02`.  
  
 Para obter mais informações sobre [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , veja [Instâncias do cluster de failover do AlwaysOn &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).  
  
##  <a name="FCMrestrictions"></a> Restrições em relação ao uso do Gerenciador de Cluster de Failover do WSFC com grupos de disponibilidade  
 Não use o Gerenciador de Cluster de Failover para manipular grupos de disponibilidade, por exemplo:  
  
-   Não adicione nem remova recursos no serviço clusterizado (grupo de recursos) para o grupo de disponibilidade.  
  
-   Não altere nenhuma propriedade do grupo de disponibilidade, como os proprietários possíveis e os proprietários preferenciais. Essas propriedades são definidas automaticamente pelo grupo de disponibilidade.  
  
-   **Não use o Gerenciador de Cluster de Failover para mover grupos de disponibilidade para nós diferentes ou para fazer o failover de grupos de disponibilidade.** O Gerenciador de Cluster de Failover não reconhece o status da sincronização das réplicas de disponibilidade, e isso pode resultar em um longo tempo de inatividade. Você deve usar [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  

  >[!WARNING]
  > Usando o Gerenciador de Cluster de Failover para mover uma *instância de cluster de failover* que hospeda um grupo de disponibilidade para um nó que *já* está hospedando uma réplica do mesmo grupo de disponibilidade pode resultar na perda da réplica do grupo de disponibilidade, impedindo que ele seja colocado online no nó de destino. Um único nó de um cluster de failover não pode hospedar mais de uma réplica do mesmo grupo de disponibilidade. Para obter mais informações sobre como isso ocorre e como recuperar, consulte o blog [Replica unexpectedly dropped in availability group](https://blogs.msdn.microsoft.com/alwaysonpro/2014/02/03/issue-replica-unexpectedly-dropped-in-availability-group/) (Réplica removida inesperadamente no grupo de disponibilidade). 
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
  
-   **Blogs:**  
  
     [Configurar o Windows Failover Clustering para SQL Server (grupo de disponibilidade ou FCI) com segurança limitada](https://blogs.msdn.microsoft.com/sqlalwayson/2012/06/05/configure-windows-failover-clustering-for-sql-server-availability-group-or-fci-with-limited-security/)  
  
     [Blogs da equipe do Always On do SQL Server: o blog oficial da equipe do Always On do SQL Server](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [Blogs dos engenheiros do CSS SQL Server](https://blogs.msdn.com/b/psssql/)  
  
-   **Whitepapers:**  
  
     [Always On Architecture Guide: Building a High Availability and Disaster Recovery Solution by Using Failover Cluster Instances and Availability Groups](https://msdn.microsoft.com/library/jj215886.aspx) (Guia de arquitetura do Always On: criando uma solução de alta disponibilidade e de recuperação de desastre usando instâncias de cluster de failover e grupos de disponibilidade)  
  
     [Guia de soluções AlwaysOn do Microsoft SQL Server para alta disponibilidade e recuperação de desastre](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [White papers da Microsoft para SQL Server 2012](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [White papers da equipe de consultoria do cliente do SQL Server](https://sqlcat.com/)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Habilitar e desabilitar Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)   
 [Monitorar grupos de disponibilidade &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Instâncias do cluster de failover do AlwaysOn &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)  
  
  
