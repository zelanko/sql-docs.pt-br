---
title: MSSQLSERVER_2511 | Microsoft Docs
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
- 2511 (Database Engine error)
ms.assetid: 9a00c0ed-eb4b-4fae-8016-192396006c37
caps.latest.revision: 12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9045011f151479b9f6643172542e6fe3c3bdf7b1
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver2511"></a>MSSQLSERVER_2511
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|2511|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC_KEYS_OUT_OF_ORDER|  
|Texto da mensagem|Erro de tabela: ID de objeto %d, ID de índice %d, ID de partição %I64d, ID de unidade de alocação %I64d (tipo %.*ls). As chaves estão fora da ordem na página %S_PGID, slots %d e %d.|  
  
## <a name="explanation"></a>Explicação  
Chaves fora de ordem foram detectadas no índice especificado. A página em que as chaves estão contidas pode estar corrompida.  
  
## <a name="user-action"></a>Ação do usuário  
Reconstrua o índice especificado usando a instrução ALTER INDEX REBUILD.  
  
