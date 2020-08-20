---
description: classe de evento Trace File Close
title: Classe de evento Trace File Close | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Trace File Close event class
ms.assetid: 128b7bac-cb64-43e7-ae9b-87b7d2ebb4ef
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d4e3dc2071abd0b8ce81662bc5075fa056bf4bb9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470605"
---
# <a name="trace-file-close-event-class"></a>classe de evento Trace File Close
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
   A classe de evento **Trace File Close** indica que um arquivo de rastreamento foi fechado durante a substituição de um arquivo de rastreamento.  
  
## <a name="trace-file-close-event-class-data-columns"></a>Colunas de dados de classe do evento Trace File Close  
  
|Nome da coluna de dados|Tipo de dados|Descrição|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**EventClass**|**int**|Tipo de evento = 150.|27|Não|  
|**EventSequence**|**int**|O carimbo de data e hora exclusivo do evento disparado no rastreamento. Este número aumenta de uma unidade a cada evento disparado.|51|Não|  
|**FileName**|**nvarchar**|O nome lógico do arquivo de rastreamento que está sendo fechado.|36|Sim|  
|**IsSystem**|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, NULL = usuário. O valor sempre é 1 para esta classe de evento.|60|Sim|  
|**LoginName**|**nvarchar**|Nome de logon do usuário (logon de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou as credenciais de logon do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows no formato DOMÍNIO/nomedousuário). O valor sempre é "sa" para esta classe de evento.|11|Sim|  
|**ObjectID**|**int**|ID do rastreamento, atribuída pelo sistema.|22|Sim|  
|**ServerName**|**nvarchar**|Nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|Não|  
|**SessionLoginName**|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, o **SessionLoginName** mostrará o Logon1 e o **LoginName** mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|**SPID**|**int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|**StartTime**|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
  
## <a name="see-also"></a>Consulte Também  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
