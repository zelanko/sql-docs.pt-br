---
title: Cache, atualização e desempenho do Replication Monitor
description: Saiba mais sobre cache, atualização e otimização de desempenho do Replication Monitor no SSMS (SQL Server Management Studio).
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], Replication Monitor
- cache [SQL Server], replication
- Replication Monitor, caching
- refreshing data
- Replication Monitor, refreshing
ms.assetid: a2d8b666-ed41-4f86-b2b8-c8e118416ab7
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 0661822f2c39d197460d19bb01adc847151dfa35
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2019
ms.locfileid: "75320611"
---
# <a name="caching-refresh-and-replication-monitor-performance"></a>Cache, atualização e desempenho do Replication Monitor
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] O Replication Monitor é projetado para monitorar um número grande de computadores em um sistema de produção de forma eficaz. As consultas que o Replication Monitor usa para executar cálculos e reunir dados são armazenadas em cache e atualizadas periodicamente. O armazenamento em cache reduz o número de consultas e cálculos necessários conforme diferentes páginas são exibidas no Replication Monitor, e permite que a monitoração seja bem-escalonada para usuários múltiplos.  
  
 A atualização do cache é controlada por um trabalho do Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , o **Atualizador de monitoração de replicação para distribuição**. O trabalho é executado continuamente, mas a agenda para a atualização de cache é baseada na espera de certo tempo após a atualização anterior:  
  
-   Se tiverem ocorrido alterações de histórico de agente desde que o cache foi criado pela última vez, o tempo de espera será de pelo menos: 4 segundos; ou a quantidade de tempo necessária para criar o cache anterior.  
  
-   Se não tiver ocorrido nenhuma alteração de histórico do agente desde que o cache foi criado pela última vez (pode ter havido outras alterações), o tempo de espera será de no máximo: 30 segundos; ou a quantidade de tempo necessária para criar o cache anterior.  
  
## <a name="refreshing-the-replication-monitor-user-interface"></a>Atualizando a interface de usuário do Replication Monitor  
 A interface de usuário do Replication Monitor pode ser atualizada das formas a seguir:  
  
-   A janela principal do Replication Monitor (incluindo todas as guias), é atualizada automaticamente a cada cinco segundos por padrão. Atualizações automáticas não forçam a atualização do cache; a interface do usuário mostra a versão mais recente dos dados do cache. Para personalizar a taxa de atualização usada para todas as janelas associadas com um Publicador, edite as configurações do Publicador. Também é possível desabilitar as atualizações automáticas para um Publicador.  
  
-   As janelas de detalhe que são executadas a partir do Replication Monitor não são automaticamente atualizadas por padrão, com exceção das janelas relacionadas a assinaturas de mesclagem que estão sendo sincronizadas. Se você especificar que as janelas de detalhes devem ser atualizadas automaticamente, elas serão atualizadas na mesma agenda que a janela principal do Replication Monitor.  
  
-   Todas as janelas podem ser atualizadas manualmente pressionando F5 ou clicando com o botão direito em um nó na árvore do Replication Monitor e, em seguida, clicando em **Atualizar**. Atualizações manuais forçam uma atualização do cache.  
  
 Para obter mais informações, consulte [Atualizar dados no Replication Monitor](../../../relational-databases/replication/monitor/refresh-data-in-replication-monitor.md).  
  
## <a name="performance-considerations"></a>Considerações sobre desempenho  
 Embora o Replication Monitor seja projetado para executar de forma eficaz, esteja atento ao seguinte:  
  
-   Se tiver um grande número de publicações e assinaturas, considere definir uma agenda de atualização automática menos frequente para a interface do usuário.  
  
-   Evite executar várias instâncias do Replication Monitor simultaneamente.  
  
-   Evite registrar um número grande de Distribuidores e configurar o Replication Monitor para conectar-se automaticamente a todos eles.  
  
## <a name="see-also"></a>Consulte Também  
 [Executar trabalhos de manutenção de replicação &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/administration/run-replication-maintenance-jobs-sql-server-management-studio.md)   
 [Monitorando a Replicação](../../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
