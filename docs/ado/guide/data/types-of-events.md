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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c02d8d115a4336470c0e0d32aebabea63c05ab0b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67923810"
---
# <a name="types-of-events"></a>Tipos de eventos
Há dois tipos básicos de eventos. "Serão eventos", que são chamados antes de uma operação ser iniciada, normalmente incluem "o" em seus nomes-por exemplo, **WillChangeRecordset** ou **WillConnect**. Eventos que são chamados após a conclusão de um evento geralmente incluem "concluído" em seus nomes-por exemplo, **RecordChangeComplete** ou **ConnectComplete**. Existem exceções-como **InfoMessage** -mas elas ocorrem após a conclusão da operação associada.  
  
## <a name="will-events"></a>Eventos serão  
 Os manipuladores de eventos chamados antes do início da operação oferecem a oportunidade de examinar ou modificar os parâmetros da operação e, em seguida, cancelar a operação ou permitir que ela seja concluída. Essas rotinas de manipulador de eventos geralmente têm nomes no <strong>formulário**.</strong>  
  
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
