---
title: Conectividade de cliente AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: d8a1b81d60ef691e02d4b69cc71fa961bbaddf18
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67793429"
---
# <a name="always-on-client-connectivity-sql-server"></a>Conectividade de cliente AlwaysOn (SQL Server)
  Este tópico descreve considerações sobre conectividade de clientes para Grupos de Disponibilidade AlwaysOn, inclusive pré-requisitos, restrições e recomendações para configurações e parâmetros de clientes.  
  
 
  
##  <a name="client-connectivity-support"></a><a name="ClientConnSupport"></a>Suporte à conectividade do cliente  
 A seção abaixo oferece informações sobre o suporte ao [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] para conectividade de cliente.  
  
 **Suporte de driver**  
  
 A tabela a seguir resume o suporte ao driver para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]:  
  
|Driver|Failover de várias sub-redes|Tentativa de aplicativo|Roteamento somente leitura|Failover de várias sub-redes: failover mais rápido de ponto de extremidade de sub-rede simples|Failover de várias sub-redes: resolução de instância nomeada para instâncias clusterizadas SQL|  
|------------|----------------------------|------------------------|------------------------|--------------------------------------------------------------------|-----------------------------------------------------------------------------------|  
|SQL Native Client 11.0 ODBC|Sim|Sim|Sim|Sim|Sim|  
|SQL Native Client 11.0 OLEDB|Não|Sim|Sim|Não|Não|  
|ADO.NET com o patch de conectividade do .NET Framework 4,0**<sup>*</sup>** |Sim|Sim|Sim|Sim|Sim|  
|ADO.NET com o .NET Framework 3,5 SP1 com patch de conectividade**<sup>**</sup>** |Sim|Sim|Sim|Sim|Sim|  
|Microsoft JDBC driver 4.0 para SQL Server|Sim|Sim|Sim|Sim|Sim|  
  
 **<sup>*</sup>** Baixe o patch de conectividade para ADO .NET com .NET Framework 4,0 [https://support.microsoft.com/kb/2600211](https://support.microsoft.com/kb/2600211):.  
  
 **<sup>**</sup>* * Baixe o patch de conectividade para ADO.NET com o .NET Framework 3,5 [https://support.microsoft.com/kb/2654347](https://support.microsoft.com/kb/2654347)SP1:.  
  
> [!IMPORTANT]  
>  Para se conectar a um ouvinte de grupo de disponibilidade, um cliente deve usar uma cadeia de conexão TCP.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Criação e configuração de grupos de disponibilidade &#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)  
  
-   [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  

  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Clustering de failover e Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [Pré-requisitos, restrições e recomendações para Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [Ouvintes de grupo de disponibilidade, conectividade de cliente e failover de aplicativo &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [Sobre o acesso de conexão de cliente a réplicas de disponibilidade &#40;SQL Server&#41;](about-client-connection-access-to-availability-replicas-sql-server.md)   
 [Guia de soluções do Microsoft SQL Server AlwaysOn para alta disponibilidade e recuperação de desastres](https://go.microsoft.com/fwlink/?LinkId=227600)   
 [Blog da equipe do SQL Server AlwaysOn: o blog oficial da equipe do SQL Server AlwaysOn](https://blogs.msdn.com/b/sqlalwayson/)   
 [Um atraso de tempo longo ocorre quando você reconecta uma conexão IPSec de um computador que está executando o Windows Server 2003, Windows Vista, Windows Server 2008, Windows 7 ou Windows Server 2008 R2](https://support.microsoft.com/kb/980915)   
 [O Serviço de cluster leva cerca de 30 segundos para fazer failover de endereços IP IPv6 no Windows Server 2008 R2](https://support.microsoft.com/kb/2578113)   
 [Operação de failover lenta se não existir nenhum roteador entre o cluster e um servidor de aplicativos](https://support.microsoft.com/kb/2582281)  
  
  
