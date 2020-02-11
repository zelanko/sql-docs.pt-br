---
title: Método CancelUpdate (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::CancelUpdate
helpviewer_keywords:
- CancelUpdate method [ADO]
ms.assetid: eaa856cc-c786-462e-890c-c896261b1741
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fa9e680e1626311f2cc10aa7c79fb583841fbc38
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67920110"
---
# <a name="cancelupdate-method-ado"></a>Método CancelUpdate (ADO)
Cancela as alterações feitas na linha atual ou nova de um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) ou na coleção [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) de um objeto [Record](../../../ado/reference/ado-api/record-object-ado.md) , antes de chamar o método [Update](../../../ado/reference/ado-api/update-method.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.CancelUpdaterecord.Fields.CancelUpdate  
```  
  
## <a name="remarks"></a>Comentários  
  
## <a name="recordset"></a>Conjunto de registros  
 Use o método **CancelUpdate** para cancelar as alterações feitas na linha atual ou para descartar uma linha recém-adicionada. Não é possível cancelar as alterações na linha atual ou em uma nova linha depois de chamar o método **Update** , a menos que as alterações façam parte de uma transação que você possa reverter com o método [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) ou parte de uma atualização do lote. No caso de uma atualização em lotes, você pode cancelar a **atualização** com o método **CancelUpdate** ou [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) .  
  
 Se você estiver adicionando uma nova linha ao chamar o método **CancelUpdate** , a linha atual se tornará a linha que era atual antes da chamada [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) .  
  
 Se você estiver no modo de edição e quiser sair do registro atual (por exemplo, usando os métodos [move](../../../ado/reference/ado-api/move-method-ado.md), [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)ou [Close](../../../ado/reference/ado-api/close-method-ado.md) ), poderá usar o **CancelUpdate** para cancelar as alterações pendentes. Talvez seja necessário fazer isso se a atualização não puder ser postada com êxito à fonte de dados. Por exemplo, uma tentativa de exclusão que falha devido a violações de integridade referencial deixará o **conjunto de registros** no modo de edição após uma chamada para [delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md).  
  
## <a name="record"></a>Registro  
 O método **CancelUpdate** cancela todas as inserções ou exclusões pendentes de objetos de [campo](../../../ado/reference/ado-api/field-object.md) e cancela atualizações pendentes de campos existentes e os restaura aos valores originais. A propriedade [status](../../../ado/reference/ado-api/status-property-ado-recordset.md) de todos os campos na coleção **Fields** é definida como **adFieldOK**.  
  
## <a name="applies-to"></a>Aplica-se A  
  
|||  
|-|-|  
|[Coleção Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos Update e CancelUpdate (VB)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vb.md)   
 [Exemplo dos métodos Update e CancelUpdate (VC + +)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vc.md)   
 [Método AddNew (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Método Cancel (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Método Cancel (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [Método CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Método CancelUpdate (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Propriedade EditMode](../../../ado/reference/ado-api/editmode-property.md)   
 [Método Update](../../../ado/reference/ado-api/update-method.md)
