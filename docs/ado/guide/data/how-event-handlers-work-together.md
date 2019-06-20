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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: cb02a96e6ee3d28c67e21996677c02b58fc97c07
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66718384"
---
# <a name="how-event-handlers-work-together"></a>Como os manipuladores de eventos funcionam em conjunto
A menos que você está programando no Visual Basic, todos os manipuladores de eventos **Conexão** e **Recordset** eventos devem ser implementados, independentemente se você realmente processar todos os eventos. A quantidade de trabalho de implementação, que você precisa fazer depende de sua linguagem de programação. Para obter mais informações, consulte [instanciação de evento ADO por linguagem](../../../ado/guide/data/ado-event-instantiation-by-language.md).  
  
## <a name="paired-event-handlers"></a>Manipuladores de eventos emparelhado  
 Cada manipulador de eventos será deve possuir um **concluir** manipulador de eventos. Por exemplo, quando seu aplicativo altera o valor de um campo, o **eventos WillChangeField** manipulador de eventos é chamado. Se a alteração for aceitável, seu aplicativo deixa o **adStatus** parâmetro inalterado e a operação é executada. Quando a operação for concluída, uma **FieldChangeComplete** evento notifica seu aplicativo que a operação for concluída. Se ela foi concluída com êxito, **adStatus** contém **adStatusOK**; caso contrário, **adStatus** contém **adStatusErrorsOccurred** e Você deve verificar a **erro** objeto para determinar a causa do erro.  
  
 Quando **eventos WillChangeField** é chamado, você pode determinar que a alteração não deve ser feita. Nesse caso, defina **adStatus** para **adStatusCancel.** A operação será cancelada e o **FieldChangeComplete** evento recebe um **adStatus** valor de **adStatusErrorsOccurred**. O **erro** objeto contém **adErrOperationCancelled** para que seu **FieldChangeComplete** manipulador sabe que a operação foi cancelada. No entanto, você precisará verificar o valor da **adStatus** parâmetro antes de alterá-lo, porque a definição **adStatus** para **adStatusCancel** não tem nenhum efeito se o parâmetro foi definido para **adStatusCantDeny** na entrada para o procedimento.  
  
 Às vezes, uma operação pode gerar mais de um evento. Por exemplo, o **conjunto de registros** objeto tiver emparelhado eventos para **campo** alterações e **registro** alterações. Quando seu aplicativo altera o valor de uma **campo**, o **eventos WillChangeField** manipulador de eventos é chamado. Se ele determinar que a operação possa continuar, o **eventos WillChangeRecord** também é criado o manipulador de eventos. Se esse manipulador também permite que o evento continuar, a alteração for feita e o **FieldChangeComplete** e **RecordChangeComplete** são chamados de manipuladores de eventos. A ordem em que os manipuladores de eventos será de uma determinada operação são chamados não é definida, assim, você deve evitar escrever código que depende de manipuladores de chamada em uma sequência específica.  
  
 Em instâncias quando vários eventos serão são gerados, um dos eventos pode cancelar a operação pendente. Por exemplo, quando seu aplicativo altera o valor de uma **campo**, ambos **eventos WillChangeField** e **eventos WillChangeRecord** normalmente seriam chamados de manipuladores de eventos. No entanto, se a operação foi cancelada no primeiro manipulador de eventos, seus associado **Complete** manipulador é chamado imediatamente com **adStatusOperationCancelled**. O segundo manipulador nunca é chamado. Se, no entanto, o primeiro manipulador de eventos permite que o evento prossiga, o manipulador de eventos será chamado. Se, em seguida, cancela a operação, ambos **concluir** eventos serão chamados como nos exemplos anteriores.  
  
## <a name="unpaired-event-handlers"></a>Manipuladores de eventos não emparelhados  
 Desde que o status aprovado para o evento não é **adStatusCantDeny**, você pode desativar as notificações de eventos para qualquer evento retornando **adStatusUnwantedEvent** no *Status*parâmetro. Por exemplo, quando seu **Complete** manipulador de eventos é chamado na primeira vez, você pode retornar **adStatusUnwantedEvent**. Posteriormente, você receberá apenas **serão** eventos. No entanto, alguns eventos podem ser disparados por mais de um motivo. Nesse caso, o evento terá um *motivo* parâmetro. Quando você retornar **adStatusUnwantedEvent**, você irá parar de receber notificações para o evento apenas quando eles ocorrem por esse motivo específico. Em outras palavras, você receberá potencialmente notificação para cada motivo possível que o evento foi disparado.  
  
 Única **serão** manipuladores de eventos podem ser útil quando você deseja examinar os parâmetros que serão usados em uma operação. Você pode modificar os parâmetros da operação ou cancelar a operação.  
  
 Como alternativa, deixar **concluir** notificação de eventos habilitada. Quando o primeiro manipulador de eventos será é chamado, retornará **adStatusUnwantedEvent**. Posteriormente, você receberá apenas **concluir** eventos.  
  
 Única **concluir** manipuladores de eventos podem ser útil para gerenciamento de operações assíncronas. Cada operação assíncrona tem apropriado **concluir** eventos.  
  
 Por exemplo, pode levar muito tempo para popular um grande [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto. Se seu aplicativo é escrito adequadamente, você poderá iniciar um `Recordset.Open(...,adAsyncExecute)` operação e continuar com outro processamento. Eventualmente, você será notificado quando o **conjunto de registros** é populado por uma **ExecuteComplete** eventos.  
  
## <a name="single-event-handlers-and-multiple-objects"></a>Manipuladores de eventos único e vários objetos  
 A flexibilidade de uma linguagem de programação como Microsoft Visual C++® permite que você tenha um eventos de processo do manipulador de eventos de vários objetos. Por exemplo, você pode ter uma **Disconnect** eventos de processo do manipulador de eventos de várias **Conexão** objetos. Se uma das conexões terminou, o **desconectar** seria chamado manipulador de eventos. Você pode dizer ao qual conexão causou o evento porque o parâmetro de objeto do manipulador de eventos seria definido para os respectivos **Conexão** objeto.  
  
> [!NOTE]
>  Essa técnica não pode ser usada no Visual Basic, porque esse idioma pode correlacionar a apenas um objeto a um manipulador de eventos.  
  
## <a name="see-also"></a>Consulte também  
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Instanciação de evento ADO por linguagem](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [Parâmetros de evento](../../../ado/guide/data/event-parameters.md)   
 [Tipos de eventos](../../../ado/guide/data/types-of-events.md)
