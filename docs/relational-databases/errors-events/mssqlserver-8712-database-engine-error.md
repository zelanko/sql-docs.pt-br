---
title: MSSQLSERVER_8712 | Microsoft Docs
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
- 8712 (Database Engine error)
ms.assetid: 292fb3bc-062e-41e4-a566-b5d3d0b21977
caps.latest.revision: 12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fdd6aaa98a9a36ff46ef0580af3cf66a6baf594c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver8712"></a>MSSQLSERVER_8712
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|8712|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|USEPLAN_ERR_NO_INDEX|  
|Texto da mensagem|O índice '%.*ls', especificado na dica USE PLAN, não existe. Especifique um índice existente ou crie um índice com o nome especificado.|  
  
## <a name="explanation"></a>Explicação  
Um índice especificado na dica USE PLAN não existe.  
  
## <a name="user-action"></a>Ação do usuário  
Verifique se todos os índices que estão especificados na dica USE PLAN existem.  
  
## <a name="see-also"></a>Consulte Também  
[Query Hints &#40;Transact-SQL&#41; [Dicas de consulta (Transact-SQL)]](~/t-sql/queries/hints-transact-sql-query.md)  
[Guias de plano](~/relational-databases/performance/plan-guides.md)  
  
