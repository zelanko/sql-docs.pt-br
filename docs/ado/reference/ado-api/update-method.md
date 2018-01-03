---
title: "Método Update | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Recordset15::Update
helpviewer_keywords: Update method [ADO]
ms.assetid: 6b2a9c31-1a7e-40db-8a53-30720d0f6cc1
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f7d416b0d132af4d2f1d2145de577ca930eaeef9
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="update-method"></a>Método Update
Salva as alterações feitas à linha atual de um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto, ou o [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleção de um [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.Update Fields, Values  
record.Fields.Update  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Fields*  
 Opcional. Um **Variant** que representa um único nome, ou um **Variant** matriz que representa os nomes ou posições ordinais de campos que você deseja modificar.  
  
 *Valores*  
 Opcional. Um **Variant** que representa um único valor, ou um **Variant** matriz que representa valores de campos no novo registro.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="recordset"></a>Conjunto de registros  
 Use o **atualização** método para salvar as alterações feitas para o registro atual de um **registros** objeto desde a chamada a [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) método ou desde alterar quaisquer valores de campo em um registro existente. O **registros** objeto deve dar suporte a atualizações.  
  
 Para definir valores de campo, siga um destes procedimentos:  
  
-   Atribuir valores a um [campo](../../../ado/reference/ado-api/field-object.md) do objeto [valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade e chame o **atualização** método.  
  
-   Passar um nome de campo e um valor como argumentos com o **atualização** chamar.  
  
-   Passe uma matriz de nomes de campo e uma matriz de valores com o **atualização** chamar.  
  
 Quando você usa conjuntos de campos e valores, deve haver um número igual de elementos em matrizes. Além disso, a ordem dos nomes de campo deve corresponder à ordem de valores de campo. Se o número e a ordem dos campos e valores não coincidirem, ocorrerá um erro.  
  
 Se o **registros** objeto oferece suporte a atualização em lotes, você pode armazenar em cache várias alterações para um ou mais registros localmente até que você chame o [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) método. Se você estiver editando o registro atual ou adicionar um novo registro, quando você chama o **UpdateBatch** método ADO automaticamente chamará o **atualização** método para salvar as alterações pendentes para o registro atual antes de transmitir as alterações em lotes para o provedor.  
  
 Se você mover de registro estiver adicionando ou editando antes de chamar o **atualização** , ADO será automaticamente da chamada do método **atualização** para salvar as alterações. Você deve chamar o [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) método se você deseja cancelar as alterações feitas no registro atual ou descartar um registro recém-adicionada.  
  
 O registro atual permanece atual depois de chamar o **atualização** método.  
  
## <a name="record"></a>Record  
 O **atualização** método finaliza adições, exclusões e atualizações para campos de [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleção de um **registro** objeto.  
  
 Por exemplo, os campos excluídos com o **excluir** método são marcados para exclusão imediatamente, mas permanecem na coleção. O **atualização** método deve ser chamado para realmente excluir esses campos da coleção do provedor.  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Coleção Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos CancelUpdate (VB) e atualização](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vb.md)   
 [Exemplo dos métodos CancelUpdate (VC + +) e atualização](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vc.md)   
 [Método AddNew (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Método CancelUpdate (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Propriedade EditMode](../../../ado/reference/ado-api/editmode-property.md)   
 [Método UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)
