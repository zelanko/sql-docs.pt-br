---
title: Objeto user (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- User
helpviewer_keywords:
- User object [ADOX]
ms.assetid: f68e32ce-ef7c-407d-bdb5-d280947ae0e2
author: rothja
ms.author: jroth
ms.openlocfilehash: 55315ab64f87c6aba1c988c752c4e21811fef35c
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762707"
---
# <a name="user-object-adox"></a>Objeto User (ADOX)
Representa uma conta de usuário que tem permissões de acesso em um banco de dados protegido.  
  
## <a name="remarks"></a>Comentários  
 A coleção de [usuários](../../../ado/reference/adox-api/users-collection-adox.md) de um [Catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) representa todos os usuários do catálogo. A coleção de **usuários** para um [grupo](../../../ado/reference/adox-api/group-object-adox.md) representa apenas os usuários do grupo específico.  
  
 Com as propriedades, coleções e métodos de um objeto de **usuário** , você pode:  
  
-   Identifique o usuário com a propriedade [Name](../../../ado/reference/adox-api/name-property-adox.md) .  
  
-   Altere a senha de um usuário com o método [ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md) .  
  
-   Determine se um usuário tem permissões de leitura, gravação ou exclusão com os métodos [getPermissions](../../../ado/reference/adox-api/getpermissions-method-adox.md) e [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md) .  
  
-   Acesse os grupos aos quais um usuário pertence à coleção de [grupos](../../../ado/reference/adox-api/groups-collection-adox.md) .  
  
-   Acesse propriedades específicas do provedor com a coleção [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) .  
  
-   Determinar o [ParentCatalog](../../../ado/reference/adox-api/parentcatalog-property-adox.md) para um usuário.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto User](../../../ado/reference/adox-api/user-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos getPermissions e SetPermissions (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Coleção groups (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [Coleção Users (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)
