---
title: "Colunas de dados de auditoria de segurança | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: Security Audit event category [SQL Server]
ms.assetid: fac1a7f9-5961-4f4b-bb04-847616b505d7
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d827295c68028d54d64bbb91447aa7ab22eaaa77
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="security-audit-data-columns"></a>Colunas de dados de auditoria de segurança
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]A categoria de evento de auditoria de segurança tem as seguintes classes de evento:  
  
||||  
|-|-|-|  
|**ID do evento**|**Nome do evento**|**Descrição do evento**|  
|1|Audit Login|Coleta todos os novos eventos de conexão desde o início do rastreamento; por exemplo, quando um cliente solicita uma conexão a um servidor executando uma instância do SQL Server.|  
|2|Audit Logout|Coleta todos os novos eventos de desconexão desde o início do rastreamento; por exemplo, quando um cliente emite um comando de desconexão.|  
|4|Audit Server Starts And Stops|Registra as atividades de desligar, iniciar e pausar serviço.|  
|18|Audit Object Permission Event|Registra alterações na permissão do objeto.|  
|19|Evento de Operações de Administração de Auditoria|Registra backup/restore/synchronize/attach/detach/imageload/imagesave do servidor.|  
  
 As tabelas a seguir listam as colunas de dados de cada uma dessas classes de evento.  
  
## <a name="audit-login"></a>Audit Login  
  
|||||  
|-|-|-|-|  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Severity|22|1|Nível de severidade de uma exceção.|  
|Êxito|23|1|1 = êxito. 0 = falha (por exemplo, 1 significa êxito de uma verificação de permissões e 0 significa uma falha dessa verificação).|  
|Erro|24|1|Número de erro de um determinado evento.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|NTUserName|32|8|Nome do usuário do Windows.|  
|NTDomainName|33|8|O domínio do Windows ao qual o usuário pertence.|  
|ClientHostName|35|8|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o nome do host for fornecido pelo cliente.|  
|ClientProcessID|36|1|A ID do processo do aplicativo cliente.|  
|ApplicationName|37|8|Nome da aplicação cliente que criou a conexão ao servidor. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|  
|NTCanonicalUserName|40|8|Nome do usuário na forma canônica. Por exemplo, engineering.microsoft.com/software/someone.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="audit-logout"></a>Audit Logout  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Horário em que o evento foi encerrado. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duração|5|2|Período de tempo (em milissegundos) utilizado pelo evento.|  
|CPUTime|6|2|Tempo da CPU (em milissegundos) usado pelo evento.|  
|Êxito|23|1|1 = êxito. 0 = falha (por exemplo, 1 significa êxito de uma verificação de permissões e 0 significa uma falha dessa verificação).|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|NTUserName|32|8|Nome do usuário do Windows.|  
|NTDomainName|33|8|O domínio do Windows ao qual o usuário pertence.|  
|ClientHostName|35|8|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o nome do host for fornecido pelo cliente.|  
|ClientProcessID|36|1|A ID do processo do aplicativo cliente.|  
|ApplicationName|37|8|Nome da aplicação cliente que criou a conexão ao servidor. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|  
|NTCanonicalUserName|40|8|Nome do usuário na forma canônica. Por exemplo, engineering.microsoft.com/software/someone.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="audit-server-starts-and-stops"></a>Audit Server Starts And Stops  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|EventSubclass|1|1|A Subclasse de Evento oferece informações adicionais sobre cada classe de evento:<br /><br /> 1: desligamento da instância<br /><br /> 2: instância iniciada<br /><br /> 3: instância pausada<br /><br /> 4 = continuação da instância|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Severity|22|1|Nível de severidade de uma exceção.|  
|Êxito|23|1|1 = êxito. 0 = falha (por exemplo, 1 significa êxito de uma verificação de permissões e 0 significa uma falha dessa verificação).|  
|Erro|24|1|Número de erro de um determinado evento.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="audit-object-permission-event"></a>Audit Object Permission Event  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|ObjectID|11|8|ID do objeto (note que esta é uma cadeia de caracteres).|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectName|13|8|Nome do objeto.|  
|ObjectPath|14|8|Caminho do objeto. Uma lista de pais separados por vírgulas, começando com o pai do objeto.|  
|ObjectReference|15|8|Referência ao objeto. Codificado como XML para todos os pais, usando marcas para descrever o objeto.|  
|Severity|22|1|Nível de severidade de uma exceção.|  
|Êxito|23|1|1 = êxito. 0 = falha (por exemplo, 1 significa êxito de uma verificação de permissões e 0 significa uma falha dessa verificação).|  
|Erro|24|1|Número de erro de um determinado evento.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|NTUserName|32|8|Nome do usuário do Windows.|  
|NTDomainName|33|8|O domínio do Windows ao qual o usuário pertence.|  
|ClientHostName|35|8|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o nome do host for fornecido pelo cliente.|  
|ClientProcessID|36|1|A ID do processo do aplicativo cliente.|  
|ApplicationName|37|8|Nome da aplicação cliente que criou a conexão ao servidor. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|  
|SessionID|39|8|GUID da sessão.|  
|NTCanonicalUserName|40|8|Nome do usuário na forma canônica. Por exemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|ID de processo de servidor. Isso identifica exclusivamente uma sessão de usuário. Corresponde diretamente ao GUID de sessão usado pelo XML/A.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="audit-admin-operations-event"></a>Evento de Operações de Administração de Auditoria  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventSubclass|1|1|A Subclasse de Evento oferece informações adicionais sobre cada classe de evento:<br /><br /> 1: **Backup**<br /><br /> 2: **Restore**<br /><br /> 3: **Synchronize**<br /><br /> 4: **Detach**<br /><br /> 5: **Attach**<br /><br /> 6: **ImageLoad**<br /><br /> 7: **ImageSave**|  
|Severity|22|1|Nível de severidade de uma exceção.|  
|Êxito|23|1|1 = êxito. 0 = falha (por exemplo, 1 significa êxito de uma verificação de permissões e 0 significa uma falha dessa verificação).|  
|Erro|24|1|Número de erro de um determinado evento.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|NTUserName|32|8|Nome do usuário do Windows.|  
|NTDomainName|33|8|O domínio do Windows ao qual o usuário pertence.|  
|ClientHostName|35|8|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o nome do host for fornecido pelo cliente.|  
|ClientProcessID|36|1|A ID do processo do aplicativo cliente.|  
|ApplicationName|37|8|Nome da aplicação cliente que criou a conexão ao servidor. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|  
|SessionID|39|8|GUID da sessão.|  
|NTCanonicalUserName|40|8|Nome do usuário na forma canônica. Por exemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|ID de processo de servidor. Isso identifica exclusivamente uma sessão de usuário. Corresponde diretamente ao GUID de sessão usado pelo XML/A.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="see-also"></a>Consulte Também  
 [Categoria de evento de auditoria de segurança](../../analysis-services/trace-events/security-audit-event-category.md)  
  
  
