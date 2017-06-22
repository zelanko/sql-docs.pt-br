---
title: "Configurações de distribuidor | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.monitor.DistributorSettings.f1
helpviewer_keywords:
- Distributor Settings dialog box
ms.assetid: 8276a521-bdd1-4783-bdb6-7ab43499c0ca
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f86500a4461bc2da64c7f3a3d8906bb919b28628
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="distributor-settings"></a>Configurações de distribuidor
  A caixa de diálogo **Configurações do Distribuidor** permite alterar configurações para Distribuidores que foram adicionados ao painel esquerdo no Replication Monitor.  
  
## <a name="options"></a>Opções  
 **Conectar automaticamente quando o Replication Monitor for iniciado**  
 Selecione para permitir que o Monitor de Replicação conecte-se ao Distribuidor e recupere informações de status.  
  
 **Conexão**  
 Clique para exibir a caixa de diálogo **Conectar ao Servidor** . Isso permite que você visualize e altere as credenciais e propriedades de conexão que o Replication Monitor usa para se conectar ao Distribuidor.  
  
 **Atualizar automaticamente o status deste Distribuidor e de suas publicações**  
 Selecione para permitir que o Monitor de Replicação atualize automaticamente o status para o Distribuidor. Se essa opção for selecionada, o Replication Monitor pesquisará no Distribuidor informações de status com base no intervalo de sondagem pela opção **Taxa de atualização** . Para obter mais informações sobre atualização no Replication Monitor, consulte [Caching, Refresh, and Replication Monitor Performance](../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md).  
  
 **Taxa de atualização**  
 Insira um valor (em segundos) para especificar a frequência de sondagem do Replication Monitor no Distribuidor, por status. Valores inferiores resultam em sondagem mais frequente. Isto poderá afetar o desempenho no Distribuidor se você estiver monitorando muitos Publicadores. Recomendamos que você teste seu sistema para determinar um valor apropriado. A configuração da **Taxa de Atualização** será também usada se você selecionar **Atualização Automática** em qualquer uma das janelas de detalhes no Replication Monitor.  
  
 **Mostre para todos os Publicadores deste Distribuidor no grupo a seguir**  
 Selecione um grupo de Publicadores na lista. O Publicador é exibido nesse grupo no painel esquerdo. Grupos fornecem uma forma de organizar Publicadores e não afetam a maneira como a replicação funciona.  
  
 **Novo grupo**  
 Clique para criar um novo grupo de Publicadores. Um grupo de Publicadores é um modo conveniente de organizar Publicadores no Replication Monitor. Grupos não afetam a replicação de dados ou a relação entre servidores em uma topologia de replicação.  
  
## <a name="see-also"></a>Consulte também  
 [Iniciar o Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Monitorando a Replicação](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
