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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7c9892ddc3be28e63dae0f3f6440cc4a668498e3
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764903"
---
# <a name="getobjectowner-method-adox"></a>Método GetObjectOwner (ADOX)
Retorna o proprietário de um objeto em um [Catálogo](../../../ado/reference/adox-api/catalog-object-adox.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Owner = Catalog.GetObjectOwner(ObjectName, ObjectType [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um valor de **cadeia de caracteres** que especifica o [nome](../../../ado/reference/adox-api/name-property-adox.md) do [usuário](../../../ado/reference/adox-api/user-object-adox.md) ou [grupo](../../../ado/reference/adox-api/group-object-adox.md) que possui o objeto.  
  
#### <a name="parameters"></a>Parâmetros  
 *ObjectName*  
 Um valor de **cadeia de caracteres** que especifica o nome do objeto para o qual retornar o proprietário.  
  
 *ObjectType*  
 Um valor **longo** que pode ser uma das constantes [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) , que especifica o tipo do objeto para o qual obter o proprietário.  
  
 *ObjectTypeId*  
 Opcional. Um valor de **variante** que especifica o GUID para um tipo de objeto de provedor não definido pela especificação de OLE DB. Esse parâmetro será necessário se *objecttype* for definido como **adPermObjProviderSpecific**; caso contrário, ele não será usado.  
  
## <a name="remarks"></a>Comentários  
 Ocorrerá um erro se o provedor não der suporte ao retorno de proprietários de objeto.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos GetObjectOwner e SetObjectOwner (VB)](../../../ado/reference/adox-api/getobjectowner-and-setobjectowner-methods-example-vb.md)   
 [Método SetObjectOwner](../../../ado/reference/adox-api/setobjectowner-method.md)
