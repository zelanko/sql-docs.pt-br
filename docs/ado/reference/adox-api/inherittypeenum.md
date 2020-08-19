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
ms.openlocfilehash: dfa4d6c15cc7d26dbfe964947bd09a04e2f75128
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439848"
---
# <a name="inherittypeenum"></a>InheritTypeEnum
Especifica como os objetos herdarão as permissões definidas com [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md).  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adInheritBoth**|3|Os objetos e outros contêineres contidos no objeto primário herdam a entrada.|  
|**adInheritContainers**|2|Outros contêineres que estão contidos pelo objeto primário herdam a entrada.|  
|**adInheritNone**|0|Padrão. Nenhuma herança ocorre.|  
|**adInheritNoPropagate**|4|Os sinalizadores **adInheritObjects** e **adInheritContainers** não são propagados para uma entrada herdada.|  
|**adInheritObjects**|1|Os objetos que não são de contêiner no contêiner herdam as permissões.|  
  
## <a name="applies-to"></a>Aplica-se A  
 [Método SetPermissions (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)
