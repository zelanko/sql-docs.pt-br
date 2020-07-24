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
author: rothja
ms.author: jroth
ms.openlocfilehash: fe7d97909a2d38e548a072245b08110b1d61eb3c
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86943158"
---
# <a name="objecttypeenum"></a>ObjectTypeEnum
Especifica o tipo de objeto de banco de dados para o qual definir permissões ou propriedade.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adPermObjColumn**|2|O objeto é uma coluna.|  
|**adPermObjDatabase**|3|O objeto é um banco de dados.|  
|**adPermObjProcedure**|4|O objeto é um procedimento.|  
|**adPermObjProviderSpecific**|-1|O objeto é um tipo definido pelo provedor. Ocorrerá um erro se o parâmetro *objecttype* for **adPermObjProviderSpecific** e um *objecttipaid* não for fornecido.|  
|**adPermObjTable**|1|O objeto é uma tabela.|  
|**adPermObjView**|5|O objeto é uma exibição.|  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Método GetObjectOwner (ADOX)](../../../ado/reference/adox-api/getobjectowner-method-adox.md)  
        [Método GetPermissions (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)  
    :::column-end:::
    :::column:::
        [Método SetObjectOwner](../../../ado/reference/adox-api/setobjectowner-method.md)  
        [Método SetPermissions (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)  
    :::column-end:::
:::row-end:::
