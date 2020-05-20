---
title: Propriedade Status (conjunto de registros ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::GetStatus
- Recordset15::Status
helpviewer_keywords:
- Status property [ADO Recordset]
ms.assetid: 41d70d89-880f-4850-9d17-19d9790cc8eb
author: rothja
ms.author: jroth
ms.openlocfilehash: d3ba9ad977fe02a712a675b8a9e4bae4b3d038b1
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759732"
---
# <a name="status-property-ado-recordset"></a>Propriedade Status (Conjunto de registros ADO)
Indica o status do registro atual em relação às atualizações em lote ou outras operações em massa.  
  
## <a name="return-value"></a>Valor Retornado  
 Retorna uma soma de um ou mais valores [RecordStatusEnum](../../../ado/reference/ado-api/recordstatusenum.md) .  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **status** para ver quais alterações estão pendentes para os registros modificados durante a atualização do lote. Você também pode usar a propriedade **status** para exibir o status dos registros que falham durante operações em massa, como quando você chama os métodos [Ressync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)ou [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) em um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) ou define a propriedade [Filter](../../../ado/reference/ado-api/filter-property.md) em um objeto **Recordset** para uma matriz de indicadores. Com essa propriedade, você pode determinar como um determinado registro falhou e resolvê-lo de acordo.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade Status (conjunto de registros) (VB)](../../../ado/reference/ado-api/status-property-example-recordset-vb.md)   
 [Exemplo da propriedade Status (VC++)](../../../ado/reference/ado-api/status-property-example-vc.md)   
