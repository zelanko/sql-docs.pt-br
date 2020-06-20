---
title: MSSQLSERVER_2511 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2511 (Database Engine error)
ms.assetid: 9a00c0ed-eb4b-4fae-8016-192396006c37
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 23e91b0d64140329639cf57f3a336cd2eab8e4e8
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85034513"
---
# <a name="mssqlserver_2511"></a>MSSQLSERVER_2511
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|2511|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC_KEYS_OUT_OF_ORDER|  
|Texto da mensagem|Erro de tabela: ID de objeto %d, ID de índice %d, ID de partição %I64d, ID de unidade de alocação %I64d (tipo %.*ls). As chaves estão fora da ordem na página %S_PGID, slots %d e %d.|  
  
## <a name="explanation"></a>Explicação  
 Chaves fora de ordem foram detectadas no índice especificado. A página em que as chaves estão contidas pode estar corrompida.  
  
## <a name="user-action"></a>Ação do usuário  
 Reconstrua o índice especificado usando a instrução ALTER INDEX REBUILD.  
  
  
