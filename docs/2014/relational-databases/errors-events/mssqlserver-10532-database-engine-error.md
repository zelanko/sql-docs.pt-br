---
title: MSSQLSERVER_10532 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10532 (Database Engine error)
ms.assetid: 01da29ee-bf67-433f-8148-587a7e8d1d76
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cda3117df524ba90f322bbb99d6db98ee989ab71
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62870625"
---
# <a name="mssqlserver_10532"></a>MSSQLSERVER_10532
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|10532|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|PG_NO_ELIGIBLE_STMT|  
|Texto da mensagem|Não é possível criar o guia de plano '%.\*ls' porque o lote ou o módulo especificado por `@plan_handle` não contém uma instrução qualificada para um guia de plano. Especifique outro valor para `@plan_handle`.|  
  
## <a name="explanation"></a>Explicação  
 O lote ou o módulo especificado por `@plan_handle` não contém uma instrução qualificada para um guia de plano.  
  
## <a name="user-action"></a>Ação do usuário  
 Especifique outro valor para `@plan_handle`.  
  
## <a name="see-also"></a>Consulte Também  
 [Guias de plano](../performance/plan-guides.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
