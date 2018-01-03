---
title: InheritTypeEnum | Microsoft Docs
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
f1_keywords: InheritTypeEnum
helpviewer_keywords: InheritTypeEnum enumeration [ADOX]
ms.assetid: c2f6ce79-c4b3-4d40-ac95-21025208f991
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 33635119675c7ebe69f7c8a6d17f5c687d8785bb
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
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
