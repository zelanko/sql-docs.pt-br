---
title: Classe de evento QN:Template | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: event-classes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- event classes [SQL Server], QN:Template
ms.assetid: 9f752040-5901-42e1-8fdc-105528d9960a
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 343f80e278b2974afa2b252bab97bcb124de0799
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="qntemplate-event-class"></a>Classe de evento QN:Template
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  O evento QN:Template fornece informações sobre o uso interno de modelos de consulta. Os modelos de consulta são o mecanismo que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] usa para compartilhar definições de uma consulta para notificação. Esses modelos são criados junto com tabelas de parâmetros. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] cria um evento desse tipo quando um modelo de consulta é criado, usado ou destruído.  
  
## <a name="qntemplate-event-class-data-columns"></a>Coluna de dados de classe de evento QN:Template  
  
|Coluna de dados|Tipo|Description|Número da coluna|Filtrável|  
|-----------------|----------|-----------------|-------------------|----------------|  
|ApplicationName|**nvarchar**|O nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|ClientProcessID|**int**|A ID atribuída pelo computador host ao processo em que está sendo executado o aplicativo cliente. Essa coluna de dados será populada se a ID do processo do cliente for fornecida pelo cliente.|9|Sim|  
|DatabaseID|**int**|A ID do banco de dados especificada pela instrução de *banco de dados* USE ou a ID do banco de dados padrão se nenhuma instrução de *banco de dados*USE tiver sido emitida para determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados Server Name for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|DatabaseName|**nvarchar**|O nome do banco de dados no qual a instrução do usuário está sendo executada.|35|Sim|  
|EventClass|**int**|Tipo de evento = 201.|27|não|  
|EventSequence|**int**|Número de sequência para esse evento.|51|não|  
|EventSubClass|**nvarchar**|O tipo de subclasse de evento, fornecendo mais informações sobre cada classe de evento. Essa coluna pode conter os seguintes valores:<br /><br /> Modelo criado: indica que um modelo de notificação de consulta foi criado no banco de dados.<br /><br /> Modelo encontrado: indica quando um modelo de notificação de consulta é reutilizado.<br /><br /> Modelo descartado: indica quando um modelo de notificação de consulta é removido do banco de dados.|21|Sim|  
|GroupID|**int**|ID do grupo de carga de trabalho no qual o evento de Rastreamento do SQL dispara.|66|Sim|  
|HostName|**nvarchar**|O nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o nome do host for fornecido pelo cliente. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|IsSystem|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário.<br /><br /> 0 = usuário<br /><br /> 1 = sistema|60|não|  
|LoginName|**nvarchar**|O nome do logon do usuário (logon de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou as credenciais de logon do Windows na forma de *DOMAIN\Username*).|11|não|  
|LoginSID|**imagem**|Número SID (identificação de segurança) do usuário que fez logon. Você pode encontrar essas informações na exibição de catálogo sys.server_principals. Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|NTDomainName|**nvarchar**|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|NTUserName|**nvarchar**|O nome do usuário proprietário da conexão que gerou este evento.|6|Sim|  
|RequestID|**int**|Identificador da solicitação que contém a instrução.|49|Sim|  
|ServerName|**nvarchar**|O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|não|  
|SessionLoginName|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, se um aplicativo se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando Logon1 e executar uma instrução como Logon2, o SessionLoginName mostrará "Logon1" e LoginName mostrará "Logon2". Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|SPID|**int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|StartTime|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
|TextData|**ntext**|Retorna um documento XML que contém informações específicas para esse evento. Esse documento está de acordo com o esquema XML disponível na página [SQL Server Query Notification Profiler Event Schema](http://go.microsoft.com/fwlink/?LinkId=63331) .|1|Sim|  
  
  
