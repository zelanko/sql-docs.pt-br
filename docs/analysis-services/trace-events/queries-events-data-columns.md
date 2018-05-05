---
title: Colunas de dados de eventos de consultas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Queries Events event category
ms.assetid: 28aa7df5-3e1f-4f4f-8a1c-8bbd29d5da13
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 56d1a00189416a8fbc96a256a3ba428385f8660e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="queries-events-data-columns"></a>Colunas de dados de eventos de consulta
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  A categoria de evento Queries Events tem as seguintes classes de evento:  
  
|**ID do evento**|**Nome do evento**|**Descrição do evento**|  
|------------------|--------------------|---------------------------|  
|9|Query Begin|Início da consulta.|  
|10|Query End|Término da consulta.|  
  
 As tabelas a seguir listam as colunas de dados de cada uma dessas classes de evento.  
  
## <a name="query-begin-classdata-columns"></a>Classe Query Begin - Colunas de dados  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|EventSubclass|1|1|A subclasse de evento oferece informações adicionais sobre cada classe de evento.<br /><br /> 0: MDXQuery<br /><br /> 1: DMXQuery<br /><br /> 2: SQLQuery<br /><br /> 3: DAXQuery|  
|CurrentTime|2|5|Contém a hora atual do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Contém a hora em que o evento iniciou, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|ConnectionID|25|1|Contém a ID de conexão exclusiva associada ao evento de consulta.|  
|DatabaseName|28|8|Contém o nome do banco de dados no qual a consulta está em execução.|  
|NTUserName|32|8|Contém o nome de usuário do Windows associado ao evento de consulta.|  
|NTDomainName|33|8|Contém a conta de domínio do Windows associada ao evento de consulta.|  
|ClientProcessID|36|1|Contém a ID de processo do aplicativo cliente.|  
|ApplicationName|37|8|Contém o nome do aplicativo cliente que criou a conexão com o servidor. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|  
|SessionID|39|8|Contém a ID exclusiva de sessão da solicitação de XMLA.|  
|NTCanonicalUserName|40|8|Contém o nome de usuário do Windows associado ao evento de consulta. O nome de usuário está na forma canônica. Por exemplo, engineering.microsoft.com/software/user.|  
|SPID|41|1|Contém a identificação do processo do servidor (SPID) que identifica de modo exclusivo a sessão de usuário associada ao evento de consulta. A SPID corresponde diretamente à GUID de sessão usada pelo XMLA.|  
|TextData|42|9|Contém os dados de texto associados ao evento de consulta.|  
|ServerName|43|8|Contém o nome da instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] na qual ocorreu o evento de consulta.|  
|RequestParameters|44|9|Contém os parâmetros das consultas parametrizadas e dos comandos associados ao evento de consulta.|  
|RequestProperties|45|9|Contém as propriedades da solicitação XMLA.|  
  
## <a name="query-end-classdata-columns"></a>Classe Query End - Colunas de dados  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|EventSubclass|1|1|A subclasse de evento oferece informações adicionais sobre cada classe de evento.<br /><br /> 0: MDXQuery<br /><br /> 1: DMXQuery<br /><br /> 2: SQLQuery<br /><br /> 3: DAXQuery|  
|CurrentTime|2|5|Contém a hora atual do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Contém a hora em que o evento iniciou, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Contém a hora em que o evento terminou. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duration|5|2|Contém a quantidade de tempo decorrido (em milissegundos) utilizado pelo evento.|  
|CPUTime|6|2|Contém a quantidade de tempo da CPU (em milissegundos) usado pelo evento.|  
|Severity|22|1|Contém o nível de severidade de uma exceção associada ao evento de consulta. Os valores são:<br /><br /> 0 = Êxito<br /><br /> 1 = Informativo<br /><br /> 2 = Aviso<br /><br /> 3 = Erro|  
|Success|23|1|Contém o êxito ou a falha do evento de consulta. Os valores são:<br /><br /> 0 = Falha<br /><br /> 1 = Êxito|  
|Erro|24|1|Contém o número de erro de qualquer erro associado ao evento de consulta.|  
|ConnectionID|25|1|Contém a ID de conexão exclusiva associada ao evento de consulta.|  
|DatabaseName|28|8|Contém o nome do banco de dados no qual a consulta está em execução.|  
|NTUserName|32|8|Contém o nome de usuário do Windows associado ao evento de consulta.|  
|NTDomainName|33|8|Contém a conta de domínio do Windows associada ao evento de consulta.|  
|ClientProcessID|36|1|Contém a ID de processo do aplicativo cliente.|  
|ApplicationName|37|8|Contém o nome do aplicativo cliente que criou a conexão com o servidor. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|  
|SessionID|39|8|Contém a ID exclusiva de sessão da solicitação de XMLA.|  
|NTCanonicalUserName|40|8|Contém o nome de usuário do Windows associado ao evento de consulta. O nome de usuário está na forma canônica. Por exemplo, engineering.microsoft.com/software/user.|  
|SPID|41|1|Contém a identificação do processo do servidor (SPID) que identifica de modo exclusivo a sessão de usuário associada ao evento de consulta. A SPID corresponde diretamente à GUID de sessão usada pelo XMLA.|  
|TextData|42|9|Contém os dados de texto associados ao evento de consulta.|  
|ServerName|43|8|Contém o nome da instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] na qual ocorreu o evento de consulta.|  
  
## <a name="see-also"></a>Consulte também  
 [Categoria Queries Events](../../analysis-services/trace-events/queries-events-category.md)  
  
  
