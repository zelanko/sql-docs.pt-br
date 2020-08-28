---
description: Propriedade ActiveCommand (ADO)
title: Propriedade ActiveCommand (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: df737543e8cc09735c7da413b89406b6f2385079
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88977147"
---
# <a name="activecommand-property-ado"></a>Propriedade ActiveCommand (ADO)
Indica o objeto de [comando](./command-object-ado.md) que criou o objeto [Recordset](./recordset-object-ado.md) associado.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna uma **variante** que contém um objeto de **comando** . O padrão é uma referência de objeto nulo.  
  
## <a name="remarks"></a>Comentários  
 A propriedade **ActiveCommand** é somente leitura.  
  
 Se um objeto de **comando** não foi usado para criar o **conjunto de registros**atual, uma referência de objeto **nulo** será retornada.  
  
 Use essa propriedade para localizar o objeto de **comando** associado quando você receber apenas o objeto **Recordset** resultante.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade ActiveCommand (VB)](./activecommand-property-example-vb.md)   
 [Exemplo da propriedade ActiveCommand (JScript)](./activecommand-property-example-jscript.md)   
 [Exemplo da propriedade ActiveCommand (VC + +)](./activecommand-property-example-vc.md)   
 [Objeto Command (ADO)](./command-object-ado.md)