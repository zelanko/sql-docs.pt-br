---
title: MSSQLSERVER_5231 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5231 (Database Engine error)
ms.assetid: 6954ae84-ed0b-4f4c-9d0a-e73f3d71476c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6c57150dd8fac6dab1c2c9cf6fdf7cefbdb1b5f8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62913575"
---
# <a name="mssqlserver5231"></a>MSSQLSERVER_5231
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|5231|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC4_DEADLOCK_SKIPPED_OBJECT|  
|Texto da mensagem|ID de objeto O_ID (objeto 'NAME'): Ocorreu um deadlock ao tentar bloquear este objeto para verificação. Esse objeto foi ignorado e não será processado.|  
  
## <a name="explanation"></a>Explicação  
Ocorreu um deadlock quando DBCC estava tentando bloquear o objeto, e DBCC foi escolhido como vítima do deadlock. O objeto não será processado.  
  
## <a name="user-action"></a>Ação do usuário  
None  
  
