---
title: Parâmetros de evento | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Error parameter [ADO]
- Object parameter [ADO]
- Status parameter [ADO]
- events [ADO], parameters
- Reason parameter [ADO]
- event parameters [ADO]
ms.assetid: bd5c5afa-d301-4899-acda-40f98a6afa4d
author: rothja
ms.author: jroth
ms.openlocfilehash: 32e3cd177089fb99009490b82941928e091ab7c6
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763187"
---
# <a name="event-parameters"></a>Parâmetros de evento
Cada manipulador de eventos tem um parâmetro de status que controla o manipulador de eventos. Para eventos completos, esse parâmetro também é usado para indicar o êxito ou a falha da operação que gerou o evento. Os eventos mais completos também têm um parâmetro de erro para fornecer informações sobre qualquer erro que possa ter ocorrido e um ou mais parâmetros de objeto que se referem aos objetos ADO usados para executar a operação. Por exemplo, o evento [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md) inclui parâmetros de objeto para o **comando**, **conjunto de registros**e objetos de **conexão** associados ao evento. No exemplo a seguir do Microsoft® Visual Basic®, você pode ver os objetos pCommand, precaboset e pConnection que representam o **comando**, o **conjunto de registros**e os objetos de **conexão** usados pelo método **Execute** .  
  
```  
Private Sub connEvent_ExecuteComplete(ByVal RecordsAffected As Long, _  
     ByVal pError As ADODB.Error, _  
     adStatus As ADODB.EventStatusEnum, _  
     ByVal pCommand As ADODB.Command, _  
     ByVal pRecordset As ADODB.Recordset, _  
     ByVal pConnection As ADODB.Connection)  
```  
  
 Exceto para o objeto **Error** , os mesmos parâmetros serão passados para os eventos. Isso permite que você examine cada um dos objetos que serão usados na operação pendente e determine se a operação deve ter permissão para ser concluída.  
  
 Alguns manipuladores de eventos têm um parâmetro *Reason* , que fornece informações adicionais sobre por que o evento ocorreu. Por exemplo, os eventos **WillMove** e **MoveComplete** podem ocorrer devido a qualquer um dos métodos de navegação (**MoveNext**, **MovePrevious**e assim por diante) sendo chamados ou como resultado de uma repetição.  
  
## <a name="status-parameter"></a>Parâmetro de status  
 Quando a rotina do manipulador de eventos é chamada, o parâmetro *status* é definido como um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**adStatusOK**|Passado para os eventos concluídos e completos. Esse valor significa que a operação que causou o evento foi concluída com êxito.|  
|**adStatusErrorsOccurred**|Passado somente para eventos de conclusão. Esse valor significa que a operação que causou o evento não foi bem-sucedida ou um evento será cancelado na operação. Verifique o parâmetro de *erro* para obter mais detalhes.|  
|**adStatusCantDeny**|Passados apenas para eventos serão. Esse valor significa que a operação não pode ser cancelada pelo evento. Ele deve ser executado.|  
  
 Se você determinar em seu evento será que a operação deve continuar, deixe o parâmetro de *status* inalterado. Desde que o parâmetro status de entrada não tenha sido definido como **adStatusCantDeny**, no entanto, você pode cancelar a operação pendente alterando o *status* para **adStatusCancel**. Quando você faz isso, o evento complete associado à operação tem seu parâmetro de *status* definido como **adStatusErrorsOccurred**. O objeto de **erro** passado para o evento complete conterá o valor **adErrOperationCancelled**.  
  
 Se você não quiser mais processar um evento, poderá definir o *status* como **adStatusUnwantedEvent** e seu aplicativo não receberá mais a notificação desse evento. No entanto, lembre-se de que alguns eventos podem ser gerados por mais de um motivo. Nesse caso, você deve especificar **adStatusUnwantedEvent** para cada motivo possível. Por exemplo, para interromper o recebimento de notificação de eventos **RecordChange** pendentes, você deve definir o parâmetro de *status* como **adStatusUnwantedEvent** para **adRsnAddNew**, **adRsnDelete**, **adRsnUpdate**, **adRsnUndoUpdate**, **adRsnUndoAddNew**, **adRsnUndoDelete**e **adRsnFirstChange** conforme eles ocorrem.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**adStatusUnwantedEvent**|Solicite que este manipulador de eventos não receba notificações adicionais.|  
|**adStatusCancel**|Solicitação de cancelamento da operação que está prestes a ocorrer.|  
  
## <a name="error-parameter"></a>Parâmetro de erro  
 O parâmetro de *erro* é uma referência a um objeto de [erro](../../../ado/reference/ado-api/error-object.md) ADO. Quando o parâmetro *status* é definido como **adStatusErrorsOccurred**, o objeto **Error** contém detalhes sobre o motivo da falha da operação. Se o evento a ser associado a um evento completo tiver cancelado a operação definindo o parâmetro *status* como **adStatusCancel**, o objeto de erro será sempre definido como **adErrOperationCancelled**.  
  
## <a name="object-parameter"></a>Parâmetro de objeto  
 Cada evento recebe um ou mais objetos que representam os objetos envolvidos na operação. Por exemplo, o evento **ExecuteComplete** recebe um objeto de **comando** , um objeto **Recordset** e um objeto **Connection** .  
  
## <a name="reason-parameter"></a>Parâmetro de motivo  
 O parâmetro *Reason* , *adReason*, fornece informações adicionais sobre o motivo da ocorrência do evento. Eventos com um parâmetro *adReason* podem ser chamados várias vezes, mesmo para a mesma operação, por um motivo diferente a cada vez. Por exemplo, o manipulador de eventos **WillChangeRecord** é chamado para operações que estão prestes a fazer ou desfazer a inserção, exclusão ou modificação de um registro. Se você quiser processar um evento somente quando ele ocorrer por um motivo específico, você poderá usar o parâmetro *adReason* para filtrar as ocorrências nas quais você não está interessado. Por exemplo, se você quisesse processar eventos de alteração de registro somente quando eles ocorrerem porque um registro foi adicionado, você poderá usar algo semelhante ao seguinte.  
  
```  
' BeginEventExampleVB01  
Private Sub rsTest_WillChangeRecord(ByVal adReason As ADODB.EventReasonEnum, ByVal cRecords As Long, adStatus As ADODB.EventStatusEnum, ByVal pRecordset As ADODB.Recordset)  
   If adReason = adRsnAddNew Then  
       ' Process event  
       '...  
   Else  
       ' Cancel event notification for all  
       ' other possible adReason values.  
       adStatus = adStatusUnwantedEvent  
   End If  
End Sub  
' EndEventExampleVB01  
```  
  
 Nesse caso, a notificação pode potencialmente ocorrer por cada uma das outras razões. No entanto, ele ocorrerá apenas uma vez por cada motivo. Depois que a notificação ocorrer uma vez por cada motivo, você receberá uma notificação apenas para a adição de um novo registro.  
  
 Por outro lado, você precisa definir *adStatus* como **adStatusUnwantedEvent** apenas uma vez para solicitar que um manipulador de eventos sem um parâmetro **adReason** pare de receber notificações de eventos.  
  
## <a name="see-also"></a>Consulte Também  
 [Resumo do manipulador de eventos do ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Instanciação de evento ADO por idioma](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [Como os manipuladores de eventos funcionam juntos](../../../ado/guide/data/how-event-handlers-work-together.md)   
 [Tipos de eventos](../../../ado/guide/data/types-of-events.md)
