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
ms.openlocfilehash: 452259b6e4e406d7a406211a9e9b42ebbf60da53
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925221"
---
# <a name="handling-ado-events"></a>Manipular eventos ADO
O modelo de evento ADO dá suporte a determinadas operações de ADO síncronas e assíncronas que emitem *eventos*, ou notificações, antes que a operação seja iniciada ou após ser concluída. Um evento é, na verdade, uma chamada para uma rotina de manipulador de eventos que você define em seu aplicativo.  
  
 Se você fornecer funções de manipulador ou procedimentos para o grupo de eventos que ocorrem antes do início da operação, poderá examinar ou modificar os parâmetros que foram passados para a operação. Como ele ainda não foi executado, você pode cancelar a operação ou permitir que ela seja concluída.  
  
 Os eventos que ocorrem após a conclusão de uma operação são especialmente importantes se você usar o ADO de forma assíncrona. Por exemplo, um aplicativo que inicia um [conjunto de registros assíncrono.](../../../ado/reference/ado-api/open-method-ado-recordset.md) a operação de abertura é notificada por um evento de execução completa quando a operação é concluída.  
  
 O uso do modelo de evento ADO adiciona alguma sobrecarga ao seu aplicativo, mas fornece muito mais flexibilidade do que outros métodos de lidar com operações assíncronas, como o monitoramento da propriedade [State](../../../ado/reference/ado-api/state-property-ado.md) de um objeto com um loop.  
  
> [!NOTE]
>  Para lidar com eventos, o ADO precisa ter uma bomba de mensagem ou ser usada em um modelo STA (single-threaded apartment). Os eventos ADO são manipulados internamente pela criação de uma janela oculta. O ADO envia mensagens para essa janela quando os eventos precisam ser acionados. Isso é feito para garantir que os eventos sejam enviados para o thread que chamou **IConnectionPoint:: Advise** no ponto de conexão. Essa arquitetura pode causar problemas quando o thread que deve receber as notificações não bombea as mensagens da janela. Problemas potenciais incluem eventos ADO que não estão sendo entregues ao thread e as difusões de janela global expiram e possivelmente atrasando o sistema inteiro porque as janelas ocultas não processam as mensagens. Os threads STA normalmente têm uma bomba de mensagem em execução, portanto, esse problema não se manifesta em threads STA. Os threads MTA, no entanto, normalmente não têm uma bomba de mensagem, portanto, o problema normalmente se manifestará em threads MTA.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)  
  
-   [Tipos de eventos](../../../ado/guide/data/types-of-events.md)  
  
-   [Parâmetros de evento](../../../ado/guide/data/event-parameters.md)  
  
-   [Como os manipuladores de eventos funcionam em conjunto](../../../ado/guide/data/how-event-handlers-work-together.md)  
  
-   [Instanciação de evento ADO por linguagem](../../../ado/guide/data/ado-event-instantiation-by-language.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Resumo do manipulador de eventos do ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Instanciação de evento ADO por idioma](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [Eventos ADO](../../../ado/reference/ado-api/ado-events.md)   
 [Parâmetros do evento](../../../ado/guide/data/event-parameters.md)   
 [Tipos de eventos](../../../ado/guide/data/types-of-events.md)
