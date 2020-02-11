---
title: Propriedade EditMode | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::EditMode
helpviewer_keywords:
- EditMode property
ms.assetid: a1b04bb2-8c8b-47f9-8477-bfd0368b6f68
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c0ffc6fb258799b0ab0bb03e7acbd922f6a67d1f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67918978"
---
# <a name="editmode-property"></a>Propriedade EditMode
Indica o status de edição do registro atual.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um valor [EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md) .  
  
## <a name="remarks"></a>Comentários  
 O ADO mantém um buffer de edição associado ao registro atual. Esta propriedade indica se foram feitas alterações nesse buffer ou se um novo registro foi criado. Use a propriedade **EditMode** para determinar o status de edição do registro atual. Você pode testar as alterações pendentes se um processo de edição tiver sido interrompido e determinar se você precisa usar o método [Update](../../../ado/reference/ado-api/update-method.md) ou [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) .  
  
 No *modo de atualização imediata* , a propriedade **EditMode** é redefinida como **adEditNone** depois que uma chamada bem-sucedida para o método **Update** é chamada. Quando uma chamada para [delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md) não exclui com êxito o registro ou os registros na fonte de dados (por exemplo, devido a violações de integridade referencial), [o conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) permanece no modo de edição (**EditMode** = **adEditInProgress**). Portanto, **CancelUpdate** deve ser chamado antes de mover o registro atual (por exemplo, [move](../../../ado/reference/ado-api/move-method-ado.md), [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)ou [Close](../../../ado/reference/ado-api/close-method-ado.md) ).  
  
 No *modo de atualização em lotes* (no qual o provedor armazena em cache várias alterações e as grava na fonte de dados subjacente somente quando você chama o método [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) ), o valor da propriedade **EditMode** é alterado quando a primeira operação é executada e não é redefinido por uma chamada para o método **Update** . As operações subsequentes não alteram o valor da propriedade **EditMode** , mesmo que operações diferentes sejam executadas. Por exemplo, se a primeira operação for adicionar um novo registro e o segundo fizer alterações em um registro existente, a propriedade de **EditMode** ainda será **adEditAdd**. A propriedade **EditMode** não é redefinida como **adEditNone** até depois da chamada para **UpdateBatch**. Para determinar quais operações foram executadas, defina a propriedade [Filter](../../../ado/reference/ado-api/filter-property.md) como [adFilterPending](../../../ado/reference/ado-api/filtergroupenum.md) para que somente os registros com alterações pendentes sejam visíveis e examine a propriedade [status](../../../ado/reference/ado-api/status-property-ado-recordset.md) de cada registro para determinar quais alterações foram feitas nos dados.  
  
> [!NOTE]
>  **EditMode** só poderá retornar um valor válido se houver um registro atual. O **EditMode** retornará um erro se [BOF ou EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) for true ou se o registro atual tiver sido excluído.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades CursorType, LockType e EditMode (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [Exemplo das propriedades CursorType, LockType e EditMode (VC + +)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [Método AddNew (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Método Delete (conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Método CancelUpdate (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Método Update](../../../ado/reference/ado-api/update-method.md)
