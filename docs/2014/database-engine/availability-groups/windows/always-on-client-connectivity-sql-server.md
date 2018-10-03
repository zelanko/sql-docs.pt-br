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
ms.openlocfilehash: 53f514e83e980e0a91184581d186bcb4046727c3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48192737"
---
# <a name="always-on-client-connectivity-sql-server"></a>Conectividade de cliente AlwaysOn (SQL Server)
  Este tópico descreve considerações sobre conectividade de clientes para Grupos de Disponibilidade AlwaysOn, inclusive pré-requisitos, restrições e recomendações para configurações e parâmetros de clientes.  
  
 
  
##  <a name="ClientConnSupport"></a> Suporte à conectividade de cliente  
 A seção abaixo oferece informações sobre o suporte ao [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] para conectividade de cliente.  
  
 **Suporte de driver**  
  
 A tabela a seguir resume o suporte ao driver para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]:  
  
|Driver|Failover de várias sub-redes|Tentativa de aplicativo|Roteamento somente leitura|Failover de várias sub-redes: failover mais rápido de ponto de extremidade de sub-rede simples|Failover de várias sub-redes: resolução de instância nomeada para instâncias clusterizadas SQL|  
|------------|----------------------------|------------------------|------------------------|--------------------------------------------------------------------|-----------------------------------------------------------------------------------|  
|SQL Native Client 11.0 ODBC|Sim|Sim|Sim|Sim|Sim|  
|SQL Native Client 11.0 OLEDB|não|Sim|Sim|não|não|  
|ADO.NET com .NET Framework 4.0 com patch de conectividade**<sup>*</sup>**|Sim|Sim|Sim|Sim|Sim|  
|ADO.NET com .NET Framework 3.5 SP1 com patch de conectividade **<sup>**</sup>**|Sim|Sim|Sim|Sim|Sim|  
|Microsoft JDBC driver 4.0 para SQL Server|Sim|Sim|Sim|Sim|Sim|  
  
 **<sup>*</sup>**  Baixe o patch de conectividade para ADO .NET com .NET Framework 4.0: [ http://support.microsoft.com/kb/2600211 ](http://support.microsoft.com/kb/2600211).  
  
 **<sup>**</sup>* * Baixe o patch de conectividade para ADO.NET com .NET Framework 3.5 SP1: [ http://support.microsoft.com/kb/2654347 ](http://support.microsoft.com/kb/2654347).  
  
> [!IMPORTANT]  
>  Para se conectar a um ouvinte de grupo de disponibilidade, um cliente deve usar uma cadeia de conexão TCP.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Criação e configuração de grupos de disponibilidade &#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)  
  
-   [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  

  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Clustering de failover e grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativo &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [Sobre o acesso de conexão de cliente a réplicas de disponibilidade &#40;SQL Server&#41;](about-client-connection-access-to-availability-replicas-sql-server.md)   
 [Guia de soluções do Microsoft SQL Server AlwaysOn para alta disponibilidade e recuperação de desastres](http://go.microsoft.com/fwlink/?LinkId=227600)   
 [Blog da equipe do AlwaysOn do SQL Server: O SQL Server AlwaysOn Team Blog oficial](http://blogs.msdn.com/b/sqlalwayson/)   
 [Ocorre um atraso muito longo ao reconectar uma conexão IPsec de um computador que executa o Windows Server 2003, Windows Vista, Windows Server 2008, Windows 7 ou Windows Server 2008 R2](http://support.microsoft.com/kb/980915)   
 [O serviço de Cluster leva aproximadamente 30 segundos para fazer failover de endereços IP IPv6 no Windows Server 2008 R2](http://support.microsoft.com/kb/2578113)   
 [Operação de failover lenta se não existir nenhum roteador entre o cluster e um servidor de aplicativos](http://support.microsoft.com/kb/2582281)  
  
  
