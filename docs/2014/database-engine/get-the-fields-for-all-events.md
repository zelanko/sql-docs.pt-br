---
title: Obter os campos de todos os eventos | Microsoft Docs
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
- extended events [SQL Server], getting fields
- xe
ms.assetid: 4e4ee03f-5bca-42ed-a37c-db1c82e3aad2
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: fac62e2160086d920e3e73e770eaaf1cc82e0b88
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119781"
---
# <a name="get-the-fields-for-all-events"></a>Obter os campos de todos os eventos
  A realização desta tarefa envolve o uso do Editor de Consulta no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
 Encerradas as instruções do procedimento, a guia **Resultados** do Editor de Consultas exibe as seguintes colunas:  
  
-   package_name  
  
-   event_name  
  
-   event_field  
  
-   field_type  
  
-   column_type  
  
 Você pode usar as informações acima ao configurar sessões de eventos que usam o destino da segmentação. Para obter mais informações, consulte [SQL Server Extended Events Targets](../../2014/database-engine/sql-server-extended-events-targets.md).  
  
## <a name="before-you-begin"></a>Antes de começar  
 Antes de criar uma sessão Eventos Estendidos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , é útil obter informações sobre os campos associados aos eventos.  
  
## <a name="to-get-the-fields-for-all-events-using-query-editor"></a>Para obter os campos de todos os eventos usando o Editor de Consulta  
  
-   No Editor de Consultas, emita as seguintes instruções:  
  
    ```  
    select p.name package_name, o.name event_name, c.name event_field, c.type_name field_type, c.column_type column_type  
    from sys.dm_xe_objects o  
    join sys.dm_xe_packages p  
          on o.package_guid = p.guid  
    join sys.dm_xe_object_columns c  
          on o.name = c.object_name  
    where o.object_type = 'event'  
    order by package_name, event_name  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [sys.dm_xe_objects &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql)   
 [sys.dm_xe_packages &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-packages-transact-sql)  
  
  
