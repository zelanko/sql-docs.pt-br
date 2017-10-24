---
title: Estado de propriedade (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Command25::State
helpviewer_keywords:
- State property [ADO]
ms.assetid: 0b993bac-2653-40b1-bcbb-5b57b6aae2bf
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: efd795c5ae1095a11520215994185987e9cf2b32
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="state-property-ado"></a>Propriedade State (ADO)
Indica para todos os objetos aplicáveis, se o estado do objeto está aberto ou fechado. Se o objeto estiver executando um método assíncrono, indica se o estado atual do objeto está se conectando, execução ou recuperar.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um **longo** valor que pode ser um [ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md) valor. O valor padrão é **adStateClosed**.  
  
## <a name="remarks"></a>Comentários  
 Você pode usar o **estado** propriedade para determinar o estado atual de um objeto fornecido a qualquer momento.  
  
 O objeto **estado** propriedade pode ter uma combinação de valores. Por exemplo, se estiver executando uma instrução, essa propriedade terá um valor combinado de **adStateOpen** e **adStateExecuting**.  
  
 O **estado** propriedade é somente leitura.  
  
## <a name="applies-to"></a>Aplica-se a  
  
||||  
|-|-|-|  
|[Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)||  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de propriedades de estado (VB), ConnectionTimeout e ConnectionString](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [Exemplo de propriedades de estado (VC + +), ConnectionTimeout e ConnectionString](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   

