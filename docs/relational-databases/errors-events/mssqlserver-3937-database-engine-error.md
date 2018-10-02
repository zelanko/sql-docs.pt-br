---
title: MSSQLSERVER_3937 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3937 (Database Engine error)
ms.assetid: 312d5bbe-c8de-42db-af4b-4ccb448ce6ef
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3cb93f99d996cc992fc47873b2a3863caec7ec6d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47761794"
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
