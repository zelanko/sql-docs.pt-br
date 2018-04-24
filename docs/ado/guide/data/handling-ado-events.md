---
title: Manipulação de eventos de ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO]
- ADO, events
- event handlers [ADO]
ms.assetid: e9003457-0762-48b3-942f-0820266b158f
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e03bf8916836cf271aa77546d71c60049b39235e
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="handling-ado-events"></a>Manipulação de eventos de ADO
O modelo de evento do ADO dá suporte a determinadas operações síncronas e assíncronas do ADO que emitem *eventos*, ou notificações, antes do início da operação ou após a sua conclusão. Um evento é realmente uma chamada para uma rotina de manipulador de eventos que você define no seu aplicativo.  
  
 Se você fornecer procedimentos ou funções de manipulador para o grupo de eventos que ocorrem antes do início da operação, você pode examinar ou modificar os parâmetros que foram passados para a operação. Porque ele não tiver sido executado ainda, você pode cancelar a operação ou permitir que ela seja concluída.  
  
 Os eventos que ocorrem após a conclusão de uma operação são especialmente importantes se você usar ADO de forma assíncrona. Por exemplo, um aplicativo que inicia uma assíncrona [Recordset.Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) operação é notificada por um evento de conclusão de execução quando conclui a operação.  
  
 Usar o modelo de evento do ADO aumenta a sobrecarga de seu aplicativo, mas fornece muito mais flexibilidade do que outros métodos para lidar com operações assíncronas, como monitoramento de [estado](../../../ado/reference/ado-api/state-property-ado.md) propriedade de um objeto com um loop.  
  
> [!NOTE]
>  Para manipular eventos, ADO precisa ter uma bomba de mensagem ou ser usado em um modelo de single-threaded apartment (STA). Eventos de ADO são tratados internamente por meio da criação de uma janela oculta. ADO envia mensagens para esta janela quando eventos precisam ser acionado. Isso é feito para garantir que os eventos são enviados para o thread de chamada **IConnectionPoint::** no ponto de conexão. Essa arquitetura pode causar problemas quando o thread que deve receber as notificações não bomba de mensagens de janela. Problemas em potencial incluem eventos de ADO não estão sendo distribuídos para o thread e transmissões de janela global tempo limite e possivelmente lento todo o sistema porque os windows ocultos não processam as mensagens. Threads STA normalmente têm um bombeamento de mensagens em execução para que esse problema não se manifestar em threads STA. Threads do MTA, no entanto, normalmente não tem uma bomba de mensagem para que o problema será normalmente se manifestar em threads do MTA.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)  
  
-   [Tipos de eventos](../../../ado/guide/data/types-of-events.md)  
  
-   [Parâmetros de evento](../../../ado/guide/data/event-parameters.md)  
  
-   [Como os manipuladores de eventos funcionam em conjunto](../../../ado/guide/data/how-event-handlers-work-together.md)  
  
-   [Instanciação de evento ADO por linguagem](../../../ado/guide/data/ado-event-instantiation-by-language.md)  
  
## <a name="see-also"></a>Consulte também  
 [Resumo de manipulador de eventos de ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Instanciação de evento ADO por idioma](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [Eventos de ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Parâmetros de evento](../../../ado/guide/data/event-parameters.md)   
 [Tipos de eventos](../../../ado/guide/data/types-of-events.md)
