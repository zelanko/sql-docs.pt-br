---
title: InheritTypeEnum | Microsoft Docs
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
- InheritTypeEnum
helpviewer_keywords:
- InheritTypeEnum enumeration [ADOX]
ms.assetid: c2f6ce79-c4b3-4d40-ac95-21025208f991
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: de2281f5badafc7c2140347ab96dfb7251f98ed2
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="inherittypeenum"></a>InheritTypeEnum
Especifica como objetos herdarão as permissões definidas com [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md).  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adInheritBoth**|3|Objetos e outros contêineres contidos pelo objeto principal herdam a entrada.|  
|**adInheritContainers**|2|Outros contêineres que estão contidos no objeto principal herdam a entrada.|  
|**adInheritNone**|0|Padrão. Nenhuma herança ocorre.|  
|**adInheritNoPropagate**|4|O **adInheritObjects** e **adInheritContainers** sinalizadores não são propagados para uma entrada herdada.|  
|**adInheritObjects**|1|Objetos não-recipiente no recipiente herdam as permissões.|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Método SetPermissions (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)
