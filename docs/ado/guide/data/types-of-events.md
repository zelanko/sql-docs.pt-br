---
title: Tipos de eventos | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- EventComplete event [ADO]
- events [ADO], types
- Will events [ADO]
- complete events [ADO]
- WillEvent event [ADO]
ms.assetid: f3327ea0-635a-43d4-bd78-c1674f62f1a2
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 502c77b55eb0e3a60497fa10bf9fe8c8a412dc4d
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="types-of-events"></a>Tipos de eventos
Há dois tipos básicos de eventos. "Será eventos," que é chamado antes do início de uma operação, geralmente incluem "Será" em seus nomes — por exemplo, **WillChangeRecordset** ou **WillConnect**. Os eventos que são chamados após um evento foi concluído normalmente incluem "Completo" em seus nomes — por exemplo, **RecordChangeComplete** ou **ConnectComplete**. Existem exceções — como **InfoMessage** — mas elas ocorrem após a operação associada.  
  
## <a name="will-events"></a>Será eventos  
 Manipuladores de eventos é chamado antes do início da operação oferece a oportunidade de examinar ou modificar os parâmetros de operação e, em seguida, cancelar a operação ou permitir que ela seja concluída. Essas rotinas de manipulador de eventos geralmente têm nomes no formato * *será*evento** *.  
  
## <a name="complete-events"></a>Eventos de conclusão  
 Chamado após a conclusão de uma operação de manipuladores de eventos podem notificar o aplicativo que uma operação foi concluída. Esse é um manipulador de eventos também é notificado quando um manipulador de eventos será cancela uma operação pendente. Essas rotinas de manipulador de eventos geralmente têm nomes no formato ** *evento*concluir**.  
  
 Será e eventos de conclusão são geralmente usados em pares.  
  
## <a name="other-events"></a>Outros eventos  
 Manipuladores de eventos — ou seja, os eventos cujos nomes não estão no formato * *será*evento** * ou ** *evento*concluir** — são chamados somente Depois que uma operação é concluída. Esses eventos são **Disconnect**, **EndOfRecordset**, e **InfoMessage**.  
  
## <a name="see-also"></a>Consulte também  
 [Resumo de manipulador de eventos de ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Instanciação de evento ADO por idioma](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [Parâmetros de evento](../../../ado/guide/data/event-parameters.md)   
 [Como os manipuladores de eventos funcionam em conjunto](../../../ado/guide/data/how-event-handlers-work-together.md)

