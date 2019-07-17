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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918978"
---
# <a name="editmode-property"></a>Propriedade EditMode
Indica o status de edição do registro atual.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um [EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md) valor.  
  
## <a name="remarks"></a>Comentários  
 ADO mantém um buffer de edição associado ao registro atual. Essa propriedade indica se foram feitas alterações a esse buffer, ou se um novo registro tiver sido criado. Use o **EditMode** propriedade para determinar o status de edição do registro atual. Você pode testar as alterações pendentes se um processo de edição foi interrompido e determinar se é necessário usar o [atualização](../../../ado/reference/ado-api/update-method.md) ou [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) método.  
  
 No *modo de atualização imediata* as **EditMode** propriedade é redefinida como **adEditNone** após uma chamada bem-sucedida para o **atualizar** método é chamado . Quando uma chamada para [exclua](../../../ado/reference/ado-api/delete-method-ado-recordset.md) com êxito exclui o registro ou registros na fonte de dados (por exemplo, devido a violações de integridade referencial), o [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) permanece no modo de edição (**EditMode** = **adEditInProgress**). Portanto, **CancelUpdate** deve ser chamado antes de passar fora do registro atual (por exemplo, com [mover](../../../ado/reference/ado-api/move-method-ado.md), [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md), ou [fechar](../../../ado/reference/ado-api/close-method-ado.md) ).  
  
 Na *modo de atualização em lotes* (em que o provedor armazena em cache várias alterações e os grava em fonte de dados subjacente somente quando você chama o [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) método), o valor da **EditMode**  propriedade é alterada quando a primeira operação é executada e ela não é redefinida por uma chamada para o **atualização** método. As operações subsequentes não alteram o valor da **EditMode** propriedade, mesmo se diferentes operações são executadas. Por exemplo, se a primeira operação é adicionar um novo registro, e o segundo faz alterações a um existente gravar, a propriedade de **EditMode** ainda estará **adEditAdd**. O **EditMode** propriedade não é redefinida para **adEditNone** até após a chamada para **UpdateBatch**. Para determinar quais operações foram executadas, defina as [filtro](../../../ado/reference/ado-api/filter-property.md) propriedade [adFilterPending](../../../ado/reference/ado-api/filtergroupenum.md) para que somente os registros com alterações pendentes serão visíveis e examinar o [Status](../../../ado/reference/ado-api/status-property-ado-recordset.md) propriedade de cada registro para determinar quais alterações foram feitas aos dados.  
  
> [!NOTE]
>  **EditMode** pode retornar um valor válido somente se houver um registro atual. **EditMode** retornará um erro se [BOF ou EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) for true, ou se o registro atual tiver sido excluído.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [CursorType, LockType, EditMode exemplo das propriedades e (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType, LockType, EditMode exemplo das propriedades e (VC + +)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [Método AddNew (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Excluir método (conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Método CancelUpdate (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Método Update](../../../ado/reference/ado-api/update-method.md)
