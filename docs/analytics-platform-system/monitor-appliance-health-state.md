---
title: Monitor de estado de integridade de dispositivo (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 91132e3c-3137-4670-adaa-8a7b234fb8d2
caps.latest.revision: "12"
ms.openlocfilehash: dad3355061bafcbbfa3a34b21d2043b0411129ba
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="monitor-appliance-health-state"></a>Monitor de estado de integridade de dispositivo
Este tópico explica como monitorar o estado de um dispositivo de PDW do SQL Server usando o Console de administração, ou consultar diretamente as exibições de gerenciamento dinâmico do SQL Server PDW.  
  
## <a name="to-monitor-the-appliance-state"></a>Para monitorar o estado do dispositivo  
Um administrador de sistema pode usar o Console de administração ou o SQL Server PDW exibições de gerenciamento dinâmico (DMVs) para recuperar a hierarquia completa de nós, componentes e software. O diagrama a seguir oferece uma compreensão de alto nível dos componentes que monitora o SQL Server PDW.  
  
![Visão geral do monitoramento](./media/monitor-appliance-health-state/SQL_Server_PDW_Monitoring_Overview.png "SQL_Server_PDW_Monitoring_Overview")  
  
### <a name="monitor-component-status-by-using-the-admin-console"></a>Monitorar o Status do componente usando o Console de administração  
Para recuperar o status do componente usando o Console de administração:  
  
1.  Clique no **estado do dispositivo** guia.  
  
2.  Na página de estado do aplicativo, clique em um nó específico para exibir os detalhes do nó.  
  
    ![Estado de Console de Admin do PDW](./media/monitor-appliance-health-state/SQL_Server_PDW_AdminConsol_State.png "SQL_Server_PDW_AdminConsol_State")  
  
### <a name="monitor-component-status-by-using-system-views"></a>Monitorar o Status do componente por meio de exibições do sistema  
Para recuperar o status do componente por meio de exibições do sistema, use [sys.dm_pdw_component_health_status](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md). Por exemplo, a consulta a seguir recupera o status de todos os componentes.  
  
```sql  
SELECT   
   s.[pdw_node_id],  
   n.[name] as [node_name],  
   n.[address] ,  
   g.[group_id] ,  
   g.[group_name] ,  
   c.[component_id] ,  
   c.[component_name] ,  
   s.[component_instance_id] ,   
   p.[property_name] ,  
   s.[property_value] ,  
   s.[update_time]  
FROM [sys].[dm_pdw_component_health_status] AS s  
JOIN sys.dm_pdw_nodes AS n   
   ON s.[pdw_node_id] = n.[pdw_node_id]  
JOIN [sys].[pdw_health_components] AS c   
   ON s.[component_id] = c.[component_id]  
JOIN [sys].[pdw_health_component_groups] AS g   
   ON c.[group_id] = g.[group_id]  
JOIN [sys].[pdw_health_component_properties] AS p   
   ON s.[property_id] = p.[property_id] AND s.[component_id] = p.[component_id]  
WHERE p.property_name = 'Status'  
ORDER BY  
   s.[pdw_node_id],  
   g.[group_name] ,   
   s.[component_instance_id] ,  
   c.[component_name] ,   
   p.[property_name];  
```  
  
Possíveis valores retornados para a propriedade de Status são:  
  
-   Ok  
  
-   Não crítica  
  
-   Crítico  
  
-   Unknown (desconhecido)  
  
-   Sem suporte  
  
-   Inacessível  
  
-   Irrecuperável  
  
Para ver todas as propriedades de todos os componentes, remova o `WHERE  p.property_name = 'Status'` cláusula.  
  
O **[update_time]** coluna mostra a última vez em que o componente foi sondado por agentes de integridade do SQL Server PDW.  
  
> [!CAUTION]  
> Certifique-se de investigar o problema, quando um componente não foi sondado por 5 minutos ou mais; pode haver um alerta que indica um problema com as pulsações do software.  
  
## <a name="see-also"></a>Consulte também  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Monitoramento de dispositivo &#40; Analytics Platform System &#41;](appliance-monitoring.md)  
  
