---
title: Classe de evento QN:Dynamics | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- event classes [SQL Server], QN:Dynamics
ms.assetid: 3c1ffa0c-c9e5-40a6-a26b-28339f60ebc3
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6a27968b6c0e8b5d66d2e39870309bf75f2211b5
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
---
# <a name="qndynamics-event-class"></a>Classe de evento QN:Dynamics
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  A classe de evento QN:Dynamics fornece informações sobre a atividade de segundo plano que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] executa para dar suporte a notificações de consulta. Dentro do [!INCLUDE[ssDE](../../includes/ssde-md.md)], um thread em segundo plano monitora tempos-limite de assinatura, assinaturas pendentes a serem acionadas e destruição de tabela de parâmetros.  
  
## <a name="qndynamics-event-class-data-columns"></a>Coluna de dados de classe de evento QN:Dynamics  
  
|Coluna de dados|Tipo|Descrição|Número da coluna|Filtrável|  
|-----------------|----------|-----------------|-------------------|----------------|  
|ApplicationName|**nvarchar**|O nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|ClientProcessID|**int**|A ID atribuída pelo computador host ao processo em que está sendo executado o aplicativo cliente. Essa coluna de dados será populada se a ID do processo do cliente for fornecida pelo cliente.|9|Sim|  
|DatabaseID|**int**|A ID do banco de dados especificada pela instrução de *banco de dados* USE ou a ID do banco de dados padrão se nenhuma instrução de *banco de dados*USE tiver sido emitida para determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados Server Name for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|DatabaseName|**nvarchar**|O nome do banco de dados no qual a instrução do usuário está sendo executada.|35|Sim|  
|EventClass|**int**|Tipo de evento = 202|27|não|  
|EventSequence|**int**|Número de sequência para esse evento.|51|não|  
|EventSubClass|**nvarchar**|O tipo de subclasse de evento, fornecendo mais informações sobre cada classe de evento. Essa coluna pode conter os seguintes valores:<br /><br /> **Execução do relógio iniciada**: indica que o thread em segundo plano no [!INCLUDE[ssDE](../../includes/ssde-md.md)] que programa tabelas de parâmetro expiradas para limpeza foi iniciado.<br /><br /> **Execução do relógio concluída**: indica que o thread em segundo plano no [!INCLUDE[ssDE](../../includes/ssde-md.md)] que programa tabelas de parâmetro expiradas para limpeza foi concluído.<br /><br /> **Tarefa mestre de limpeza iniciada**: indica quando a limpeza (coleta de lixo) para a remoção de dados expirados de assinatura de notificação de consulta é iniciada.<br /><br /> **Tarefa mestre de limpeza concluída**: indica quando a limpeza (coleta de lixo) para a remoção de dados expirados de assinatura de notificação de consulta é concluída.<br /><br /> **Tarefa mestre de limpeza ignorada**: indica que [!INCLUDE[ssDE](../../includes/ssde-md.md)] não executou a limpeza (coleta de lixo) para remoção de dados expirados de assinatura de notificação de consulta.|21|Sim|  
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
  
  
