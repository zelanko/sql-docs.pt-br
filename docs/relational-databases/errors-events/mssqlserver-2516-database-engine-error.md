---
title: MSSQLSERVER_2516 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 2516 (Database Engine error)
ms.assetid: 79ed14b5-f53c-40c6-8334-8a083f732207
caps.latest.revision: "19"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 7893577f260f379e06029a11c6117916709d32cf
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver2516"></a>MSSQLSERVER_2516
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|2516|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC_REPAIR_DIFF_MAP_INVALIDATED|  
|Texto da mensagem|A correção invalidou o bitmap diferencial do banco de dados NAME. A cadeia de backup diferencial foi quebrada. Execute um backup total de banco de dados antes de executar um backup diferencial.|  
  
## <a name="explanation"></a>Explicação  
Essa mensagem informativa é retornada quando o erro MSSQLEngine_2515 é corrigido.  
  
## <a name="user-action"></a>Ação do usuário  
Execute um backup total do banco de dados.  
  
## <a name="see-also"></a>Consulte também  
[Criar um backup completo de banco de dados &#40;SQL Server&#41;](~/relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
