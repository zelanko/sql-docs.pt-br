---
description: Objeto Group (ADOX)
title: Objeto Group (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Group
helpviewer_keywords:
- group object [ADOX]
ms.assetid: 55ef0ade-68ea-4da5-8aa5-4cd27d1f6d1e
author: rothja
ms.author: jroth
ms.openlocfilehash: aeeaf4d849efbfe2549a1c4f20b3689048b43a24
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440008"
---
# <a name="group-object-adox"></a>Objeto Group (ADOX)
Representa uma conta de grupo que tem permissões de acesso em um banco de dados protegido.  
  
## <a name="remarks"></a>Comentários  
 A coleção de [grupos](../../../ado/reference/adox-api/groups-collection-adox.md) de um [Catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) representa todas as contas de grupo do catálogo. A coleção de **grupos** de um [usuário](../../../ado/reference/adox-api/user-object-adox.md) representa apenas o grupo ao qual o usuário pertence.  
  
 Com as propriedades, coleções e métodos de um objeto de **grupo** , você pode:  
  
-   Identifique o grupo com a propriedade [Name](../../../ado/reference/adox-api/name-property-adox.md) .  
  
-   Determine se um grupo tem permissões de leitura, gravação ou exclusão com os métodos [getPermissions](../../../ado/reference/adox-api/getpermissions-method-adox.md) e [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md) .  
  
-   Acesse as contas de usuário que têm associações no grupo com a coleção de [usuários](../../../ado/reference/adox-api/users-collection-adox.md) .  
  
-   Acesse propriedades específicas do provedor com a coleção [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) .  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto Group](../../../ado/reference/adox-api/group-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Coleção groups (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [Coleção Users (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)
