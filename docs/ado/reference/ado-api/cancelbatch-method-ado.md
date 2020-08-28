---
description: Método CancelBatch (ADO)
title: Método CancelBatch (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 0baf8d291bbb45961163dfc80106724c48d71613
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975577"
---
# <a name="cancelbatch-method-ado"></a>Método CancelBatch (ADO)
Cancela uma atualização de lote pendente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.CancelBatchAffectRecords  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *AffectRecords*  
 Opcional. Um valor [AffectEnum](./affectenum.md) que indica quantos registros o método **CancelBatch** afetará.  
  
## <a name="remarks"></a>Comentários  
 Use o método **CancelBatch** para cancelar todas as atualizações pendentes em um [conjunto de registros](./recordset-object-ado.md) no modo de atualização do lote. Se o **conjunto de registros** estiver no modo de atualização imediata, chamar **CancelBatch** sem **adAffectCurrent** gerará um erro.  
  
 Se você estiver editando o registro atual ou estiver adicionando um novo registro ao chamar **CancelBatch**, o ADO primeiro chama o método [CancelUpdate](./cancelupdate-method-ado.md) para cancelar as alterações em cache. Depois disso, todas as alterações pendentes no **conjunto de registros** serão canceladas.  
  
 O registro atual pode ser interminável após uma chamada **CancelBatch** , especialmente se você estivesse no processo de adicionar um novo registro. Por esse motivo, é prudente definir a posição do registro atual como um local conhecido no conjunto de **registros** após a chamada **CancelBatch** . Por exemplo, chame o método [MoveFirst](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md) .  
  
 Se a tentativa de cancelar as atualizações pendentes falhar devido a um conflito com os dados subjacentes (por exemplo, se um registro tiver sido excluído por outro usuário), o provedor retornará avisos para a coleção de [erros](./errors-collection-ado.md) , mas não interromperá a execução do programa. Um erro de tempo de execução ocorrerá somente se houver conflitos em todos os registros solicitados. Use a propriedade [Filter](./filter-property.md) (**adFilterAffectedRecords**) e a propriedade [status](./status-property-ado-recordset.md) para localizar registros com conflitos.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos UpdateBatch e CancelBatch (VB)](./updatebatch-and-cancelbatch-methods-example-vb.md)   
 [Exemplo dos métodos UpdateBatch e CancelBatch (VC + +)](./updatebatch-and-cancelbatch-methods-example-vc.md)   
 [Método Cancel (ADO)](./cancel-method-ado.md)   
 [Método Cancel (RDS)](../rds-api/cancel-method-rds.md)   
 [Método CancelUpdate (ADO)](./cancelupdate-method-ado.md)   
 [Método CancelUpdate (RDS)](../rds-api/cancelupdate-method-rds.md)   
 [Método Clear (ADO)](./clear-method-ado.md)   
 [Propriedade LockType (ADO)](./locktype-property-ado.md)   
 [Método UpdateBatch](./updatebatch-method.md)