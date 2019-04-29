---
title: Estado de propriedade (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command25::State
helpviewer_keywords:
- State property [ADO]
ms.assetid: 0b993bac-2653-40b1-bcbb-5b57b6aae2bf
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 98d3e61b37eb22ebaf793252f49b2b11621abd80
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63027665"
---
# <a name="state-property-ado"></a>Propriedade State (ADO)
Indica para todos os objetos aplicáveis se o estado do objeto é aberto ou fechado. Se o objeto está em execução a um método assíncrono, indica se o estado atual do objeto é conectar-se, em execução ou recuperar.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um **longo** valor que pode ser um [ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md) valor. O valor padrão é **adStateClosed**.  
  
## <a name="remarks"></a>Comentários  
 Você pode usar o **estado** propriedade para determinar o estado atual de um determinado objeto em qualquer momento.  
  
 O objeto **estado** propriedade pode ter uma combinação de valores. Por exemplo, se a execução de uma instrução, essa propriedade terá um valor combinado de **adStateOpen** e **adStateExecuting**.  
  
 O **estado** propriedade é somente leitura.  
  
## <a name="applies-to"></a>Aplica-se a  
  
||||  
|-|-|-|  
|[Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)||  
  
## <a name="see-also"></a>Consulte também  
 [ConnectionString, ConnectionTimeout e exemplo de propriedades de estado (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString, ConnectionTimeout e exemplo de propriedades de estado (VC + +)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
