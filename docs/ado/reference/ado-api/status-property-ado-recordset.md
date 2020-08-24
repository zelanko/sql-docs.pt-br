---
description: Propriedade Status (Conjunto de registros ADO)
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
ms.openlocfilehash: cea09babfd2dacf35705adc71cddcdee99aad544
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777295"
---
# <a name="status-property-ado-recordset"></a>Propriedade Status (Conjunto de registros ADO)
Indica o status do registro atual em relação às atualizações em lote ou outras operações em massa.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna uma soma de um ou mais valores [RecordStatusEnum](./recordstatusenum.md) .  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **status** para ver quais alterações estão pendentes para os registros modificados durante a atualização do lote. Você também pode usar a propriedade **status** para exibir o status dos registros que falham durante operações em massa, como quando você chama os métodos [Ressync](./resync-method.md), [UpdateBatch](./updatebatch-method.md)ou [CancelBatch](./cancelbatch-method-ado.md) em um objeto [Recordset](./recordset-object-ado.md) ou define a propriedade [Filter](./filter-property.md) em um objeto **Recordset** para uma matriz de indicadores. Com essa propriedade, você pode determinar como um determinado registro falhou e resolvê-lo de acordo.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade Status (conjunto de registros) (VB)](./status-property-example-recordset-vb.md)   
 [Exemplo da propriedade Status (VC++)](./status-property-example-vc.md)