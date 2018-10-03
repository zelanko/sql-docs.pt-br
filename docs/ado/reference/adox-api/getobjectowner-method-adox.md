---
title: Método GetObjectOwner (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Catalog::raw_GetObjectOwner
- _Catalog::GetObjectOwner
helpviewer_keywords:
- GetObjectOwner method [ADOX]
ms.assetid: 8965adf0-9075-4125-8142-73eb700029c3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9b2c967ac293ed59fde6494e12c2afc2c5b6de90
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47687204"
---
# <a name="getobjectowner-method-adox"></a>Método GetObjectOwner (ADOX)
Retorna o proprietário de um objeto em um [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Owner = Catalog.GetObjectOwner(ObjectName, ObjectType [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um **cadeia de caracteres** valor que especifica a [nome](../../../ado/reference/adox-api/name-property-adox.md) dos [usuário](../../../ado/reference/adox-api/user-object-adox.md) ou [grupo](../../../ado/reference/adox-api/group-object-adox.md) que possui o objeto.  
  
#### <a name="parameters"></a>Parâmetros  
 *ObjectName*  
 Um **cadeia de caracteres** valor que especifica o nome do objeto para o qual retornar o proprietário.  
  
 *ObjectType*  
 Um **longo** valor que pode ser um dos [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) constantes, que especifica o tipo de objeto para o qual obter o proprietário.  
  
 *ObjectTypeId*  
 Opcional. Um **Variant** valor que especifica o GUID de um tipo de objeto de provedor não definido pela especificação do OLE DB. Esse parâmetro é necessário se *ObjectType* é definido como **adPermObjProviderSpecific**; caso contrário, ele não é usado.  
  
## <a name="remarks"></a>Comentários  
 Ocorrerá um erro se o provedor não dá suporte a proprietários de objetos de retorno.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>Consulte também  
 [GetObjectOwner e Setobjectowner (VB) métodos](../../../ado/reference/adox-api/getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [Método SetObjectOwner](../../../ado/reference/adox-api/setobjectowner-method.md)
