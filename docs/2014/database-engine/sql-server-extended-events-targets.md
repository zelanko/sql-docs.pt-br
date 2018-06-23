---
title: Destinos de eventos estendidos do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- targets [SQL Server extended events]
- extended events [SQL Server], targets
ms.assetid: e281684c-40d1-4cf9-a0d4-7ea1ecffa384
caps.latest.revision: 50
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: dbd3b218390cc1a49f7256a7f2cb79228ff8c3c7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009386"
---
# <a name="sql-server-extended-events-targets"></a>SQL Server Extended Events Targets
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Destinos de eventos estendidos são consumidores de evento. Os destinos podem gravar em um arquivo, armazenar dados de evento em um buffer de memória ou agregar dados de evento. Os destinos podem processar dados de forma síncrona ou assíncrona.  
  
 O design de Eventos Estendidos assegura que os destinos tenham a garantia de receber eventos somente uma vez por sessão.  
  
 Os Eventos Estendidos fornecem os seguintes destinos que você pode usar em uma sessão de Eventos Estendidos:  
  
-   [Contador de eventos](../../2014/database-engine/event-counter-target.md)  
  
     Conta todos os eventos especificados que ocorrem durante uma sessão de Eventos Estendidos. Use para obter informações sobre as características da carga de trabalho sem adicionar a sobrecarga de uma coleção de eventos completa. Este é um destino síncrono.  
  
-   [Arquivo de evento](../../2014/database-engine/event-file-target.md)  
  
     Use para gravar a saída da sessão de evento de buffers de memória completos em disco. Este é um destino assíncrono.  
  
-   [Emparelhamento de eventos](../../2014/database-engine/event-pairing-target.md)  
  
     Muitos tipos de eventos ocorrem em pares, como aquisições e liberações de bloqueio. Use para determinar quando um evento emparelhado especificado não ocorre em um conjunto correspondente. Este é um destino assíncrono.  
  
-   [Rastreamento de eventos do Windows (ETW)](../relational-databases/extended-events/event-tracing-for-windows-target.md)  
  
     Use para correlacionar eventos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com o sistema operacional Windows ou dados de eventos de aplicativos. Este é um destino síncrono.  
  
-   [Histograma](../../2014/database-engine/histogram-target.md)  
  
     Use para contar o número de vezes que um evento especificado ocorre com base em uma coluna de eventos ou uma ação específica. Este é um destino assíncrono.  
  
-   [Buffer de anel](../../2014/database-engine/ring-buffer-target.md)  
  
     Use para manter os dados do evento na memória em uma base PEPS (primeiro a entrar, primeiro a sair) ou em uma base PEPS por evento. Este é um destino assíncrono.  
  
## <a name="see-also"></a>Consulte também  
 [Eventos estendidos](../relational-databases/extended-events/extended-events.md)   
 [Pacotes de eventos estendidos do SQL Server](../relational-databases/extended-events/sql-server-extended-events-packages.md)   
 [Sessões de eventos estendidos do SQL Server](../relational-databases/extended-events/sql-server-extended-events-sessions.md)   
 [Mecanismo de eventos estendidos do SQL Server](../relational-databases/extended-events/sql-server-extended-events-engine.md)  
  
  