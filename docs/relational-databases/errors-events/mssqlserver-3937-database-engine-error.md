---
title: MSSQLSERVER_3937 | Microsoft Docs
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
- 3937 (Database Engine error)
ms.assetid: 312d5bbe-c8de-42db-af4b-4ccb448ce6ef
caps.latest.revision: 12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6f02486a0a113f2e589a5f17d40344c374c1d853
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver3937"></a>MSSQLSERVER_3937
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|MSSQLSERVER|  
|ID do evento|3937|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|XACT_FILESTREAM_ROLLBACK_ERROR|  
|Texto da mensagem|Erro ao tentar notificar o driver do filtro FILESTREAM que uma transação foi revertida. Código de erro: 0x%0x.|  
  
## <a name="explanation"></a>Explicação  
Um erro foi retornado pelo driver de RsFx ao emitir uma notificação de reversão para uma transação. Isso provavelmente foi provocado por uma falta de recurso. Isso pode causar um pequeno vazamento de memória no driver do filtro de RsFx, mas ele será liberado quando o processo sqlservr.exe que criou a transação sair.  
  
## <a name="user-action"></a>Ação do usuário  
