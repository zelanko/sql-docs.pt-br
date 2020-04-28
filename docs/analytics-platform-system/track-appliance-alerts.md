---
title: Controlar os alertas do dispositivo
description: Acompanhe alertas de dispositivo no Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 03568666367bf6273f197994f572bbbbd62bb42e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74399941"
---
# <a name="track-appliance-alerts-in-analytics-platform-system"></a>Rastrear alertas do dispositivo no Analytics Platform System
Este tópico explica como usar o console de administração e exibições do sistema para rastrear alertas em um dispositivo SQL Server PDW.  
  
## <a name="to-track-appliance-alerts"></a>Para acompanhar os alertas do dispositivo  
SQL Server PDW cria alertas para problemas de hardware e software que precisam de atenção. Cada alerta contém um título e uma descrição do problema.  
  
SQL Server PDW registra alertas na DMV [Sys. dm_pdw_component_health_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-alerts-transact-sql.md) . O sistema retém um limite de 10.000 alertas e exclui o alerta mais antigo primeiro quando o limite é excedido.  
  
### <a name="view-alerts-by-using-the-admin-console"></a>Exibir alertas usando o console de administração  
Há uma guia **alertas** para a região do PDW e para a região de malha do dispositivo. Após a ocorrência do failover, o evento de failover é incluído no número de alertas na página. Há uma página para a região do PDW e para a região de malha do dispositivo. Cada página de integridade tem uma guia. Para saber mais sobre um alerta, clique na página **integridade** , na guia **alertas** e em um alerta.  
  
![Alertas do Console de Admin do PDW](./media/track-appliance-alerts/SQL_Server_PDW_AdminConsole_AlertsV2.png "SQL_Server_PDW_AdminConsole_AlertsV2")  
  
Na página **alertas** :  
  
-   Para exibir o histórico de alertas, clique no link **examinar histórico de alertas** .  
  
-   Para exibir o componente de alerta e seus valores de propriedade atuais, clique na linha de alerta.  
  
-   Para exibir detalhes sobre o nó que disparou o alerta, clique no nome do nó.  
  
### <a name="view-alerts-by-using-the-system-views"></a>Exibir alertas usando as exibições do sistema  
Para exibir alertas usando exibições do sistema, consulte [Sys. dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md). Essa DMV mostra alertas que não foram corrigidos. Para obter ajuda com os alertas e erros de triagem, use o DMV [Sys. dm_pdw_errors](../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md) .  
  
O exemplo a seguir é uma consulta comum para exibir os alertas atuais.  
  
```sql  
SELECT   
    aa.[pdw_node_id],  
    n.[name] AS [node_name],  
    g.[group_name] ,  
    c.[component_name] ,  
    aa.[component_instance_id] ,   
    a.[alert_name] ,  
    a.[state] ,  
    a.[severity] ,  
    aa.[current_value] ,  
    aa.[previous_value] ,  
    aa.[create_time] ,  
    a.[description]   
FROM [sys].[dm_pdw_component_health_active_alerts] AS aa  
    INNER JOIN sys.dm_pdw_nodes AS n   
        ON aa.[pdw_node_id] = n.[pdw_node_id]  
    INNER JOIN [sys].[pdw_health_components] AS c   
        ON aa.[component_id] = c.[component_id]  
    INNER JOIN [sys].[pdw_health_component_groups] AS g   
        ON c.[group_id] = g.[group_id]  
    INNER JOIN [sys].[pdw_health_alerts] AS a   
        ON aa.[alert_id] = a.[alert_id] and aa.[component_id] = c.[component_id]  
ORDER BY  
    a.alert_id ,  
    aa.[pdw_node_id];  
```  
  
## <a name="see-also"></a>Consulte Também  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->
[Monitoramento de dispositivo &#40;o sistema de plataforma de análise&#41;](appliance-monitoring.md)  
  
