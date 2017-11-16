---
title: MSSQLSERVER_5242 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 5242 (Database Engine error)
ms.assetid: 712b1a10-2f87-41df-a111-1ed9f14102d4
caps.latest.revision: "15"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 5cdf9006f511709715627c17c7ada22326c5e67f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver5242"></a>MSSQLSERVER_5242
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do Evento|5242|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico||  
|Texto da mensagem|Foi detectada uma inconsistência durante uma operação interna no banco de dados '%.*ls' (ID:%d) na página %S_PGID. Contate o suporte técnico. Número de referência %ld.|  
  
## <a name="explanation"></a>Explicação  
Ocorreu uma inconsistência estrutural na página do banco de dados referenciada na mensagem de erro.  
  
## <a name="see-also"></a>Consulte também  
[DBCC CHECKDB &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
[Arquivos e grupos de arquivos do banco de dados](~/relational-databases/databases/database-files-and-filegroups.md)  
  
