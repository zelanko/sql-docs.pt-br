---
title: Classe de evento Showplan XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
topic_type:
- apiref
helpviewer_keywords:
- Showplan XML event class
ms.assetid: 8e22de84-8890-414a-93e4-aebfaa057d7f
caps.latest.revision: 37
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7e0d3c58a594c9a857f7793feef6c228f9954f93
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019194"
---
# <a name="showplan-xml-event-class"></a>classe de evento Showplan XML
  A classe de evento Showplan XML ocorre quando o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa uma instrução SQL. Inclua a classe do evento Showplan XML para identificar os operadores de plano de execução. Essa classe de evento armazena cada evento como um documento XML bem definido.  
  
 Quando a classe de evento Showplan XML estiver incluída em um rastreamento, a quantidade de sobrecarga será um obstáculo significativo ao desempenho. O Showplan XML armazena um plano de consulta que é criado quando a consulta é otimizada. Para minimizar a sobrecarga gerada, limite o uso dessa classe de evento para rastreamentos que monitorem problemas específicos em breves períodos de tempo.  
  
 Os documentos Showplan XML têm um esquema associado a eles. Esse esquema pode ser encontrado no [Site da Microsoft](http://go.microsoft.com/fwlink/?LinkId=41740)ou como parte da instalação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="showplan-xml-event-class-data-columns"></a>Colunas de dados da classe de evento Showplan XML  
  
|Nome da coluna de dados|Tipo de dados|Description|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|Nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|BinaryData|`image`|Custo estimado da consulta.|2|não|  
|ClientProcessID|`int`|ID atribuída pelo computador host ao processo em que o aplicativo cliente está sendo executado. Essa coluna de dados será populada se a ID do processo do cliente for fornecida pelo cliente.|9|Sim|  
|DatabaseID|`int`|A ID do banco de dados especificada pela instrução USE *database* ou a ID do banco de dados padrão se nenhuma instrução USE *database*tiver sido emitida para determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados ServerName for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|DatabaseName|`nvarchar`|Nome do banco de dados.|35|não|  
|Event Class|`int`|Tipo de evento = 122.|27|não|  
|EventSequence|`int`|A sequência de determinado evento dentro da solicitação.|51|não|  
|GroupID|`int`|ID do grupo de carga de trabalho no qual o evento de Rastreamento do SQL dispara.|66|Sim|  
|HostName|`nvarchar`|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o nome do host for fornecido pelo cliente. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|Integer Data|`integer`|Número estimado de linhas retornadas.|25|Sim|  
|IsSystem|`int`|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|LineNumber|`int`|Exibe o número da linha que contém o erro.|5|Sim|  
|LoginName|`nvarchar`|Nome de logon do usuário (logon de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou as credenciais de logon do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows no formato DOMÍNIO/nomedousuário).|11|Sim|  
|LoginSID|`image`|Número SID (identificação de segurança) do usuário que fez logon. Você pode encontrar essas informações na exibição de catálogo sys.server_principals. Cada SID é exclusivo para cada logon no servidor.|41|não|  
|NestLevel|`int`|Inteiro que representa os dados retornados por @@NESTLEVEL.|29|Sim|  
|NTDomainName|`nvarchar`|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|ObjectID|`int`|ID de objeto atribuída pelo sistema.|22|Sim|  
|ObjectName|`nvarchar`|Nome do objeto que está sendo referenciado.|34|Sim|  
|ObjectType|`int`|Valor que representa o tipo do objeto envolvido no evento. Esse valor corresponde à coluna do tipo na exibição do catálogo sys.objects. Para obter valores, consulte [Coluna de evento de rastreamento ObjectType](objecttype-trace-event-column.md).|28|Sim|  
|RequestID|`int`|ID da solicitação que contém a instrução.|49|Sim|  
|ServerName|`nvarchar`|Nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|não|  
|SessionLoginName|`nvarchar`|Nome de logon do usuário que originou a sessão. Por exemplo, ao se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, SessionLoginName mostrará o Logon1 e LoginName mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|SPID|`int`|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|StartTime|`datetime`|Hora de início do evento, se disponível.|14|Sim|  
|TextData|`ntext`|Valor do texto dependente da classe de evento capturada no rastreamento.|1|Sim|  
|TransactionID|`bigint`|ID da transação atribuída pelo sistema.|4|Sim|  
|XactSequence|`bigint`|Token usado para descrever a transação atual.|50|Sim|  
  
## <a name="see-also"></a>Consulte também  
 [Eventos estendidos](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Referência de operadores físicos e lógicos de plano de execução](../showplan-logical-and-physical-operators-reference.md)  
  
  
