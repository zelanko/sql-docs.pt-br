---
title: Suporte de driver e conectividade de cliente para grupos de disponibilidade
description: 'Este tópico descreve as considerações sobre conectividade de cliente para Grupos de Disponibilidade AlwaysOn, incluindo pré-requisitos, restrições e recomendações para configurações de cliente. '
ms.custom: seodec18
ms.date: 07/28/2020
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
ms.openlocfilehash: 3fa77d1c6796220937a6966a5e4202c7f029ddd8
ms.sourcegitcommit: 6ab28d954f3a63168463321a8bc6ecced099b247
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/05/2020
ms.locfileid: "87790319"
---
# <a name="driver-and-client-connectivity-support-for-availability-groups"></a>Suporte de driver e conectividade de cliente para grupos de disponibilidade
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

  Este tópico descreve as considerações sobre conectividade de cliente para Grupos de Disponibilidade AlwaysOn, incluindo pré-requisitos, restrições e recomendações para configurações de cliente.  
  
 
##  <a name="client-connectivity-support"></a><a name="ClientConnSupport"></a> Suporte à conectividade de cliente  
 A seção abaixo oferece informações sobre o suporte ao [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] para conectividade de cliente.  
  
 **Suporte de driver**  
  
 A tabela a seguir resume o suporte ao driver para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]:  
  
|Driver|Failover de várias sub-redes|Tentativa de aplicativo|Roteamento somente leitura|Failover de várias sub-redes: failover mais rápido de ponto de extremidade de sub-rede simples|Failover de várias sub-redes: resolução de instância nomeada para instâncias clusterizadas SQL|  
|------------|----------------------------|------------------------|------------------------|--------------------------------------------------------------------|-----------------------------------------------------------------------------------|  
|SQL Native Client 11.0 ODBC|Sim|Sim|Sim|Sim|Sim|  
|SQL Native Client 11.0 OLEDB|Não|Sim|Sim|Não|Não|  
|ADO.NET com .NET Framework 4.0 com patch de conectividade*|Sim|Sim|Sim|Sim|Sim|  
|ADO.NET com .NET Framework 3.5 SP1 com patch de conectividade**|Sim|Sim|Sim|Sim|Sim|  
|[Microsoft ODBC Driver 13.1+ for SQL Server](../../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)|Sim|Sim|Sim|Sim|Sim|
|[Microsoft JDBC Driver 4.0+ para SQL Server](../../../connect/oledb/oledb-driver-for-sql-server.md)|Sim|Sim|Sim|Sim|Sim| 
|[Driver do Microsoft OLE DB para SQL Server](../../../connect/jdbc/microsoft-jdbc-driver-for-sql-server.md)|Sim|Sim|Sim|Sim|Sim| 
  
 *Baixe o patch de conectividade para ADO .NET com o .NET Framework 4.0: [https://support.microsoft.com/kb/2600211](https://support.microsoft.com/kb/2600211).  
  
 **Baixe o patch de conectividade para ADO.NET com o .NET Framework 3.5 SP1: [https://support.microsoft.com/kb/2654347](https://support.microsoft.com/kb/2654347).  
 
 \* Baixe o novo Microsoft OLE DB Driver para SQL Server: [https://aka.ms/downloadmsoledbsql](https://aka.ms/downloadmsoledbsql).  

> [!IMPORTANT]  
>  Para se conectar a um ouvinte de grupo de disponibilidade, um cliente deve usar uma cadeia de conexão TCP.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Criação e configuração de grupos de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)  
  
-   [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Clustering de failover e Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)   
 [Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativo &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)   
 [Sobre o acesso de conexão de cliente a réplicas de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)   
 [Guia de soluções do Microsoft SQL Server AlwaysOn para alta disponibilidade e recuperação de desastre](https://go.microsoft.com/fwlink/?LinkId=227600)   
 [Blog da equipe do Always On do SQL Server: o blog oficial da equipe do Always On do SQL Server](https://blogs.msdn.microsoft.com/sqlalwayson/)   
 [Ocorre um atraso muito longo ao reconectar uma conexão IPsec de um computador que executa o Windows Server 2003, Windows Vista, Windows Server 2008, Windows 7 ou Windows Server 2008 R2](https://support.microsoft.com/kb/980915)   
 [O serviço de Cluster leva aproximadamente 30 segundos para fazer failover de endereços IP IPv6 no Windows Server 2008 R2](https://support.microsoft.com/kb/2578113)   
 [Operação de failover lenta se não existir nenhum roteador entre o cluster e um servidor de aplicativos](https://support.microsoft.com/kb/2582281)  
  
  
