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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2e44bc264b5fd3e21e35042243ee81f7834c60b2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63161636"
---
# <a name="event-parameters"></a>Parâmetros de evento
Cada manipulador de eventos tem um parâmetro de status que controla o manipulador de eventos. Para eventos de conclusão, esse parâmetro também é usado para indicar o êxito ou falha da operação que gerou o evento. Eventos mais completos também tem um parâmetro de erro para fornecer informações sobre qualquer erro que possam ter ocorrido e um ou mais parâmetros de objeto que se referem os objetos do ADO usados para executar a operação. Por exemplo, o [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md) evento inclui parâmetros de objeto para o **comando**, **conjunto de registros**, e **Conexão** objetos associado ao evento. No exemplo a seguir do Microsoft® Visual Basic®, você pode ver o pCommand, pRecordset e pConnection objetos que representam o **comando**, **conjunto de registros**, e **Conexão** objetos que são usados pelo **Execute** método.  
  
```  
Private Sub connEvent_ExecuteComplete(ByVal RecordsAffected As Long, _  
     ByVal pError As ADODB.Error, _  
     adStatus As ADODB.EventStatusEnum, _  
     ByVal pCommand As ADODB.Command, _  
     ByVal pRecordset As ADODB.Recordset, _  
     ByVal pConnection As ADODB.Connection)  
```  
  
 Exceto para o **erro** do objeto, os mesmos parâmetros são passados para os eventos serão. Isso permite a você examinar cada um dos objetos que serão usados na operação pendente e determinam se a operação deve ter permissão para concluir.  
  
 Alguns manipuladores de eventos têm uma *motivo* parâmetro, que fornece informações adicionais sobre por que o evento ocorreu. Por exemplo, o **eventos WillMove** e **MoveComplete** eventos podem ocorrer devido a qualquer um dos métodos de navegação (**MoveNext**, **MovePrevious**e assim por diante) sendo chamado ou como resultado de uma repetição de consulta.  
  
## <a name="status-parameter"></a>Parâmetro de status  
 Quando a rotina do manipulador de eventos é chamada, o *Status* parâmetro é definido como um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**adStatusOK**|Passado para será e eventos de conclusão. Esse valor significa que a operação que causou o evento foi concluído com êxito.|  
|**adStatusErrorsOccurred**|Passado para apenas os eventos de conclusão. Esse valor significa que a operação que causou o evento não foi bem-sucedida, ou um evento será cancelou a operação. Verifique as *erro* parâmetro para obter mais detalhes.|  
|**adStatusCantDeny**|Passado para apenas os eventos serão. Esse valor significa que a operação não pode ser cancelada pelo evento será. Ele deve ser executado.|  
  
 Se você determinar que o evento será que a operação deve continuar, deixe o *Status* parâmetro inalterado. Desde que o parâmetro de status de entrada não foi definido como **adStatusCantDeny**, no entanto, você pode cancelar a operação pendente alterando *Status* para **adStatusCancel**. Quando você fizer isso, o evento de conclusão associado à operação tem seu *Status* parâmetro definido como **adStatusErrorsOccurred**. O **erro** objeto passado para o evento de conclusão conterá o valor **adErrOperationCancelled**.  
  
 Se você não deseja mais processar um evento, você pode definir *Status* à **adStatusUnwantedEvent** e seu aplicativo não receberá a notificação de que o evento. No entanto, lembre-se de que alguns eventos podem ser gerados por mais de um motivo. Nesse caso, você deve especificar **adStatusUnwantedEvent** para cada motivo possíveis. Por exemplo, para interromper o recebimento da notificação pendente **RecordChange** eventos, você deve definir o *Status* parâmetro **adStatusUnwantedEvent** para  **adRsnAddNew**, **adRsnDelete**, **adRsnUpdate**, **adRsnUndoUpdate**, **adRsnUndoAddNew**, **adRsnUndoDelete**, e **adRsnFirstChange** conforme elas ocorrem.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**adStatusUnwantedEvent**|Solicite que esse manipulador de eventos não receber nenhuma notificação adicional.|  
|**adStatusCancel**|Solicite o cancelamento da operação que está prestes a ocorrer.|  
  
## <a name="error-parameter"></a>Erro de parâmetro  
 O *erro* parâmetro é uma referência a um ADO [erro](../../../ado/reference/ado-api/error-object.md) objeto. Quando o *Status* parâmetro for definido como **adStatusErrorsOccurred**, o **erro** objeto contém detalhes sobre por que a operação falhou. Se o evento será associado a um evento de conclusão cancelou a operação, definindo a *Status* parâmetro **adStatusCancel**, o objeto de erro é sempre definido como  **adErrOperationCancelled**.  
  
## <a name="object-parameter"></a>Parâmetro de objeto  
 Cada evento recebe um ou mais objetos que representam os objetos que estão envolvidos na operação. Por exemplo, o **ExecuteComplete** evento recebe um **comando** objeto, uma **conjunto de registros** objeto e um **Conexão** objeto.  
  
## <a name="reason-parameter"></a>Parâmetro de motivo  
 O *motivo* parâmetro, *adReason*, fornece informações adicionais sobre por que o evento ocorreu. Eventos com um *adReason* parâmetro pode ser chamado várias vezes, até mesmo para a mesma operação, por um motivo diferente cada vez. Por exemplo, o **eventos WillChangeRecord** manipulador de eventos é chamado para operações que estão prestes a fazer ou desfazer a inserção, exclusão ou modificação de um registro. Se você quiser processar um evento somente quando ele ocorre por um motivo específico, você pode usar o *adReason* parâmetro para filtrar as ocorrências que você não está interessado. Por exemplo, se você quisesse processar eventos de alteração de registro somente quando eles ocorrerem porque um registro foi adicionado, você pode usar algo semelhante ao seguinte.  
  
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
  
 Nesse caso, a notificação potencialmente pode ocorrer para cada um dos outros motivos. No entanto, ele ocorrerá apenas uma vez para cada motivo. Depois que a notificação ocorreu uma vez para cada motivo, você receberá uma notificação apenas para a adição de um novo registro.  
  
 Por outro lado, você precisará definir *adStatus* à **adStatusUnwantedEvent** apenas uma vez para solicitar que um manipulador de eventos sem uma **adReason** evento de recebimento de parada de parâmetro notificações.  
  
## <a name="see-also"></a>Consulte também  
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Instanciação de evento ADO por linguagem](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [Como os manipuladores de eventos funcionam juntos](../../../ado/guide/data/how-event-handlers-work-together.md)   
 [Tipos de eventos](../../../ado/guide/data/types-of-events.md)
