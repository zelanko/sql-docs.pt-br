---
title: Como os manipuladores de eventos funcionam juntos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO], about event handlers
- unpaired event handlers [ADO]
- paired event handlers [ADO]
- single event handlers [ADO]
- event handlers [ADO]
- multiple object event handlers [ADO]
ms.assetid: a86c8a02-dd69-420d-8a47-0188b339858d
author: rothja
ms.author: jroth
ms.openlocfilehash: 98144b1dacb406de4f57f9d051547640edd09397
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758102"
---
# <a name="how-event-handlers-work-together"></a>Como os manipuladores de eventos funcionam em conjunto
A menos que você esteja programando em Visual Basic, todos os manipuladores de eventos para eventos de **conexão** e **conjunto de registros** devem ser implementados, independentemente de você realmente processar todos os eventos. A quantidade de trabalho de implementação que você precisa fazer depende da linguagem de programação. Para obter mais informações, consulte [instanciação de evento ADO por idioma](../../../ado/guide/data/ado-event-instantiation-by-language.md).  
  
## <a name="paired-event-handlers"></a>Manipuladores de eventos emparelhados  
 Cada manipulador de eventos terá um manipulador de eventos **completo** associado. Por exemplo, quando seu aplicativo altera o valor de um campo, o manipulador de eventos **WillChangeField** é chamado. Se a alteração for aceitável, o aplicativo deixará o parâmetro **adStatus** inalterado e a operação será executada. Quando a operação for concluída, um evento **FieldChangeComplete** notificará seu aplicativo de que a operação foi concluída. Se for concluído com êxito, **adStatus** conterá **adStatusOK**; caso contrário, **adStatus** conterá **adStatusErrorsOccurred** e você deverá verificar o objeto de **erro** para determinar a causa do erro.  
  
 Quando **WillChangeField** é chamado, você pode determinar que a alteração não deve ser feita. Nesse caso, defina **adStatus** como **adStatusCancel.** A operação é cancelada e o evento **FieldChangeComplete** recebe um valor de **adStatus** de **adStatusErrorsOccurred**. O objeto de **erro** contém **adErrOperationCancelled** para que o manipulador de **FieldChangeComplete** saiba que a operação foi cancelada. No entanto, você precisa verificar o valor do parâmetro **adStatus** antes de alterá-lo, pois a definição de **adStatus** como **adStatusCancel** não tem efeito se o parâmetro foi definido como **adStatusCantDeny** na entrada para o procedimento.  
  
 Às vezes, uma operação pode gerar mais de um evento. Por exemplo, o objeto **Recordset** tem eventos emparelhados para alterações de **campo** e alterações de **registro** . Quando seu aplicativo altera o valor de um **campo**, o manipulador de eventos **WillChangeField** é chamado. Se ele determinar que a operação pode continuar, o manipulador de eventos **WillChangeRecord** também será gerado. Se esse manipulador também permitir que o evento Continue, a alteração será feita e os manipuladores de eventos **FieldChangeComplete** e **RecordChangeComplete** serão chamados. A ordem na qual os manipuladores de eventos serão chamados para uma determinada operação é chamada não é definida, portanto, você deve evitar escrever código que dependa da chamada de manipuladores em uma determinada sequência.  
  
 Em instâncias quando vários eventos serão gerados, um dos eventos poderá cancelar a operação pendente. Por exemplo, quando o aplicativo altera o valor de um **campo**, os manipuladores de eventos **WillChangeField** e **WillChangeRecord** normalmente seriam chamados. No entanto, se a operação for cancelada no primeiro manipulador de eventos, seu manipulador **completo** associado será chamado imediatamente com **adStatusOperationCancelled**. O segundo manipulador nunca é chamado. No entanto, se o primeiro manipulador de eventos permitir que o evento prossiga, o outro manipulador de eventos será chamado. Se, em seguida, cancelar a operação, os eventos **completos** serão chamados como nos exemplos anteriores.  
  
## <a name="unpaired-event-handlers"></a>Manipuladores de eventos não emparelhados  
 Desde que o status passado para o evento não seja **adStatusCantDeny**, você pode desativar as notificações de eventos para qualquer evento retornando **AdStatusUnwantedEvent** no parâmetro *status* . Por exemplo, quando o manipulador de eventos **completo** é chamado pela primeira vez, você pode retornar **adStatusUnwantedEvent**. Posteriormente, você receberá **apenas eventos** . No entanto, alguns eventos podem ser disparados por mais de um motivo. Nesse caso, o evento terá um parâmetro *Reason* . Ao retornar **adStatusUnwantedEvent**, você deixará de receber notificações para esse evento somente quando eles ocorrerem por esse motivo específico. Em outras palavras, você potencialmente receberá uma notificação para cada possível motivo pelo qual o evento poderia ser disparado.  
  
 Manipuladores **de eventos únicos** podem ser úteis quando você deseja examinar os parâmetros que serão usados em uma operação. Você pode modificar esses parâmetros de operação ou cancelar a operação.  
  
 Como alternativa, deixe a notificação de evento **completa** habilitada. Quando seu primeiro manipulador de eventos for chamado, retorne **adStatusUnwantedEvent**. Posteriormente, você receberá apenas eventos **completos** .  
  
 Manipuladores de eventos de **execução** única podem ser úteis para gerenciar operações assíncronas. Cada operação assíncrona tem um evento de **conclusão** apropriado.  
  
 Por exemplo, pode levar muito tempo para popular um grande objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) . Se seu aplicativo for gravado corretamente, você poderá iniciar uma `Recordset.Open(...,adAsyncExecute)` operação e continuar com outro processamento. Eventualmente, você será notificado quando o **conjunto de registros** for preenchido por um evento **ExecuteComplete** .  
  
## <a name="single-event-handlers-and-multiple-objects"></a>Manipuladores de eventos únicos e vários objetos  
 A flexibilidade de uma linguagem de programação como Microsoft Visual C++® permite que um manipulador de eventos processe eventos de vários objetos. Por exemplo, você poderia ter um manipulador de eventos de **desconexão** que processa eventos de vários objetos de **conexão** . Se uma das conexões terminar, o manipulador de eventos de **desconexão** será chamado. Você pode informar qual conexão causou o evento porque o parâmetro do objeto manipulador de eventos seria definido como o objeto de **conexão** correspondente.  
  
> [!NOTE]
>  Essa técnica não pode ser usada em Visual Basic porque essa linguagem pode correlacionar apenas um objeto a um manipulador de eventos.  
  
## <a name="see-also"></a>Consulte Também  
 [Resumo do manipulador de eventos do ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Instanciação de evento ADO por idioma](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [Parâmetros do evento](../../../ado/guide/data/event-parameters.md)   
 [Tipos de eventos](../../../ado/guide/data/types-of-events.md)
