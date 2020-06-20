---
title: Classe de evento Bitmap Warning | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Bitmap Warning event class
ms.assetid: 5bf9b4e3-0eba-4e67-8ba9-30ca4b48e1d4
author: stevestein
ms.author: sstein
ms.openlocfilehash: a59a1ecfc740cc7c3a07d8a41acfa51fb1623716
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85030732"
---
# <a name="bitmap-warning-event-class"></a>classe de evento Bitmap Warning
  A classe de evento **Bitmap Warning** pode ser usada para monitorar o uso de filtro de bitmap em consultas. A subclasse de evento pode ser usada para informar quando filtros de bitmap forem desabilitados em uma consulta.  
  
## <a name="bitmap-warning-event-class-data-columns"></a>Colunas de dados de classe de evento Bitmap Warning  
  
|Nome da coluna de dados|Tipo de dados|DESCRIÇÃO|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|`nvarchar`|Nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|**ClientProcessID**|`int`|ID atribuída pelo computador host ao processo em que o aplicativo cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer a ID de processo do cliente.|9|Sim|  
|**DatabaseID**|`int`|O identificador do banco de dados especificado pela instrução USE *database* ou o banco de dados padrão se nenhuma instrução USE *database* tiver sido emitida para determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados **ServerName** for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|**DatabaseName**|`nvarchar`|Nome do banco de dados no qual a instrução do usuário está sendo executada.|35|Sim|  
|**EventClass**|`int`|Tipo de evento = 212.|27|Não|  
|**EventSequence**|`int`|Sequência de um determinado evento na solicitação.|51|Não|  
|**EventSubClass**|`int`|Tipo de subclasse de evento. 0 = filtro de bitmap está desabilitado.|21|Sim|  
|**HostName**|`nvarchar`|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o nome do host for fornecido pelo cliente. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|**IsSystem**|`int`|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|**LoginName**|`nvarchar`|Nome do logon do usuário ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon de segurança do ou as credenciais de logon do Windows na forma de *domínio \ nomedeusuário*).|11|Sim|  
|**LoginSid**|`image`|Número SID (identificação de segurança) do usuário que fez logon. Você pode encontrar essas informações na exibição de catálogo **sys.server_principals** . Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|**NTDomainName**|`nvarchar`|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|**NTUserName**|`nvarchar`|Nome do usuário do Windows.|6|Sim|  
|**ObjectID**|`int`|ID do nó da raiz da equipe hash envolvida na repartição. Corresponde ao ID do nó no plano de execução.|22|Sim|  
|**RequestID**|`int`|O ID da solicitação que contém a instrução.|49|Sim|  
|**ServerName**|`nvarchar`|Nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|Não|  
|**SessionLoginName**|`nvarchar`|Nome de logon do usuário que originou a sessão. Por exemplo, se você se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando Login1 e executar uma instrução como Login2, **SessionLoginName** mostrará Login1 e **LoginName** mostrará Login2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|**SPID**|`int`|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|**StartTime**|`datetime`|Hora em que o evento foi iniciado, se disponível.|14|Sim|  
|**TransactionID**|`bigint`|ID da transação atribuída pelo sistema.|4|Sim|  
|**XactSequence**|`bigint`|Token que descreve a transação atual.|50|Sim|  
  
  
