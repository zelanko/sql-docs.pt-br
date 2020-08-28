---
description: Método SetPermissions (ADOX)
title: Método SetPermissions (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 1333fc42f98ba787cfcc139b40932038307e5592
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983287"
---
# <a name="setpermissions-method-adox"></a>Método SetPermissions (ADOX)
Especifica as permissões para um [grupo](./group-object-adox.md) ou [usuário](./user-object-adox.md) em um objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
GroupOrUser.SetPermissions Name, ObjectType, Action, Rights [, Inherit] [, ObjectTypeId]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Nome*  
 Um valor de **cadeia de caracteres** que especifica o nome do objeto para o qual definir permissões.  
  
 *ObjectType*  
 Um valor **longo** que pode ser uma das constantes [ObjectTypeEnum](./objecttypeenum.md) , que especifica o tipo do objeto para o qual obter permissões.  
  
 *Ação*  
 Um valor **longo** que pode ser uma das constantes [ActionEnum](./actionenum.md) que especifica o tipo de ação a ser executada ao definir permissões.  
  
 *Direitos*  
 Um valor **longo** que pode ser um bitmask de uma ou mais constantes [RightsEnum](./rightsenum.md) , que indica os direitos a serem definidos.  
  
 *Herd*  
 Opcional. Um valor **longo** que pode ser uma das constantes [InheritTypeEnum](./inherittypeenum.md) , que especifica como os objetos herdarão essas permissões. O valor padrão é **adInheritNone**.  
  
 *ObjectTypeId*  
 Opcional. Um valor **Variant** que especifica o GUID para um tipo de objeto de provedor que não é definido pela especificação de OLE DB. Esse parâmetro será necessário se *objecttype* for definido como **adPermObjProviderSpecific**; caso contrário, ele não será usado.  
  
## <a name="remarks"></a>Comentários  
 Ocorrerá um erro se o provedor não der suporte à configuração de direitos de acesso para grupos ou usuários.  
  
> [!NOTE]
>  Ao chamar **SetPermissions**, a configuração de ações para **adAccessRevoke** substitui as configurações do parâmetro de *direitos* . Não defina *ações* para **adAccessRevoke** se desejar que os direitos especificados no parâmetro *Rights* tenham efeito.  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Objeto Group (ADOX)](./group-object-adox.md)  
    :::column-end:::
    :::column:::
        [Objeto User (ADOX)](./user-object-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos getPermissions e SetPermissions (VB)](./getpermissions-and-setpermissions-methods-example-vb.md)   
 [Método getPermissions (ADOX)](./getpermissions-method-adox.md)   
 [Propriedade Name (ADOX)](./name-property-adox.md)