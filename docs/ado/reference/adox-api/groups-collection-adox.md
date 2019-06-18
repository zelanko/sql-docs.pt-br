---
title: Grupos de coleção (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Groups
- User::Groups
- Catalog::Groups
helpviewer_keywords:
- Groups collection [ADOX]
ms.assetid: 09aa7b0a-69d5-4564-80a7-20ad8189670f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5e0fe23c41f6a22a05e6a4c1d61f94a357f3c28c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66706673"
---
# <a name="groups-collection-adox"></a>Coleção Groups (ADOX)
Contém todos os armazenados [grupo](../../../ado/reference/adox-api/group-object-adox.md) objetos de um catálogo ou do usuário.  
  
## <a name="remarks"></a>Comentários  
 O **grupos** coleção de uma [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) representa todas as contas de grupo do catálogo. O **grupos** coleção para uma [usuário](../../../ado/reference/adox-api/user-object-adox.md) representa somente o grupo ao qual o usuário pertence.  
  
 O [Append](../../../ado/reference/adox-api/append-method-adox-groups.md) método para um **grupos** coleção é exclusiva para ADOX. Você pode:  
  
-   Adicionar um novo grupo de segurança à coleção com o **Append** método.  
  
 As propriedades e os métodos restantes são padrão para coleções do ADO. Você pode:  
  
-   Acessar um grupo na coleção com o [Item](../../../ado/reference/ado-api/item-property-ado.md) propriedade.  
  
-   Retornar o número de grupos contidos na coleção com o [contagem](../../../ado/reference/ado-api/count-property-ado.md) propriedade.  
  
-   Remover um grupo de coleção com o [excluir](../../../ado/reference/adox-api/delete-method-adox-collections.md) método.  
  
-   Atualizar os objetos na coleção para refletir o esquema de banco de dados atual com o [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) método.  
  
> [!NOTE]
>  Antes de acrescentar uma **grupo** do objeto para o **grupos** coleção de um **usuário** objeto, um **grupo** objeto com o mesmo [ Nome da](../../../ado/reference/adox-api/name-property-adox.md) como aquela a ser acrescentado já deve existir na **grupos** coleção da **catálogo**.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos da coleção Groups](../../../ado/reference/adox-api/groups-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Objeto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Objeto Group (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)
