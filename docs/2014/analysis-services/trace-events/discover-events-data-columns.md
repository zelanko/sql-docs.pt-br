---
title: Colunas de dados de eventos de identificação | Microsoft Docs
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
- Discover Events event category
ms.assetid: 10ec598e-5b51-4767-b4f7-42e261d96a40
caps.latest.revision: 29
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3437445c242c2e6ab759119ceb644807eea0cfd1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37265382"
---
# <a name="discover-events-data-columns"></a>Colunas de dados de eventos de identificação
  A categoria Discover Events tem as seguintes classes de evento:  
  
-   Classe Discover Begin  
  
-   Classe Discover End  
  
 As tabelas a seguir listam as colunas de dados de cada uma dessas classes de evento.  
  
## <a name="discover-begin-classdata-columns"></a>Classe Discover Begin - Colunas de dados  
  
|||||  
|-|-|-|-|  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|EventSubclass|1|1|A subclasse de evento oferece informações adicionais sobre cada classe de evento. Estes são os valor válido: pares de nome:<br /><br /> 0: **DBSCHEMA_CATALOGS**<br />1: **DBSCHEMA_TABLES**<br />2: **DBSCHEMA_COLUMNS**<br />3: **DBSCHEMA_PROVIDER_TYPES**<br />4: **MDSCHEMA_CUBES**<br />5: **MDSCHEMA_DIMENSIONS**<br />6: **MDSCHEMA_HIERARCHIES**<br />7: **MDSCHEMA_LEVELS**<br />8: **MDSCHEMA_MEASURES**<br />9: **MDSCHEMA_PROPERTIES**<br />10: **MDSCHEMA_MEMBERS**<br />11: **MDSCHEMA_FUNCTIONS**<br />12: **MDSCHEMA_ACTIONS**<br />13: **MDSCHEMA_SETS**<br />14: **DISCOVER_INSTANCES**<br />15: **MDSCHEMA_KPIS**<br />16: **MDSCHEMA_MEASURESGROUPS**<br />17: **MDSCHEMA_COMMANDS**<br />18: **DMSCHEMA_MINING_SERVICES**<br />19: **DMSCHEMA_MINING_SERVICE_PARAMETERS**<br />20: **DMSCHEMA_MINING_FUNCTIONS**<br />21: **DMSCHEMA_MINING_MODEL_CONTENT**<br />22: **DMSCHEMA_MINING_MODEL_XML**<br />23: **DMSCHEMA_MINING_MODELS**<br />24: **DMSCHEMA_MINING_COLUMNS**<br />25: **DISCOVER_DATASOURCES**<br />26: **DISCOVER_PROPERTIES**<br />27: **DISCOVER_SCHEMA_ROWSETS**<br />28: **DISCOVER_ENUMERATORS**<br />29: **DISCOVER_KEYWORDS**<br />30: **DISCOVER_LITERALS**<br />31: **DISCOVER_XML_METADATA**<br />32: **DISCOVER_TRACES**<br />33: **DISCOVER_TRACE_DEFINITION_PROVIDERINFO**<br />34: **DISCOVER_TRACE_COLUMNS**<br />35: **DISCOVER_TRACE_EVENT_CATEGORIES**<br />36: **DMSCHEMA_MINING_STRUCTURES**<br />37: **DMSCHEMA_MINING_STRUCTURE_COLUMNS**<br />38: **DISCOVER_MASTER_KEY**<br />39: **MDSCHEMA_INPUT_DATASOURCES**<br />40: **DISCOVER_LOCATIONS**<br />41: **DISCOVER_PARTITION_DIMENSION_STAT**<br />42: **DISCOVER_PARTITION_STAT**<br />43: **DISCOVER_DIMENSION_STAT**<br />44: **MDSCHEMA_MEASUREGROUP_DIMENSIONS**<br />45: **DISCOVER_XEVENT_TRACE_DEFINITION**|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|ConnectionID|25|1|Contém a ID de conexão exclusiva associada ao evento de identificação.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|NTUserName|32|8|Contém o nome de usuário do Windows associado ao evento de identificação. O nome de usuário está na forma canônica. Por exemplo, engineering.microsoft.com/software/user.|  
|NTDomainName|33|8|Contém o domínio do Windows associado ao evento de identificação.|  
|ClientProcessID|36|1|Contém a ID de processo do aplicativo cliente.|  
|ApplicationName|37|8|Nome da aplicação cliente que criou a conexão ao servidor. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|  
|SessionID|39|8|Contém a ID de sessão associada ao evento de identificação.|  
|NTCanonicalUserName|40|8|Contém o nome de usuário do Windows associado ao evento de identificação. O nome de usuário está na forma canônica. Por exemplo, engineering.microsoft.com/software/user.|  
|SPID|41|1|Contém a identificação do processo do servidor (SPID) que identifica de modo exclusivo a sessão de usuário associada ao evento de identificação. A SPID corresponde diretamente à GUID de sessão usada pelo XMLA.|  
|TextData|42|9|Contém os dados de texto associados ao evento.|  
|ServerName|43|8|Contém o nome da instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] na qual o evento de identificação ocorreu.|  
|RequestProperties|45|9|Contém as propriedades de solicitação de XML for Analysis (XMLA) associadas ao evento de identificação.|  
  
## <a name="discover-end-classdata-columns"></a>Classe Discover End - Colunas de dados  
  
