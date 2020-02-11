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
ms.openlocfilehash: d2a2f23360cf3ce032d14af7ca475d5c2c3ea638
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67921672"
---
# <a name="activecommand-property-ado"></a>Propriedade ActiveCommand (ADO)
Indica o objeto de [comando](../../../ado/reference/ado-api/command-object-ado.md) que criou o objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) associado.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna uma **variante** que contém um objeto de **comando** . O padrão é uma referência de objeto nulo.  
  
## <a name="remarks"></a>Comentários  
 A propriedade **ActiveCommand** é somente leitura.  
  
 Se um objeto de **comando** não foi usado para criar o **conjunto de registros**atual, uma referência de objeto **nulo** será retornada.  
  
 Use essa propriedade para localizar o objeto de **comando** associado quando você receber apenas o objeto **Recordset** resultante.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade ActiveCommand (VB)](../../../ado/reference/ado-api/activecommand-property-example-vb.md)   
 [Exemplo da propriedade ActiveCommand (JScript)](../../../ado/reference/ado-api/activecommand-property-example-jscript.md)   
 [Exemplo da propriedade ActiveCommand (VC + +)](../../../ado/reference/ado-api/activecommand-property-example-vc.md)   
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)
