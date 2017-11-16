---
title: MSSQLSERVER_2546 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 2546 (Database Engine error)
ms.assetid: c8f0e1b4-c7c4-45f2-9221-746714172313
caps.latest.revision: "20"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: b13b71f78995fc1c516e5dba76953f91b541bfd4
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver2546"></a>MSSQLSERVER_2546
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|2546|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC_INDEX_MARKED_DISABLED|  
|Texto da mensagem|O índice 'INDEX_NAME' na tabela 'OBJECT_NAME' está marcado como desabilitado. Reconstrua o índice para colocá-lo online.|  
  
## <a name="explanation"></a>Explicação  
O índice especificado está marcado como offline ou está desabilitado. Por isso, não é possível verificá-lo.  
  
## <a name="user-action"></a>Ação do usuário  
Reconstrua o índice usando a instrução ALTER INDEX.  
  
## <a name="see-also"></a>Consulte também  
[ALTER INDEX &#40;Transact-SQL&#41;](~/t-sql/statements/alter-index-transact-sql.md)  
[Reorganizar e recompilar índices](~/relational-databases/indexes/reorganize-and-rebuild-indexes.md)  
  
