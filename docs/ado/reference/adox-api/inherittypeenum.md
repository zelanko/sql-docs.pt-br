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
author: rothja
ms.author: jroth
ms.openlocfilehash: f420d7d49ad24188f5210001af1209427478f3f6
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82746677"
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
