---
title: Como os manipuladores de eventos funcionam em conjunto | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO], about event handlers
- unpaired event handlers [ADO]
- paired event handlers [ADO]
- single event handlers [ADO]
- event handlers [ADO]
- multiple object event handlers [ADO]
ms.assetid: a86c8a02-dd69-420d-8a47-0188b339858d
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5a50612e9bd16eafc2afb74c39ba2e5de7285e5a
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35271965"
---
# <a name="how-event-handlers-work-together"></a>Como os manipuladores de eventos funcionam em conjunto
A menos que você estiver programando no Visual Basic, todos os manipuladores de eventos para **Conexão** e **registros** eventos devem ser implementados, independentemente se você realmente processar todos os eventos. A quantidade de trabalho de implementação, que você precisa fazer depende de sua linguagem de programação. Para obter mais informações, consulte [ADO instanciação de eventos por idioma](../../../ado/guide/data/ado-event-instantiation-by-language.md).  
  
## <a name="paired-event-handlers"></a>Manipuladores de eventos par  
 Cada manipulador de eventos será possui um tipo de **concluir** manipulador de eventos. Por exemplo, quando seu aplicativo altera o valor de um campo, o **WillChangeField** manipulador de eventos é chamado. Se a alteração for aceitável, seu aplicativo deixa o **adStatus** parâmetro inalterados e a operação é executada. Quando a operação for concluída, um **FieldChangeComplete** evento notifica o aplicativo que a operação seja concluída. Se ela foi concluída com êxito, **adStatus** contém **adStatusOK**; caso contrário, **adStatus** contém **adStatusErrorsOccurred** e Você deve verificar o **erro** objeto para determinar a causa do erro.  
  
 Quando **WillChangeField** é chamado, você pode determinar que a alteração não deve ser feita. Nesse caso, defina **adStatus** para **adStatusCancel.** A operação será cancelada e o **FieldChangeComplete** evento recebe um **adStatus** valor **adStatusErrorsOccurred**. O **erro** objeto contém **adErrOperationCancelled** para que seu **FieldChangeComplete** manipulador sabe que a operação foi cancelada. No entanto, você precisa verificar o valor da **adStatus** parâmetro antes de alterá-lo, porque a definição **adStatus** para **adStatusCancel** não tem efeito se o parâmetro foi definido para **adStatusCantDeny** na entrada para o procedimento.  
  
 Às vezes, uma operação pode gerar mais de um evento. Por exemplo, o **registros** objeto tiver emparelhado eventos para **campo** alterações e **registro** alterações. Quando seu aplicativo altera o valor de um **campo**, o **WillChangeField** manipulador de eventos é chamado. Se determinar que a operação possa continuar, o **WillChangeRecord** também é criado o manipulador de eventos. Se esse manipulador também permite que o evento continuar, a alteração é feita e o **FieldChangeComplete** e **RecordChangeComplete** manipuladores de eventos são chamados. A ordem em que são chamados de manipuladores de eventos será para uma determinada operação não é definida, portanto evite escrever código que depende de chamar manipuladores em uma determinada sequência.  
  
 Em instâncias quando vários eventos serão forem gerados, um dos eventos pode cancelar a operação pendente. Por exemplo, quando seu aplicativo altera o valor de um **campo**, ambos **WillChangeField** e **WillChangeRecord** manipuladores de eventos normalmente serão chamados. No entanto, se a operação foi cancelada no primeiro manipulador de eventos, seus associado **concluir** manipulador é chamado imediatamente com **adStatusOperationCancelled**. O segundo manipulador nunca será chamado. Se, no entanto, o primeiro manipulador de eventos permite que o evento continuar, o manipulador de eventos será chamado. Se, em seguida, cancela a operação, ambos **concluir** eventos serão chamados como nos exemplos anteriores.  
  
## <a name="unpaired-event-handlers"></a>Manipuladores de eventos não emparelhados  
 Desde que o status é passado para o evento não será **adStatusCantDeny**, você pode desativar as notificações de eventos para qualquer evento retornando **adStatusUnwantedEvent** no *Status*parâmetro. Por exemplo, quando seu **concluir** manipulador de eventos é chamado na primeira vez, você pode retornar **adStatusUnwantedEvent**. Posteriormente, você receberá apenas **será** eventos. No entanto, alguns eventos podem ser acionados por mais de um motivo. Nesse caso, o evento terá um *motivo* parâmetro. Ao retornar **adStatusUnwantedEvent**, você irá parar de receber notificações para o evento somente quando eles ocorrem por esse motivo específico. Em outras palavras, você receberá potencialmente notificação para cada motivo possível que o evento foi disparado.  
  
 Único **será** manipuladores de eventos podem ser útil quando você deseja examinar os parâmetros que serão usados em uma operação. Você pode modificar os parâmetros da operação ou cancelar a operação.  
  
 Como alternativa, deixe **concluir** notificação de eventos habilitada. Quando o primeiro manipulador de eventos será é chamado, retornar **adStatusUnwantedEvent**. Posteriormente, você receberá apenas **concluir** eventos.  
  
 Único **concluir** manipuladores de eventos podem ser útil para gerenciar operações assíncronas. Cada operação assíncrona tenha adequados **concluir** eventos.  
  
 Por exemplo, pode levar muito tempo para popular um grande [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto. Se seu aplicativo é escrito corretamente, você pode iniciar um `Recordset.Open(...,adAsyncExecute)` operação e continuar com outros tipos de processamento. Eventualmente será notificado quando o **registros** é preenchido por um **ExecuteComplete** eventos.  
  
## <a name="single-event-handlers-and-multiple-objects"></a>Manipuladores de evento único e vários objetos  
 A flexibilidade de uma linguagem de programação como Microsoft Visual C++® permite que você tenha um eventos do processo de manipulador de eventos de vários objetos. Por exemplo, você pode ter uma **Disconnect** eventos do processo de manipulador de eventos de vários **Conexão** objetos. Se uma das conexões terminou, o **Disconnect** manipulador de eventos será chamado. Você pode dizer qual conexão causou o evento porque o parâmetro de objeto do manipulador de eventos deve ser definido como correspondente **Conexão** objeto.  
  
> [!NOTE]
>  Essa técnica não pode ser usada no Visual Basic, porque o idioma pode correlacionar apenas um objeto para um manipulador de eventos.  
  
## <a name="see-also"></a>Consulte também  
 [Resumo de manipulador de eventos de ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Instanciação de evento ADO por idioma](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [Parâmetros de evento](../../../ado/guide/data/event-parameters.md)   
 [Tipos de eventos](../../../ado/guide/data/types-of-events.md)
