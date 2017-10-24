---
title: Propriedade NamedParameters (ADO) | Microsoft Docs
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
- _Command::NamedParameters
helpviewer_keywords:
- NamedParameters property [ADO]
ms.assetid: 42409387-026c-435f-a9b1-bf4167095875
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 613f4cb52c6225d573d314b83f26c220e7caabfc
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="namedparameters-property-ado"></a>Propriedade NamedParameters (ADO)
Indica se os nomes de parâmetros devem ser passados para o provedor.  
  
## <a name="remarks"></a>Comentários  
 Quando essa propriedade é true, o ADO passa o valor da **nome** propriedade de cada parâmetro no **parâmetro** coleta para o [o objeto de comando](../../../ado/reference/ado-api/command-object-ado.md). O provedor usa um nome de parâmetro para corresponder parâmetros no **CommandText** ou **CommandStream** propriedades. Se essa propriedade for false (padrão), os nomes de parâmetro são ignorados e o provedor usa a ordem dos parâmetros para corresponder valores para parâmetros no **CommandText** ou **CommandStream** propriedades.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [Propriedade CommandStream (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [Coleção Parameters (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)

