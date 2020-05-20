---
title: Tipos de eventos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- EventComplete event [ADO]
- events [ADO], types
- Will events [ADO]
- complete events [ADO]
- WillEvent event [ADO]
ms.assetid: f3327ea0-635a-43d4-bd78-c1674f62f1a2
author: rothja
ms.author: jroth
ms.openlocfilehash: f8d0dd197b5f74b25aad2f7e9e888165c2dc02ba
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759022"
---
# <a name="types-of-events"></a>Tipos de eventos
Há dois tipos básicos de eventos. "Serão eventos", que são chamados antes de uma operação ser iniciada, normalmente incluem "o" em seus nomes-por exemplo, **WillChangeRecordset** ou **WillConnect**. Eventos que são chamados após a conclusão de um evento geralmente incluem "concluído" em seus nomes-por exemplo, **RecordChangeComplete** ou **ConnectComplete**. Existem exceções-como **InfoMessage** -mas elas ocorrem após a conclusão da operação associada.  
  
## <a name="will-events"></a>Eventos serão  
 Os manipuladores de eventos chamados antes do início da operação oferecem a oportunidade de examinar ou modificar os parâmetros da operação e, em seguida, cancelar a operação ou permitir que ela seja concluída. Essas rotinas de manipulador de eventos geralmente têm nomes no <strong>formulário*Event*.</strong>  
  
## <a name="complete-events"></a>Concluir eventos  
 Os manipuladores de eventos chamados após a conclusão de uma operação podem notificar o aplicativo de que uma operação foi concluída. Esse manipulador de eventos também é notificado quando um manipulador de eventos for cancelar uma operação pendente. Essas rotinas de manipulador de eventos geralmente têm nomes de <strong> *evento*de formulário concluídos</strong>.  
  
 Os eventos serão normalmente usados em pares.  
  
## <a name="other-events"></a>Outros eventos  
 Os outros manipuladores de eventos – ou seja, os eventos cujos nomes não estão no formato <strong>serão*Event* </strong> ou <strong> *Event*Complete</strong> -são chamados somente após a conclusão de uma operação. Esses eventos são **Disconnect**, **EndOfRecordset**e **InfoMessage**.  
  
## <a name="see-also"></a>Consulte Também  
 [Resumo do manipulador de eventos do ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Instanciação de evento ADO por idioma](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [Parâmetros do evento](../../../ado/guide/data/event-parameters.md)   
 [Como os manipuladores de eventos funcionam em conjunto](../../../ado/guide/data/how-event-handlers-work-together.md)
