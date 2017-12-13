---
title: "Colunas de dados de eventos de notificação | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: Notification Events event category
ms.assetid: 0ecf06da-1586-415a-9da8-60d4c634f030
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 39c93ff427048fe1893dd78f8fe35abc0b52885b
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="notification-events-data-columns"></a>Colunas de dados de eventos de notificação
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Eventos de notificação são eventos que não são causados diretamente por usuários do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Por exemplo, as notificações acontecem por causa de usuários que atualizam tabelas base para cache pró-ativo.  
  
 A categoria Notifications Events tem a seguinte classe de evento:  
  
|**ID do evento**|**Nome do evento**|**Descrição do evento**|  
|------------------|--------------------|---------------------------|  
|39|Notification|Evento de notificação.|  
|40|User Defined|Evento definido pelo usuário.|  
  
 A tabela a seguir lista as colunas de dados da classe de evento.  
  
## <a name="notification"></a>Notification  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|EventSubclass|1|1|A subclasse de evento oferece informações adicionais sobre cada classe de evento.<br /><br /> A seguinte **Id da Subclasse**:<br />                      Os pares do**Nome da Subclasse** são definidos:<br /><br /> 0: Início de Cache Proativo<br /><br /> 1: Final do Cache Proativo<br /><br /> 2: Flight Recorder Iniciado<br /><br /> 3: Flight Recorder Parado<br /><br /> 4: Propriedades de Configuração Atualizadas<br /><br /> 5: Rastreamento do SQL<br /><br /> 6: Objeto Criado<br /><br /> 7: Objeto Excluído<br /><br /> 8: Objeto Alterado<br /><br /> 9: Início da Sondagem do Cache Proativo<br /><br /> 10: Final da Sondagem do Cache Proativo<br /><br /> 11: Início do Instantâneo do Flight Recorder<br /><br /> 12: Final do Instantâneo do Flight Recorder<br /><br /> 13: Cache Proativo: objeto notificável atualizado<br /><br /> 14: Processamento Lento: iniciar processamento<br /><br /> 15: Processamento Lento: processamento concluído<br /><br /> 16: Início do Evento SessionOpened<br /><br /> 17: Final do Evento SessionOpened<br /><br /> 18: Início do Evento SessionClosing<br /><br /> 19: Final do Evento SessionClosing<br /><br /> 20: Início do Evento CubeOpened<br /><br /> 21: Final do Evento CubeOpened<br /><br /> 22: Início do Evento CubeClosing<br /><br /> 23: Final do Evento CubeClosing<br /><br /> 24: Anulação da transação solicitada|  
|CurrentTime|2|5|Contém a hora atual do evento de notificação, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Contém a hora em que o evento iniciou, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Contém a hora em que o evento terminou. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duration|5|2|Contém a quantidade de tempo (em milissegundos) utilizado pelo evento.|  
|IntegerData|10|1|Contém os dados inteiros associados ao evento de notificação. Quando a coluna EventSubclass é igual a 8, os valores são:<br /><br /> 1 = Criado<br /><br /> 2 = Excluído<br /><br /> 3 = Propriedades de objeto alteradas<br /><br /> 4 = Propriedades dos filhos do objeto alteradas<br /><br /> 6 = Filhos adicionados<br /><br /> 7 = Filhos excluídos<br /><br /> 8 = Objeto completamente processado<br /><br /> 9 = Objeto parcialmente processado<br /><br /> 10 = Objeto não processado<br /><br /> 11 = Objeto completamente otimizado<br /><br /> 12 = Objeto parcialmente otimizado<br /><br /> 13 = Objeto não otimizado|  
|ObjectID|11|8|Contém a ID de Objeto para a qual esta notificação é emitida; este é um valor da cadeia de caracteres.|  
|ObjectType|12|1|Contém o tipo de objeto associado ao evento de notificação.|  
|ObjectName|13|8|Contém o nome do objeto associado ao evento de notificação.|  
|ObjectPath|14|8|Contém o caminho do objeto associado ao evento de notificação. O caminho é retornado como uma lista de pais separados por vírgula, começando com o pai do objeto.|  
|ObjectReference|15|8|Contém a referência de objeto para o evento final do relatório de andamento. A referência de objeto é codificada como XML por todos os pais usando marcas para descrever o objeto.|  
|ConnectionID|25|1|Contém a ID de conexão exclusiva associada ao evento de notificação.|  
|DatabaseName|28|8|Contém o nome do banco de dados no qual o evento de notificação ocorreu.|  
|NTUserName|32|8|Contém o nome de usuário do Windows associado ao evento de notificação.|  
|NTDomainName|33|8|O domínio do Windows ao qual o usuário pertence.|  
|SessionID|39|8|Contém a ID de sessão associada ao evento de notificação.|  
|NTCanonicalUserName|40|8|Contém o nome de usuário do Windows associado ao evento de notificação. O nome de usuário está na forma canônica. Por exemplo, engineering.microsoft.com/software/user.|  
|SPID|41|1|Contém a identificação do processo do servidor (SPID) que identifica de modo exclusivo a sessão de usuário associada ao evento de notificação. A SPID corresponde diretamente à GUID de sessão usada pelo XMLA.|  
|TextData|42|9|Contém os dados de texto associados ao evento de notificação.|  
|ServerName|43|8|Contém o nome da instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] na qual ocorreu o evento de notificação.|  
|RequestProperties|45|9|Contém as propriedades da solicitação XMLA.|  
  
## <a name="user-defined"></a>User Defined  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|EventSubclass|1|1|Uma subclasse de evento de usuário específico que fornece informações adicionais sobre cada classe de evento.|  
|CurrentTime|2|5|Contém a hora atual do evento de notificação, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|IntegerData|10|1|Informações de evento definidas por um usuário específico.|  
|ConnectionID|25|1|Contém a ID de conexão exclusiva associada ao evento de notificação.|  
|DatabaseName|28|8|Contém o nome do banco de dados no qual o evento de notificação ocorreu.|  
|NTUserName|32|8|Contém o nome de usuário do Windows associado ao evento de notificação.|  
|NTDomainName|33|8|O domínio do Windows ao qual o usuário pertence.|  
|SessionID|39|8|Contém a ID de sessão associada ao evento de notificação.|  
|NTCanonicalUserName|40|8|Contém o nome de usuário do Windows associado ao evento de notificação. O nome de usuário está na forma canônica. Por exemplo, engineering.microsoft.com/software/user.|  
|SPID|41|1|Contém a identificação do processo do servidor (SPID) que identifica de modo exclusivo a sessão de usuário associada ao evento de notificação. A SPID corresponde diretamente à GUID de sessão usada pelo XMLA.|  
|TextData|42|9|Contém os dados de texto associados ao evento de notificação.|  
|ServerName|43|8|Contém o nome da instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] na qual ocorreu o evento de notificação.|  
  
## <a name="see-also"></a>Consulte também  
 [Notification Events Event Category](../../analysis-services/trace-events/notification-events-event-category.md)  
  
  
