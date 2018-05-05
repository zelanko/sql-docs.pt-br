---
title: Colunas de dados de eventos de processamento de consulta | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 81a522bd-440d-406c-a524-3af44a3af101
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 117cab8b57631b1a95dea9baa0e86e918cabf81f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="query-processing-events-data-columns"></a>Colunas de dados de eventos de processamento de consulta
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  A categoria de evento Query Processing Events tem as seguintes classes de evento:  
  
|**ID do evento**|**Nome do evento**|**Descrição do evento**|  
|------------------|--------------------|---------------------------|  
|70|Início do Cubo de Consulta|Início do cubo de consulta.|  
|71|Final do Cubo de Consulta|Término do cubo de consulta.|  
|72|Calculate Non Empty Begin|Início de cálculo de não vazio.|  
|73|Calculate Non Empty Current|Calcular não vazio atual.|  
|74|Calculate Non Empty End|Término de cálculo de não vazio.|  
|75|Serialize Results Begin|Início da serialização de resultados.|  
|76|Serializar Resultados Atuais|Serializar resultados atuais.|  
|77|Serializar Final de Resultados|Serializar final de resultados.|  
|78|Executar Início do Script do MDX|Executar início do script do MDX.|  
|79|Executar Script do MDX Atual|Executar script do MDX atual. Preterido.|  
|80|Execute Final do Script do MDX|Executar final do script do MDX.|  
|81|Dimensão da consulta|Dimensão da consulta.|  
|11|Subcubo de consulta|Subcubo de consulta, a Otimização Baseada em Uso.|  
|12|Subcubo de consulta detalhado|Subcubo de consulta com informações detalhadas. Este evento pode ter um impacto negativo no desempenho quando ativado.|  
|60|Obter Dados de Agregação|Responder a consulta obtendo dados de agregação. Este evento pode ter um impacto negativo no desempenho quando ativado.|  
|61|Obter Dados de Cache|Responder a consulta obtendo dados de um dos caches. Este evento pode ter um impacto negativo no desempenho quando ativado.|  
|82|Início da Consulta VertiPaq SE|Consulta VertiPaq SE|  
|83|Final da Consulta VertiPaq SE|Consulta VertiPaq SE|  
|84|Uso de recurso|Leituras de relatórios, gravações, uso da cpu após final de comandos e consultas.|  
|85|VertiPaq SE Query Cache Match|Uso do cache de consulta VertiPaq SE|  
|98|Direct Query Begin|Início da consulta direta.|  
|99|Direct Query End|Término da consulta direta.|  
  
 As tabelas a seguir listam as colunas de dados de cada uma dessas classes de evento.  
  
## <a name="query-cube-begin"></a>Início do Cubo de Consulta  
  
|||||  
|-|-|-|-|  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Horário em que o evento foi encerrado. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duration|5|2|Período de tempo (em milissegundos) utilizado pelo evento.|  
|CPUTime|6|2|Tempo da CPU (em milissegundos) usado pelo evento.|  
|ProgressTotal|9|1|Andamento total.|  
|IntegerData|10|1|Dados Integer.|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectPath|14|8|Caminho do objeto. Uma lista de pais separados por vírgulas, começando com o pai do objeto.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|NTCanonicalUserName|40|8|Nome do usuário na forma canônica. Por exemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|ID de processo de servidor. Isso identifica exclusivamente uma sessão de usuário. Corresponde diretamente ao GUID de sessão usado pelo XML/A.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="query-cube-end"></a>Final do Cubo de Consulta  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Horário em que o evento foi encerrado. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duration|5|2|Período de tempo (em milissegundos) utilizado pelo evento.|  
|CPUTime|6|2|Tempo da CPU (em milissegundos) usado pelo evento.|  
|ProgressTotal|9|1|Andamento total.|  
|IntegerData|10|1|Dados Integer.|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectPath|14|8|Caminho do objeto. Uma lista de pais separados por vírgulas, começando com o pai do objeto.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|NTCanonicalUserName|40|8|Nome do usuário na forma canônica. Por exemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|ID de processo de servidor. Isso identifica exclusivamente uma sessão de usuário. Corresponde diretamente ao GUID de sessão usado pelo XML/A.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="calculate-non-empty-begin"></a>Calculate Non Empty Begin  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Horário em que o evento foi encerrado. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duration|5|2|Período de tempo (em milissegundos) utilizado pelo evento.|  
|CPUTime|6|2|Tempo da CPU (em milissegundos) usado pelo evento.|  
|ProgressTotal|9|1|Andamento total.|  
|IntegerData|10|1|Dados Integer.|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectPath|14|8|Caminho do objeto. Uma lista de pais separados por vírgulas, começando com o pai do objeto.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|NTCanonicalUserName|40|8|Nome do usuário na forma canônica. Por exemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|ID de processo de servidor. Isso identifica exclusivamente uma sessão de usuário. Corresponde diretamente ao GUID de sessão usado pelo XML/A.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="calculate-non-empty-current"></a>Calculate Non Empty Current  
  
