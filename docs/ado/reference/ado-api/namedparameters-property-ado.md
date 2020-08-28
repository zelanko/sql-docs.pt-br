---
description: Propriedade NamedParameters (ADO)
title: Propriedade namedParameters (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Command::NamedParameters
helpviewer_keywords:
- NamedParameters property [ADO]
ms.assetid: 42409387-026c-435f-a9b1-bf4167095875
author: rothja
ms.author: jroth
ms.openlocfilehash: 18552a7d15a5dbe36a05c7391d0fd7e2ab3a6d94
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990487"
---
# <a name="namedparameters-property-ado"></a>Propriedade NamedParameters (ADO)
Indica se os nomes de parâmetro devem ser passados para o provedor.  
  
## <a name="remarks"></a>Comentários  
 Quando essa propriedade é true, o ADO passa o valor da propriedade **Name** de cada parâmetro na coleção de **parâmetros** para o [objeto Command](./command-object-ado.md). O provedor usa um nome de parâmetro para corresponder parâmetros nas propriedades **CommandText** ou **CommandStream** . Se essa propriedade for false (o padrão), os nomes de parâmetros serão ignorados e o provedor usará a ordem dos parâmetros para corresponder valores aos parâmetros nas propriedades **CommandText** ou **CommandStream** .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Command (ADO)](./command-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedade CommandText (ADO)](./commandtext-property-ado.md)   
 [Propriedade CommandStream (ADO)](./commandstream-property-ado.md)   
 [Coleção Parameters (ADO)](./parameters-collection-ado.md)