---
description: Eventos WillChangeField e FieldChangeComplete (ADO)
title: Eventos WillChangeField e FieldChangeComplete (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldChangeComplete
- Recordset::WillChangeField
- Recordset::FieldChangeComplete
- WillChangeField
helpviewer_keywords:
- WillChangeField event [ADO]
- fieldchangecomplete event [ADO]
ms.assetid: 3e49fb89-c45b-4d39-823e-3cc887c59b37
author: rothja
ms.author: jroth
ms.openlocfilehash: 84c861c2a344276a80ea8e8fd98f84aeb2bb7cbc
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776895"
---
# <a name="willchangefield-and-fieldchangecomplete-events-ado"></a>Eventos WillChangeField e FieldChangeComplete (ADO)
O evento **WillChangeField** é chamado antes de uma operação pendente Alterar o valor de um ou mais objetos de [campo](./field-object.md) no [conjunto de registros](./recordset-object-ado.md). O evento **FieldChangeComplete** é chamado depois que o valor de um ou mais objetos de **campo** é alterado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
WillChangeField cFields, Fields, adStatus, pRecordset  
FieldChangeComplete cFields, Fields, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *cFields*  
 Um **longo** que indica o número de objetos **Field** em *campos*.  
  
 *Fields*  
 Para **WillChangeField**, o parâmetro *Fields* é uma matriz de **variantes** que contém objetos de **campo** com os valores originais. Para **FieldChangeComplete**, o parâmetro *Fields* é uma matriz de **variantes** que contém objetos de **campo** com os valores alterados.  
  
 *pError*  
 Um objeto de [erro](./error-object.md) . Ele descreve o erro que ocorreu se o valor de *adStatus* for **adStatusErrorsOccurred**; caso contrário, ele não será definido.  
  
 *adStatus*  
 Um valor de status de [EventStatusEnum](./eventstatusenum.md) .  
  
 Quando **WillChangeField** for chamado, esse parâmetro será definido como **adStatusOK** se a operação que causou o evento tiver sido bem-sucedida. Ele será definido como **adStatusCantDeny** se esse evento não puder solicitar o cancelamento da operação pendente.  
  
 Quando **FieldChangeComplete** for chamado, esse parâmetro será definido como **adStatusOK** se a operação que causou o evento foi bem-sucedida ou para **adStatusErrorsOccurred** se a operação falhar.  
  
 Antes de **WillChangeField** retornar, defina esse parâmetro como **adStatusCancel** para o cancelamento de solicitação da operação pendente.  
  
 Antes de **FieldChangeComplete** retornar, defina esse parâmetro como **adStatusUnwantedEvent** para evitar notificações subsequentes.  
  
 *pRecordset*  
 Um objeto **Recordset** . O **conjunto de registros** para o qual esse evento ocorreu.  
  
## <a name="remarks"></a>Comentários  
 Um evento **WillChangeField** ou **FieldChangeComplete** pode ocorrer ao definir a propriedade [Value](./value-property-ado.md) e chamar o método [Update](./update-method.md) com parâmetros de matriz de campo e valor.  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do modelo de eventos ADO (VC + +)](./ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos ADO](../../guide/data/ado-event-handler-summary.md)