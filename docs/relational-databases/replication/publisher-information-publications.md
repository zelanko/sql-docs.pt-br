---
title: "Informações sobre o publicador, publicações | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.monitor.publisherinfo.publications.f1
ms.assetid: 0b2e3d4e-03b7-4c31-8f96-48648d750010
caps.latest.revision: "27"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b003b3d18832f83fc1c57ea34c83e6da9dfab46c
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="publisher-information-publications"></a>Informações do Publicador, Publicações
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] A guia **Publicações** fornece informações resumidas sobre todas as publicações no Publicador selecionado no painel esquerdo.  
  
## <a name="options"></a>Opções  
 Para alterar a forma como a grade exibe os dados, clique com o botão direito do mouse na grade e clique em uma destas opções:  
  
-   **Classificar**: classifique uma ou mais colunas na caixa de diálogo **Classificar Colunas** .  
  
-   **Selecionar Colunas para Mostrar**: selecione quais colunas devem ser exibidas e a ordem em que devem ser exibidas, na caixa de diálogo **Selecionar Colunas** .  
  
-   **Filtrar**: filtre linhas na grade com base em valores de colunas da caixa de diálogo **Configurações de Filtro** .  
  
-   **Limpar Filtro**: limpe as configurações de filtro da grade.  
  
 As configurações de filtro são específicas de cada grade. A seleção e a classificação da coluna são aplicadas a todas as grades do mesmo tipo, como a grade de publicações de cada Publicador.  
  
 **Status**  
 O estado de cada publicação que é determinado pelo status de prioridade mais alta de suas assinaturas. Por padrão, a grade que contém informações de publicação é classificada pela coluna **Status** . A lista a seguir mostra os valores de status possíveis e a ordem de classificação dos valores (por exemplo, erros são sempre mostrados na parte superior da grade):  
  
-   Erro  
  
-   Desempenho crítico  
  
-   Tentando novamente comando com falha  
  
-   OK  
  
 O valor de status **Desempenho Crítico** é relevante para assinaturas transacionais e assinaturas de mesclagem; em assinaturas transacionais, ele só poderá ser exibido se for definido um limite. Para obter informações sobre medidas de desempenho e definir limites, consulte [Monitor Performance with Replication Monitor](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md) (Monitorar o desempenho com o Replication Monitor) e [Set Thresholds and Warnings in Replication Monitor](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md) (Definir limites e avisos no Replication Monitor).  
  
 **Publicação**  
 O nome de cada publicação, no formato *PublicationDatabaseName: PublicationName*.  
  
 **Assinaturas**  
 O número de assinaturas para cada publicação.  
  
 **Sincronizando**  
 O número de assinaturas que está sendo sincronizado no momento para cada publicação:  
  
-   Na replicação transacional, "sincronizando" significa que o Distribution Agent está sendo executado, mas os dados não estão sendo necessariamente replicados.  
  
-   Na replicação de mesclagem, "sincronizando" significa que o Merge Agent está sendo executado e que os dados estão sendo replicados no momento.  
  
-   Na replicação de instantâneo, "sincronizando" significa que o Distribution Agent está sendo executado e que os dados estão sendo replicados no momento.  
  
 **Desempenho Médio Atual** e **Pior Desempenho Atual**  
 Somente[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores. A classificação de desempenho médio e do pior desempenho atual, respectivamente, para todas as assinaturas em uma publicação. As classificações têm base nas medidas mais atuais calculadas pelo Replication Monitor e não refletem o desempenho de uma assinatura ao longo de tempo.  
  
 Para replicação transacional, o Replication Monitor exibe só um valor para publicações com limites de desempenho definidos. Se os limites de desempenho não estiverem definidos para uma publicação, essa coluna exibirá **Não Habilitado**. Para replicação de mesclagem, o Replication Monitor exibe um valor após a ocorrência de cinco sincronizações com 50 ou mais alterações cada no mesmo tipo de conexão (discada ou LAN). Se houver menos de cinco sincronizações com 50 ou mais alterações ou se a sincronização mais recente tiver menos de 50 alterações, essa coluna ficará em branco.  
  
 A classificação de desempenho é um dos seguintes valores:  
  
-   Excelente  
  
-   Bom  
  
-   Razoável  
  
-   Fraco  
  
-   Crítico  
  
 Para obter mais informações sobre como as classificações de desempenho são definidas e como os limites de desempenho são configurados, consulte [Monitorar o desempenho com o Replication Monitor](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar o Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Exibir informações e executar tarefas para um Publicador &#40;Replication Monitor&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)   
 [Monitorando a Replicação](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
