---
title: InheritTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- InheritTypeEnum
helpviewer_keywords:
- InheritTypeEnum enumeration [ADOX]
ms.assetid: c2f6ce79-c4b3-4d40-ac95-21025208f991
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b17bdd7204ec52ef5a2fc27d7bc364be7f017189
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66706497"
---
# <a name="inherittypeenum"></a>InheritTypeEnum
Especifica como objetos herdarão as permissões definidas com [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md).  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adInheritBoth**|3|Objetos e outros contêineres contidos pelo objeto principal herdam a entrada.|  
|**adInheritContainers**|2|Outros contêineres que estão contidos pelo objeto principal herdam a entrada.|  
|**adInheritNone**|0|Padrão. Nenhuma herança ocorre.|  
|**adInheritNoPropagate**|4|O **adInheritObjects** e **adInheritContainers** sinalizadores não são propagados para uma entrada herdada.|  
|**adInheritObjects**|1|Objetos não-recipiente no contêiner herdam as permissões.|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Método SetPermissions (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)
