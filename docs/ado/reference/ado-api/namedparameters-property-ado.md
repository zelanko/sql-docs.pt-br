---
title: Propriedade NamedParameters (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: _Command::NamedParameters
helpviewer_keywords: NamedParameters property [ADO]
ms.assetid: 42409387-026c-435f-a9b1-bf4167095875
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 357cfc37c90822ca97ae5ca1349f0bc6743d4859
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="namedparameters-property-ado"></a>Propriedade NamedParameters (ADO)
Indica se os nomes de parâmetros devem ser passados para o provedor.  
  
## <a name="remarks"></a>Remarks  
 Quando essa propriedade é true, o ADO passa o valor da **nome** propriedade de cada parâmetro no **parâmetro** coleta para o [o objeto de comando](../../../ado/reference/ado-api/command-object-ado.md). O provedor usa um nome de parâmetro para corresponder parâmetros no **CommandText** ou **CommandStream** propriedades. Se essa propriedade for false (padrão), os nomes de parâmetro são ignorados e o provedor usa a ordem dos parâmetros para corresponder valores para parâmetros no **CommandText** ou **CommandStream** propriedades.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedade CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [Propriedade CommandStream (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [Coleção Parameters (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
