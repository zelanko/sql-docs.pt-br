---
title: MSSQLSERVER_3937 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
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
ms.openlocfilehash: 263747514a29b61f82b308078decbe2967c6fb6b
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
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
