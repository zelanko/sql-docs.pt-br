---
description: Coleção Users (ADOX)
title: Coleção Users (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Group::Users
- Users
- Catalog::Users
helpviewer_keywords:
- Users collection [ADOX]
ms.assetid: 0a30fa74-6f10-4410-bd70-882e7c43cd46
author: rothja
ms.author: jroth
ms.openlocfilehash: a1f511e637696e5b14905bcccba50cb13737d6e7
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983027"
---
# <a name="users-collection-adox"></a>Coleção Users (ADOX)
Contém todos os objetos de [usuário](./user-object-adox.md) armazenados de um [Catálogo](./catalog-object-adox.md) ou [grupo](./group-object-adox.md).  
  
## <a name="remarks"></a>Comentários  
 A coleção de **usuários** de um [Catálogo](./catalog-object-adox.md) representa todos os usuários do catálogo. A coleção de **usuários** para um [grupo](./group-object-adox.md) representa apenas os usuários que têm uma associação no grupo específico.  
  
 O método [Append](./append-method-adox-users.md) para uma coleção de **usuários** é exclusivo para o ADOX. Você pode:  
  
-   Adicione um novo usuário à coleção usando o método **Append** .  
  
 As propriedades e os métodos restantes são standard para coleções de ADO. Você pode:  
  
-   Acesse um usuário na coleção com a propriedade [Item](../ado-api/item-property-ado.md) .  
  
-   Retorna o número de usuários contidos na coleção com a propriedade [Count](../ado-api/count-property-ado.md) .  
  
-   Remova um usuário da coleção com o método [delete](./delete-method-adox-collections.md) .  
  
-   Atualize os objetos na coleção para refletir o esquema do banco de dados atual com o método [Refresh](../ado-api/refresh-method-ado.md) .  
  
> [!NOTE]
>  Antes de acrescentar um objeto de **usuário** à coleção de **usuários** de um objeto de **grupo** , um objeto de **usuário** com o mesmo [nome](./name-property-adox.md) que aquele a ser anexado já deve existir na coleção de **usuários** do **Catálogo**.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos da coleção Users](./users-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos getPermissions e SetPermissions (VB)](./getpermissions-and-setpermissions-methods-example-vb.md)   
 [Objeto de catálogo (ADOX)](./catalog-object-adox.md)   
 [Objeto User (ADOX)](./user-object-adox.md)