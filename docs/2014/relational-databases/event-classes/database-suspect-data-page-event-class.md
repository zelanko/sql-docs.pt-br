---
title: Classe de evento Database Suspect Data Page | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
topic_type:
- apiref
helpviewer_keywords:
- event notifications [SQL Server], database mirroring
- suspect_pages system table
- database mirroring [SQL Server], event notifications
- Database Suspect Data Page event class
ms.assetid: 098e1443-a8a0-425c-9311-0a479b1370ed
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e6f92e92474b6d923ad355e8ae0a5ddb1499fb14
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120158"
---
# <a name="database-suspect-data-page-event-class"></a>classe de evento Database Suspect Data Page
  A classe do evento **Database Suspect Data Page** indica quando uma página é acrescentada à tabela [suspect_pages](/sql/relational-databases/system-tables/suspect-pages-transact-sql) no [msdb](../databases/msdb-database.md). Inclua esta classe de evento em rastreamentos que estiverem monitorando a ocorrência de páginas suspeitas.  
  
> [!NOTE]  
>  Esse evento é gerado de forma assíncrona por meio da inserção de uma linha correspondente na tabela **suspect_pages** . Portanto, uma tarefa escutando esse evento pode não encontrar a entrada **suspect_pages** correspondente imediatamente.  
  
 Quando a classe do evento **Database Suspect Data Page** é incluída em um rastreamento, a sobrecarga relativa é baixa. A sobrecarga poderá ser maior se o número de páginas suspeitas aumentar, por exemplo, se uma unidade de disco estiver com problemas.  
  
## <a name="database-suspect-data-page-event-class-data-columns"></a>Colunas de dados da classe de evento Database Suspect Data Page  
  
|Nome da coluna de dados|Tipo de Dados|Description|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|O ID do banco de dados para o qual foi levantado o evento de página suspeita. Isso é igual à coluna **database_id** da tabela **suspect_pages** .|3|Sim|  
|**EventClass**|**int**|O tipo do evento é 213.|27|não|  
|**EventSequence**|**int**|Sequência de classe de evento em lote.|51|não|  
|**SPID**|**int**|ID da tarefa do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que encontrou a página suspeita.|12|Sim|  
|**StartTime**|**datetime**|Hora que o evento ocorreu.|14|Sim|  
|**ObjectID**|**int**|ID do arquivo do banco de dados que encontrou a página suspeita. Isso é igual à coluna **file_id** da tabela **suspect_pages** .|22|Sim|  
|**ObjectID2**|**int**|ID da página suspeita no arquivo. Isso é igual à coluna **page_id** da tabela **suspect_pages** .|56|Sim|  
|**Erro**|**int**|Tipo de erro que foi encontrado. Este valor é igual ao valor **event_type** da página na tabela **suspect_pages** .|31|Sim|  
  
## <a name="see-also"></a>Consulte também  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Gerenciar a tabela suspect_pages &#40;SQL Server&#41;](../backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  
