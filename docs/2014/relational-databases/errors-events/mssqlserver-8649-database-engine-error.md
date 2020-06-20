---
title: MSSQLSERVER_8649 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 8649 (Database Engine error)
ms.assetid: 992dbc74-7c3a-498b-9f1b-b28387640677
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b39ed0d8ffe5f7f601b6cb1393596d0d6546e557
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85031779"
---
# <a name="mssqlserver_8649"></a>MSSQLSERVER_8649
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|8649|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|COST_TOO_HIGH|  
|Texto da mensagem|A consulta foi cancelada porque seu custo estimado (%d) excede o limite configurado de %d. Contate o administrador do sistema.|  
  
## <a name="explanation"></a>Explicação  
 A consulta foi cancelada porque seu custo estimado excede o limite configurado para QUERY_GOVERNOR_COST_LIMIT.  
  
## <a name="user-action"></a>Ação do usuário  
 Defina a opção QUERY_GOVERNOR_COST_LIMIT com um valor mais alto.  
  
## <a name="see-also"></a>Consulte Também  
 [SET QUERY_GOVERNOR_COST_LIMIT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-query-governor-cost-limit-transact-sql)  
  
  
