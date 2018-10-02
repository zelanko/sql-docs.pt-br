---
title: Conectividade de cliente AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 04/26/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
- Availability Groups [SQL Server], prerequisites and restrictions
- Availability Groups [SQL Server], client connectivity
ms.assetid: b456448d-1757-48c8-8bbb-2d1c2d6d61e9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ee9f18e30c19ed1318f28bb4ae97bf137ec679c0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47753860"
---
# <a name="always-on-client-connectivity-sql-server"></a>Conectividade de cliente AlwaysOn (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve considerações sobre conectividade de clientes para Grupos de Disponibilidade AlwaysOn, incluindo pré-requisitos, restrições e recomendações para configurações e definições de clientes.  
  
 **Neste tópico:**  
  
-   [Suporte à conectividade de cliente](#ClientConnSupport)  
  
-   [Tarefas relacionadas](#RelatedTasks)  
  
##  <a name="ClientConnSupport"></a> Suporte à conectividade de cliente  
 A seção abaixo oferece informações sobre o suporte ao [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] para conectividade de cliente.  
  
 **Suporte de driver**  
  
 A tabela a seguir resume o suporte ao driver para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]:  
  
|Driver|Failover de várias sub-redes|Tentativa de aplicativo|Roteamento somente leitura|Failover de várias sub-redes: failover mais rápido de ponto de extremidade de sub-rede simples|Failover de várias sub-redes: resolução de instância nomeada para instâncias clusterizadas SQL|  
|------------|----------------------------|------------------------|------------------------|--------------------------------------------------------------------|-----------------------------------------------------------------------------------|  
|SQL Native Client 11.0 ODBC|Sim|Sim|Sim|Sim|Sim|  
|SQL Native Client 11.0 OLEDB|não|Sim|Sim|não|não|  
|ADO.NET com .NET Framework 4.0 com patch de conectividade*|Sim|Sim|Sim|Sim|Sim|  
|ADO.NET com .NET Framework 3.5 SP1 com patch de conectividade**|Sim|Sim|Sim|Sim|Sim|  
|Microsoft JDBC driver 4.0 para SQL Server|Sim|Sim|Sim|Sim|Sim| 
|Driver do Microsoft OLE DB para SQL Server|Sim|Sim|Sim|Sim|Sim| 
  
 *Baixe o patch de conectividade para ADO .NET com o .NET Framework 4.0: [http://support.microsoft.com/kb/2600211](http://support.microsoft.com/kb/2600211).  
  
 **Baixe o patch de conectividade para ADO.NET com o .NET Framework 3.5 SP1: [http://support.microsoft.com/kb/2654347](http://support.microsoft.com/kb/2654347).  
 
 * Baixe o novo Microsoft OLE DB Driver para SQL Server: [https://www.microsoft.com/en-us/download/details.aspx?id=56730 ](https://www.microsoft.com/en-us/download/details.aspx?id=56730).  

> [!IMPORTANT]  
>  Para se conectar a um ouvinte de grupo de disponibilidade, um cliente deve usar uma cadeia de conexão TCP.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Criação e configuração de grupos de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)  
  
-   [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Clustering de failover e Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)   
 [Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativo &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)   
 [Sobre o acesso de conexão de cliente a réplicas de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)   
 [Guia de soluções do Microsoft SQL Server AlwaysOn para alta disponibilidade e recuperação de desastre](http://go.microsoft.com/fwlink/?LinkId=227600)   
 [Blog da equipe do SQL Server AlwaysOn: o blog oficial da equipe do SQL Server AlwaysOn](https://blogs.msdn.microsoft.com/sqlalwayson/)   
 [Ocorre um atraso muito longo ao reconectar uma conexão IPsec de um computador que executa o Windows Server 2003, Windows Vista, Windows Server 2008, Windows 7 ou Windows Server 2008 R2](http://support.microsoft.com/kb/980915)   
 [O serviço de Cluster leva aproximadamente 30 segundos para fazer failover de endereços IP IPv6 no Windows Server 2008 R2](http://support.microsoft.com/kb/2578113)   
 [Operação de failover lenta se não existir nenhum roteador entre o cluster e um servidor de aplicativos](http://support.microsoft.com/kb/2582281)  
  
  
