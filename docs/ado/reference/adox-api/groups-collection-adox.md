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
manager: craigg
ms.openlocfilehash: e6b8aea077af67c882830220da9ce24b802e25e5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47801425"
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
