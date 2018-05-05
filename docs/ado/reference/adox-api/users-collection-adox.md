---
title: Coleção de usuários (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Group::Users
- Users
- Catalog::Users
helpviewer_keywords:
- Users collection [ADOX]
ms.assetid: 0a30fa74-6f10-4410-bd70-882e7c43cd46
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1a9b34813f614248669b77113491c9383ef477a3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="users-collection-adox"></a>Coleção de usuários (ADOX)
Contém todos os armazenados [usuário](../../../ado/reference/adox-api/user-object-adox.md) objetos de um [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) ou [grupo](../../../ado/reference/adox-api/group-object-adox.md).  
  
## <a name="remarks"></a>Remarks  
 O **usuários** coleção de um [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) representa usuários todos do catálogo. O **usuários** coleção para um [grupo](../../../ado/reference/adox-api/group-object-adox.md) representa apenas os usuários que têm uma associação no grupo específico.  
  
 O [Append](../../../ado/reference/adox-api/append-method-adox-users.md) método para um **usuários** coleção é exclusiva para ADOX. Você pode:  
  
-   Adicionar um novo usuário à coleção usando o **Append** método.  
  
 As propriedades e os métodos restantes são padrão para coleções de ADO. Você pode:  
  
-   Acesso de um usuário na coleção com o [Item](../../../ado/reference/ado-api/item-property-ado.md) propriedade.  
  
-   Retorna o número de usuários que estão contidos na coleção com o [contagem](../../../ado/reference/ado-api/count-property-ado.md) propriedade.  
  
-   Remover um usuário da coleção com o [excluir](../../../ado/reference/adox-api/delete-method-adox-collections.md) método.  
  
-   Atualizar os objetos na coleção para refletir o esquema do banco de dados atual com o [atualização](../../../ado/reference/ado-api/refresh-method-ado.md) método.  
  
> [!NOTE]
>  Antes de anexar um **usuário** o objeto para o **usuários** coleção de um **grupo** objeto, um **usuário** objeto com o mesmo [nome ](../../../ado/reference/adox-api/name-property-adox.md) como um a ser acrescentada já deve existir no **usuários** coleção do **catálogo**.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos da coleção Users](../../../ado/reference/adox-api/users-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de métodos de SetPermissions (VB) e GetPermissions](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Objeto de catálogo (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Objeto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)
