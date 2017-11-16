---
title: MSSQLSERVER_3937 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 3937 (Database Engine error)
ms.assetid: 312d5bbe-c8de-42db-af4b-4ccb448ce6ef
caps.latest.revision: "12"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 113385d8dd09b70f4d058fb24a113f7065866eeb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver3937"></a>MSSQLSERVER_3937
  
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
