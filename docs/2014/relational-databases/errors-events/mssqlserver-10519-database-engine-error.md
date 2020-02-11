---
title: MSSQLSERVER_10519 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10519 (Database Engine error)
ms.assetid: 3be393a1-b186-41ae-afb9-a3d07ff354bb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6bb9c6f7fddc9ba0d4430b42ba5472a59c29e3cf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62916231"
---
# <a name="mssqlserver_10519"></a>MSSQLSERVER_10519
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|10519|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|PG_INCOMPATIBLE_STMT_AND_HINTS|  
|Texto da mensagem|Não é possível criar o guia de plano '%.\*ls' porque as dicas especificadas em `@hints` não podem ser aplicadas à instrução especificada por `@stmt` ou `@statement_start_offset`. Verifique se as dicas podem ser aplicadas à instrução.|  
  
## <a name="explanation"></a>Explicação  
 Não é possível aplicar as dicas especificadas em `@hints` à instrução especificada por `@stmt` ou `@statement_start_offset`.  
  
## <a name="user-action"></a>Ação do usuário  
 Especifique dicas que possam ser aplicadas à instrução.  
  
## <a name="see-also"></a>Consulte Também  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [Guias de plano](../performance/plan-guides.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