|||||  
|-|-|-|-|  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|EventClass|0|1|Contém a classe de evento; ela é usada para categorizar eventos.|  
|EventSubclass|1|1|A subclasse de evento oferece informações adicionais sobre cada classe de evento. Estes são os valor válido: pares de nome:<br /><br /> 0: **DBSCHEMA_CATALOGS**<br />1: **DBSCHEMA_TABLES**<br />2: **DBSCHEMA_COLUMNS**<br />3: **DBSCHEMA_PROVIDER_TYPES**<br />4: **MDSCHEMA_CUBES**<br />5: **MDSCHEMA_DIMENSIONS**<br />6: **MDSCHEMA_HIERARCHIES**<br />7: **MDSCHEMA_LEVELS**<br />8: **MDSCHEMA_MEASURES**<br />9: **MDSCHEMA_PROPERTIES**<br />10: **MDSCHEMA_MEMBERS**<br />11: **MDSCHEMA_FUNCTIONS**<br />12: **MDSCHEMA_ACTIONS**<br />13: **MDSCHEMA_SETS**<br />14: **DISCOVER_INSTANCES**<br />15: **MDSCHEMA_KPIS**<br />16: **MDSCHEMA_MEASURESGROUPS**<br />17: **MDSCHEMA_COMMANDS**<br />18: **DMSCHEMA_MINING_SERVICES**<br />19: **DMSCHEMA_MINING_SERVICE_PARAMETERS**<br />20: **DMSCHEMA_MINING_FUNCTIONS**<br />21: **DMSCHEMA_MINING_MODEL_CONTENT**<br />22: **DMSCHEMA_MINING_MODEL_XML**<br />23: **DMSCHEMA_MINING_MODELS**<br />24: **DMSCHEMA_MINING_COLUMNS**<br />25: **DISCOVER_DATASOURCES**<br />26: **DISCOVER_PROPERTIES**<br />27: **DISCOVER_SCHEMA_ROWSETS**<br />28: **DISCOVER_ENUMERATORS**<br />29: **DISCOVER_KEYWORDS**<br />30: **DISCOVER_LITERALS**<br />31: **DISCOVER_XML_METADATA**<br />32: **DISCOVER_TRACES**<br />33: **DISCOVER_TRACE_DEFINITION_PROVIDERINFO**<br />34: **DISCOVER_TRACE_COLUMNS**<br />35: **DISCOVER_TRACE_EVENT_CATEGORIES**<br />36: **DMSCHEMA_MINING_STRUCTURES**<br />37: **DMSCHEMA_MINING_STRUCTURE_COLUMNS**<br />38: **DISCOVER_MASTER_KEY**<br />39: **MDSCHEMA_INPUT_DATASOURCES**<br />40: **DISCOVER_LOCATIONS**<br />41: **DISCOVER_PARTITION_DIMENSION_STAT**<br />42: **DISCOVER_PARTITION_STAT**<br />43: **DISCOVER_DIMENSION_STAT**<br />44: **MDSCHEMA_MEASUREGROUP_DIMENSIONS**<br />45: **DISCOVER_XEVENT_TRACE_DEFINITION**|  
|CurrentTime|2|5|Contém a hora atual do evento de identificação, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Contém a hora (se disponível) em que o evento final de identificação foi iniciado. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Contém a hora em que o evento terminou. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duração|5|2|Contém o período de tempo aproximado da duração (milissegundos) do evento de identificação.|  
|CPUTime|6|2|Contém a quantidade de tempo da CPU (em milissegundos) usado pelo evento.|  
|Severity|22|1|Contém o nível de severidade de uma exceção.|  
|Êxito|23|1|Contém o êxito ou a falha do evento de identificação. Os valores são:<br /><br /> 0 = Falha<br /><br /> 1 = Êxito|  
|Erro|24|1|Contém o número de erro de qualquer erro associado ao evento de identificação.|  
|ConnectionID|25|1|Contém a ID de conexão exclusiva associada ao evento de identificação.|  
|DatabaseName|28|8|Contém o nome do banco de dados no qual o evento de identificação ocorreu.|  
|NTUserName|32|8|Contém o nome de usuário do Windows associado ao evento de permissão de objetos.|  
|NTDomainName|33|8|Contém a conta de domínio do Windows associada ao evento de identificação.|  
|ClientProcessID|36|1|Contém a ID de processo de cliente do aplicativo que iniciou o evento.|  
|ApplicationName|37|8|Contém o nome do aplicativo cliente que criou a conexão com o servidor. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|  
|SessionID|39|8|Contém a ID de sessão associada ao evento de identificação.|  
|NTCanonicalUserName|40|8|Contém o nome de usuário do Windows associado ao evento de permissão de objetos. O nome de usuário está na forma canônica. Por exemplo, engineering.microsoft.com/software/user.|  
|SPID|41|1|Contém a identificação do processo do servidor (SPID) que identifica de modo exclusivo a sessão de usuário associada ao evento final de identificação. A SPID corresponde diretamente à GUID de sessão usada pelo XMLA.|  
|TextData|42|9|Contém os dados de texto associados ao evento.|  
|ServerName|43|8|Contém o nome da instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] na qual o evento de identificação ocorreu.|  
|RequestProperties|45|9|Contém as propriedades na solicitação XMLA.|  
  
## <a name="see-also"></a>Consulte também  
 [Categoria de evento Descobrir eventos](discover-events-event-category.md)  
  
  
