---
title: Obter os parâmetros configuráveis para o argumento ADD TARGET | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- extended events [SQL Server], ADD TARGET argument
- xe
ms.assetid: 08454543-c5c8-4ca3-9af9-f1d82264471c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a66a4e77b3858b769aef287e68cac18b8b8514ea
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66064798"
---
# <a name="get-the-configurable-parameters-for-the-add-target-argument"></a>Obter os parâmetros configuráveis para o argumento ADD TARGET
  A realização desta tarefa envolve o uso do Editor de Consulta no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
 Encerradas as instruções do procedimento, a guia **Resultados** do Editor de Consultas exibe as seguintes colunas:  
  
-   package_name  
  
-   target_name  
  
-   parameter_name  
  
-   parameter_type  
  
-   required  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
 Antes de criar uma sessão de Eventos Estendidos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , é proveitoso descobrir quais parâmetros podem ser definidos para o uso do argumento ADD TARGET em CREAT EVENT SESSION ou ALTER EVENT SESSION.  
  
### <a name="to-get-the-configurable-parameters-for-the-add-target-argument-using-query-editor"></a>Para obter os parâmetros configuráveis para o argumento ADD TARGET usando o Editor de Consultas  
  
-   No Editor de Consultas, emita as seguintes instruções:  
  
    ```  
    SELECT p.name package_name, o.name target_name, c.name parameter_name,   
    c.type_name parameter_type, CASE c.capabilities_desc WHEN 'mandatory' THEN 'yes' ELSE 'no' END   
    required   
    FROM sys.dm_xe_objects o JOIN sys.dm_xe_packages p ON o.package_guid = p.guid   
    JOIN sys.dm_xe_object_columns c ON o.name = c.object_name AND c.column_type = 'customizable'  
    WHERE o.object_type = 'target'   
    ORDER BY package_name, target_name, required DESC  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)   
 [sys.dm_xe_objects &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql)   
 [sys.dm_xe_packages &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-packages-transact-sql)  
  
  
