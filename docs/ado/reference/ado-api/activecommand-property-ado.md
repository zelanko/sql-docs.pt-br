---
title: Propriedade ActiveCommand (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::ActiveCommand
helpviewer_keywords:
- ActiveCommand property [ADO]
ms.assetid: fb4088d5-5968-42d6-aeaa-3955046bb4da
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8aa86180edc4117e89863bb232a2faa95d010272
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="activecommand-property-ado"></a>Propriedade ActiveCommand (ADO)
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
