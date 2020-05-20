---
title: Método SetObjectOwner | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Catalog::SetObjectOwner
- _Catalog::raw_SetObjectOwner
helpviewer_keywords:
- SetObjectOwner method [ADOX]
ms.assetid: e5170a37-9d6e-43db-bfb6-9b6631fa3048
author: rothja
ms.author: jroth
ms.openlocfilehash: 615e62ad8a22c50851ea50a2a8511e0859b54652
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763307"
---
# <a name="setobjectowner-method"></a>Método SetObjectOwner
Especifica o proprietário de um objeto em um [Catálogo](../../../ado/reference/adox-api/catalog-object-adox.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Catalog.SetObjectOwner ObjectName, ObjectType, OwnerName [,ObjectTypeId]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *ObjectName*  
 Um valor de **cadeia de caracteres** que especifica o nome do objeto para o qual especificar o proprietário.  
  
 *ObjectType*  
 Um valor **longo** que pode ser uma das constantes [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) que especifica o tipo de proprietário.  
  
 *OwnerName*  
 Um valor de **cadeia de caracteres** que especifica o [nome](../../../ado/reference/adox-api/name-property-adox.md) do [usuário](../../../ado/reference/adox-api/user-object-adox.md) ou [grupo](../../../ado/reference/adox-api/group-object-adox.md) para o qual o objeto é proprietário.  
  
 *ObjectTypeId*  
 Opcional. Um valor **Variant** que especifica o GUID para um tipo de objeto de provedor que não é definido pela especificação de OLE DB. Esse parâmetro será necessário se *objecttype* for definido como **adPermObjProviderSpecific**; caso contrário, ele não será usado.  
  
## <a name="remarks"></a>Comentários  
 Ocorrerá um erro se o provedor não oferecer suporte à especificação de proprietários de objeto.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos GetObjectOwner e SetObjectOwner (VB)](../../../ado/reference/adox-api/getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [Método GetObjectOwner (ADOX)](../../../ado/reference/adox-api/getobjectowner-method-adox.md)
