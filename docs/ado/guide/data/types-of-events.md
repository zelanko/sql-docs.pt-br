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
manager: craigg
ms.openlocfilehash: 461b9ea2196fed61587b1a9e20cc21feced258da
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52535048"
---
# <a name="types-of-events"></a>Tipos de eventos
Há dois tipos básicos de eventos. "Será eventos," que é chamado antes do início de uma operação, geralmente incluem "Será" em seus nomes - por exemplo, **eventos WillChangeRecordset** ou **WillConnect**. Eventos que são chamados após um evento foi concluído normalmente incluem "Concluído" em seus nomes - por exemplo, **RecordChangeComplete** ou **eventos ConnectComplete**. Existem exceções - como **InfoMessage** - mas eles ocorrem após a operação associada foi concluída.  
  
## <a name="will-events"></a>Será eventos  
 Manipuladores de eventos chamado antes do início da operação de oferece a você a oportunidade de examinar ou modificar os parâmetros da operação e, em seguida, cancelar a operação ou permitir que ela seja concluída. Essas rotinas de manipulador de eventos geralmente têm nomes no formato **serão*evento * * *.  
  
## <a name="complete-events"></a>Eventos de conclusão  
 Chamado após a conclusão de uma operação de manipuladores de eventos podem notificar o aplicativo que concluiu uma operação. Um manipulador de eventos desse tipo também é notificado quando um manipulador de eventos será cancela uma operação pendente. Essas rotinas de manipulador de eventos geralmente têm nomes no formato ***evento * concluir**.  
  
 Será e eventos de conclusão normalmente são usados em pares.  
  
## <a name="other-events"></a>Outros eventos  
 Os manipuladores de eventos - ou seja, os eventos cujos nomes não estão no formato **serão * evento*** ou ***evento * concluir** -são chamados somente depois que uma operação é concluída. Esses eventos são **Disconnect**, **EndOfRecordset**, e **InfoMessage**.  
  
## <a name="see-also"></a>Consulte também  
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Instanciação de evento ADO por linguagem](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [Parâmetros de evento](../../../ado/guide/data/event-parameters.md)   
 [Como os manipuladores de eventos funcionam em conjunto](../../../ado/guide/data/how-event-handlers-work-together.md)
