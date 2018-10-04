---
title: Propriedade ActiveCommand (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::ActiveCommand
helpviewer_keywords:
- ActiveCommand property [ADO]
ms.assetid: fb4088d5-5968-42d6-aeaa-3955046bb4da
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4dfdb60f9a394fa4d11e9b66ffb1f4b205881293
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47705534"
---
# <a name="activecommand-property-ado"></a>Propriedade ActiveCommand (ADO)
Indica o [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto que criou associado [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um **Variant** que contém uma **comando** objeto. O padrão é uma referência de objeto nulo.  
  
## <a name="remarks"></a>Comentários  
 O **ActiveCommand** propriedade é somente leitura.  
  
 Se um **comando** objeto não foi usado para criar atual **conjunto de registros**, em seguida, um **nulo** referência de objeto é retornada.  
  
 Use essa propriedade para localizar associado **comando** objeto quando você tem apenas resultante **Recordset** objeto.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo da propriedade ActiveCommand (VB)](../../../ado/reference/ado-api/activecommand-property-example-vb.md)   
 [Exemplo da propriedade ActiveCommand (JScript)](../../../ado/reference/ado-api/activecommand-property-example-jscript.md)   
 [Exemplo da propriedade ActiveCommand (VC + +)](../../../ado/reference/ado-api/activecommand-property-example-vc.md)   
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)
