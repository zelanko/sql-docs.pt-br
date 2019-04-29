---
title: MSSQLSERVER_10531 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10531 (Database Engine error)
ms.assetid: bb40e994-231c-44ce-933f-8d767fb2f450
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7324979238eda7f3ee63a709c199878350edb82d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62916193"
---
# <a name="mssqlserver10531"></a>MSSQLSERVER_10531
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|10531|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|PG_NO_ELIGIBLE_STMT|  
|Texto da mensagem|Não é possível criar o guia de plano '%.*ls' do cache porque o usuário não tem as permissões adequadas. Conceda a permissão VIEW SERVER STATE para o usuário que está criando o guia de plano.|  
  
## <a name="explanation"></a>Explicação  
 O usuário não tem as permissões adequadas para criar o guia de plano especificado a partir do cache de planos.  
  
## <a name="user-action"></a>Ação do usuário  
 Conceda a permissão VIEW SERVER STATE ao usuário que está criando o guia de plano.  
  
## <a name="see-also"></a>Consulte também  
 [Guias de plano](../performance/plan-guides.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
