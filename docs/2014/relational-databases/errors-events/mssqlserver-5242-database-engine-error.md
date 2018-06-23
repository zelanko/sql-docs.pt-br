---
title: MSSQLSERVER_5242 | Microsoft Docs
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
- 5242 (Database Engine error)
ms.assetid: 712b1a10-2f87-41df-a111-1ed9f14102d4
caps.latest.revision: 14
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: c9b1f477feed3215544018dc28cda840253022ab
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116593"
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
 [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)   
 [Arquivos e grupos de arquivos do banco de dados](../databases/database-files-and-filegroups.md)  
  
  
