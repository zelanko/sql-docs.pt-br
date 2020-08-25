---
description: InheritTypeEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: d1fed614d90bbf53fdb2198e3ddd657a1e44acd1
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770115"
---
# <a name="inherittypeenum"></a>InheritTypeEnum
Especifica como os objetos herdarão as permissões definidas com [SetPermissions](./setpermissions-method-adox.md).  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adInheritBoth**|3|Os objetos e outros contêineres contidos no objeto primário herdam a entrada.|  
|**adInheritContainers**|2|Outros contêineres que estão contidos pelo objeto primário herdam a entrada.|  
|**adInheritNone**|0|Padrão. Nenhuma herança ocorre.|  
|**adInheritNoPropagate**|4|Os sinalizadores **adInheritObjects** e **adInheritContainers** não são propagados para uma entrada herdada.|  
|**adInheritObjects**|1|Os objetos que não são de contêiner no contêiner herdam as permissões.|  
  
## <a name="applies-to"></a>Aplica-se A  
 [Método SetPermissions (ADOX)](./setpermissions-method-adox.md)