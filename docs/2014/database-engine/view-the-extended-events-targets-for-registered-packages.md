---
title: Exibir os destinos de eventos estendidos de pacotes registrados | Microsoft Docs
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
- viewing event targets
- extended events [SQL Server], viewing targets
ms.assetid: 4985aa5f-ac99-49f6-852c-9d25916549e9
caps.latest.revision: 12
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 1c5552ca54f3297226fad6a15de2d5c80bc49067
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006694"
---
# <a name="view-the-extended-events-targets-for-registered-packages"></a>Exibir os destinos dos Eventos Estendidos de pacotes registrados
  Antes de criar uma sessão de Eventos Estendidos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , determine quais destinos de Eventos Estendidos estão disponíveis. Essa tarefa envolve o uso do Editor de Consultas no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para executar o seguinte procedimento.  
  
 Encerradas as instruções do procedimento, a guia **Resultados** do Editor de Consultas exibirá estas duas colunas:  
  
-   package_name  
  
-   target_name  
  
## <a name="to-view-the-extended-events-targets-for-registered-packages-using-query-editor"></a>Para exibir os destinos de Eventos Estendidos de pacotes registrados usando o Editor de Consulta  
  
-   No Editor de Consultas, emita as seguintes instruções:  
  
    ```  
    USE msdb  
    SELECT p.name package_name, o.name target_name  
    FROM sys.dm_xe_objects o  
    JOIN sys.dm_xe_packages p  
         ON o.package_guid = p.guid  
    WHERE o.object_type = 'target'  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Destinos de eventos estendidos do SQL Server](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [sys.dm_xe_objects &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql)   
 [sys.dm_xe_packages &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-packages-transact-sql)  
  
  
