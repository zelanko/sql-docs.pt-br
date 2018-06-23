---
title: MSSQLSERVER_2511 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 2511 (Database Engine error)
ms.assetid: 9a00c0ed-eb4b-4fae-8016-192396006c37
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 9cfc320d29448dfa829e8741643d79df5c80061f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115218"
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
  
  