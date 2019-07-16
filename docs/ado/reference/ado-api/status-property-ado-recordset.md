---
title: Propriedade status (conjunto de registros ADO) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1d91c3e92be7679ad6fbbb4a4ee7bd1bb6a48422
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916833"
---
# <a name="status-property-ado-recordset"></a>Propriedade Status (Conjunto de registros ADO)
Indica o status do registro atual em relação a atualizações em lotes ou outras operações em massa.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna uma soma de um ou mais [RecordStatusEnum](../../../ado/reference/ado-api/recordstatusenum.md) valores.  
  
## <a name="remarks"></a>Comentários  
 Use o **Status** propriedade para ver as alterações que estão pendentes para os registros modificados durante a atualização em lotes. Você também pode usar o **Status** propriedade para exibir o status dos registros que falham durante as operações em massa, como quando você chama o [ressincronizar](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), ou [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) métodos em um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) de objeto, ou defina o [filtro](../../../ado/reference/ado-api/filter-property.md) propriedade em um **Recordset** objeto em uma matriz de indicadores. Com essa propriedade, você pode determinar como um determinado registro falha e resolvê-lo adequadamente.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo da propriedade status (conjunto de registros) (VB)](../../../ado/reference/ado-api/status-property-example-recordset-vb.md)   
 [Exemplo da propriedade Status (VC++)](../../../ado/reference/ado-api/status-property-example-vc.md)   
