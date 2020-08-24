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
ms.openlocfilehash: 0442ca3bd785269fed49dc86d982971a8feec4ea
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770415"
---
# <a name="group-object-adox"></a>Objeto Group (ADOX)
Representa uma conta de grupo que tem permissões de acesso em um banco de dados protegido.  
  
## <a name="remarks"></a>Comentários  
 A coleção de [grupos](./groups-collection-adox.md) de um [Catálogo](./catalog-object-adox.md) representa todas as contas de grupo do catálogo. A coleção de **grupos** de um [usuário](./user-object-adox.md) representa apenas o grupo ao qual o usuário pertence.  
  
 Com as propriedades, coleções e métodos de um objeto de **grupo** , você pode:  
  
-   Identifique o grupo com a propriedade [Name](./name-property-adox.md) .  
  
-   Determine se um grupo tem permissões de leitura, gravação ou exclusão com os métodos [getPermissions](./getpermissions-method-adox.md) e [SetPermissions](./setpermissions-method-adox.md) .  
  
-   Acesse as contas de usuário que têm associações no grupo com a coleção de [usuários](./users-collection-adox.md) .  
  
-   Acesse propriedades específicas do provedor com a coleção [Properties](../ado-api/properties-collection-ado.md) .  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto Group](./group-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Coleção groups (ADOX)](./groups-collection-adox.md)   
 [Coleção Users (ADOX)](./users-collection-adox.md)