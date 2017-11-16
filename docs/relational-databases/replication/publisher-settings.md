---
title: "Configurações do Publicador | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.monitor.publishersettings.f1
helpviewer_keywords: Publisher Settings dialog box
ms.assetid: 4fb70427-082d-4179-82a1-34b235accc43
caps.latest.revision: "19"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3fca314477bfb6abf1532c6510ab391872cb36a2
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="publisher-settings"></a>Configurações do Publicador
  A caixa de diálogo **Configurações do Publicador** permite alterar configurações para Publicadores adicionados ao painel esquerdo no Replication Monitor.  
  
## <a name="options"></a>Opções  
 **Conexão do Publicador**  
 Clique para iniciar a caixa de diálogo **Conectar ao Servidor** que permite que você visualize e altere as credenciais e propriedades de conexão que o Replication Monitor usa para se conectar a um Publicador.  
  
 **Conexão do Distribuidor**  
 Exibido somente se o Publicador usar um Distribuidor remoto. Clique para iniciar a caixa de diálogo **Conectar ao Servidor** que permite que você visualize e altere as credenciais e propriedades de conexão que o Replication Monitor usa para se conectar a um Distribuidor remoto.  
  
 **Conectar automaticamente quando o Replication Monitor for iniciado**  
 Selecione para permitir que o Replication Monitor faça conexão automática com o Distribuidor e recupere informações de status para o Publicador selecionado na grade, na parte superior da caixa de diálogo. Se essa caixa de seleção estiver desmarcada, você terá de fazer a conexão manualmente após iniciar o Replication Monitor: clique com o botão direito no Publicador no painel esquerdo do Replication Monitor, e clique em **Conectar**.  
  
 **Atualizar automaticamente o status deste Publicador e de suas publicações**  
 Selecione para permitir que o Replication Monitor atualize automaticamente o status do Publicador selecionado na grade, na parte superior da caixa de diálogo. Se essa opção for selecionada, o Replication Monitor pesquisará no Distribuidor informações de status sobre o Publicador e suas publicações. O intervalo da sondagem é definido pela opção **Taxa de Atualização** . Para obter mais informações sobre a atualização no Replication Monitor, consulte [Cache, atualização e desempenho do Replication Monitor](../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md).  
  
 **Taxa de atualização**  
 Insira um valor (em segundos) para especificar a frequência de sondagem do Replication Monitor no Distribuidor, por status. Valores mais baixos resultam em sondagens mais frequentes, que podem afetar o desempenho no Distribuidor se você estiver monitorando um grande número de Publicadores. É recomendado que você teste seu sistema para determinar um valor apropriado. A configuração da **Taxa de Atualização** será também usada se você selecionar **Atualização Automática** em qualquer uma das janelas de detalhes no Replication Monitor.  
  
 **Mostrar este Publicador no grupo a seguir**  
 Selecione um grupo de Publicadores na lista. O Publicador é exibido nesse grupo no painel esquerdo. Grupos fornecem uma forma de organizar Publicadores e não causam nenhum efeito em funções de replicação.  
  
 **Novo grupo**  
 Clique para criar um novo grupo de Publicadores. Um grupo de Publicadores é um modo conveniente de organizar Publicadores no Replication Monitor. Grupos não afetam a replicação de dados ou a relação entre servidores em uma topologia de replicação.  
  
## <a name="see-also"></a>Consulte também  
 [Iniciar o Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Monitorando a Replicação](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
