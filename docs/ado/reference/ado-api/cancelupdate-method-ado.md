---
title: "Método CancelUpdate (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::CancelUpdate
helpviewer_keywords:
- CancelUpdate method [ADO]
ms.assetid: eaa856cc-c786-462e-890c-c896261b1741
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9a85b135d743b356f5e4f5bd28e6bb2f2bb1eec0
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="cancelupdate-method-ado"></a>Método CancelUpdate (ADO)
Cancela as alterações feitas na linha atual ou nova de um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto, ou o [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleção de um [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto antes de chamar o [atualização ](../../../ado/reference/ado-api/update-method.md) método.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.CancelUpdaterecord.Fields.CancelUpdate  
```  
  
## <a name="remarks"></a>Comentários  
  
## <a name="recordset"></a>Conjunto de registros  
 Use o **CancelUpdate** método para cancelar as alterações feitas na linha atual ou para descartar uma linha adicionada recentemente. Você não pode cancelar as alterações para a linha atual ou uma nova linha depois de chamar o **atualização** método, a menos que as alterações são parte de uma transação que é possível revertê-lo com o [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) método ou parte de uma atualização em lotes. No caso de uma atualização em lotes, você pode cancelar o **atualizar** com o **CancelUpdate** ou [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) método.  
  
 Se você estiver adicionando uma nova linha ao chamar o **CancelUpdate** método, a linha atual se tornará a linha atual antes do [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) chamar.  
  
 Se você estiver no modo de edição e desejar mover fora do registro atual (por exemplo, usando o [mover](../../../ado/reference/ado-api/move-method-ado.md), [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md), ou [fechar](../../../ado/reference/ado-api/close-method-ado.md) métodos), você pode usar ** CancelUpdate** para cancelar todas as alterações pendentes. Talvez seja necessário fazer isso se a atualização não pode ser lançada com êxito para a fonte de dados. Por exemplo, uma tentativa excluir falhar devido a violações de integridade referencial deixará o **registros** no modo de edição após uma chamada para [excluir](../../../ado/reference/ado-api/delete-method-ado-recordset.md).  
  
## <a name="record"></a>Record  
 O **CancelUpdate** método cancela pendentes inserções ou exclusões de [campo](../../../ado/reference/ado-api/field-object.md) objetos e cancela as atualizações de campos existentes pendentes e restaurá-las aos seus valores originais. O [Status](../../../ado/reference/ado-api/status-property-ado-recordset.md) propriedade de todos os campos de **campos** coleção é definida como **adFieldOK**.  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Coleção Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo dos métodos CancelUpdate (VB) e atualização](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vb.md)   
 [Exemplo dos métodos CancelUpdate (VC + +) e atualização](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vc.md)   
 [Método AddNew (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Método Cancel (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Método Cancel (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [Método CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Método CancelUpdate (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Propriedade EditMode](../../../ado/reference/ado-api/editmode-property.md)   
 [Método Update](../../../ado/reference/ado-api/update-method.md)

