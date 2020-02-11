---
title: Classe de evento Degree of Parallelism (7.0 Insert) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Degree of Parallelism event class
ms.assetid: 6753ef30-890f-47a3-b0b6-8abb184e1d83
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 56a87741b104a49f98a3cba05dc65d911774774d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62662894"
---
# <a name="degree-of-parallelism-70-insert-event-class"></a>Classe de evento Degree of Parallelism (7.0 Insert)
  A classe de evento **Degree of Parallelism (7.0 Insert)** ocorre sempre que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa uma instrução SELECT, INSERT, UPDATE ou DELETE.  
  
 Quando a classe de evento for incluída em um rastreamento, a quantidade de sobrecarga pode impedir o desempenho se esses eventos ocorrem com frequência. Para minimizar a sobrecarga, limite o uso desta classe de evento em rastreamentos que monitoram brevemente problemas específicos.  
  
## <a name="degree-of-parallelism-70-insert-event-class-data-columns"></a>Colunas de dados de classe de evento Degree of Parallelism (7.0 Insert)  
  
|Nome da coluna de dados|Tipo de dados|DESCRIÇÃO|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|Nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|**BinaryData**|**imagem**|Número de CPUs usadas para completar o processo com base nos seguintes valores:<br /><br /> 0x00000000: indica um plano serial em execução em série.<br /><br /> 0x01000000 indica um plano paralelo em execução em série.<br /><br /> >= 0x02000000: indica um plano paralelo em execução em paralelo.|2|Não|  
|**ClientProcessID**|**int**|ID atribuída pelo computador host ao processo em que o aplicativo cliente está sendo executado. Essa coluna de dados será populada se a ID do processo do cliente for fornecida pelo cliente.|9|Sim|  
|**DatabaseID**|**int**|ID do banco de dados especificado pela instrução de banco de dados USE ou o banco de dados padrão se nenhuma instrução de banco de dados USE tiver sido emitida para uma determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados **ServerName** for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|**DatabaseName**|**nvarchar**|Nome do banco de dados no qual a instrução do usuário está sendo executada.|35|Sim|  
|**Event Class**|**int**|Tipo de evento = 28.|27|Não|  
|**EventSequence**|**int**|Sequência de um determinado evento na solicitação.|51|Não|  
|**EventSubClass**|**int**|Indica a instrução executada, com base nos seguintes valores:<br /><br /> 1= Selecionar<br /><br /> 2 = Inserir<br /><br /> 3 = Atualização<br /><br /> 4 = Excluir|21|Não|  
|**GroupID**|**int**|ID do grupo de carga de trabalho no qual o evento de Rastreamento do SQL dispara.|66|Sim|  
|**HostName**|**nvarchar**|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o nome do host for fornecido pelo cliente. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|**Integer Data**|**int**|A quantidade de “memória de workspace", em kilobyte, que foi concedida à consulta para executar operações envolvendo operações de hash, classificação ou criação de índice. A memória será adquirida durante execução conforme seja necessária.|25|Sim|  
|**IsSystem**|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|**LoginName**|**nvarchar**|Nome de logon do usuário (logon de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou as credenciais de logon do Windows na forma de DOMAIN\\*username*).|11|Sim|  
|**LoginSid**|**imagem**|Número SID (identificação de segurança) do usuário que fez logon. Você pode encontrar essas informações na exibição de catálogo sys.server_principals. Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|**NTDomainName**|**nvarchar**|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|**NTUserName**|**nvarchar**|Nome do usuário do Windows.|6|Sim|  
|**RequestID**|**int**|Solicite a identificação que iniciou a consulta de texto completo.|49|Sim|  
|**ServerName**|**nvarchar**|Nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|Não|  
|**SessionLoginName**|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, o **SessionLoginName** mostrará o Logon1 e o **LoginName** mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|**SPID**|**int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|**StartTime**|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
|**TransactionID**|**bigint**|ID da transação atribuída pelo sistema.|4|Sim|  
  
## <a name="see-also"></a>Consulte Também  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)  
  
  
