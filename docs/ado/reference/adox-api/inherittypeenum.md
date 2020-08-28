---
description: InheritTypeEnum
title: InheritTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 37c6eba57eb7efb05d2b718e294e33b9616cac77
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984097"
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