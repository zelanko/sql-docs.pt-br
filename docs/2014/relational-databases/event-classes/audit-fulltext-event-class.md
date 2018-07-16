---
title: Classe de evento Audit Fulltext | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 95e4c5fd-e16f-446e-b42b-105495a8f39a
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dbd6822239b33e2d0e89dbbd6c062437cb3a68fc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37283472"
---
# <a name="audit-fulltext-event-class"></a>Classe de evento Audit Fulltext
  A classe de evento **Audit Fulltext** ocorre quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se conecta e se comunica com o processo de daemon de filtro de texto completo.  
  
## <a name="audit-fulltext-event-class-data-columns"></a>Colunas de dados da classe de evento Audit Fulltext  
  
|Nome da coluna de dados|Tipo de dados|Description|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**Erro**|**int**|O número de erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , se esse evento informar um erro.|31|Sim|  
|**EventSequence**|**int**|A sequência de determinado evento dentro da solicitação.|51|não|  
|**EventSubClass**|**int**|Tipo de conexão usado pelo logon. 1 = Não em pool, 2 = Em pool.|21|Sim|  
|**IsSystem**|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|**SessionLoginName**|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, o **SessionLoginName** mostrará o Logon1 e o **LoginName** mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|**SPID**|**int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|**StartTime**|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
|**Êxito**|**int**|1 = êxito. 0 = falha. Por exemplo, o valor 1 indica êxito em uma verificação de permissões e o valor 0 indica falha nessa verificação.|23|Sim|  
|**TargetLoginName**|**int**|Para ações direcionadas a um logon (por exemplo, adição de um novo logon), o nome do logon de destino.|42|Sim|  
|**TargetLoginSid**|**int**|Para ações direcionadas a um logon (por exemplo, adição de um novo logon), o SID (número de ID de segurança) do logon de destino.|43|Sim|  
|**TextData**|**ntext**|Informações sobre o evento de texto completo. Normalmente este campo fornece informações sobre a conexão entre o processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o processo de daemon de filtro de texto completo|1|Sim|  
  
## <a name="see-also"></a>Consulte também  
 [Eventos estendidos](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
