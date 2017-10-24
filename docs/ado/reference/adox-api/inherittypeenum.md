---
title: InheritTypeEnum | Microsoft Docs
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
- InheritTypeEnum
helpviewer_keywords:
- InheritTypeEnum enumeration [ADOX]
ms.assetid: c2f6ce79-c4b3-4d40-ac95-21025208f991
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 36570c508955b82ccd403e9af10895edc1584d9f
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="inherittypeenum"></a>InheritTypeEnum
Especifica como objetos herdarão as permissões definidas com [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md).  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adInheritBoth**|3|Objetos e outros contêineres contidos pelo objeto principal herdam a entrada.|  
|**adInheritContainers**|2|Outros contêineres que estão contidos no objeto principal herdam a entrada.|  
|**adInheritNone**|0|Padrão. Nenhuma herança ocorre.|  
|**adInheritNoPropagate**|4|O **adInheritObjects** e **adInheritContainers** sinalizadores não são propagados para uma entrada herdada.|  
|**adInheritObjects**|1|Objetos não-recipiente no recipiente herdam as permissões.|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Método SetPermissions (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)

