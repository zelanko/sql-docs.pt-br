---
title: Controlar os alertas do dispositivo - Analytics Platform System | Microsoft Docs
description: Controlar os alertas de dispositivo no sistema de plataforma de análise.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 82803e6f20e4a710f317e2e7a541c4a1c72ed08d
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
ms.locfileid: "31539266"
---
# <a name="track-appliance-alerts-in-analytics-platform-system"></a>Controlar os alertas do dispositivo no Analytics Platform System
Este tópico explica como usar o Console de administração e as exibições do sistema para rastrear alertas em um dispositivo de PDW do SQL Server.  
  
## <a name="to-track-appliance-alerts"></a>Para controlar o dispositivo de alertas  
SQL Server PDW cria alertas para problemas de hardware e software que precisam de atenção. Cada alerta contém um título e uma descrição do problema.  
  
SQL Server PDW logs e alertas [sys.dm_pdw_component_health_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-alerts-transact-sql.md) DMV. O sistema mantém um limite de 10.000 alertas e exclui o alerta mais antigo primeiro quando o limite for excedido.  
  
### <a name="view-alerts-by-using-the-admin-console"></a>Exibir alertas usando o Console de administração  
Há um **alertas** guia para a região PDW, região HDI e para a região de malha do dispositivo. Após o failover, o evento de failover está incluído no número de alertas na página. Há uma página para a região PDW, região HDI e para a região de malha do dispositivo. Cada página de integridade tem uma guia. Para saber mais sobre um alerta, clique o **integridade** página, o **alertas** guia e, em seguida, clique em um alerta.  
  
![PDW Admin Console Alerts](./media/track-appliance-alerts/SQL_Server_PDW_AdminConsole_AlertsV2.png "SQL_Server_PDW_AdminConsole_AlertsV2")  
  
Sobre o **alertas** página:  
  
-   Para exibir o histórico do alerta, clique no **histórico de alertas de revisão** link.  
  
-   Para exibir o componente de alerta e seus valores de propriedade atual, clique na linha de alerta.  
  
-   Para exibir detalhes sobre o nó que gerou o alerta, clique no nome do nó.  
  
### <a name="view-alerts-by-using-the-system-views"></a>Exibir alertas usando as exibições do sistema  
Para exibir alertas usando exibições do sistema, consulte [sys.dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md). Essa DMV mostra alertas que não foram corrigidos. Para obter ajuda com erros e separação de alertas, use o [sys.dm_pdw_errors](../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md) DMV.  
  
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
  
## <a name="see-also"></a>Consulte também  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->
[Monitoramento de dispositivo &#40;Analytics Platform System&#41;](appliance-monitoring.md)  
  
