---
title: Propriedade ActiveCommand (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset20::ActiveCommand
helpviewer_keywords:
- ActiveCommand property [ADO]
ms.assetid: fb4088d5-5968-42d6-aeaa-3955046bb4da
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eee93cce3f7868ff9c71a83a462e5073d3e2d722
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="activecommand-property-ado"></a>ActiveCommand Property (ADO)
Indica o [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto criado associado [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um **Variant** que contém um **comando** objeto. Padrão é uma referência de objeto nulo.  
  
## <a name="remarks"></a>Remarks  
 O **ActiveCommand** propriedade é somente leitura.  
  
 Se um **comando** objeto não foi usado para criar atual **registros**, em seguida, um **nulo** referência de objeto é retornada.  
  
 Use esta propriedade para localizar associado **comando** objeto quando você terá apenas resultante **registros** objeto.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de propriedade ActiveCommand (VB)](../../../ado/reference/ado-api/activecommand-property-example-vb.md)   
 [Exemplo de propriedade ActiveCommand (JScript)](../../../ado/reference/ado-api/activecommand-property-example-jscript.md)   
 [Exemplo de propriedade ActiveCommand (VC + +)](../../../ado/reference/ado-api/activecommand-property-example-vc.md)   
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)
