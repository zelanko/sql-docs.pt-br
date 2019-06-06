---
title: Atualizar método | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Update
helpviewer_keywords:
- Update method [ADO]
ms.assetid: 6b2a9c31-1a7e-40db-8a53-30720d0f6cc1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e48185f0524a920d52092540f5e3ed6d8546edfe
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66710504"
---
# <a name="update-method"></a>Método Update
Salva as alterações feitas na linha atual de um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto, ou o [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleção de um [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.Update Fields, Values  
record.Fields.Update  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Fields*  
 Opcional. Um **Variant** que representa um único nome, ou um **Variant** matriz que representa os nomes ou as posições ordinais do campo ou campos que você deseja modificar.  
  
 *Valores*  
 Opcional. Um **Variant** que representa um único valor, ou um **Variant** matriz que representa os valores para o campo ou campos no novo registro.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="recordset"></a>Conjunto de registros  
 Use o **atualização** método para salvar as alterações feitas no registro atual de uma **conjunto de registros** objeto desde a chamada a [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) método ou desde que alterar quaisquer valores de campo em um registro existente. O **Recordset** objeto deve dar suporte a atualizações.  
  
 Para definir valores de campo, siga um destes procedimentos:  
  
-   Atribuir valores a um [campo](../../../ado/reference/ado-api/field-object.md) do objeto [valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade e chame o **atualização** método.  
  
-   Passar um nome de campo e um valor como argumentos com o **atualização** chamar.  
  
-   Passe uma matriz de nomes de campo e uma matriz de valores com o **atualização** chamar.  
  
 Quando você usa matrizes de campos e valores, deve haver um número igual de elementos em ambas as matrizes. Além disso, a ordem dos nomes de campo deve corresponder a ordem dos valores de campo. Se o número e a ordem dos campos e valores não coincidirem, ocorrerá um erro.  
  
 Se o **conjunto de registros** objeto dá suporte à atualização em lotes, você pode armazenar em cache várias alterações para um ou mais registros localmente até que você chame a [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) método. Se você estiver editando o registro atual ou adicionar um novo registro, quando você chama o **UpdateBatch** método, ADO chamará automaticamente a **atualização** método para salvar todas as alterações pendentes no registro atual antes de transmitir as alterações em lote para o provedor.  
  
 Se você mover do registro estiver adicionando ou editando antes de chamar o **atualização** método, ADO chamará automaticamente **atualização** para salvar as alterações. Você deve chamar o [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) método se você quiser cancelar todas as alterações feitas no registro atual ou descartar um registro recém-adicionado.  
  
 O registro atual permanece atual depois de chamar o **atualização** método.  
  
## <a name="record"></a>Record  
 O **atualização** método finaliza adições, exclusões e atualizações de campos na [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleção de um **registro** objeto.  
  
 Por exemplo, os campos excluídos com o **excluir** método são marcados para exclusão imediatamente, mas permanecem na coleção. O **atualização** método deve ser chamado para excluir, na verdade, esses campos da coleção do provedor.  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Coleção Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Atualização e exemplo dos métodos CancelUpdate (VB)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vb.md)   
 [Exemplo dos métodos CancelUpdate (VC + +) e atualização](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vc.md)   
 [Método AddNew (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Método CancelUpdate (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Propriedade EditMode](../../../ado/reference/ado-api/editmode-property.md)   
 [Método UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)
