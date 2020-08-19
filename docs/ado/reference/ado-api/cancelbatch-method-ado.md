---
description: Método CancelBatch (ADO)
title: Método CancelBatch (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_CancelBatch
- Recordset15::CancelBatch
helpviewer_keywords:
- CancelBatch method [ADO]
ms.assetid: dbdc2574-e44e-4d95-b03d-4a5d9e9adf3c
author: rothja
ms.author: jroth
ms.openlocfilehash: f8fa4d02dd10325726c83a6b645ebdd5b94397f9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451028"
---
# <a name="cancelbatch-method-ado"></a>Método CancelBatch (ADO)
Cancela uma atualização de lote pendente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.CancelBatchAffectRecords  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *AffectRecords*  
 Opcional. Um valor [AffectEnum](../../../ado/reference/ado-api/affectenum.md) que indica quantos registros o método **CancelBatch** afetará.  
  
## <a name="remarks"></a>Comentários  
 Use o método **CancelBatch** para cancelar todas as atualizações pendentes em um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) no modo de atualização do lote. Se o **conjunto de registros** estiver no modo de atualização imediata, chamar **CancelBatch** sem **adAffectCurrent** gerará um erro.  
  
 Se você estiver editando o registro atual ou estiver adicionando um novo registro ao chamar **CancelBatch**, o ADO primeiro chama o método [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) para cancelar as alterações em cache. Depois disso, todas as alterações pendentes no **conjunto de registros** serão canceladas.  
  
 O registro atual pode ser interminável após uma chamada **CancelBatch** , especialmente se você estivesse no processo de adicionar um novo registro. Por esse motivo, é prudente definir a posição do registro atual como um local conhecido no conjunto de **registros** após a chamada **CancelBatch** . Por exemplo, chame o método [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) .  
  
 Se a tentativa de cancelar as atualizações pendentes falhar devido a um conflito com os dados subjacentes (por exemplo, se um registro tiver sido excluído por outro usuário), o provedor retornará avisos para a coleção de [erros](../../../ado/reference/ado-api/errors-collection-ado.md) , mas não interromperá a execução do programa. Um erro de tempo de execução ocorrerá somente se houver conflitos em todos os registros solicitados. Use a propriedade [Filter](../../../ado/reference/ado-api/filter-property.md) (**adFilterAffectedRecords**) e a propriedade [status](../../../ado/reference/ado-api/status-property-ado-recordset.md) para localizar registros com conflitos.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos UpdateBatch e CancelBatch (VB)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vb.md)   
 [Exemplo dos métodos UpdateBatch e CancelBatch (VC + +)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vc.md)   
 [Método Cancel (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Método Cancel (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [Método CancelUpdate (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Método CancelUpdate (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Método Clear (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [Propriedade LockType (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)   
 [Método UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)
