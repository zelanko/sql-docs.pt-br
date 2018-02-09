---
title: "Método GetObjectOwner (ADOX) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Catalog::raw_GetObjectOwner
- _Catalog::GetObjectOwner
helpviewer_keywords:
- GetObjectOwner method [ADOX]
ms.assetid: 8965adf0-9075-4125-8142-73eb700029c3
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 51092c3cf38f9b8ae9d5d81bbbea0177df097f1d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="getobjectowner-method-adox"></a>Método GetObjectOwner (ADOX)
Retorna o proprietário de um objeto em um [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Owner = Catalog.GetObjectOwner(ObjectName, ObjectType [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um **cadeia de caracteres** valor que especifica o [nome](../../../ado/reference/adox-api/name-property-adox.md) do [usuário](../../../ado/reference/adox-api/user-object-adox.md) ou [grupo](../../../ado/reference/adox-api/group-object-adox.md) que possui o objeto.  
  
#### <a name="parameters"></a>Parâmetros  
 *ObjectName*  
 Um **cadeia de caracteres** valor que especifica o nome do objeto para o qual retornar o proprietário.  
  
 *ObjectType*  
 Um **longo** valor que pode ser um do [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) constantes, que especifica o tipo de objeto para o qual obter o proprietário.  
  
 *ObjectTypeId*  
 Opcional. Um **Variant** valor que especifica o GUID de um tipo de objeto de provedor não definido pela especificação do OLE DB. Esse parâmetro é necessário se *ObjectType* é definido como **adPermObjProviderSpecific**; caso contrário, ele não é usado.  
  
## <a name="remarks"></a>Remarks  
 Se o provedor não dá suporte a retorno proprietários de objeto, ocorrerá um erro.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de métodos de SetObjectOwner (VB) e GetObjectOwner](../../../ado/reference/adox-api/getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [Método SetObjectOwner](../../../ado/reference/adox-api/setobjectowner-method.md)
