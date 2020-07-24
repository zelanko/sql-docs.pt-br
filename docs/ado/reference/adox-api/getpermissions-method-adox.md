---
title: Método getPermissions (ADOX) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 221b340cd8df2a9bfc2bfdb19e3e46b18d3a2c57
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942698"
---
# <a name="getpermissions-method-adox"></a>Método GetPermissions (ADOX)
Retorna as permissões para um [grupo](../../../ado/reference/adox-api/group-object-adox.md) ou [usuário](../../../ado/reference/adox-api/user-object-adox.md) em um contêiner de objeto ou objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ReturnValue=GroupOrUser.GetPermissions(Name, ObjectType    [,ObjectTypeId])  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um valor **longo** que especifica um bitmask que contém as permissões que o grupo ou o usuário tem no objeto. Esse valor pode ser uma ou mais das constantes [RightsEnum](../../../ado/reference/adox-api/rightsenum.md) .  
  
#### <a name="parameters"></a>Parâmetros  
 *Nome*  
 Um valor **Variant** que especifica o nome do objeto para o qual definir permissões. Defina *nome* como um valor nulo se você quiser obter as permissões para o contêiner de objeto.  
  
 *ObjectType*  
 Um valor **longo** que pode ser uma das constantes [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) , que especifica o tipo do objeto para o qual obter permissões.  
  
 *ObjectTypeId*  
 Opcional. Um valor de **variante** que especifica o GUID para um tipo de objeto de provedor não definido pela especificação de OLE DB. Esse parâmetro será necessário se *objecttype* for definido como **adPermObjProviderSpecific**; caso contrário, ele não será usado.  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Objeto Group (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)  
    :::column-end:::
    :::column:::
        [Objeto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos getPermissions e SetPermissions (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Propriedade Name (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)   
 [Método SetPermissions (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)
