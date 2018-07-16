---
title: Descobrir o estado do servidor Events Data Columns | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Discover Server State event category
ms.assetid: fbacb187-a4d1-4aa4-be3b-3ddd175f9e19
caps.latest.revision: 31
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 49aeff626e1b227974da0e122b2a94ed28c5d917
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37196086"
---
# <a name="discover-server-state-events-data-columns"></a>Colunas de dados de eventos de identificação do estado do servidor
  A categoria de evento Discover Server State tem as seguintes classes de evento:  
  
|**ID do evento**|**Nome do evento**|**Descrição do evento**|  
|------------------|--------------------|---------------------------|  
|33|Server State Discover Begin|Início do Server State Discover.|  
|34|Server State Discover Data|Conteúdo do Server State Discover Response.|  
|35|Server State Discover End|Final do Server State Discover.|  
  
 As tabelas a seguir listam as colunas de dados de cada uma dessas classes de evento.  
  
## <a name="server-state-discover-begin-classdata-columns"></a>Classe Server State Discover Begin - Colunas de dados  
  
|||||  
|-|-|-|-|  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|EventSubclass|1|1|A Subclasse de Evento oferece informações adicionais sobre cada classe de evento:<br /><br /> 1: **DISCOVER_CONNECTIONS**<br /><br /> 2: **DISCOVER_SESSIONS**<br /><br /> 3: **DISCOVER_TRANSACTIONS**<br /><br /> 6: **DISCOVER_DB_CONNECTIONS**<br /><br /> 7: **DISCOVER_JOBS**<br /><br /> 8: **DISCOVER_LOCKS**<br /><br /> 12: **DISCOVER_PERFORMANCE_COUNTERS**<br /><br /> 13: **DISCOVER_MEMORYUSAGE**<br /><br /> 14: **DISCOVER_JOB_PROGRESS**<br /><br /> 15: **DISCOVER_MEMORYGRANT**|  
|CurrentTime|2|5|Contém a hora atual do evento de descoberta de estado do servidor, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Contém a hora em que o evento iniciou, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|ConnectionID|25|1|Contém a ID de conexão exclusiva associada ao evento de identificação do estado do servidor.|  
|NTUserName|32|8|Contém a conta de usuário do Windows associada ao evento de identificação do estado do servidor.|  
|NTDomainName|33|8|Contém a conta de domínio do Windows associada ao evento de identificação do estado do servidor.|  
|ClientProcessID|36|1|Contém a ID de processo do aplicativo cliente que criou a conexão ao servidor.|  
|ApplicationName|37|8|Contém o nome do aplicativo cliente que criou a conexão com o servidor. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|  
|SessionID|39|8|Contém a ID de sessão associada ao evento de identificação do estado do servidor.|  
|NTCanonicalUserName|40|8|Contém o nome de usuário do Windows associado ao evento de identificação do estado do servidor. O nome de usuário está na forma canônica. Por exemplo, engineering.microsoft.com/software/user.|  
|SPID|41|1|Contém a identificação do processo do servidor (SPID) que identifica de modo exclusivo a sessão de usuário associada ao evento de identificação do estado do servidor. A SPID corresponde diretamente à GUID de sessão usada pelo XMLA.|  
|TextData|42|9|Contém os dados de texto associados ao evento.|  
|ServerName|43|8|Contém o nome da instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] na qual o evento de identificação do estado do servidor ocorreu.|  
|RequestProperties|45|9|Contém as propriedades da solicitação XMLA atual.|  
  
## <a name="server-state-discover-data-classdata-columns"></a>Classe Server State Discover Data - Colunas de dados  
  
