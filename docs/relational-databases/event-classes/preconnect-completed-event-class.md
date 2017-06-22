---
title: Classe de evento PreConnect:Completed | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- PreConnect:Completed Event Class
ms.assetid: 7ed2f620-6511-4985-9961-d2927c2b1759
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5f6bba668ddd25925ede8fe8cf71e4f1775f3dd9
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="preconnectcompleted-event-class"></a>Classe de evento PreConnect:Completed
  A classe de evento PreConnect:Completed indica quando um gatilho LOGON ou a função de classificação do Administrador de Recursos conclui a execução.  
  
## <a name="preconnectcompleted-event-class-data-columns"></a>Colunas de dados da classe de evento PreConnect:Completed  
  
|Nome da coluna de dados|Tipo de dados|Descrição|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|EventClass|**int**|216|27|Não|  
|SPID|**int**|O ID de processo de servidor que dispara este evento.|12|Sim|  
|EventSubClass|**int**|1 para a função de classificador definida pelo usuário.|21|Sim|  
|StartTime|**datetime**|A hora que inicia a função de classificador definida pelo usuário.|14|Sim|  
|EndTime|**datetime**|A hora que inicia a função de classificador definida pelo usuário.|15|Sim|  
|Duration|**bigint**|O número de hora, em microssegundo, usado pela função de classificação.|13|Sim|  
|ObjectID|**int**|A ID do objeto do classificador definido pelo usuário.|22|Sim|  
|CPU|**int**|Uso de CPU em milissegundos.|18|Sim|  
|Reads|**int**|O número de leituras lógicas.|16|Sim|  
|Writes|**int**|O número de gravações lógicas.|17|Sim|  
|GroupID|**int**|O ID do grupo de cargas de trabalho classificado.|66|Sim|  
|Erro|**int**|O último número do erro, caso a função de classificação definida pelo usuário não seja executada.|31|Sim|  
|Estado|**int**|O estado do último erro.|30|Sim|  
|TargetUserName|**sysname**|O valor de retorno (nome do grupo de cargas de trabalho) para a função de classificação definida pelo usuário, caso o sistema não consiga encontrar um grupo ativo correspondente. Caso contrário, essa coluna será definida como NULL.|39|Sim|  
|ObjectName|**nvarchar(256)**|O nome de duas partes da função de classificador definida pelo usuário. Por exemplo, dbo.classifier.|34|Sim|  
  
## <a name="see-also"></a>Consulte também  
 [Eventos estendidos](../../relational-databases/extended-events/extended-events.md)   
 [Classe de evento PreConnect:Starting](../../relational-databases/event-classes/preconnect-starting-event-class.md)   
 [Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md)  
  
  
