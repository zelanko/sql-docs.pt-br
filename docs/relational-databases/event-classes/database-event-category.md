---
title: Categoria de Evento de Banco de Dados | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- event classes [SQL Server], Database event category
- Database event category [SQL Server]
- SQL Server event classes, Database event category
ms.assetid: b61af738-f144-4992-b0b2-d44cb7240991
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cf3fd2a6cd222320e55b7336272bf9f662b81694
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68009572"
---
# <a name="database-event-category"></a>Categoria de evento Database
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  A categoria de evento **Database** contém classes de eventos para monitorar o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|DESCRIÇÃO|  
|-----------|-----------------|  
|[Classe de evento Data File Auto Grow](../../relational-databases/event-classes/data-file-auto-grow-event-class.md)|Indica que o arquivo de dados cresceu automaticamente. Este evento não será disparado se o arquivo de dados crescer explicitamente através de ALTER DATABASE.|  
|[Classe de evento Data File Auto Shrink](../../relational-databases/event-classes/data-file-auto-shrink-event-class.md)|Indica que o arquivo de dados foi reduzido.|  
|[Classe de evento Database Mirroring Connection](../../relational-databases/event-classes/database-mirroring-connection-event-class.md)|Um evento gerado para informar o status de uma conexão de transporte para espelhamento de banco de dados.|  
|[Classe de evento Database Mirroring State Change](../../relational-databases/event-classes/database-mirroring-state-change-event-class.md)|Indica quando o estado de um banco de dados espelhado é alterado.|  
|[Classe de evento Database Suspect Data Page](../../relational-databases/event-classes/database-suspect-data-page-event-class.md)|Indica quando uma página é adicionada à tabela **suspect_pages** no banco de dados **msdb** .|  
|[Classe de evento Log File Auto Grow](../../relational-databases/event-classes/log-file-auto-grow-event-class.md)|Indica que o arquivo de log cresceu automaticamente. Esse evento não será acionado se o arquivo de log crescer explicitamente por meio de ALTER DATABASE.|  
|[Classe de evento Log File Auto Shrink](../../relational-databases/event-classes/log-file-auto-shrink-event-class.md)|Indica que o arquivo de log cresceu automaticamente. Este evento não será disparado se o arquivo de log for reduzido explicitamente através de ALTER DATABASE.|  
  
## <a name="see-also"></a>Consulte Também  
 [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)  
  
  
