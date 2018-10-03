---
title: Colunas de dados de eventos de sessão | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Session Events event category
ms.assetid: 35853451-6768-4a02-8b8f-81a8ae37a333
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 27ec02ffdebcba27a21b3c559e569e20921204a4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48055847"
---
# <a name="session-events-data-columns"></a>Colunas de dados de eventos de sessão
  A categoria Session Events tem a seguinte classe de evento:  
  
|**ID do evento**|**Nome do evento**|**Descrição do evento**|  
|------------------|--------------------|---------------------------|  
|41|Existing Connection|Conexão existente de usuário.|  
|42|Existing Session|Sessão existente.|  
|43|Session Initialize|Inicialização de sessão.|  
  
 A tabela a seguir lista as colunas de dados dessa classe de evento.  
  
## <a name="existing-connection"></a>Existing Connection  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|NTUserName|32|8|Nome do usuário do Windows.|  
|NTDomainName|33|8|O domínio do Windows ao qual o usuário pertence.|  
|ClientHostName|35|8|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o nome do host for fornecido pelo cliente.|  
|ClientProcessID|36|1|A ID do processo do aplicativo cliente.|  
|ApplicationName|37|8|Nome da aplicação cliente que criou a conexão ao servidor. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|  
|SPID|41|1|ID de processo de servidor. Isso identifica exclusivamente uma sessão de usuário. Corresponde diretamente ao GUID de sessão usado pelo XML/A.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="existing-session"></a>Existing Session  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duração|5|2|Período de tempo (em milissegundos) utilizado pelo evento.|  
|CPUTime|6|2|Tempo da CPU (em milissegundos) usado pelo evento.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|NTUserName|32|8|Nome do usuário do Windows.|  
|NTDomainName|33|8|O domínio do Windows ao qual o usuário pertence.|  
|ClientHostName|35|8|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o nome do host for fornecido pelo cliente.|  
|ClientProcessID|36|1|A ID do processo do aplicativo cliente.|  
|ApplicationName|37|8|Nome da aplicação cliente que criou a conexão ao servidor. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|  
|NTCanonicalUserName|40|8|Nome do usuário na forma canônica. Por exemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|ID de processo de servidor. Isso identifica exclusivamente uma sessão de usuário. Corresponde diretamente ao GUID de sessão usado pelo XML/A.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
|RequestProperties|45|9|Propriedades de solicitação XMLA|  
  
## <a name="session-initialize"></a>Session Initialize  
  
|||||  
|-|-|-|-|  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|NTUserName|32|8|Nome do usuário do Windows.|  
|NTDomainName|33|8|O domínio do Windows ao qual o usuário pertence.|  
|ClientHostName|35|8|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o nome do host for fornecido pelo cliente.|  
|ClientProcessID|36|1|A ID do processo do aplicativo cliente.|  
|ApplicationName|37|8|Nome da aplicação cliente que criou a conexão ao servidor. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|  
|NTCanonicalUserName|40|8|Nome do usuário na forma canônica. Por exemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|ID de processo de servidor. Isso identifica exclusivamente uma sessão de usuário. Corresponde diretamente ao GUID de sessão usado pelo XML/A.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
|RequestProperties|45|9|Propriedades de solicitação XMLA|  
  
## <a name="see-also"></a>Consulte também  
 [Categoria de evento de auditoria de segurança](security-audit-event-category.md)  
  
  
