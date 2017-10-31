---
title: MSSQLSERVER_2511 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 2511 (Database Engine error)
ms.assetid: 9a00c0ed-eb4b-4fae-8016-192396006c37
caps.latest.revision: 12
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4105d5c9c2d1feb387e29002224ce9496e358210
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver2511"></a>MSSQLSERVER_2511
  
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
  

