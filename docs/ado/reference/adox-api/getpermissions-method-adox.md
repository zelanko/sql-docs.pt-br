---
title: Método GetPermissions (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _User25::GetPermissions
- _Group25::raw_GetPermissions
- _Group25::GetPermissions
- _User25::raw_GetPermissions
helpviewer_keywords:
- GetPermissions method [ADOX]
ms.assetid: df201c1f-c76a-465d-98f0-83b7fc36e6e3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6517b09e682853492cd129e0c43abfd7164ed2e7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63313267"
---
# <a name="getpermissions-method-adox"></a>Método GetPermissions (ADOX)
Retorna as permissões para um [grupo](../../../ado/reference/adox-api/group-object-adox.md) ou [usuário](../../../ado/reference/adox-api/user-object-adox.md) em um objeto ou um contêiner de objetos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ReturnValue=GroupOrUser.GetPermissions(Name, ObjectType    [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um **longo** valor que especifica uma máscara de bits que contém as permissões que o grupo ou usuário tem sobre o objeto. Esse valor pode ser um ou mais dos [RightsEnum](../../../ado/reference/adox-api/rightsenum.md) constantes.  
  
#### <a name="parameters"></a>Parâmetros  
 *Nome*  
 Um **Variant** valor que especifica o nome do objeto para o qual definir as permissões. Definir *nome* com um valor nulo, se você quiser obter as permissões para o objeto recipiente.  
  
 *ObjectType*  
 Um **longo** valor que pode ser um dos [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) constantes, que especifica o tipo de objeto para o qual obter as permissões.  
  
 *ObjectTypeId*  
 Opcional. Um **Variant** valor que especifica o GUID de um tipo de objeto de provedor não definido pela especificação do OLE DB. Esse parâmetro é necessário se *ObjectType* é definido como **adPermObjProviderSpecific**; caso contrário, ele não é usado.  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Objeto Group (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[Objeto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|  
  
## <a name="see-also"></a>Consulte também  
 [GetPermissions e SetPermissions métodos (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Propriedade Name (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)   
 [Método SetPermissions (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)
