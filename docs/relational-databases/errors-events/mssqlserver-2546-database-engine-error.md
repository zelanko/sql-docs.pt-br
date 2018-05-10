---
title: MSSQLSERVER_2546 | Microsoft Docs
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
- 2546 (Database Engine error)
ms.assetid: c8f0e1b4-c7c4-45f2-9221-746714172313
caps.latest.revision: 20
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: aa504a0068e444ca0c423791000582bee782fb40
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver2546"></a>MSSQLSERVER_2546
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
## <a name="see-also"></a>Consulte Também  
[ALTER INDEX &#40;Transact-SQL&#41;](~/t-sql/statements/alter-index-transact-sql.md)  
[Reorganizar e recompilar índices](~/relational-databases/indexes/reorganize-and-rebuild-indexes.md)  
  
