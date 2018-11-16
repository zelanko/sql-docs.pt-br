---
title: Monitoramento de dispositivo - Analytics Platform System | Microsoft Docs
description: Este guia de monitoramento do dispositivo descreve as ferramentas e tarefas para monitorar o dispositivo do Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 100a587814e62a6455d25e78a3defca973f39bf6
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51696084"
---
# <a name="appliance-monitoring-for-analytics-platform-system"></a>Monitoramento de dispositivo para o Analytics Platform System
Este guia de monitoramento do dispositivo descreve as ferramentas e tarefas para monitorar o dispositivo do Analytics Platform System.  
  
## <a name="Basics"></a>Noções básicas e ferramentas de monitoramento  
Os valores e informações que podem ser monitoradas no dispositivo de PDW do SQL Server são abrangentes. Por exemplo, a seguir é típicos de tarefas de monitoramento.  
  
-   Verifique se há qualquer alerta emitida pelo SQL Server PDW.  
  
-   Monitor de hardware com falha.  
  
-   Monitor para problemas de conectividade de rede.  
  
-   Verifique se há erros retornados aos usuários durante o processamento de consulta.  
  
-   Exiba o número de sessões atualmente ativas e consultas.  
  
-   Verifique o status de cargas, backups e restaurações.  
  
### <a name="appliance-monitoring-tools"></a>Ferramentas de monitoramento de dispositivo  
Há várias ferramentas disponíveis para monitorar o dispositivo.  
  
Console de administração  
SQL Server PDW tem um Console de administração. Isso é uma ferramenta baseada na web que exibe informações sobre consultas, carrega, backup e restauração, bloqueios, sessões, alertas e estado do dispositivo. O Console de administração é executado no dispositivo; os usuários se conectar ao Console do administrador por meio do Internet Explorer. Para obter mais informações, consulte:  
  
-   [Monitorar o dispositivo usando o Console de administração do &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
![PDW Admin Console Alerts](./media/appliance-monitoring/SQL_Server_PDW_AdminConsol_Queries.png "SQL_Server_PDW_AdminConsol_Queries")  
  
Exibições do sistema  
SQL Server PDW inclui exibições do sistema abrangentes que permitem que você obtenha informações detalhadas sobre a integridade do dispositivo, o estado e o desempenho. Para obter uma lista de exibições do sistema para tarefas de monitoramento, consulte:  
  
-   [Monitorar o dispositivo por meio de exibições do sistema &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-views.md)  
  
System Center Operations Manager (SCOM)  
SQL Server PDW tem ampla integração com o Systems Center Operations Manager. Os pacotes de gerenciamento para SQL Server PDW estão disponíveis como um download gratuito. Para obter mais informações sobre como usar o System Center para monitorar o SQL Server PDW, consulte o seguinte:  
  
-   [Monitorar o dispositivo usando o System Center Operations Manager &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
Soluções personalizadas  
Para situações quando o System Center não está disponível com o seu data center, ferramentas de monitoramento, você pode monitorar o dispositivo usando uma solução de monitoramento de terceiros. Instalação de agentes de software externo não é suportada atualmente no PDW, mas a maioria das soluções de monitoramento dão suporte a Transact\-integração do SQL, para que o administrador do sistema possa implementar Transact direto\-consultas SQL em seu PDW dispositivo.  
  
Se sua solução de monitoramento não oferece suporte direto Transact\-consultas SQL, ou você não tem uma ferramenta de monitoramento e, em seguida, você pode usar scripts para executar tarefas de monitoramento, como enviar email quando ocorrer um alerta.  Wiki do TechNet contém um exemplo de solução de monitoramento com script.  
  
-   [Exemplo de monitoramento para SQL Server PDW do Power Shell](https://go.microsoft.com/fwlink/?LinkId=248020)  
   
## <a name="Tasks"></a>Relacionados a tarefas de monitoramento  
  
|Tarefa de monitoramento|Description|  
|-------------------|---------------|  
|Monitore o dispositivo usando o Console de administração.|[Monitorar o dispositivo usando o Console de administração do &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)|  
|Monitore o dispositivo por meio de exibições do sistema.|[Monitorar o dispositivo por meio de exibições do sistema &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-views.md)|  
|Monitorar o dispositivo usando o System Center|[Monitorar o dispositivo usando o System Center Operations Manager &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)|  
|Monitore o estado do dispositivo.|[Monitor de estado de integridade de dispositivo &#40;Analytics Platform System&#41;](monitor-appliance-health-state.md)|  
|Monitoramento de pulsação.|[Enviar comentários de telemetria à Microsoft &#40;SQL Server PDW&#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md)|  
|Controlar os alertas do dispositivo.|[Controlar os alertas do dispositivo &#40;Analytics Platform System&#41;](track-appliance-alerts.md)|  
|Determine quanta capacidade está sendo usada.|[Exibir a utilização de capacidade &#40;Analytics Platform System&#41;](view-capacity-utilization.md)|  
|Determine a frequência de sondagem de dispositivo.|[Determinar a frequência de sondagem &#40;Analytics Platform System&#41;](determine-polling-frequency.md)|  
|Quando ocorre uma falha no cluster, determinar qual cluster falhado de nó.|[Determinar qual nó de Cluster não &#40;Analytics Platform System&#41;](determine-which-cluster-node-failed.md)|  


<!-- MISSING LINKS |Monitor loads.|[Monitor Loads &#40;SQL Server PDW&#41;](../sqlpdw/monitor-loads-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor backups and restores.|[Monitor Backups and Restores &#40;SQL Server PDW&#41;](../sqlpdw/monitor-backups-and-restores-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor the active queries.|[Monitoring Active Queries &#40;SQL Server PDW&#41;](../sqlpdw/monitoring-active-queries-sql-server-pdw.md)|  -->  
  
## <a name="see-also"></a>Consulte também  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Tarefas de gerenciamento de dispositivo &#40;Analytics Platform System&#41;](appliance-management-tasks.md)  
  
