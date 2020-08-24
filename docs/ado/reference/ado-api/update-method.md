---
description: Método Update
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 819e6ebaa3932f19a693cb3d50651f7c451200e6
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776995"
---
# <a name="update-method"></a>Método Update
Salva as alterações feitas na linha atual de um objeto [Recordset](./recordset-object-ado.md) ou a coleção [Fields](./fields-collection-ado.md) de um objeto [Record](./record-object-ado.md) .  
  
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
 Use o método **Update** para salvar as alterações feitas no registro atual de um objeto **Recordset** desde a chamada do método [AddNew](./addnew-method-ado.md) ou desde a alteração de qualquer valor de campo em um registro existente. O objeto **Recordset** deve dar suporte a atualizações.  
  
 Para definir valores de campo, siga um destes procedimentos:  
  
-   Atribua valores à propriedade [Value](./value-property-ado.md) do objeto [Field](./field-object.md) e chame o método **Update** .  
  
-   Passe um nome de campo e um valor como argumentos com a chamada de **atualização** .  
  
-   Passe uma matriz de nomes de campo e uma matriz de valores com a chamada de **atualização** .  
  
 Quando você usa matrizes de campos e valores, deve haver um número igual de elementos em ambas as matrizes. Além disso, a ordem dos nomes de campo deve corresponder à ordem dos valores de campo. Se o número e a ordem dos campos e valores não corresponderem, ocorrerá um erro.  
  
 Se o objeto **Recordset** oferecer suporte à atualização em lotes, você poderá armazenar em cache várias alterações em um ou mais registros localmente até chamar o método [UpdateBatch](./updatebatch-method.md) . Se você estiver editando o registro atual ou adicionando um novo registro ao chamar o método **UpdateBatch** , o ADO chamará automaticamente o método **Update** para salvar as alterações pendentes no registro atual antes de transmitir as alterações em lote para o provedor.  
  
 Se você mover do registro que está adicionando ou editando antes de chamar o método **Update** , o ADO automaticamente chamará **Update** para salvar as alterações. Você deve chamar o método [CancelUpdate](./cancelupdate-method-ado.md) se quiser cancelar as alterações feitas no registro atual ou descartar um registro recém-adicionado.  
  
 O registro atual permanece atual depois que você chama o método **Update** .  
  
## <a name="record"></a>Record  
 O método **Update** finaliza adições, exclusões e atualizações em campos na coleção [Fields](./fields-collection-ado.md) de um objeto **Record** .  
  
 Por exemplo, os campos excluídos com o método **delete** são marcados para exclusão imediatamente, mas permanecem na coleção. O método **Update** deve ser chamado para realmente excluir esses campos da coleção do provedor.  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Coleção Fields (ADO)](./fields-collection-ado.md)  
    :::column-end:::
    :::column:::
        [Objeto Recordset (ADO)](./recordset-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos Update e CancelUpdate (VB)](./update-and-cancelupdate-methods-example-vb.md)   
 [Exemplo dos métodos Update e CancelUpdate (VC + +)](./update-and-cancelupdate-methods-example-vc.md)   
 [Método AddNew (ADO)](./addnew-method-ado.md)   
 [Método CancelUpdate (ADO)](./cancelupdate-method-ado.md)   
 [Propriedade EditMode](./editmode-property.md)   
 [Método UpdateBatch](./updatebatch-method.md)