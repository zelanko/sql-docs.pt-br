---
title: Coleção Users (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8dc465261748c1efd340e78ddc2f3e12d601e931
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47678564"
---
# <a name="users-collection-adox"></a>Coleção Users (ADOX)
Contém todos os armazenados [usuário](../../../ado/reference/adox-api/user-object-adox.md) objetos de uma [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) ou [grupo](../../../ado/reference/adox-api/group-object-adox.md).  
  
## <a name="remarks"></a>Comentários  
 O **os usuários** coleção de uma [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) representa usuários de todos os do catálogo. O **os usuários** coleção para uma [grupo](../../../ado/reference/adox-api/group-object-adox.md) representa apenas os usuários que têm uma associação no grupo específico.  
  
 O [Append](../../../ado/reference/adox-api/append-method-adox-users.md) método para um **usuários** coleção é exclusiva para ADOX. Você pode:  
  
-   Adicionar um novo usuário à coleção usando o **Append** método.  
  
 As propriedades e os métodos restantes são padrão para coleções do ADO. Você pode:  
  
-   Acesso de um usuário na coleção com o [Item](../../../ado/reference/ado-api/item-property-ado.md) propriedade.  
  
-   Retornar o número de usuários que estão contidos na coleção com o [contagem](../../../ado/reference/ado-api/count-property-ado.md) propriedade.  
  
-   Remover um usuário da coleção com o [excluir](../../../ado/reference/adox-api/delete-method-adox-collections.md) método.  
  
-   Atualizar os objetos na coleção para refletir o esquema do banco de dados atual com o [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) método.  
  
> [!NOTE]
>  Antes de acrescentar uma **usuário** do objeto para o **usuários** coleção de um **grupo** objeto, um **usuário** objeto com o mesmo [nome ](../../../ado/reference/adox-api/name-property-adox.md) como aquela a ser acrescentado já deve existir na **os usuários** coleção dos **catálogo**.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos da coleção Users](../../../ado/reference/adox-api/users-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [GetPermissions e SetPermissions métodos (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Objeto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Objeto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)