|||||  
|-|-|-|-|  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|EventSubclass|1|1|A Subclasse de Evento oferece informações adicionais sobre cada classe de evento:<br /><br /> 1: Obter dados<br /><br /> 2: Processar membros calculados<br /><br /> 3: Postar ordem|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Horário em que o evento foi encerrado. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duration|5|2|Período de tempo (em milissegundos) utilizado pelo evento.|  
|CPUTime|6|2|Tempo da CPU (em milissegundos) usado pelo evento.|  
|ProgressTotal|9|1|Andamento total.|  
|IntegerData|10|1|Dados Integer.|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectPath|14|8|Caminho do objeto. Uma lista de pais separados por vírgulas, começando com o pai do objeto.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|NTCanonicalUserName|40|8|Nome do usuário na forma canônica. Por exemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|ID de processo de servidor. Isso identifica exclusivamente uma sessão de usuário. Corresponde diretamente ao GUID de sessão usado pelo XML/A.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="calculate-non-empty-end"></a>Calculate Non Empty End  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Horário em que o evento foi encerrado. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duration|5|2|Período de tempo (em milissegundos) utilizado pelo evento.|  
|CPUTime|6|2|Tempo da CPU (em milissegundos) usado pelo evento.|  
|ProgressTotal|9|1|Andamento total.|  
|IntegerData|10|1|Dados Integer.|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectPath|14|8|Caminho do objeto. Uma lista de pais separados por vírgulas, começando com o pai do objeto.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|NTCanonicalUserName|40|8|Nome do usuário na forma canônica. Por exemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|ID de processo de servidor. Isso identifica exclusivamente uma sessão de usuário. Corresponde diretamente ao GUID de sessão usado pelo XML/A.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="serialize-results-begin"></a>Serialize Results Begin  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Horário em que o evento foi encerrado. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duration|5|2|Período de tempo (em milissegundos) utilizado pelo evento.|  
|CPUTime|6|2|Tempo da CPU (em milissegundos) usado pelo evento.|  
|ProgressTotal|9|1|Andamento total.|  
|IntegerData|10|1|Dados Integer.|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectPath|14|8|Caminho do objeto. Uma lista de pais separados por vírgulas, começando com o pai do objeto.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|NTCanonicalUserName|40|8|Nome do usuário na forma canônica. Por exemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|ID de processo de servidor. Isso identifica exclusivamente uma sessão de usuário. Corresponde diretamente ao GUID de sessão usado pelo XML/A.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="serialize-results-current"></a>Serializar Resultados Atuais  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|EventSubclass|1|1|A subclasse de evento oferece informações adicionais sobre cada classe de evento.<br /><br /> 1: Serializar eixos<br /><br /> 2: Serializar células<br /><br /> 3: Serializar conjunto de linhas SQL<br /><br /> 4: Serializar conjunto de linhas bidimensional|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Horário em que o evento foi encerrado. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duration|5|2|Período de tempo (em milissegundos) utilizado pelo evento.|  
|CPUTime|6|2|Tempo da CPU (em milissegundos) usado pelo evento.|  
|ProgressTotal|9|1|Andamento total.|  
|IntegerData|10|1|Dados Integer.|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectPath|14|8|Caminho do objeto. Uma lista de pais separados por vírgulas, começando com o pai do objeto.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|NTCanonicalUserName|40|8|Nome do usuário na forma canônica. Por exemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|ID de processo de servidor. Isso identifica exclusivamente uma sessão de usuário. Corresponde diretamente ao GUID de sessão usado pelo XML/A.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="serialize-results-end"></a>Serializar Final de Resultados  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Horário em que o evento foi encerrado. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duration|5|2|Período de tempo (em milissegundos) utilizado pelo evento.|  
|CPUTime|6|2|Tempo da CPU (em milissegundos) usado pelo evento.|  
|ProgressTotal|9|1|Andamento total.|  
|IntegerData|10|1|Dados Integer.|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectPath|14|8|Caminho do objeto. Uma lista de pais separados por vírgulas, começando com o pai do objeto.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|NTCanonicalUserName|40|8|Nome do usuário na forma canônica. Por exemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|ID de processo de servidor. Isso identifica exclusivamente uma sessão de usuário. Corresponde diretamente ao GUID de sessão usado pelo XML/A.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="execute-mdx-script-begin"></a>Executar Início do Script do MDX  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|EventSubclass|1|1|A Subclasse de Evento oferece informações adicionais sobre cada classe de evento:<br /><br /> 1: Script MDX<br /><br /> 2: Comando de script MDX|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Horário em que o evento foi encerrado. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duration|5|2|Período de tempo (em milissegundos) utilizado pelo evento.|  
|CPUTime|6|2|Tempo da CPU (em milissegundos) usado pelo evento.|  
|ProgressTotal|9|1|Andamento total.|  
|IntegerData|10|1|Dados Integer.|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectPath|14|8|Caminho do objeto. Uma lista de pais separados por vírgulas, começando com o pai do objeto.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|NTCanonicalUserName|40|8|Nome do usuário na forma canônica. Por exemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|ID de processo de servidor. Isso identifica exclusivamente uma sessão de usuário. Corresponde diretamente ao GUID de sessão usado pelo XML/A.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="execute-mdx-script-current"></a>Executar Script do MDX Atual  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Horário em que o evento foi encerrado. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duration|5|2|Período de tempo (em milissegundos) utilizado pelo evento.|  
|CPUTime|6|2|Tempo da CPU (em milissegundos) usado pelo evento.|  
|ProgressTotal|9|1|Andamento total.|  
|IntegerData|10|1|Dados Integer.|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectPath|14|8|Caminho do objeto. Uma lista de pais separados por vírgulas, começando com o pai do objeto.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|NTCanonicalUserName|40|8|Nome do usuário na forma canônica. Por exemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|ID de processo de servidor. Isso identifica exclusivamente uma sessão de usuário. Corresponde diretamente ao GUID de sessão usado pelo XML/A.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="execute-mdx-script-end"></a>Execute Final do Script do MDX  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|EventSubclass|1|1|A Subclasse de Evento oferece informações adicionais sobre cada classe de evento:<br /><br /> 1: Script MDX<br /><br /> 2: Comando de script MDX|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Horário em que o evento foi encerrado. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duration|5|2|Período de tempo (em milissegundos) utilizado pelo evento.|  
|CPUTime|6|2|Tempo da CPU (em milissegundos) usado pelo evento.|  
|ProgressTotal|9|1|Andamento total.|  
|IntegerData|10|1|Dados Integer.|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectPath|14|8|Caminho do objeto. Uma lista de pais separados por vírgulas, começando com o pai do objeto.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|NTCanonicalUserName|40|8|Nome do usuário na forma canônica. Por exemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|ID de processo de servidor. Isso identifica exclusivamente uma sessão de usuário. Corresponde diretamente ao GUID de sessão usado pelo XML/A.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="query-dimension"></a>Dimensão da consulta  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|EventSubclass|1|1|A subclasse de evento oferece informações adicionais sobre cada classe de evento.<br /><br /> 1: Dados armazenados em cache<br /><br /> 2: Dados não armazenados em cache|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Horário em que o evento foi encerrado. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duration|5|2|Período de tempo (em milissegundos) utilizado pelo evento.|  
|CPUTime|6|2|Tempo da CPU (em milissegundos) usado pelo evento.|  
|ProgressTotal|9|1|Andamento total.|  
|IntegerData|10|1|Dados Integer.|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectPath|14|8|Caminho do objeto. Uma lista de pais separados por vírgulas, começando com o pai do objeto.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|NTCanonicalUserName|40|8|Nome do usuário na forma canônica. Por exemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|ID de processo de servidor. Isso identifica exclusivamente uma sessão de usuário. Corresponde diretamente ao GUID de sessão usado pelo XML/A.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="query-subcube"></a>Subcubo de consulta  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|EventSubclass|1|1|A Subclasse de Evento oferece informações adicionais sobre cada classe de evento:<br /><br /> 1: Dados armazenados em cache<br /><br /> 2: Dados não armazenados em cache<br /><br /> 3: Dados internos<br /><br /> 4: Dados SQL<br /><br /> 11: Alteração estrutural do grupo de medidas<br /><br /> 12: Exclusão do grupos de medidas|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Horário em que o evento foi encerrado. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duration|5|2|Período de tempo (em milissegundos) utilizado pelo evento.|  
|CPUTime|6|2|Tempo da CPU (em milissegundos) usado pelo evento.|  
|ObjectPath|14|8|Caminho do objeto. Uma lista de pais separados por vírgulas, começando com o pai do objeto.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|SessionID|39|8|GUID da sessão.|  
|NTCanonicalUserName|40|8|Nome do usuário na forma canônica. Por exemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|ID de processo de servidor. Isso identifica exclusivamente uma sessão de usuário. Corresponde diretamente ao GUID de sessão usado pelo XML/A.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="query-subcube-verbose"></a>Subcubo de consulta detalhado  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|EventSubclass|1|1|A Subclasse de Evento oferece informações adicionais sobre cada classe de evento:<br /><br /> 21: Dados armazenados em cache<br /><br /> 22: Dados não armazenados em cache<br /><br /> 23: Dados internos<br /><br /> 24: Dados SQL|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Horário em que o evento foi encerrado. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duration|5|2|Período de tempo (em milissegundos) utilizado pelo evento.|  
|CPUTime|6|2|Tempo da CPU (em milissegundos) usado pelo evento.|  
|ObjectPath|14|8|Caminho do objeto. Uma lista de pais separados por vírgulas, começando com o pai do objeto.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|SessionID|39|8|GUID da sessão.|  
|NTCanonicalUserName|40|8|Nome do usuário na forma canônica. Por exemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|ID de processo de servidor. Isso identifica exclusivamente uma sessão de usuário. Corresponde diretamente ao GUID de sessão usado pelo XML/A.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="get-data-from-aggregation"></a>Obter Dados de Agregação  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Horário em que o evento foi encerrado. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duration|5|2|Período de tempo (em milissegundos) utilizado pelo evento.|  
|CPUTime|6|2|Tempo da CPU (em milissegundos) usado pelo evento.|  
|ObjectPath|14|8|Caminho do objeto. Uma lista de pais separados por vírgulas, começando com o pai do objeto.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|SessionID|39|8|GUID da sessão.|  
|NTCanonicalUserName|40|8|Nome do usuário na forma canônica. Por exemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|ID de processo de servidor. Isso identifica exclusivamente uma sessão de usuário. Corresponde diretamente ao GUID de sessão usado pelo XML/A.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="get-data-from-cache"></a>Obter Dados de Cache  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|EventSubclass|1|1|A subclasse de evento oferece informações adicionais sobre cada classe de evento.<br /><br /> 1: Obter dados de cache do grupo de medidas<br /><br /> 2: Obter dados de cache simples<br /><br /> 3: Obter dados de cache de cálculo<br /><br /> 4: Obter dados de cache persistente|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Horário em que o evento foi encerrado. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duration|5|2|Período de tempo (em milissegundos) utilizado pelo evento.|  
|CPUTime|6|2|Tempo da CPU (em milissegundos) usado pelo evento.|  
|ObjectPath|14|8|Caminho do objeto. Uma lista de pais separados por vírgulas, começando com o pai do objeto.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|SessionID|39|8|GUID da sessão.|  
|NTCanonicalUserName|40|8|Nome do usuário na forma canônica. Por exemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|ID de processo de servidor. Isso identifica exclusivamente uma sessão de usuário. Corresponde diretamente ao GUID de sessão usado pelo XML/A.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="vertipaq-se-query-begin"></a>Início da Consulta VertiPaq SE  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|EventSubclass|1|1|A Subclasse de Evento oferece informações adicionais sobre cada classe de evento:<br /><br /> 0: Verificação de VertiPaq<br /><br /> 1: Consulta de tabela<br /><br /> 2: Consulta de processamento de hierarquia de usuário<br /><br /> 10: Verificação interna de VertiPaq<br /><br /> 11: Consulta interna de tabela<br /><br /> 12: Consulta interna de processamento de hierarquia de usuário|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|JobID|7|1|ID do trabalho para andamento.|  
|SessionType|8|8|Tipo de sessão (qual entidade causou a operação).|  
|ObjectID|11|8|ID do objeto (note que esta é uma cadeia de caracteres).|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectName|13|8|Nome do objeto.|  
|ObjectPath|14|8|Caminho do objeto. Uma lista de pais separados por vírgulas, começando com o pai do objeto.|  
|ObjectReference|15|8|Referência ao objeto. Codificado como XML para todos os pais, usando marcas para descrever o objeto.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|NTUserName|32|8|Nome do usuário do Windows.|  
|NTDomainName|33|8|O domínio do Windows ao qual o usuário pertence.|  
|SessionID|39|8|GUID da sessão.|  
|NTCanonicalUserName|40|8|Nome do usuário na forma canônica. Por exemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|ID de processo de servidor. Isso identifica exclusivamente uma sessão de usuário. Corresponde diretamente ao GUID de sessão usado pelo XML/A.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="vertipaq-se-query-end"></a>Final da Consulta VertiPaq SE  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|EventSubclass|1|1|A subclasse de evento oferece informações adicionais sobre cada classe de evento.<br /><br /> 0: Verificação de VertiPaq<br /><br /> 1: Consulta de tabela<br /><br /> 10: Verificação interna de VertiPaq<br /><br /> 11: Consulta interna de tabela|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Horário em que o evento foi encerrado. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duration|5|2|Período de tempo (em milissegundos) utilizado pelo evento.|  
|CPUTime|6|2|Tempo da CPU (em milissegundos) usado pelo evento.|  
|JobID|7|1|ID do trabalho para andamento.|  
|SessionType|8|8|Tipo de sessão (qual entidade causou a operação).|  
|ProgressTotal|9|1|Andamento total.|  
|IntegerData|10|1|Dados Integer.|  
|ObjectID|11|8|ID do objeto (note que esta é uma cadeia de caracteres).|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectName|13|8|Nome do objeto.|  
|ObjectPath|14|8|Caminho do objeto. Uma lista de pais separados por vírgulas, começando com o pai do objeto.|  
|ObjectReference|15|8|Referência ao objeto. Codificado como XML para todos os pais, usando marcas para descrever o objeto.|  
|Severity|22|1|Nível de severidade de uma exceção.|  
|Success|23|1|1 = êxito. 0 = falha (por exemplo, 1 significa êxito de uma verificação de permissões e 0 significa uma falha dessa verificação).|  
|Erro|24|1|Número de erro de um determinado evento.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|NTUserName|32|8|Nome do usuário do Windows.|  
|NTDomainName|33|8|O domínio do Windows ao qual o usuário pertence.|  
|SessionID|39|8|GUID da sessão.|  
|NTCanonicalUserName|40|8|Nome do usuário na forma canônica. Por exemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|ID de processo de servidor. Isso identifica exclusivamente uma sessão de usuário. Corresponde diretamente ao GUID de sessão usado pelo XML/A.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="resource-usage"></a>Uso de recurso  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|NTUserName|32|8|Nome do usuário do Windows.|  
|NTDomainName|33|8|O domínio do Windows ao qual o usuário pertence.|  
|ClientProcessID|36|1|A ID do processo do aplicativo cliente.|  
|ApplicationName|37|8|Nome da aplicação cliente que criou a conexão ao servidor. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|  
|SessionID|39|8|GUID da sessão.|  
|NTCanonicalUserName|40|8|Nome do usuário na forma canônica. Por exemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|ID de processo de servidor. Isso identifica exclusivamente uma sessão de usuário. Corresponde diretamente ao GUID de sessão usado pelo XML/A.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="vertipaq-se-query-cache-match"></a>VertiPaq SE Query Cache Match  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|EventSubclass|1|1|A Subclasse de Evento oferece informações adicionais sobre cada classe de evento:<br /><br /> 0: Correspondência exata do cache de VertiPaq|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|JobID|7|1|ID do trabalho para andamento.|  
|SessionType|8|8|Tipo de sessão (qual entidade causou a operação).|  
|ObjectID|11|8|ID do objeto (note que esta é uma cadeia de caracteres).|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectName|13|8|Nome do objeto.|  
|ObjectPath|14|8|Caminho do objeto. Uma lista de pais separados por vírgulas, começando com o pai do objeto.|  
|ObjectReference|15|8|Referência ao objeto. Codificado como XML para todos os pais, usando marcas para descrever o objeto.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|NTUserName|32|8|Nome do usuário do Windows.|  
|NTDomainName|33|8|O domínio do Windows ao qual o usuário pertence.|  
|SessionID|39|8|GUID da sessão.|  
|NTCanonicalUserName|40|8|Nome do usuário na forma canônica. Por exemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|ID de processo de servidor. Isso identifica exclusivamente uma sessão de usuário. Corresponde diretamente ao GUID de sessão usado pelo XML/A.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="direct-query-begin"></a>Direct Query Begin  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Horário em que o evento foi encerrado. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duration|5|2|Período de tempo (em milissegundos) utilizado pelo evento.|  
|CPUTime|6|2|Tempo da CPU (em milissegundos) usado pelo evento.|  
|JobID|7|1|ID do trabalho para andamento.|  
|SessionType|8|8|Tipo de sessão (qual entidade causou a operação).|  
|IntegerData|10|1|Dados Integer.|  
|ObjectID|11|8|ID do objeto (note que esta é uma cadeia de caracteres).|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectName|13|8|Nome do objeto.|  
|ObjectPath|14|8|Caminho do objeto. Uma lista de pais separados por vírgulas, começando com o pai do objeto.|  
|Severity|22|1|Nível de severidade de uma exceção.|  
|Success|23|1|1 = êxito. 0 = falha (por exemplo, 1 significa êxito de uma verificação de permissões e 0 significa uma falha dessa verificação).|  
|Erro|24|1|Número de erro de um determinado evento.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|ClientProcessID|36|1|A ID do processo do aplicativo cliente.|  
|SessionID|39|8|GUID da sessão.|  
|SPID|41|1|ID de processo de servidor. Isso identifica exclusivamente uma sessão de usuário. Corresponde diretamente ao GUID de sessão usado pelo XML/A.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="direct-query-end"></a>Direct Query End  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|CurrentTime|2|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Horário de início do evento, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Horário em que o evento foi encerrado. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duration|5|2|Período de tempo (em milissegundos) utilizado pelo evento.|  
|CPUTime|6|2|Tempo da CPU (em milissegundos) usado pelo evento.|  
|JobID|7|1|ID do trabalho para andamento.|  
|SessionType|8|8|Tipo de sessão (qual entidade causou a operação).|  
|IntegerData|10|1|Dados Integer.|  
|ObjectID|11|8|ID do objeto (note que esta é uma cadeia de caracteres).|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectName|13|8|Nome do objeto.|  
|ObjectPath|14|8|Caminho do objeto. Uma lista de pais separados por vírgulas, começando com o pai do objeto.|  
|Severity|22|1|Nível de severidade de uma exceção.|  
|Success|23|1|1 = êxito. 0 = falha (por exemplo, 1 significa êxito de uma verificação de permissões e 0 significa uma falha dessa verificação).|  
|Erro|24|1|Número de erro de um determinado evento.|  
|ConnectionID|25|1|ID de conexão exclusiva.|  
|DatabaseName|28|8|Nome do banco de dados no qual a instrução do usuário está sendo executada.|  
|ClientProcessID|36|1|A ID do processo do aplicativo cliente.|  
|SessionID|39|8|GUID da sessão.|  
|SPID|41|1|ID de processo de servidor. Isso identifica exclusivamente uma sessão de usuário. Corresponde diretamente ao GUID de sessão usado pelo XML/A.|  
|TextData|42|9|Dados de texto associados ao evento.|  
|ServerName|43|8|Nome do servidor que gera o evento.|  
  
## <a name="see-also"></a>Consulte também  
 [Categoria de eventos de processamento de consulta](../../analysis-services/trace-events/query-processing-events-category.md)  
  
  
