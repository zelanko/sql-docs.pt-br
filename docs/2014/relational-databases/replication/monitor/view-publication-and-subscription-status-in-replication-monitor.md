---
title: Exibir o status da publicação e da assinatura no Replication Monitor | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Log Reader Agent, monitoring
- Merge Agent, monitoring
- Queue Reader Agent, monitoring
- publications [SQL Server replication], viewing information
- Snapshot Agent, monitoring
- Distribution Agent, monitoring
- monitoring performance [SQL Server replication], publication status
- monitoring performance [SQL Server replication], subscription status
- subscriptions [SQL Server replication], viewing status
- Replication Monitor, publication and subscription status
ms.assetid: 16590771-9867-463e-a973-36a5c145ac16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9dad3a2c5f7073ea63608ba5234061a3ffa2102c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/25/2020
ms.locfileid: "62666916"
---
# <a name="view-publication-and-subscription-status-in-replication-monitor"></a>Exibir o status da publicação e da assinatura no Replication Monitor
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] O Replication Monitor exibe informações de status para publicações e assinaturas:  
  
-   O status de uma publicação é determinado pelo status de prioridade mais alta de suas assinaturas. Por exemplo, se uma assinatura para uma publicação tiver um erro e outra tiver um problema de desempenho, será exibido um status de erro para a publicação.  
  
-   O status de uma assinatura é determinado pelo status dos agentes que servem à assinatura. Para a replicação de mesclagem, esse é o Merge Agent. Para a replicação transacional, esse é o Log Reader Agent ou o Distribution Agent (é exibido o status com maior prioridade; o status também pode ser determinado pelo Queue Reader Agent, se forem usadas assinaturas de atualização em fila). Para replicação de instantâneo, esse é o Snapshot Agent ou o Distribution Agent (é exibido o status com maior prioridade).  
  
 As tabelas nas seções a seguir, listam os possíveis valores de status para publicações e assinaturas. Três dos valores de status só serão exibidos caso um limite seja atingido ou excedido:  
  
-   Assinatura perdendo a validade  
  
     Esse valor de status se aplica a todos os tipos de replicação. Para obter mais informações, consulte [Set Thresholds and Warnings in Replication Monitor](set-thresholds-and-warnings-in-replication-monitor.md).  
  
-   Desempenho crítico  
  
     Esse valor de status se aplica à replicação transacional e à replicação de mesclagem. Para mais informações, consulte [Monitorar o desempenho com o Replication Monitor](monitor-performance-with-replication-monitor.md).  
  
-   Mesclagem de execução longa  
  
     Esse valor de status se aplica à replicação de mesclagem. Para mais informações, consulte [Monitorar o desempenho com o Replication Monitor](monitor-performance-with-replication-monitor.md).  
  
 Além dos status da publicação e da assinatura, a replicação de mesclagem fornece estatísticas em nível de artigo, que fornecem informações detalhadas sobre: quanto tempo mais a fase de mesclagem demorará para terminar; quanto tempo foi gasto no processamento de um determinado artigo; o tipo de conexão que um Assinante está usando; e outras informações importantes. As estatísticas são exibidas na janela Merge Agent no Replication Monitor. As replicações de instantâneo e transacional fornecem informações detalhadas sobre o processamento do Distribution Agent.  
  
 **Para exibir o status da publicação e da assinatura**  
  
-   Replication Monitor: [exiba informações e execute tarefas usando o Replication Monitor](view-information-and-perform-tasks-replication-monitor.md).
  
  
## <a name="publication-status-values"></a>Valores de status da publicação  
 A tabela abaixo mostra os valores de status da publicação e seus ícones correspondentes em ordem de prioridade.  
  
|Status|ícone|  
|------------|----------|  
|Erro|![Ícone da interface do usuário: erro](../media/repl-icon-error.gif "Ícone da interface do usuário: erro")|  
|Desempenho crítico|![Ícone da interface do usuário: aviso](../media/repl-icon-warn.gif "Ícone da interface do usuário: aviso")|  
|Tentando novamente comando com falha|![Ícone de interface do usuário: repetição do agente de replicação](../media/repl-icon-retry.gif "Ícone de interface do usuário: repetição do agente de replicação")|  
|OK|none|  
  
