---
description: Objeto User (ADOX)
title: Objeto user (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 6e83bd40c226f1d5b5948c6475b259c799907866
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983043"
---
# <a name="user-object-adox"></a>Objeto User (ADOX)
Representa uma conta de usuário que tem permissões de acesso em um banco de dados protegido.  
  
## <a name="remarks"></a>Comentários  
 A coleção de [usuários](./users-collection-adox.md) de um [Catálogo](./catalog-object-adox.md) representa todos os usuários do catálogo. A coleção de **usuários** para um [grupo](./group-object-adox.md) representa apenas os usuários do grupo específico.  
  
 Com as propriedades, coleções e métodos de um objeto de **usuário** , você pode:  
  
-   Identifique o usuário com a propriedade [Name](./name-property-adox.md) .  
  
-   Altere a senha de um usuário com o método [ChangePassword](./changepassword-method-adox.md) .  
  
-   Determine se um usuário tem permissões de leitura, gravação ou exclusão com os métodos [getPermissions](./getpermissions-method-adox.md) e [SetPermissions](./setpermissions-method-adox.md) .  
  
-   Acesse os grupos aos quais um usuário pertence à coleção de [grupos](./groups-collection-adox.md) .  
  
-   Acesse propriedades específicas do provedor com a coleção [Properties](../ado-api/properties-collection-ado.md) .  
  
-   Determinar o [ParentCatalog](./parentcatalog-property-adox.md) para um usuário.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto User](./user-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos getPermissions e SetPermissions (VB)](./getpermissions-and-setpermissions-methods-example-vb.md)   
 [Coleção groups (ADOX)](./groups-collection-adox.md)   
 [Coleção Users (ADOX)](./users-collection-adox.md)