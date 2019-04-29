---
title: MSSQLSERVER_9003 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9003 (Database Engine error)
ms.assetid: 7fdfb391-5c6f-428b-b434-6c3d0b30fd7b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c3d994f2166ae468a731203211eeb7a784118e65
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62912458"
---
# <a name="mssqlserver9003"></a>MSSQLSERVER_9003
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|9003|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|LOG_INVALID_LSN|  
|Texto da mensagem|O número de exames do log %S_LSN passado para o exame no banco de dados '%.*ls' não é válido. Esse erro pode indicar danos nos dados ou que o arquivo de log (.ldf) não corresponde ao arquivo de dados (.mdf). Se esse erro ocorreu durante a replicação, crie a publicação novamente. Caso contrário, se o problema resultar em uma falha durante a inicialização, restaure de um backup.|  
  
## <a name="explanation"></a>Explicação  
Um componente passou um número de sequência de log inválido ao gerenciador de log do banco de dados. Isso pode causar replicação, corrompimento ou uma inconsistência entre o arquivo de dados primário e o log.  
  
## <a name="user-action"></a>Ação do usuário  
Se ele ocorreu durante replicação, recrie a publicação. Caso contrário, faça uma restauração a partir do backup.  
  
