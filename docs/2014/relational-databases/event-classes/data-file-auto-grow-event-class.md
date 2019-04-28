---
title: Classe de evento Data File Auto Grow | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Data File Auto Grow event class
ms.assetid: 63701c20-7886-454a-936f-7aea9d042cf7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8d08322000a92c3870f410652b728de0fc844104
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62663176"
---
# <a name="data-file-auto-grow-event-class"></a>classe de evento Data File Auto Grow
  A classe de evento **Data File Auto Grow** indica que o arquivo de dados pode se expandir automaticamente. Esse evento não será acionado se o arquivo de dados crescer explicitamente devido a uma instrução ALTER DATABASE.  
  
 Inclua a classe de evento **Data File Auto Grow** nos rastreamentos que monitoram o crescimento do arquivo de dados.  
  
 Quando a classe de evento **Data File Auto Grow** é incluída no rastreamento, a quantidade de sobrecarga incorrida é baixa, a menos que o arquivo de dados tenha crescimento automático frequentemente.  
  
## <a name="data-file-auto-grow-event-class-data-columns"></a>Colunas de dados da classe de evento Data File Auto Grow  
  
|Nome da coluna de dados|Tipo de dados|Descrição|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|Nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|**ClientProcessID**|**int**|ID atribuída pelo computador host ao processo em que o aplicativo cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer a ID de processo do cliente.|9|Sim|  
|**DatabaseID**|**int**|ID do banco de dados especificado pela instrução USE de *database* ou o banco de dados padrão se nenhuma instrução USE de *database* tiver sido emitida para uma determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados **ServerName** for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|**DatabaseName**|**nvarchar**|Nome do banco de dados no qual a instrução do usuário está sendo executada.|35|Sim|  
|**Duration**|**bigint**|Tempo (em milissegundos) necessário para estender o arquivo.|13|Sim|  
|**EndTime**|**datetime**|Hora de término do crescimento automático do arquivo de dados.|18|Sim|  
|**EventClass**|**int**|Tipo de evento = 92.|27|Não|  
|**EventSequence**|**int**|Sequência da classe de evento **CursorClose** no lote.|51|Não|  
|**Filename**|**nvarchar**|Nome lógico do arquivo que está sendo estendido.|36|Sim|  
|**HostName**|**nvarchar**|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer o nome do host. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|**IntegerData**|**int**|Número de páginas de 8 quilobytes (KB) em que o arquivo aumentou.|25|Sim|  
|**IsSystem**|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|**LoginName**|**nvarchar**|Nome de logon do usuário (logon de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou as credenciais de logon do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows no formato DOMÍNIO\Nomedeusuário).|11|Sim|  
|**LoginSid**|**image**|SID (identificador de segurança) do usuário que fez logon. Você pode encontrar essas informações na exibição de catálogo **sys.server_principals** . Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|**NTDomainName**|**nvarchar**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|**ServerName**|**nvarchar**|Nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|Não|  
|**SessionLoginName**|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, o **SessionLoginName** mostrará o Logon1 e o **LoginName** mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|**SPID**|**Int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|**StartTime**|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
  
## <a name="see-also"></a>Consulte também  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
