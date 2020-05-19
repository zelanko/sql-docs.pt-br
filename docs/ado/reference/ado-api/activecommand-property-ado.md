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
author: rothja
ms.author: jroth
ms.openlocfilehash: b89876366c80d20bde110da9e9d86414873e86bc
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82747472"
---
# <a name="activecommand-property-ado"></a>Propriedade ActiveCommand (ADO)
Indica o objeto de [comando](../../../ado/reference/ado-api/command-object-ado.md) que criou o objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) associado.  
  
## <a name="return-value"></a>Valor Retornado  
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
