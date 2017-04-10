---
title: "Conectividade de cliente AlwaysOn (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "05/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Grupos de disponibilidade [SQL Server], ouvinte"
  - "Grupos de Disponibilidade [SQL Server], pré-requisitos e restrições"
  - "Grupos de disponibilidade [SQL Server], conectividade de cliente"
ms.assetid: b456448d-1757-48c8-8bbb-2d1c2d6d61e9
caps.latest.revision: 22
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 21
---
# Conectividade de cliente AlwaysOn (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

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
|SQL Native Client 11.0 OLEDB|Não|Sim|Sim|Não|Não|  
|ADO.NET com .NET Framework 4.0 com patch de conectividade*|Sim|Sim|Sim|Sim|Sim|  
|ADO.NET com .NET Framework 3.5 SP1 com patch de conectividade**|Sim|Sim|Sim|Sim|Sim|  
|Microsoft JDBC driver 4.0 para SQL Server|Sim|Sim|Sim|Sim|Sim|  
  
 *Baixe o patch de conectividade para ADO.NET com .NET Framework 4.0: [http://support.microsoft.com/kb/2600211](http://support.microsoft.com/kb/2600211).  
  
 **Baixe o patch de conectividade para ADO.NET com .NET Framework 3.5 SP1: [http://support.microsoft.com/kb/2654347](http://support.microsoft.com/kb/2654347).  
  
> [!IMPORTANT]  
>  Para se conectar a um ouvinte de grupo de disponibilidade, um cliente deve usar uma cadeia de conexão TCP.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Criação e configuração de grupos de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)  
  
-   [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
## Consulte também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Clustering de failover e Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs, restrictions, recommendations - always on availability.md)   
 [Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativo &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners, client connectivity, application failover.md)   
 [Sobre o acesso de conexão de cliente a réplicas de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)   
 [Guia de soluções AlwaysOn do Microsoft SQL Server para alta disponibilidade e recuperação de desastre](http://go.microsoft.com/fwlink/?LinkId=227600)   
 [Blog da equipe do AlwaysOn do SQL Server: o blog oficial da equipe do AlwaysOn do SQL Server](http://blogs.msdn.com/b/sqlAlways%20On/)   
 [Ocorre um atraso muito longo ao reconectar uma conexão IPsec de um computador que está executando o Windows Server 2003, o Windows Vista, o Windows Server 2008, Windows 7 ou o Windows Server 2008 R2](http://support.microsoft.com/kb/980915)   
 [O serviço de cluster leva aproximadamente 30 segundos para fazer failover de endereços IP IPv6 no Windows Server 2008 R2](http://support.microsoft.com/kb/2578113)   
 [Operação de failover lenta se não existir nenhum roteador entre o cluster e um servidor de aplicativos](http://support.microsoft.com/kb/2582281)  
  
  