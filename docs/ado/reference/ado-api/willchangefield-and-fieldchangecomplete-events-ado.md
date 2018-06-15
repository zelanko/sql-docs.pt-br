---
title: WillChangeField e FieldChangeComplete eventos (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 108aea1a4f8106c3a84b411591d4866235726efc
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35282845"
---
# <a name="willchangefield-and-fieldchangecomplete-events-ado"></a>WillChangeField e FieldChangeComplete eventos (ADO)
O **WillChangeField** evento é chamado antes de uma operação pendente altera o valor de uma ou mais [campo](../../../ado/reference/ado-api/field-object.md) objetos no [registros](../../../ado/reference/ado-api/recordset-object-ado.md). O **FieldChangeComplete** evento é chamado após o valor de um ou mais **campo** objetos foi alterado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
WillChangeField cFields, Fields, adStatus, pRecordset  
FieldChangeComplete cFields, Fields, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *cFields*  
 Um **longo** que indica o número de **campo** objetos no *campos*.  
  
 *Fields*  
 Para **WillChangeField**, o *campos* parâmetro é uma matriz de **variantes** que contém **campo** objetos com os valores originais. Para **FieldChangeComplete**, o *campos* parâmetro é uma matriz de **variantes** que contém **campo** objetos com valores alterados .  
  
 *pError*  
 Um [erro](../../../ado/reference/ado-api/error-object.md) objeto. Descreve o erro ocorrido se o valor de *adStatus* é **adStatusErrorsOccurred**; caso contrário, ele não está definido.  
  
 *adStatus*  
 Um [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de status.  
  
 Quando **WillChangeField** é chamado, esse parâmetro é definido como **adStatusOK** se a operação que causou o evento foi bem-sucedida. Ele é definido como **adStatusCantDeny** se esse evento não é possível solicitar o cancelamento da operação pendente.  
  
 Quando **FieldChangeComplete** é chamado, esse parâmetro é definido como **adStatusOK** se a operação que causou o evento foi bem-sucedida, ou para **adStatusErrorsOccurred** se a operação falhou.  
  
 Antes de **WillChangeField** retorna, defina este parâmetro como **adStatusCancel** a solicitação de cancelamento da operação pendente.  
  
 Antes de **FieldChangeComplete** retorna, defina este parâmetro como **adStatusUnwantedEvent** para impedir que as notificações subsequentes.  
  
 *pRecordset*  
 Um **registros** objeto. O **registros** para que esse evento ocorreu.  
  
## <a name="remarks"></a>Remarks  
 Um **WillChangeField** ou **FieldChangeComplete** evento pode ocorrer durante a configuração de [valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade e chamar o [atualização](../../../ado/reference/ado-api/update-method.md) método com os parâmetros de matriz de campo e valor.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de modelo de eventos do ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumo do manipulador de eventos ADO](../../../ado/guide/data/ado-event-handler-summary.md)
