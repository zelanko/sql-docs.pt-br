---
title: Categoria de Evento de Banco de Dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- event classes [SQL Server], Database event category
- Database event category [SQL Server]
- SQL Server event classes, Database event category
ms.assetid: b61af738-f144-4992-b0b2-d44cb7240991
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2c68c5f735c494776c9e798b3786c6dcda048f7e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48078606"
---
# <a name="database-event-category"></a>Categoria de evento Database
  A categoria de evento **Database** contém classes de eventos para monitorar o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Classe de evento Data File Auto Grow](data-file-auto-grow-event-class.md)|Indica que o arquivo de dados cresceu automaticamente. Este evento não será disparado se o arquivo de dados crescer explicitamente através de ALTER DATABASE.|  
|[Classe de evento Data File Auto Shrink](data-file-auto-shrink-event-class.md)|Indica que o arquivo de dados foi reduzido.|  
|[Classe de evento conexão de espelhamento de banco de dados](database-mirroring-connection-event-class.md)|Um evento gerado para informar o status de uma conexão de transporte para espelhamento de banco de dados.|  
|[Classe de evento Database Mirroring State Change](database-mirroring-state-change-event-class.md)|Indica quando o estado de um banco de dados espelhado é alterado.|  
|[Classe de evento Database Suspect Data Page](database-suspect-data-page-event-class.md)|Indica quando uma página é adicionada à tabela **suspect_pages** no banco de dados **msdb** .|  
|[Classe de evento Log File Auto Grow](log-file-auto-grow-event-class.md)|Indica que o arquivo de log cresceu automaticamente. Esse evento não será acionado se o arquivo de log crescer explicitamente por meio de ALTER DATABASE.|  
|[Classe de evento Log File Auto Shrink](log-file-auto-shrink-event-class.md)|Indica que o arquivo de log cresceu automaticamente. Este evento não será disparado se o arquivo de log for reduzido explicitamente através de ALTER DATABASE.|  
  
## <a name="see-also"></a>Consulte também  
 [Eventos estendidos](../extended-events/extended-events.md)  
  
  
