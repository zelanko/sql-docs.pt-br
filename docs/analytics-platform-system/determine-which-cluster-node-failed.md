---
title: "Determinar qual nó de Cluster falhou (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1e001117-a1b6-4357-bf25-e85aba3f1cf0
caps.latest.revision: "21"
ms.openlocfilehash: 14b68f56a89d5fec57ede1a49be4dedc435353b5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="determine-which-cluster-node-failed"></a>Determinar qual nó de Cluster falhou
Este tópico descreve como determinar o nome do nó do SQL Server PDW que apresentou falha após um failover de cluster ocorreu e um alerta de failover de cluster foi ativado. Como parte de um cluster de failover de solução de problemas, você deve determinar o nome do nó com falha antes de entrar em contato com a Microsoft para ajudar a resolver o problema.  
  
## <a name="Background"></a>Plano de fundo  
Para alta disponibilidade no SQL Server PDW, o nó de controle e os nós de computação são configurados como ativos ou passivos componentes de clusters de failover do Windows. Quando um servidor ativo não responder a solicitações de sistema críticos, o servidor passivo failover e executa as funções de servidor que falhou.  
  
Após um failover de cluster, quando o SQL Server PDW relata status de nó, o servidor passivo tem uma falha sobre status. No entanto, não é óbvio qual servidor ou nó falha, especialmente se o servidor que não ainda estiver online. Para solucionar a falha do cluster, você deve determinar o nome do nó que falhou.  
  
## <a name="AdminConsoleSolution"></a>Solução do Console de administração  
  
#### <a name="to-find-the-name-of-the-node-that-failed"></a>Para localizar o nome do nó com falha  
  
1.  Abra o Console do administrador. Para obter mais informações sobre o Console de administração, consulte [monitorar o dispositivo usando o Console de administração &#40; Analytics Platform System &#41; ](monitor-the-appliance-by-using-the-admin-console.md). Após o failover, o evento de failover está incluído no número de alertas sobre o **integridade** página. Há um **integridade** página para a região PDW, região HDI e para a região de malha do dispositivo. Cada página de integridade tem um **alertas** guia. Para saber mais sobre um alerta, clique na página de integridade, a guia alertas e, em seguida, clique em um alerta.  
  
## <a name="SystemView"></a>Solução de modo de exibição do sistema  
A instrução SQL a seguir mostra como usar o [sys.dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md) exibição do sistema para localizar o nome do servidor que falhou.  
  
```sql  
SELECT  
SUBSTRING( component_instance_id, 2, charindex(' ', component_instance_id, 1)-2) AS failed_node_name,  
create_time AS failover_time  
FROM sys.dm_pdw_component_health_active_alerts  
WHERE alert_id = 500139  
ORDER BY failed_node_name;  
```  
  
