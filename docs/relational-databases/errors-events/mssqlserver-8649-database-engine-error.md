---
title: MSSQLSERVER_8649 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 8649 (Database Engine error)
ms.assetid: 992dbc74-7c3a-498b-9f1b-b28387640677
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4bea16bdc86c935da1b95adf52290234710e0b21
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver8649"></a>MSSQLSERVER_8649
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|8649|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|COST_TOO_HIGH|  
|Texto da mensagem|A consulta foi cancelada porque seu custo estimado (%d) excede o limite configurado de %d. Contate o administrador do sistema.|  
  
## <a name="explanation"></a>Explicação  
A consulta foi cancelada porque seu custo estimado excede o limite configurado para QUERY_GOVERNOR_COST_LIMIT.  
  
## <a name="user-action"></a>Ação do usuário  
Defina a opção QUERY_GOVERNOR_COST_LIMIT com um valor mais alto.  
  
## <a name="see-also"></a>Consulte também  
[SET QUERY_GOVERNOR_COST_LIMIT &#40;Transact-SQL&#41;](~/t-sql/statements/set-query-governor-cost-limit-transact-sql.md)  
  

