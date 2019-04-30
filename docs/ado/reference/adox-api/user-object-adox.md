---
title: Objeto User (ADOX) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3acdea5ae284b2e9a0ac9c28fe8430a11de8fbd4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63281574"
---
# <a name="user-object-adox"></a>Objeto User (ADOX)
Representa uma conta de usuário que tenha permissões de acesso dentro de um banco de dados protegido.  
  
## <a name="remarks"></a>Comentários  
 O [os usuários](../../../ado/reference/adox-api/users-collection-adox.md) coleção de uma [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) representa usuários de todos os do catálogo. O **os usuários** coleção para uma [grupo](../../../ado/reference/adox-api/group-object-adox.md) representa apenas os usuários do grupo específico.  
  
 Com as propriedades, coleções e métodos de um **usuário** do objeto, você pode:  
  
-   Identificar o usuário com o [nome](../../../ado/reference/adox-api/name-property-adox.md) propriedade.  
  
-   Alterar a senha para um usuário com o [ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md) método.  
  
-   Determinar se um usuário tem ler, gravar ou excluir as permissões com o [GetPermissions](../../../ado/reference/adox-api/getpermissions-method-adox.md) e [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md) métodos.  
  
-   Acessar os grupos aos quais um usuário pertence com o [grupos](../../../ado/reference/adox-api/groups-collection-adox.md) coleção.  
  
-   Acessar propriedades específicas do provedor com o [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção.  
  
-   Determinar a [ParentCatalog](../../../ado/reference/adox-api/parentcatalog-property-adox.md) para um usuário.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto User](../../../ado/reference/adox-api/user-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [GetPermissions e SetPermissions métodos (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Coleção Groups (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [Coleção Users (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)
