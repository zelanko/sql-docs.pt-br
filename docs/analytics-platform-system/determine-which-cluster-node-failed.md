---
title: Determinar o nó de cluster com falha
description: Este artigo descreve como determinar o nome do nó do sistema de plataforma de análise (APS) que falhou depois que um failover de cluster ocorreu e um alerta de failover de cluster foi gerado. Como parte da solução de problemas de um failover de cluster, você deve determinar o nome do nó que falhou antes de entrar em contato com a Microsoft para ajudar a resolver o problema.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 68ebdb7f17ddee311644e11c48eaa4b586beac74
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401203"
---
# <a name="determine-which-cluster-node-failed-for-analytics-platform-system"></a>Determinar qual nó de cluster falhou para o Analytics Platform System
Este tópico descreve como determinar o nome do nó do sistema de plataforma de análise (APS) que falhou depois que um failover de cluster ocorreu e um alerta de failover de cluster foi gerado. Como parte da solução de problemas de um failover de cluster, você deve determinar o nome do nó que falhou antes de entrar em contato com a Microsoft para ajudar a resolver o problema.  
  
## <a name="background"></a><a name="Background"></a>Tela de fundo  
Para alta disponibilidade no SQL Server PDW, o nó de controle e os nós de computação são configurados como componentes ativos ou passivos de clusters de failover do Windows. Quando um servidor ativo falha ao responder a solicitações críticas do sistema, o servidor passivo faz failover e executa as funções do servidor que falharam.  
  
Após um failover de cluster, quando SQL Server PDW relatórios sobre o status do nó, o servidor passivo tem um status de failover. No entanto, não é óbvio qual servidor ou nó falhou, especialmente se o servidor que falhou ainda estiver online. Para solucionar problemas de falha do cluster, você deve determinar o nome do nó que passou por failover.  
  
## <a name="admin-console-solution"></a><a name="AdminConsoleSolution"></a>Solução do console de administração  
  
#### <a name="to-find-the-name-of-the-node-that-failed"></a>Para localizar o nome do nó que falhou  
  
1.  Abra o console do administrador do. Para obter mais informações sobre o console de administração, consulte [monitorar o dispositivo usando o console de administração &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md). Após o failover ocorrer, o evento de failover é incluído no número de alertas na página de **integridade** . Há uma página de **integridade** para a região do PDW e para a região de malha do dispositivo. Cada página de integridade tem uma guia **alertas** . Para saber mais sobre um alerta, clique na página integridade, na guia Alertas e em um alerta.  
  
## <a name="system-view-solution"></a><a name="SystemView"></a>Solução de exibição do sistema  
A instrução SQL a seguir mostra como usar a exibição do sistema [Sys. dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md) para localizar o nome do servidor que falhou.  
  
```sql  
SELECT  
SUBSTRING( component_instance_id, 2, charindex(' ', component_instance_id, 1)-2) AS failed_node_name,  
create_time AS failover_time  
FROM sys.dm_pdw_component_health_active_alerts  
WHERE alert_id = 500139  
ORDER BY failed_node_name;  
```  
  
