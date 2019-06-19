---
title: MSSQLSERVER_2546 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2546 (Database Engine error)
ms.assetid: c8f0e1b4-c7c4-45f2-9221-746714172313
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 983c5536d08d9701fd301ace4ca8d2b5d7e76f71
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63046397"
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
  
