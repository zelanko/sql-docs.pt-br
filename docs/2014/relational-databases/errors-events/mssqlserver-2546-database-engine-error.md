---
title: MSSQLSERVER_2546 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 2546 (Database Engine error)
ms.assetid: c8f0e1b4-c7c4-45f2-9221-746714172313
caps.latest.revision: 20
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e9497598b38a7bb13b76e6e54d0b0696cb56990e
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37427075"
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
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)   
 [Reorganizar e recompilar índices](../indexes/indexes.md)  
  
  
