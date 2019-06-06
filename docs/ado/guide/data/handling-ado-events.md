---
title: Manipulando eventos ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO]
- ADO, events
- event handlers [ADO]
ms.assetid: e9003457-0762-48b3-942f-0820266b158f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 162cac52920b076e4388a74a251cd347137f49cd
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702003"
---
# <a name="handling-ado-events"></a>Manipular eventos ADO
O modelo de evento ADO dá suporte a determinadas operações síncronas e assíncronas do ADO que emitem *eventos*, ou notificações, antes do início da operação ou após a conclusão. Um evento é, na verdade, uma chamada para uma rotina de manipulador de eventos que você define no seu aplicativo.  
  
 Se você fornecer procedimentos ou funções de manipulador para o grupo de eventos que ocorrem antes do início da operação, você pode examinar ou modificar os parâmetros que foram passados para a operação. Porque ele não foi executado ainda, você pode cancelar a operação ou permitir que ela seja concluída.  
  
 Os eventos que ocorrem após a conclusão de uma operação são especialmente importantes se você usar ADO de maneira assíncrona. Por exemplo, um aplicativo que inicia um assíncrono [Recordset.Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) operação é notificada por um evento de conclusão de execução quando conclui a operação.  
  
 Usando o modelo de evento ADO adiciona alguma sobrecarga ao seu aplicativo, mas oferece muito mais flexibilidade do que outros métodos de lidar com operações assíncronas, como o monitoramento do [estado](../../../ado/reference/ado-api/state-property-ado.md) propriedade de um objeto com um loop.  
  
> [!NOTE]
>  Para manipular eventos, ADO precisa ter uma bomba de mensagem ou ser usado em um modelo de single-threaded apartment (STA). Eventos ADO são tratados internamente com a criação de uma janela oculta. ADO posta mensagens para esta janela quando eventos precisam ser acionado. Isso é feito para garantir que os eventos são enviados para o thread que chamou **IConnectionPoint::** no ponto de conexão. Essa arquitetura pode causar problemas quando o thread que deve receber as notificações não bomba de mensagens de janela. Problemas em potencial incluem eventos ADO não estão sendo distribuídos para o thread e difusões de janela global atingindo o tempo limite e, possivelmente, retardando todo o sistema porque as janelas ocultas não processar as mensagens. Os threads STA normalmente têm uma bomba de mensagens em execução para que esse problema não se manifestar em threads STA. Threads MTA, no entanto, geralmente não têm uma bomba de mensagem para que o problema geralmente se manifestará em threads MTA.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)  
  
-   [Tipos de eventos](../../../ado/guide/data/types-of-events.md)  
  
-   [Parâmetros de evento](../../../ado/guide/data/event-parameters.md)  
  
-   [Como os manipuladores de eventos funcionam em conjunto](../../../ado/guide/data/how-event-handlers-work-together.md)  
  
-   [Instanciação de evento ADO por linguagem](../../../ado/guide/data/ado-event-instantiation-by-language.md)  
  
## <a name="see-also"></a>Consulte também  
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Instanciação de evento ADO por linguagem](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [Eventos ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Parâmetros de evento](../../../ado/guide/data/event-parameters.md)   
 [Tipos de eventos](../../../ado/guide/data/types-of-events.md)
