---
description: Propriedade ActiveCommand (ADO)
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
ms.openlocfilehash: 2e8c969c8e611c8e2bff76dc045a28a9c6d6ab96
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759936"
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