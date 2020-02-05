---
title: MSSQLSERVER_8649 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8649 (Database Engine error)
ms.assetid: 992dbc74-7c3a-498b-9f1b-b28387640677
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 39d3edc1b85dba6c223cc4b4e5b3d3250b48d489
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68132287"
---
# <a name="mssqlserver_8649"></a>MSSQLSERVER_8649
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
[SET QUERY_GOVERNOR_COST_LIMIT &#40;Transact-SQL&#41;](~/t-sql/statements/set-query-governor-cost-limit-transact-sql.md)  
  
