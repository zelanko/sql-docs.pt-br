---
title: Monitorar a integridade do dispositivo
description: Como monitorar o estado de um dispositivo de sistema de plataforma de análise usando o console de administração ou consultando diretamente as exibições de gerenciamento dinâmico data warehouse dinâmica.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: b99123f81fcdddd74dc72d485d97e428ca59ed84
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74400988"
---
# <a name="monitor-appliance-health-state"></a>Monitorar estado de integridade do dispositivo
Este artigo explica como monitorar o estado de um dispositivo de sistema de plataforma de análise usando o console de administração ou consultando diretamente as exibições de gerenciamento dinâmico data warehouse dinâmica. 
  
## <a name="to-monitor-the-appliance-state"></a>Para monitorar o estado do dispositivo  
Um administrador de sistema pode usar o console de administração do ou as DMVs (exibições de gerenciamento dinâmico) do SQL Server PDW para recuperar a hierarquia completa de nós, componentes e software. O diagrama a seguir fornece uma compreensão de alto nível dos componentes que SQL Server PDW monitores.  
  
![Visão geral de monitoramento](./media/monitor-appliance-health-state/SQL_Server_PDW_Monitoring_Overview.png "SQL_Server_PDW_Monitoring_Overview")  
  
### <a name="monitor-component-status-by-using-the-admin-console"></a>Monitorar o status do componente usando o console de administração  
Para recuperar o status do componente usando o console de administração:  
  
1.  Clique na guia **estado do dispositivo** .  
  
2.  Na página estado do dispositivo, clique em um nó específico para exibir os detalhes do nó.  
  
    ![Status do Console do Administrador do PDW](./media/monitor-appliance-health-state/SQL_Server_PDW_AdminConsol_State.png "SQL_Server_PDW_AdminConsol_State")  
  
### <a name="monitor-component-status-by-using-system-views"></a>Monitorar o status do componente usando exibições do sistema  
Para recuperar o status do componente usando exibições do sistema, use [Sys. dm_pdw_component_health_status](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md). Por exemplo, a consulta a seguir recupera o status de todos os componentes.  
  
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
  
Os valores possíveis retornados para a propriedade status são:  
  
-   Ok  
  
-   Não crítico  
  
-   Crítico  
  
-   Unknown  
  
-   Sem suporte  
  
-   Inacessível  
  
-   Irrecuperável  
  
Para ver todas as propriedades de todos os componentes, remova `WHERE  p.property_name = 'Status'` a cláusula.  
  
A coluna **[update_time]** mostra a última vez em que o componente foi sondado pelos agentes de integridade SQL Server PDW.  
  
> [!CAUTION]  
> Não se esqueça de investigar o problema quando um componente não tiver sido sondado por 5 minutos ou mais; pode haver um alerta que indica um problema com as pulsações de software.  
  
## <a name="see-also"></a>Consulte Também  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Monitoramento de dispositivo &#40;o sistema de plataforma de análise&#41;](appliance-monitoring.md)  
  