## <a name="subscription-status-values"></a>Valores de status da assinatura  
 As tabelas abaixo mostram os valores de status da assinatura e seus ícones correspondentes em ordem de prioridade. É possível que uma assinatura possua dois estados ao mesmo tempo como **Expirando em breve/Expirado** e **Tentando novamente comando com falha**; é exibido o status com maior prioridade.  
  
 Os valores de status **Desempenho crítico**, **Expirando em breve/Expirado**e **Não inicializado** são avisos. Quando é exibido um aviso, o Replication Monitor também exibe se um agente está sendo executado. Por exemplo, o status poderia ser **Executando, Desempenho crítico**.  
  
### <a name="transactional-subscriptions"></a>Assinaturas transacionais  
  
|Status|ícone|  
|------------|----------|  
|Erro|![Ícone da interface do usuário: erro](../media/repl-icon-error.gif "Ícone da interface do usuário: erro")|  
|Desempenho crítico|![Ícone da interface do usuário: aviso](../media/repl-icon-warn.gif "Ícone da interface do usuário: aviso")|  
|Expirando em breve/Expirado|![Ícone da interface do usuário: aviso](../media/repl-icon-warn.gif "Ícone da interface do usuário: aviso")|  
|Assinatura não inicializada|![Ícone da interface do usuário: aviso](../media/repl-icon-warn.gif "Ícone da interface do usuário: aviso")|  
|Tentando novamente comando com falha|![Ícone de interface do usuário: repetição do agente de replicação](../media/repl-icon-retry.gif "Ícone de interface do usuário: repetição do agente de replicação")|  
|Não está sendo executado|![Ícone de interface do usuário: agente de replicação interrompido](../media/repl-icon-stopped.gif "Ícone de interface do usuário: agente de replicação interrompido")|  
|Executando|![Ícone de interface do usuário: agente de replicação em execução](../media/repl-icon-running.gif "Ícone de interface do usuário: agente de replicação em execução")|  
  
### <a name="merge-subscriptions"></a>Assinaturas de mesclagem  
  
|Status|ícone|  
|------------|----------|  
|Erro|![Ícone da interface do usuário: erro](../media/repl-icon-error.gif "Ícone da interface do usuário: erro")|  
|Desempenho crítico|![Ícone da interface do usuário: aviso](../media/repl-icon-warn.gif "Ícone da interface do usuário: aviso")|  
|Mesclagem de execução longa|![Ícone da interface do usuário: aviso](../media/repl-icon-warn.gif "Ícone da interface do usuário: aviso")|  
|Expirando em breve/Expirado|![Ícone da interface do usuário: aviso](../media/repl-icon-warn.gif "Ícone da interface do usuário: aviso")|  
|Assinatura não inicializada|![Ícone da interface do usuário: aviso](../media/repl-icon-warn.gif "Ícone da interface do usuário: aviso")|  
|Tentando novamente comando com falha|![Ícone de interface do usuário: repetição do agente de replicação](../media/repl-icon-retry.gif "Ícone de interface do usuário: repetição do agente de replicação")|  
|Sincronizando|![Ícone de interface do usuário: agente de replicação em execução](../media/repl-icon-running.gif "Ícone de interface do usuário: agente de replicação em execução")|  
|Não sincronizando|![Ícone de interface do usuário: agente de replicação interrompido](../media/repl-icon-stopped.gif "Ícone de interface do usuário: agente de replicação interrompido")|  
  
### <a name="snapshot-subscriptions"></a>Assinaturas de instantâneo  
  
|Status|ícone|  
|------------|----------|  
|Erro|![Ícone da interface do usuário: erro](../media/repl-icon-error.gif "Ícone da interface do usuário: erro")|  
|Expirando em breve/Expirado|![Ícone da interface do usuário: aviso](../media/repl-icon-warn.gif "Ícone da interface do usuário: aviso")|  
|Assinatura não inicializada|![Ícone da interface do usuário: aviso](../media/repl-icon-warn.gif "Ícone da interface do usuário: aviso")|  
|Tentando novamente comando com falha|![Ícone de interface do usuário: repetição do agente de replicação](../media/repl-icon-retry.gif "Ícone de interface do usuário: repetição do agente de replicação")|  
|Sincronizando|![Ícone de interface do usuário: agente de replicação em execução](../media/repl-icon-running.gif "Ícone de interface do usuário: agente de replicação em execução")|  
|Não sincronizando|![Ícone de interface do usuário: agente de replicação interrompido](../media/repl-icon-stopped.gif "Ícone de interface do usuário: agente de replicação interrompido")|  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorando a replicação](../monitoring-replication.md)  
  
  
