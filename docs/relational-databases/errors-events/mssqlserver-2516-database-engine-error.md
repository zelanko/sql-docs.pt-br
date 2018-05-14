---
title: MSSQLSERVER_2516 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 2516 (Database Engine error)
ms.assetid: 79ed14b5-f53c-40c6-8334-8a083f732207
caps.latest.revision: 19
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: aa283ee1c11f9cb207f00f8d79fe4af5bfb11bf0
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver2516"></a>MSSQLSERVER_2516
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
## <a name="see-also"></a>Consulte Também  
[Criar um backup completo de banco de dados &#40;SQL Server&#41;](~/relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
