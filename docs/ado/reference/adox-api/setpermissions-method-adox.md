---
title: Método SetPermissions (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- User25::SetPermissions
- User25::raw_SetPermissions
- _Group25::SetPermissions
- _Group25::raw_SetPermissions
helpviewer_keywords:
- SetPermissions method [ADOX]
ms.assetid: b7f925d7-b05c-4376-bb49-f8d2c17b8b24
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fcc44037ac746621c044bca755fd9b957356dc38
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66705799"
---
# <a name="setpermissions-method-adox"></a>Método SetPermissions (ADOX)
Especifica as permissões para um [grupo](../../../ado/reference/adox-api/group-object-adox.md) ou [usuário](../../../ado/reference/adox-api/user-object-adox.md) em um objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
GroupOrUser.SetPermissions Name, ObjectType, Action, Rights [, Inherit] [, ObjectTypeId]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Nome*  
 Um **cadeia de caracteres** valor que especifica o nome do objeto para o qual definir as permissões.  
  
 *ObjectType*  
 Um **longo** valor que pode ser um dos [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) constantes, que especifica o tipo de objeto para o qual obter as permissões.  
  
 *Ação*  
 Um **longo** valor que pode ser um dos [ActionEnum](../../../ado/reference/adox-api/actionenum.md) constantes que especifica o tipo de ação a ser executada ao definir as permissões.  
  
 *Direitos*  
 Um **longo** valor que pode ser uma máscara de bits de um ou mais da [RightsEnum](../../../ado/reference/adox-api/rightsenum.md) constantes, que indica os direitos para definir.  
  
 *Inherit*  
 Opcional. Um **longo** valor que pode ser um dos [InheritTypeEnum](../../../ado/reference/adox-api/inherittypeenum.md) constantes, que especifica como objetos herdarão essas permissões. O valor padrão é **adInheritNone**.  
  
 *ObjectTypeId*  
 Opcional. Um **Variant** valor que especifica o GUID de um tipo de objeto de provedor que não é definido pela especificação do OLE DB. Esse parâmetro é necessário se *ObjectType* é definido como **adPermObjProviderSpecific**; caso contrário, ele não é usado.  
  
## <a name="remarks"></a>Comentários  
 Se o provedor não dá suporte para configurar direitos de acesso para usuários ou grupos, ocorrerá um erro.  
  
> [!NOTE]
>  Ao chamar **SetPermissions**, definir a ações como **adAccessRevoke** substitui as configurações dos *direitos* parâmetro. Não defina *ações* à **adAccessRevoke** se você quiser que os direitos especificados no *direitos* parâmetro entrem em vigor.  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Objeto Group (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[Objeto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|  
  
## <a name="see-also"></a>Consulte também  
 [GetPermissions e SetPermissions métodos (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Método GetPermissions (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)   
 [Propriedade Name (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)
