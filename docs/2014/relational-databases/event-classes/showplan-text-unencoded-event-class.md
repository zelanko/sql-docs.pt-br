---
title: Classe de evento Showplan Text (Unencoded) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Showplan Text (Unencoded) event class
ms.assetid: 0aad4563-8caf-4971-92af-55992bc5ff2c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bd9f8c6ca62fdd9f9a856a19f3d27c2144073b52
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52801258"
---
# <a name="showplan-text-unencoded-event-class"></a>classe de evento Showplan Text (Unencoded)
  A classe de evento Showplan Text (Sem-Codificação) ocorre quando o [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa uma instrução SQL. Essa classe de evento é a mesma que a classe de evento Showplan Text, exceto pelo fato de que as informações do evento são formatadas como uma cadeia de caracteres ao invés de dados binários.  
  
 As informações incluídas são um subconjunto das informações disponíveis nas classes de evento Showplan All, Showplan XML ou Showplan XML Statistics Profile.  
  
 Quando a classe de evento Showplan Text (Unencoded) estiver incluída em um rastreamento, a quantidade de sobrecarga poderá impedir o desempenho de forma significativa. Showplan Text (Unencoded) não incorrerá em tanta sobrecarga  quanto outras classes de evento Showplan. Para minimizar a sobrecarga incorrida, limite o uso desta classe de evento a rastreamentos que monitorem problemas específicos em períodos breves de tempo.  
  
## <a name="showplan-text-unencoded-event-class-data-columns"></a>Colunas de dados da classe de evento de plano de execução (Unencoded)  
  
|Nome da coluna de dados|Tipo de dados|Descrição|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|BinaryData|`image`|Valor binário dependente da classe de evento capturada no rastreamento.|2|Sim|  
|ClientProcessID|`int`|ID atribuída pelo computador host ao processo em que o aplicativo cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer a ID de processo do cliente.|9|Sim|  
|DatabaseID|`int`|ID do banco de dados especificado pela instrução USE de *database* ou o banco de dados padrão se nenhuma instrução USE de *database* tiver sido emitida para uma determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados ServerName for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|DatabaseName|`nvarchar`|Nome do banco de dados no qual a instrução do usuário está sendo executada.|35|Sim|  
|EventClass|`int`|Tipo de evento = 68.|27|Não|  
|EventSequence|`int`|Sequência de um determinado evento na solicitação.|51|Não|  
|GroupID|`int`|ID do grupo de carga de trabalho no qual o evento de Rastreamento do SQL dispara.|66|Sim|  
|HostName|`nvarchar`|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer o nome do host. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|IntegerData|`int`|O valor inteiro dependente da classe de evento capturada no rastreamento.|25|Sim|  
|IsSystem|`int`|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|LineNumber|`int`|Exibe o número da linha que contém o erro.|5|Sim|  
|LoginName|`nvarchar`|Nome de logon do usuário (logon de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou as credenciais de logon do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows no formato DOMÍNIO/nomedousuário).|11|Sim|  
|LoginSid|`image`|Número SID (identificação de segurança) do usuário que fez logon. Você pode encontrar essas informações na exibição de catálogo sys.server_principals. Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|NestLevel|`int`|Inteiro que representa os dados retornados por @@NESTLEVEL.|29|Sim|  
|NTDomainName|`nvarchar`|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|NTUserName|`nvarchar`|Nome do usuário do Windows.|6|Sim|  
|ObjectID|`int`|ID de objeto atribuída pelo sistema.|22|Sim|  
|ObjectName|`nvarchar`|Nome do objeto que está sendo referenciado.|34|Sim|  
|ObjectType|`int`|Valor que representa o tipo do objeto envolvido no evento. Esse valor corresponde à coluna do tipo na exibição do catálogo sys.objects. Para obter valores, consulte [Coluna de evento de rastreamento ObjectType](objecttype-trace-event-column.md).|28|Sim|  
|RequestID|`int`|ID da solicitação que contém a instrução.|49|Sim|  
|ServerName|`nvarchar`|Nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|Não|  
|SessionLoginName|`nvarchar`|Nome de logon do usuário que originou a sessão. Por exemplo, ao se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, SessionLoginName mostrará o Logon1 e LoginName mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|SPID|`int`|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|StartTime|`datetime`|Hora de início do evento, se disponível.|14|Sim|  
|TextData|`ntext`|Valor do texto dependente da classe de evento capturada no rastreamento.|1|Sim|  
|TransactionID|`bigint`|ID da transação atribuída pelo sistema.|4|Sim|  
|XactSequence|`bigint`|Token que descreve a transação atual.|50|Sim|  
  
## <a name="see-also"></a>Consulte também  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Referência de operadores físicos e lógicos de plano de execução](../showplan-logical-and-physical-operators-reference.md)   
 [Classe de evento Showplan All](showplan-all-event-class.md)   
 [Classe de evento Showplan XML](showplan-xml-event-class.md)   
 [Classe de evento Showplan XML Statistics Profile](showplan-xml-statistics-profile-event-class.md)  
  
  
