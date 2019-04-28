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
ms.openlocfilehash: 1368d29801a414de866003b86c63fb4823c4a7b8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62790655"
---
# <a name="always-on-client-connectivity-sql-server"></a>Conectividade de cliente AlwaysOn (SQL Server)
  Este tópico descreve considerações sobre conectividade de clientes para Grupos de Disponibilidade AlwaysOn, inclusive pré-requisitos, restrições e recomendações para configurações e parâmetros de clientes.  
  
 
  
##  <a name="ClientConnSupport"></a> Suporte à conectividade de cliente  
 A seção abaixo oferece informações sobre o suporte ao [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] para conectividade de cliente.  
  
 **Suporte de driver**  
  
 A tabela a seguir resume o suporte ao driver para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]:  
  
|Driver|Failover de várias sub-redes|Tentativa de aplicativo|Roteamento somente leitura|Failover de várias sub-redes: Failover de ponto de extremidade de sub-rede única mais rápido|Failover de várias sub-redes: Instâncias clusterizadas de resolução de instância nomeada do SQL|  
|------------|----------------------------|------------------------|------------------------|--------------------------------------------------------------------|-----------------------------------------------------------------------------------|  
|SQL Native Client 11.0 ODBC|Sim|Sim|Sim|Sim|Sim|  
|SQL Native Client 11.0 OLEDB|Não|Sim|Sim|Não|Não|  
|ADO.NET com .NET Framework 4.0 com patch de conectividade**<sup>*</sup>**|Sim|Sim|Sim|Sim|Sim|  
|ADO.NET com .NET Framework 3.5 SP1 com patch de conectividade **<sup>**</sup>**|Sim|Sim|Sim|Sim|Sim|  
|Microsoft JDBC driver 4.0 para SQL Server|Sim|Sim|Sim|Sim|Sim|  
  
 **<sup>*</sup>**  Baixe o patch de conectividade para ADO .NET com .NET Framework 4.0: [ https://support.microsoft.com/kb/2600211 ](https://support.microsoft.com/kb/2600211).  
  
 **<sup>**</sup>* * Baixe o patch de conectividade para ADO.NET com .NET Framework 3.5 SP1: [ https://support.microsoft.com/kb/2654347 ](https://support.microsoft.com/kb/2654347).  
  
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
 [Guia de soluções do Microsoft SQL Server AlwaysOn para alta disponibilidade e recuperação de desastres](https://go.microsoft.com/fwlink/?LinkId=227600)   
 [Blog da equipe do AlwaysOn do SQL Server: O Team Blog oficial do SQL Server AlwaysOn](https://blogs.msdn.com/b/sqlalwayson/)   
 [Ocorre um atraso muito longo ao reconectar uma conexão IPsec de um computador que executa o Windows Server 2003, Windows Vista, Windows Server 2008, Windows 7 ou Windows Server 2008 R2](https://support.microsoft.com/kb/980915)   
 [O serviço de Cluster leva aproximadamente 30 segundos para fazer failover de endereços IP IPv6 no Windows Server 2008 R2](https://support.microsoft.com/kb/2578113)   
 [Operação de failover lenta se não existir nenhum roteador entre o cluster e um servidor de aplicativos](https://support.microsoft.com/kb/2582281)  
  
  
