---
title: Monitorar o desempenho com o Replication Monitor | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], Replication Monitor
- Log Reader Agent, monitoring
- Replication Monitor, performance
- Merge Agent, monitoring
- Queue Reader Agent, monitoring
- Snapshot Agent, monitoring
- Distribution Agent, monitoring
- monitoring performance [SQL Server replication]
ms.assetid: f212397d-1bfd-496b-a246-668952891d09
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: feabed59f397f2a12ca3697e5938e0540fcad228
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "76288110"
---
# <a name="monitor-performance-with-replication-monitor"></a>Monitorar o desempenho com o Replication Monitor
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  O [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Replication Monitor permite monitorar o desempenho da replicação transacional e replicação de mesclagem das seguintes formas:  
  
-   Definindo as advertências e os limites  
  
-   Exibindo as medições de desempenho  
  
-   Determinando a latência com os tokens de rastreamento (replicação transacional)  
  
-   Exibindo as estatísticas de sincronização detalhadas (replicação de mesclagem)  
  
-   Exibindo as transações e a hora de entrega (replicação transacional)  
  
## <a name="set-warnings-and-thresholds"></a>Definir avisos e limites  
 O Replication Monitor permite ativar avisos para várias condições de desempenho. Ao habilitar um aviso, você especifica um limite. Se o limite especificado for alcançado ou ultrapassado, será exibido um aviso na coluna **Status** para a assinatura e a publicação com a qual ela sincroniza (exceto se um problema com prioridade mais alta for exibido). Além de exibir de um aviso no Replication Monitor, atingir um limite também pode disparar um alerta. Você pode habilitar avisos para as seguintes condições de desempenho:  
  
-   Exceder a latência especificada (o período decorrido entre a confirmação de uma transação no Publicador e a confirmação da transação correspondente no Assinante).  
  
     Isso se aplica à replicação transacional. Se o limite especificado for atingido ou excedido, o status será exibido como **Desempenho crítico**.  
  
-   Excedendo o tempo de sincronização especificado.  
  
     Isso se aplica à replicação de mesclagem. Se o limite especificado for atingido ou excedido, o status será exibido como **Mesclagem de execução longa**. Você pode especificar limites diferentes para conexões discadas e Rede local (LAN).  
  
-   Falha no processamento do número especificado de linhas em um determinado período.  
  
     Isso se aplica à replicação de mesclagem. Se o limite especificado for atingido ou excedido, o status será exibido como **Desempenho crítico**. Você pode especificar limites diferentes para conexões discadas e LAN.  
  
 Para obter mais informações, consulte [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
## <a name="view-performance-measurements"></a>Exibir as medições de desempenho  
 O Replication Monitor exibe os valores de qualidade de desempenho para a replicação transacional e a replicação de mesclagem nas colunas **Desempenho Médio Atual** e **Pior Desempenho Atual** para publicações e na coluna **Desempenho** para assinaturas. Os valores são:  
  
-   Excelente  
  
-   Bom  
  
-   Razoável  
  
-   Fraco  
  
-   Crítico (replicação transacional somente)  
  
 Os valores são determinados das seguintes maneiras:  
  
-   Para a replicação transacional, a qualidade de desempenho é determinada pelo limite de latência. Se o limite não for definido, não será exibido um valor. A tabela a seguir mostra a correlação entre o limite e o valor de qualidade de desempenho. Por exemplo, se a latência for selecionada para 60 segundos e a latência real for de 30 segundos, a latência será 50% do limite, resultando em um valor Bom.  
  
    |Excelente|Bom|Razoável|Fraco|Crítico|  
    |---------------|----------|----------|----------|--------------|  
    |0 – 34%|35 – 59%|60 – 84%|85 – 99%|100% +|  
  
-   Para replicação de mesclagem, a qualidade do desempenho é independente (o limite de processamento da linha determina se o valor de **Performance crítica** é mostrado na coluna de **Status** ). A qualidade de desempenho é determinada comparando-se o desempenho de uma assinatura individual, do desempenho histórico médio de assinaturas, com a publicação que tem o mesmo tipo de conexão (discada ou LAN). O Replication Monitor exibe um valor após a ocorrência de cinco sincronizações com 50 ou mais alterações cada, no mesmo tipo de conexão. Se houver menos de cinco sincronizações com 50 ou mais alterações ou se a sincronização mais recente tiver menos de 50 alterações, o Replication Monitor não exibirá um valor.  
  
     A tabela seguinte mostra a correlação entre o desempenho médio e o valor de qualidade de desempenho. Por exemplo, se dez Assinantes tiverem sincronizado em uma conexão LAN com uma taxa média de 100 linhas por segundo, e uma das assinaturas sincronizar a uma taxa de 125 linhas por segundo, o desempenho da sincronização do Assinante será 125% da média, resultando em um valor Bom.  
  
    |Excelente|Bom|Razoável|Fraco|  
    |---------------|----------|----------|----------|  
    |151+%|76 – 150%|26 – 75%|0 – 25%|  
  
 Para obter mais informações sobre como exibir informações de assinatura, confira [Exibir informações e executar tarefas usando o Replication Monitor](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
## <a name="determine-latency-with-tracer-tokens"></a>Determinar a latência com os tokens de rastreamento  
 A replicação transacional permite medir a latência em um sistema inserindo um token (uma pequena quantidade de dados) no log de transações do banco de dados de publicação e registrando o tempo necessário para chegar até o Distribuidor e os Assinantes. O token permitirá também a identificação de dados que não chegam até o Distribuidor ou Assinante. Para obter mais informações, consulte [Medir a latência e validar as conexões para a replicação transacional](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md).  
  
## <a name="view-detailed-synchronization-performance-for-merge-replication"></a>Exibir o desempenho de sincronização detalhado para replicação de mesclagem  
 Para a replicação de mesclagem, o Replication Monitor exibe as estatísticas detalhadas para cada artigo processado durante a sincronização, incluindo o tempo gasto em cada fase do processamento (carregar alterações, baixar alterações e assim por diante). Ajuda a definir tabelas específicas que estão causando lentidão e é o melhor local para a solução de problemas de desempenho com assinaturas de mesclagem. Para obter mais informações sobre como exibir estatísticas detalhadas, confira [Exibir informações e executar tarefas usando o Replication Monitor](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
## <a name="view-transactions-and-delivery-time-for-transactional-replication"></a>Exibir as transações e a hora de entrega para replicação transacional  
 Para replicação transacional, o Replication Monitor exibe informações sobre o número de transações no banco de dados de distribuição que ainda não foi distribuído ao Assinante e o tempo estimado para distribuir essas transações. Para obter mais informações, confira [Exibir informações e executar tarefas usando o Replication Monitor](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorando a Replicação](../../../relational-databases/replication/monitor/monitoring-replication.md)   
 [Definir limites e avisos no Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)  
  
  
