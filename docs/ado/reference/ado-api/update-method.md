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
ms.openlocfilehash: 6ce247905afd6ed34366424f5f905d57b42d988f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67938848"
---
# <a name="update-method"></a>Método Update
Salva as alterações feitas na linha atual de um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) ou a coleção [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) de um objeto [Record](../../../ado/reference/ado-api/record-object-ado.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.Update Fields, Values  
record.Fields.Update  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Fields*  
 Opcional. Uma **variante** que representa um único nome ou uma matriz **variante** que representa nomes ou posições ordinais do campo ou campos que você deseja modificar.  
  
 *Valores*  
 Opcional. Uma **variante** que representa um único valor ou uma matriz **variante** que representa valores para o campo ou campos no novo registro.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="recordset"></a>Conjunto de registros  
 Use o método **Update** para salvar as alterações feitas no registro atual de um objeto **Recordset** desde a chamada do método [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) ou desde a alteração de qualquer valor de campo em um registro existente. O objeto **Recordset** deve dar suporte a atualizações.  
  
 Para definir valores de campo, siga um destes procedimentos:  
  
-   Atribua valores à propriedade [Value](../../../ado/reference/ado-api/value-property-ado.md) do objeto [Field](../../../ado/reference/ado-api/field-object.md) e chame o método **Update** .  
  
-   Passe um nome de campo e um valor como argumentos com a chamada de **atualização** .  
  
-   Passe uma matriz de nomes de campo e uma matriz de valores com a chamada de **atualização** .  
  
 Quando você usa matrizes de campos e valores, deve haver um número igual de elementos em ambas as matrizes. Além disso, a ordem dos nomes de campo deve corresponder à ordem dos valores de campo. Se o número e a ordem dos campos e valores não corresponderem, ocorrerá um erro.  
  
 Se o objeto **Recordset** oferecer suporte à atualização em lotes, você poderá armazenar em cache várias alterações em um ou mais registros localmente até chamar o método [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) . Se você estiver editando o registro atual ou adicionando um novo registro ao chamar o método **UpdateBatch** , o ADO chamará automaticamente o método **Update** para salvar as alterações pendentes no registro atual antes de transmitir as alterações em lote para o provedor.  
  
 Se você mover do registro que está adicionando ou editando antes de chamar o método **Update** , o ADO automaticamente chamará **Update** para salvar as alterações. Você deve chamar o método [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) se quiser cancelar as alterações feitas no registro atual ou descartar um registro recém-adicionado.  
  
 O registro atual permanece atual depois que você chama o método **Update** .  
  
## <a name="record"></a>Record  
 O método **Update** finaliza adições, exclusões e atualizações em campos na coleção [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) de um objeto **Record** .  
  
 Por exemplo, os campos excluídos com o método **delete** são marcados para exclusão imediatamente, mas permanecem na coleção. O método **Update** deve ser chamado para realmente excluir esses campos da coleção do provedor.  
  
## <a name="applies-to"></a>Aplica-se A  
  
|||  
|-|-|  
|[Coleção Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos Update e CancelUpdate (VB)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vb.md)   
 [Exemplo dos métodos Update e CancelUpdate (VC + +)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vc.md)   
 [Método AddNew (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Método CancelUpdate (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Propriedade EditMode](../../../ado/reference/ado-api/editmode-property.md)   
 [Método UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)
