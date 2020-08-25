---
description: Método SetObjectOwner
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
ms.openlocfilehash: acefd94f29b030a6bee724686e11023a354d8921
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769405"
---
# <a name="setobjectowner-method"></a>Método SetObjectOwner
Especifica o proprietário de um objeto em um [Catálogo](./catalog-object-adox.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Catalog.SetObjectOwner ObjectName, ObjectType, OwnerName [,ObjectTypeId]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *ObjectName*  
 Um valor de **cadeia de caracteres** que especifica o nome do objeto para o qual especificar o proprietário.  
  
 *ObjectType*  
 Um valor **longo** que pode ser uma das constantes [ObjectTypeEnum](./objecttypeenum.md) que especifica o tipo de proprietário.  
  
 *OwnerName*  
 Um valor de **cadeia de caracteres** que especifica o [nome](./name-property-adox.md) do [usuário](./user-object-adox.md) ou [grupo](./group-object-adox.md) para o qual o objeto é proprietário.  
  
 *ObjectTypeId*  
 Opcional. Um valor **Variant** que especifica o GUID para um tipo de objeto de provedor que não é definido pela especificação de OLE DB. Esse parâmetro será necessário se *objecttype* for definido como **adPermObjProviderSpecific**; caso contrário, ele não será usado.  
  
## <a name="remarks"></a>Comentários  
 Ocorrerá um erro se o provedor não oferecer suporte à especificação de proprietários de objeto.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Catalog (ADOX)](./catalog-object-adox.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos GetObjectOwner e SetObjectOwner (VB)](./getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [Método GetObjectOwner (ADOX)](./getobjectowner-method-adox.md)