---
title: Classe de evento CursorImplicitConversion | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- CursorImplicitConversion event class
ms.assetid: 44d12e23-146a-42e6-bb38-1f2f6a035bad
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 864e47e72809a4fe5151ee5b252a3ea99fb3a451
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39547336"
---
# <a name="cursorimplicitconversion-event-class"></a>classe de evento CursorImplicitConversion
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  A classe de evento **CursorImplicitConversion** descreve eventos de conversão cursor-implícitos que acontecem em interfaces de programação de aplicativo (APIs) ou cursores [!INCLUDE[tsql](../../includes/tsql-md.md)] . Eventos de conversão cursor-implícitos ocorrem quando [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] executa uma instrução Transact-SQL que não é suportada por cursores de servidor do tipo solicitado. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] retorna um erro que indica que o tipo de cursor foi alterado.  
  
 Inclua a classe de evento **CursorImplicitConversion** em rastreamentos que estão registrando o desempenho de cursores.  
  
 Quando essa classe de evento é incluída em um rastreamento, a quantidade de sobrecarga criada depende da frequência com que os cursores que exigem conversão implícita são usados em relação ao banco de dados durante o rastreamento. Se os cursores forem usados extensivamente, o rastreamento poderá diminuir significativamente o desempenho.  
  
## <a name="cursorimplicitconversion-event-class-data-columns"></a>Colunas de dados de classe de evento CursorImplicitConversion  
  
|Nome da coluna de dados|Tipo de dados|Descrição|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|Nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|**BinaryData**|**imagem**|Tipo de cursor resultante. Os valores são:<br /><br /> 1 = Keyset<br /><br /> 2 = Dinâmico<br /><br /> 4 = Somente avanço<br /><br /> 8 = Estático<br /><br /> 16 = De avanço rápido|2|Sim|  
|**ClientProcessID**|**int**|ID atribuída pelo computador host ao processo em que o aplicativo cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer a ID de processo do cliente.|9|Sim|  
|**DatabaseID**|**int**|A ID do banco de dados especificada pela instrução USE *database* ou a ID do banco de dados padrão se nenhuma instrução USE *database*tiver sido emitida para determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados **ServerName** for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|**DatabaseName**|**nvarchar**|Nome do banco de dados no qual a instrução do usuário está sendo executada.|35|Sim|  
|**EventClass**|**int**|Tipo de evento registrado = 76.|27|não|  
|**EventSequence**|**int**|Sequência da classe de evento **CursorClose** no lote.|51|não|  
|**GroupID**|**int**|ID do grupo de carga de trabalho no qual o evento de Rastreamento do SQL dispara.|66|Sim|  
|**Handle**|**int**|Identificador do objeto mencionado no evento.|33|Sim|  
|**HostName**|**nvarchar**|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer o nome do host. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|**IntegerData**|**int**|Tipo de cursor solicitado. Os valores são:<br /><br /> 1 = Keyset<br /><br /> 2 = Dinâmico<br /><br /> 4 = Somente avanço<br /><br /> 8 = Estático<br /><br /> 16 = De avanço rápido|25|não|  
|**IsSystem**|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|**LoginName**|**nvarchar**|Nome de logon do usuário (logon de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou as credenciais de logon do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows no formato DOMÍNIO/nomedousuário).|11|Sim|  
|**LoginSid**|**imagem**|SID (identificador de segurança) do usuário que fez logon. Você pode encontrar essas informações na exibição de catálogo **sys.server_principals** . Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|**NTDomainName**|**nvarchar**|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|**NTUserName**|**nvarchar**|Nome do usuário do Windows.|6|Sim|  
|**RequestID**|**int**|Solicitar identificador da conversão implícita.|49|Sim|  
|**ServerName**|**nvarchar**|Nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|não|  
|**SessionLoginName**|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, o **SessionLoginName** mostrará o Logon1 e o **LoginName** mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|**SPID**|**int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|**StartTime**|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
|**TransactionID**|**bigint**|ID da transação atribuída pelo sistema.|4|Sim|  
|**XactSequence**|**bigint**|Token que descreve a transação atual.|50|Sim|  
  
## <a name="see-also"></a>Consulte Também  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
