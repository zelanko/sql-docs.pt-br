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
manager: craigg
ms.openlocfilehash: 82867bf2346c69a5a30a8021c13fb64bf179607f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47682344"
---
# <a name="mssqlserver8649"></a>MSSQLSERVER_8649
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
## <a name="see-also"></a>Consulte Também  
[SET QUERY_GOVERNOR_COST_LIMIT &#40;Transact-SQL&#41;](~/t-sql/statements/set-query-governor-cost-limit-transact-sql.md)  
  
