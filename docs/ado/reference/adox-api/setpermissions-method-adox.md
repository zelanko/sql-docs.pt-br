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
ms.openlocfilehash: 50a609d0cebe70ea5127ed448e57a70881e35097
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67965222"
---
# <a name="setpermissions-method-adox"></a>Método SetPermissions (ADOX)
Especifica as permissões para um [grupo](../../../ado/reference/adox-api/group-object-adox.md) ou [usuário](../../../ado/reference/adox-api/user-object-adox.md) em um objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
GroupOrUser.SetPermissions Name, ObjectType, Action, Rights [, Inherit] [, ObjectTypeId]  
```  
  
#### <a name="parameters"></a>parâmetros  
 *Nome*  
 Um valor de **cadeia de caracteres** que especifica o nome do objeto para o qual definir permissões.  
  
 *ObjectType*  
 Um valor **longo** que pode ser uma das constantes [ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md) , que especifica o tipo do objeto para o qual obter permissões.  
  
 *Ação*  
 Um valor **longo** que pode ser uma das constantes [ActionEnum](../../../ado/reference/adox-api/actionenum.md) que especifica o tipo de ação a ser executada ao definir permissões.  
  
 *Privilégios*  
 Um valor **longo** que pode ser um bitmask de uma ou mais constantes [RightsEnum](../../../ado/reference/adox-api/rightsenum.md) , que indica os direitos a serem definidos.  
  
 *Herd*  
 Opcional. Um valor **longo** que pode ser uma das constantes [InheritTypeEnum](../../../ado/reference/adox-api/inherittypeenum.md) , que especifica como os objetos herdarão essas permissões. O valor padrão é **adInheritNone**.  
  
 *Objecttypeid*  
 Opcional. Um valor **Variant** que especifica o GUID para um tipo de objeto de provedor que não é definido pela especificação de OLE DB. Esse parâmetro será necessário se *objecttype* for definido como **adPermObjProviderSpecific**; caso contrário, ele não será usado.  
  
## <a name="remarks"></a>Comentários  
 Ocorrerá um erro se o provedor não der suporte à configuração de direitos de acesso para grupos ou usuários.  
  
> [!NOTE]
>  Ao chamar **SetPermissions**, a configuração de ações para **adAccessRevoke** substitui as configurações do parâmetro de *direitos* . Não defina *ações* para **adAccessRevoke** se desejar que os direitos especificados no parâmetro *Rights* tenham efeito.  
  
## <a name="applies-to"></a>Aplica-se A  
  
|||  
|-|-|  
|[Objeto Group (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[Objeto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos getPermissions e SetPermissions (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Método getPermissions (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)   
 [Propriedade Name (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)
