---
title: Classe de evento Deadlock Graph | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Deadlock Graph event class
ms.assetid: 20f92233-c912-4382-8993-8e2e23d03fbe
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 741fb8ac694568911c1b2b5def7bd07a8c86e8ec
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52782548"
---
# <a name="deadlock-graph-event-class"></a>Classe de evento Deadlock Graph
  A classe de evento **Deadlock Graph** fornece uma descrição XML de um deadlock. Essa classe ocorre simultaneamente com a classe de evento **Lock:Deadlock** .  
  
## <a name="deadlock-graph-event-class-data-columns"></a>Colunas de dados de classe de evento Deadlock Graph  
  
|Nome da coluna de dados|Tipo de dados|Descrição|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**EventClass**|**int**|Tipo de evento = 148.|27|Não|  
|**EventSequence**|**int**|Sequência de um determinado evento na solicitação.|51|Não|  
|**IsSystem**|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário. Esse valor é sempre 1 para esse evento.|60|Sim|  
|**LoginName**|**nvarchar**|Nome de logon do usuário (logon de segurança do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou as credenciais de logon do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows na forma DOMAIN\username). Esse valor sempre é o usuário do sistema para esse evento.|11|Sim|  
|**LoginSid**|**image**|Número SID (identificação de segurança) do usuário que fez logon. Você pode encontrar essas informações na exibição de catálogo sys.server_principals. Cada SID é exclusivo para cada logon no servidor. Esse valor é sempre o SID do usuário do sistema para esse evento.|41|Sim|  
|**ServerName**|**nvarchar**|Nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|Não|  
|**SessionLoginName**|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, o **SessionLoginName** mostrará o Logon1 e o **LoginName** mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|**SPID**|**int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|**StartTime**|**datetime**|Hora na qual o deadlock foi detectado.|14|Sim|  
|**TextData**|**ntext**|Descrição XML do deadlock.|1|Sim|  
|**TransactionID**|**bigint**|Não usado.|4|Sim|  
  
## <a name="see-also"></a>Consulte também  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Classe de evento Lock:Deadlock](lock-deadlock-event-class.md)  
  
  
