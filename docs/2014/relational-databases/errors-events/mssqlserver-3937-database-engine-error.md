---
title: MSSQLSERVER_3937 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3937 (Database Engine error)
ms.assetid: 312d5bbe-c8de-42db-af4b-4ccb448ce6ef
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1064b834d24c820da49a1791a6a319f27c27d301
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62867983"
---
# <a name="mssqlserver_3937"></a>MSSQLSERVER_3937
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|MSSQLSERVER|  
|ID do evento|3937|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|XACT_FILESTREAM_ROLLBACK_ERROR|  
|Texto da mensagem|Erro ao tentar notificar o driver do filtro FILESTREAM que uma transação foi revertida. Código de erro: 0x%0x.|  
  
## <a name="explanation"></a>Explicação  
 Um erro foi retornado pelo driver de RsFx ao emitir uma notificação de reversão para uma transação. Isso provavelmente foi provocado por uma falta de recurso. Isso pode causar um pequeno vazamento de memória no driver do filtro de RsFx, mas ele será liberado quando o processo sqlservr.exe que criou a transação sair.  
  
## <a name="user-action"></a>Ação do usuário  
  
