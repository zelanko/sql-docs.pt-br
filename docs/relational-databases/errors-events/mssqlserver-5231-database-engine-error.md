---
title: MSSQLSERVER_5231 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 5231 (Database Engine error)
ms.assetid: 6954ae84-ed0b-4f4c-9d0a-e73f3d71476c
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e79aaa4a74d7beac5ae64e6f6f231c7db15f4519
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
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
|Texto da mensagem|ID do objeto O_ID (objeto 'NAME'): ocorreu um deadlock ao tentar bloquear este objeto para verificação. Esse objeto foi ignorado e não será processado.|  
  
## <a name="explanation"></a>Explicação  
Ocorreu um deadlock quando DBCC estava tentando bloquear o objeto, e DBCC foi escolhido como vítima do deadlock. O objeto não será processado.  
  
## <a name="user-action"></a>Ação do usuário  
Nenhum  
  
