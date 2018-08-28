---
title: Classe de evento Database Suspect Data Page | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- event notifications [SQL Server], database mirroring
- suspect_pages system table
- database mirroring [SQL Server], event notifications
- Database Suspect Data Page event class
ms.assetid: 098e1443-a8a0-425c-9311-0a479b1370ed
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 591fb645cc927f5f3b7b7d7259b02b1e9c3501e2
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43070378"
---
# <a name="database-suspect-data-page-event-class"></a>classe de evento Database Suspect Data Page
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  A classe do evento **Database Suspect Data Page** indica quando uma página é acrescentada à tabela [suspect_pages](../../relational-databases/system-tables/suspect-pages-transact-sql.md) no [msdb](../../relational-databases/databases/msdb-database.md). Inclua esta classe de evento em rastreamentos que estiverem monitorando a ocorrência de páginas suspeitas.  
  
> [!NOTE]  
>  Esse evento é gerado de forma assíncrona por meio da inserção de uma linha correspondente na tabela **suspect_pages** . Portanto, uma tarefa escutando esse evento pode não encontrar a entrada **suspect_pages** correspondente imediatamente.  
  
 Quando a classe do evento **Database Suspect Data Page** é incluída em um rastreamento, a sobrecarga relativa é baixa. A sobrecarga poderá ser maior se o número de páginas suspeitas aumentar, por exemplo, se uma unidade de disco estiver com problemas.  
  
## <a name="database-suspect-data-page-event-class-data-columns"></a>Colunas de dados da classe de evento Database Suspect Data Page  
  
|Nome da coluna de dados|Tipo de Dados|Descrição|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|O ID do banco de dados para o qual foi levantado o evento de página suspeita. Isso é igual à coluna **database_id** da tabela **suspect_pages** .|3|Sim|  
|**EventClass**|**int**|O tipo do evento é 213.|27|não|  
|**EventSequence**|**int**|Sequência de classe de evento em lote.|51|não|  
|**SPID**|**int**|ID da tarefa do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que encontrou a página suspeita.|12|Sim|  
|**StartTime**|**datetime**|Hora que o evento ocorreu.|14|Sim|  
|**ObjectID**|**int**|ID do arquivo do banco de dados que encontrou a página suspeita. Isso é igual à coluna **file_id** da tabela **suspect_pages** .|22|Sim|  
|**ObjectID2**|**int**|ID da página suspeita no arquivo. Isso é igual à coluna **page_id** da tabela **suspect_pages** .|56|Sim|  
|**Erro**|**int**|Tipo de erro que foi encontrado. Este valor é igual ao valor **event_type** da página na tabela **suspect_pages** .|31|Sim|  
  
## <a name="see-also"></a>Consulte Também  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Gerenciar a tabela suspect_pages &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  
