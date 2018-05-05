---
title: InheritTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- InheritTypeEnum
helpviewer_keywords:
- InheritTypeEnum enumeration [ADOX]
ms.assetid: c2f6ce79-c4b3-4d40-ac95-21025208f991
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d4d822bd48d399b767c6676e014abe3d733aa5bc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
