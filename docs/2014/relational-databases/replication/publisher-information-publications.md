---
title: Informações sobre o publicador, publicações | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.publisherinfo.publications.f1
ms.assetid: 0b2e3d4e-03b7-4c31-8f96-48648d750010
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8614db7bd44f6ba5de8826215aed8cf123e86488
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52812168"
---
# <a name="publisher-information-publications"></a>Informações do Publicador, Publicações
  A guia **Publicações** fornece informações resumidas sobre todas as publicações no Publicador selecionado no painel esquerdo.  
  
## <a name="options"></a>Opções  
 Para alterar a forma como a grade exibe os dados, clique com o botão direito do mouse na grade e clique em uma destas opções:  
  
-   **Classificação**: Classifique uma ou mais colunas na **classificar colunas** caixa de diálogo.  
  
-   **Selecionar colunas para mostrar**: Selecione quais colunas devem ser exibidas e a ordem na qual para exibi-los de **escolher colunas** caixa de diálogo.  
  
-   **Filtro**: Filtrar linhas na grade com base em valores de colunas de **configurações de filtro** caixa de diálogo.  
  
-   **Limpar filtro**: Limpe as configurações de filtro da grade.  
  
 As configurações de filtro são específicas de cada grade. A seleção e a classificação da coluna são aplicadas a todas as grades do mesmo tipo, como a grade de publicações de cada Publicador.  
  
 **Status**  
 O estado de cada publicação que é determinado pelo status de prioridade mais alta de suas assinaturas. Por padrão, a grade que contém informações de publicação é classificada pela coluna **Status** . A lista a seguir mostra os valores de status possíveis e a ordem de classificação dos valores (por exemplo, erros são sempre mostrados na parte superior da grade):  
  
-   Erro  
  
-   Desempenho crítico  
  
-   Tentando novamente comando com falha  
  
-   OK  
  
 O valor de status **Desempenho Crítico** é relevante para assinaturas transacionais e assinaturas de mesclagem; em assinaturas transacionais, ele só poderá ser exibido se for definido um limite. Para obter informações sobre medidas de desempenho e definir limites, consulte [Monitor Performance with Replication Monitor](monitor/monitor-performance-with-replication-monitor.md) (Monitorar o desempenho com o Replication Monitor) e [Set Thresholds and Warnings in Replication Monitor](monitor/set-thresholds-and-warnings-in-replication-monitor.md) (Definir limites e avisos no Replication Monitor).  
  
 **Publicação**  
 O nome de cada publicação, no formulário *PublicationDatabaseName: PublicationName*.  
  
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
  
 Para obter mais informações sobre como as classificações de desempenho são definidas e como os limites de desempenho são configurados, consulte [Monitorar o desempenho com o Replication Monitor](monitor/monitor-performance-with-replication-monitor.md).  
  
## <a name="see-also"></a>Consulte também  
 [Iniciar o Replication Monitor](monitor/start-the-replication-monitor.md)   
 [Exibir informações e executar tarefas para um Publicador &#40;Replication Monitor&#41;](monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)   
 [Monitorando a Replicação](monitoring-replication.md)  
  
  
