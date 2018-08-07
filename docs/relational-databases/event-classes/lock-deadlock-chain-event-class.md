---
title: Classe de evento Lock:Deadlock Chain | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Deadlock Chain event class
ms.assetid: 9883127b-aa34-4235-88cc-c161cd2112cc
caps.latest.revision: 35
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: db5a4b43cfed4523af9a56df5a709ce8de0d46a6
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39565210"
---
# <a name="lockdeadlock-chain-event-class"></a>Classe de evento Lock:Deadlock Chain
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A classe de evento de Lock:Deadlock Chain é produzida para cada participante em um deadlock.  
  
 Use a classe de evento Lock:Deadlock Chain para monitorar quando as condições deadlock acontecem. Essas informações são úteis para determinar se os deadlocks estão afetando significativamente o desempenho de seu aplicativo e quais são os objetos envolvidos. Você pode examinar o código de aplicativo que modifica estes objetos para determinar se podem ser efetuadas alterações para minimizar os deadlocks.  
  
## <a name="lockdeadlock-chain-event-class-data-columns"></a>Colunas de dados de classe de evento Lock:Deadlock Chain  
  
|Nome da coluna de dados|Tipo de dados|Descrição|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|BinaryData|**imagem**|Identificador de recurso bloqueado.|2|Sim|  
|DatabaseID|**int**|ID do banco de dados ao qual esse recurso pertence. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados ServerName for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|DatabaseName|**nvarchar**|Nome do banco de dados ao qual o recurso pertence.|35|Sim|  
|EventClass|**int**|Tipo de evento = 59.|27|não|  
|EventSequence|**int**|Sequência de um determinado evento na solicitação.|51|não|  
|EventSubClass|**int**|Tipo de subclasse de evento.<br /><br /> 101=Bloqueio do tipo de recurso<br /><br /> 102=Troca do tipo de recurso|21|Sim|  
|IntegerData|**int**|Número de deadlock. Números são atribuídos, começando com 0 quando o servidor é iniciado e incrementados para cada bloqueio.|25|Sim|  
|IntegerData2|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|55|Sim|  
|IsSystem|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|LoginSid|**imagem**|Número SID (identificação de segurança) do usuário que fez logon. Você pode encontrar essas informações na exibição de catálogo sys.server_principals. Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|Modo|**int**|0=NULL - Compatível com todos os outros modos de bloqueio (LCK_M_NL)<br /><br /> 1=Bloqueio de estabilidade do esquema (LCK_M_SCH_S)<br /><br /> 2=Bloqueio de modificação de esquema (LCK_M_SCH_M)<br /><br /> 3=Bloqueio compartilhado (LCK_M_S)<br /><br /> 4=Bloqueio de atualização (LCK_M_U)<br /><br /> 5=Bloqueio exclusivo (LCK_M_X)<br /><br /> 6=Bloqueio de tentativa compartilhada (LCK_M_IS)<br /><br /> 7=Bloqueio de atualização da tentativa (LCK_M_IU)<br /><br /> 8=Bloqueio exclusivo da tentativa (LCK_M_IX)<br /><br /> 9=Compartilhado com tentativa de atualizar (LCK_M_SIU)<br /><br /> 10=Compartilhado com tentativa exclusiva (LCK_M_SIX)<br /><br /> 11=Atualizar com tentativa exclusiva (LCK_M_UIX)<br /><br /> 12=Bloqueio de atualização em massa (LCK_M_BU)<br /><br /> 13=Intervalo de chaves compartilhado/compartilhado (LCK_M_RS_S)<br /><br /> 14=Intervalo de chaves compartilhado/atualizar (LCK_M_RS_U)<br /><br /> 15=Inserção de Intervalo de Chaves NULL (LCK_M_RI_NL)<br /><br /> 16=Inserção de Intervalo de Chaves Compartilhado (LCK_M_RI_S)<br /><br /> 17=Atualização de Inserção de Intervalo de Chaves (LCK_M_RI_S)<br /><br /> 18=Inserção de intervalo de chaves exclusivo (LCK_M_RI_X)<br /><br /> 19=Intervalo de chaves compartilhado exclusivo (LCK_M_RX_S)<br /><br /> 20=Atualização de intervalo de chaves exclusivo (LCK_M_RX_U)<br /><br /> 21=Intervalo de chaves exclusivo exclusivo (LCK_M_RX_X)|32|Sim|  
|ObjectID|**int**|ID do objeto que foi bloqueado, se disponível e aplicável.|22|Sim|  
|ObjectID2|**bigint**|ID do objeto ou entidade relacionada, se disponível e aplicável.|56|Sim|  
|OwnerID|**int**|1=TRANSACTION<br /><br /> 2=CURSOR<br /><br /> 3=SESSION<br /><br /> 4=SHARED_TRANSACTION_WORKSPACE<br /><br /> 5=EXCLUSIVE_TRANSACTION_WORKSPACE|58|Sim|  
|RequestID|**int**|ID da solicitação que contém a instrução.|49|Sim|  
|ServerName|**nvarchar**|Nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|não|  
|SessionLoginName|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, ao se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, SessionLoginName mostrará o Logon1 e LoginName mostrará o Logon2. Esta coluna exibe os logons do Windows [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[msCoName](../../includes/msconame-md.md)] .|64|Sim|  
|SPID|**int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|StartTime|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
|TextData|**ntext**|Valor de texto dependente do tipo de recurso.|1|Sim|  
|TransactionID|**bigint**|ID da transação atribuída pelo sistema.|4|Sim|  
|Tipo|**int**|1=NULL_RESOURCE<br /><br /> 2=DATABASE<br /><br /> 3=FILE<br /><br /> 5=OBJECT<br /><br /> 6=PAGE<br /><br /> 7=KEY<br /><br /> 8=EXTENT<br /><br /> 9=RID<br /><br /> 10=APPLICATION<br /><br /> 11=METADATA<br /><br /> 12=AUTONAMEDB<br /><br /> 13=HOBT<br /><br /> 14=ALLOCATION_UNIT|57|Sim|  
  
## <a name="see-also"></a>Consulte Também  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sys.dm_tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)  
  
  