|||||  
|-|-|-|-|  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|EventSubclass|1|1|A Subclasse de Evento oferece informações adicionais sobre cada classe de evento:<br /><br /> 1: **DISCOVER_CONNECTIONS**<br /><br /> 2: **DISCOVER_SESSIONS**<br /><br /> 3: **DISCOVER_TRANSACTIONS**<br /><br /> 6: **DISCOVER_DB_CONNECTIONS**<br /><br /> 7: **DISCOVER_JOBS**<br /><br /> 8: **DISCOVER_LOCKS**<br /><br /> 12: **DISCOVER_PERFORMANCE_COUNTERS**<br /><br /> 13: **DISCOVER_MEMORYUSAGE**<br /><br /> 14: **DISCOVER_JOB_PROGRESS**<br /><br /> 15: **DISCOVER_MEMORYGRANT**|  
|CurrentTime|2|5|Contém a hora atual do evento de descoberta de estado do servidor, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Contém a hora em que o evento iniciou, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|ConnectionID|25|1|Contém a ID de conexão exclusiva associada ao evento de identificação do estado do servidor.|  
|SessionID|39|8|Contém a ID de sessão associada ao evento de identificação do estado do servidor.|  
|SPID|41|1|Contém a identificação do processo do servidor (SPID) que identifica de modo exclusivo a sessão de usuário associada ao evento de identificação do estado do servidor. A SPID corresponde diretamente à GUID de sessão usada pelo XMLA.|  
|TextData|42|9|Contém os dados de texto associados à resposta do servidor à solicitação de identificação.|  
|ServerName|43|8|Contém o nome da instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] na qual o evento de identificação do estado do servidor ocorreu.|  
  
## <a name="server-state-discover-end-classdata-columns"></a>Classe Server State Discover End - Colunas de dados  
  
|||||  
|-|-|-|-|  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|EventSubclass|1|1|A Subclasse de Evento oferece informações adicionais sobre cada classe de evento:<br /><br /> 1: **DISCOVER_CONNECTIONS**<br /><br /> 2: **DISCOVER_SESSIONS**<br /><br /> 3: **DISCOVER_TRANSACTIONS**<br /><br /> 6: **DISCOVER_DB_CONNECTIONS**<br /><br /> 7: **DISCOVER_JOBS**<br /><br /> 8: **DISCOVER_LOCKS**<br /><br /> 12: **DISCOVER_PERFORMANCE_COUNTERS**<br /><br /> 13: **DISCOVER_MEMORYUSAGE**<br /><br /> 14: **DISCOVER_JOB_PROGRESS**<br /><br /> 15: **DISCOVER_MEMORYGRANT**|  
|CurrentTime|2|5|Contém a hora atual do evento de descoberta de estado do servidor, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Contém a hora em que o evento iniciou, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Contém a hora em que o evento terminou. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duração|5|2|Contém a quantidade de tempo (em milissegundos) utilizado pelo evento.|  
|CPUTime|6|2|Contém a quantidade de tempo da CPU (em milissegundos) usada pelo evento de descoberta de estado do servidor.|  
|ConnectionID|25|1|Contém a ID de conexão exclusiva associada ao evento de identificação do estado do servidor.|  
|NTUserName|32|8|Contém a conta de usuário do Windows associada ao evento de identificação do estado do servidor.|  
|NTDomainName|33|8|Contém a conta de domínio do Windows associada ao evento de identificação do estado do servidor.|  
|ClientProcessID|36|1|Contém a ID do processo do aplicativo cliente que iniciou a solicitação de XMLA.|  
|ApplicationName|37|8|Contém o nome do aplicativo cliente que criou a conexão com o servidor. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|  
|SessionID|39|8|Contém a conta de domínio do Windows associada ao evento de identificação do estado do servidor.|  
|NTCanonicalUserName|40|8|Contém o nome de usuário do Windows associado ao evento de identificação do estado do servidor. O nome de usuário está na forma canônica. Por exemplo, engineering.microsoft.com/software/user.|  
|SPID|41|1|Contém a identificação do processo do servidor (SPID) que identifica de modo exclusivo a sessão de usuário associada ao evento de identificação do estado do servidor. A SPID corresponde diretamente à GUID de sessão usada pelo XMLA.|  
|TextData|42|9|Contém os dados de texto associados à resposta do servidor à solicitação de identificação.|  
|ServerName|43|8|Contém o nome da instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] na qual o evento de identificação do estado do servidor ocorreu.|  
  
## <a name="see-also"></a>Consulte também  
 [Categoria de evento Descobrir estado do servidor](discover-server-state-event-category.md)  
  
  
