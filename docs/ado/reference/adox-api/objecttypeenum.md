---
title: ObjectTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ObjectTypeEnum
helpviewer_keywords:
- ObjectTypeEnum enumeration [ADOX]
ms.assetid: 3fdecfca-aa91-4596-ad98-610f1b7f840b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ed7273b2fd24690956fa5c5ffe317ad9c00c40ee
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47751769"
---
# <a name="objecttypeenum"></a>ObjectTypeEnum
Especifica o tipo de objeto de banco de dados para o qual definir permissões ou a propriedade.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adPermObjColumn**|2|O objeto é uma coluna.|  
|**adPermObjDatabase**|3|O objeto é um banco de dados.|  
|**adPermObjProcedure**|4|O objeto é um procedimento.|  
|**adPermObjProviderSpecific**|-1|O objeto é um tipo definido pelo provedor. Ocorrerá um erro se o *ObjectType* parâmetro é **adPermObjProviderSpecific** e um *ObjectTypeId* não for fornecido.|  
|**adPermObjTable**|1|O objeto é uma tabela.|  
|**adPermObjView**|5|O objeto é um modo de exibição.|  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Método GetObjectOwner (ADOX)](../../../ado/reference/adox-api/getobjectowner-method-adox.md)|[Método GetPermissions (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)|  
|[Método SetObjectOwner](../../../ado/reference/adox-api/setobjectowner-method.md)|[Método SetPermissions (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)|
