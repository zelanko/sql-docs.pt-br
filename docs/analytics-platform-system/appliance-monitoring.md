---
title: Monitoramento de dispositivo
description: Este guia de monitoramento de dispositivo descreve as ferramentas e tarefas para monitorar o dispositivo de sistema de plataforma de análise.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: cec604ff1a93213fc6308455cadda90e6efa2d61
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401421"
---
# <a name="appliance-monitoring-for-analytics-platform-system"></a>Monitoramento de dispositivo para o Analytics Platform System
Este guia de monitoramento de dispositivo descreve as ferramentas e tarefas para monitorar o dispositivo de sistema de plataforma de análise.  
  
## <a name="Basics"></a>Noções básicas e ferramentas de monitoramento  
Os valores e as informações que podem ser monitorados no dispositivo SQL Server PDW são extensivos. Por exemplo, veja a seguir as tarefas de monitoramento típicas.  
  
-   Verifique se há alertas emitidos pelo SQL Server PDW.  
  
-   Monitor para hardware com falha.  
  
-   Monitorar problemas de conectividade de rede.  
  
-   Verifique se há erros retornados aos usuários durante o processamento da consulta.  
  
-   Exiba o número de sessões e consultas ativas no momento.  
  
-   Verifique o status de cargas, backups e restaurações.  
  
### <a name="appliance-monitoring-tools"></a>Ferramentas de monitoramento de dispositivo  
Há várias ferramentas disponíveis para monitorar o dispositivo.  
  
Console de administração  
SQL Server PDW tem um console de administração. Essa é uma ferramenta baseada na Web que exibe informações sobre consultas, cargas, backup e restauração, bloqueios, sessões, alertas e estado do dispositivo. O console de administração é executado no dispositivo; os usuários se conectam ao console de administração por meio do Internet Explorer. Para obter mais informações, consulte:  
  
-   [Monitore o dispositivo usando o console de administração &#40;o sistema de plataforma de análise&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
![Alertas do Console de Admin do PDW](./media/appliance-monitoring/SQL_Server_PDW_AdminConsol_Queries.png "SQL_Server_PDW_AdminConsol_Queries")  
  
Exibições do sistema  
O SQL Server PDW inclui exibições de sistema abrangentes que permitem que você obtenha informações detalhadas sobre a integridade, o estado e o desempenho do dispositivo. Para obter uma lista de exibições do sistema para tarefas de monitoramento, consulte:  
  
-   [Monitore o dispositivo usando as exibições do sistema &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-views.md)  
  
System Center Operations Manager (SCOM)  
SQL Server PDW tem ampla integração com o Operations Manager do Systems Center. Os pacotes de gerenciamento para SQL Server PDW estão disponíveis como um download gratuito. Para obter mais informações sobre como usar o System Center para monitorar SQL Server PDW, consulte o seguinte:  
  
-   [Monitore o dispositivo usando System Center Operations Manager &#40;o sistema de plataforma de análise&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
Soluções personalizadas  
Para situações em que o System Center não está disponível com suas ferramentas de monitoramento de data center, você pode monitorar o dispositivo usando uma solução de monitoramento de terceiros. Atualmente, não há suporte para a instalação de agentes de software externos no PDW, mas a\-maioria das soluções de monitoramento oferece suporte à integração do Transact\-SQL, de modo que o administrador do sistema possa implementar consultas diretas do Transact SQL em seu dispositivo PDW.  
  
Se sua solução de monitoramento não oferecer suporte a\-consultas diretas do Transact SQL ou se você não tiver uma ferramenta de monitoramento, poderá usar scripts para executar tarefas de monitoramento, como enviar email quando ocorrer um alerta.  O TechNet wiki contém um exemplo de solução de monitoramento com script.  
  
-   [Exemplo de monitoramento do Power Shell para SQL Server PDW](https://go.microsoft.com/fwlink/?LinkId=248020)  
   
## <a name="Tasks"></a>Tarefas de monitoramento relacionadas  
  
|Tarefa de monitoramento|DESCRIÇÃO|  
|-------------------|---------------|  
|Monitore o dispositivo usando o console do administrador.|[Monitore o dispositivo usando o console de administração &#40;o sistema de plataforma de análise&#41;](monitor-the-appliance-by-using-the-admin-console.md)|  
|Monitore o dispositivo usando exibições do sistema.|[Monitore o dispositivo usando as exibições do sistema &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-views.md)|  
|Monitorar o dispositivo usando o System Center|[Monitore o dispositivo usando System Center Operations Manager &#40;o sistema de plataforma de análise&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)|  
|Monitore o estado do dispositivo.|[Monitorar o estado de integridade do dispositivo &#40;Analytics Platform System&#41;](monitor-appliance-health-state.md)|  
|Monitoramento de pulsação.|[Enviar comentários de telemetria para o Microsoft &#40;SQL Server PDW&#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md)|  
|Acompanhe os alertas do dispositivo.|[Acompanhe os alertas do dispositivo &#40;Analytics Platform System&#41;](track-appliance-alerts.md)|  
|Determine a quantidade de capacidade que está sendo usada.|[Exibir a utilização de capacidade &#40;Analytics Platform System&#41;](view-capacity-utilization.md)|  
|Determine a frequência de sondagem do dispositivo.|[Determinar a frequência de sondagem &#40;o sistema de plataforma de análise&#41;](determine-polling-frequency.md)|  
|Quando ocorrer uma falha de cluster, determine qual nó de cluster falhou.|[Determine qual nó de cluster falhou &#40;Analytics Platform System&#41;](determine-which-cluster-node-failed.md)|  


<!-- MISSING LINKS |Monitor loads.|[Monitor Loads &#40;SQL Server PDW&#41;](../sqlpdw/monitor-loads-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor backups and restores.|[Monitor Backups and Restores &#40;SQL Server PDW&#41;](../sqlpdw/monitor-backups-and-restores-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor the active queries.|[Monitoring Active Queries &#40;SQL Server PDW&#41;](../sqlpdw/monitoring-active-queries-sql-server-pdw.md)|  -->  
  
## <a name="see-also"></a>Consulte Também  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Tarefas de gerenciamento de dispositivo &#40;Analytics Platform System&#41;](appliance-management-tasks.md)  
  
