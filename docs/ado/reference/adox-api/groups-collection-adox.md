---
title: Coleção groups (ADOX) | Microsoft Docs
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
ms.openlocfilehash: e39be3cf32f04a60e554928f66cdc6123322f19c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67966181"
---
# <a name="groups-collection-adox"></a>Coleção Groups (ADOX)
Contém todos os objetos de [grupo](../../../ado/reference/adox-api/group-object-adox.md) armazenados de um catálogo ou usuário.  
  
## <a name="remarks"></a>Comentários  
 A coleção de **grupos** de um [Catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) representa todas as contas de grupo do catálogo. A coleção de **grupos** de um [usuário](../../../ado/reference/adox-api/user-object-adox.md) representa apenas o grupo ao qual o usuário pertence.  
  
 O método [Append](../../../ado/reference/adox-api/append-method-adox-groups.md) para uma coleção de **grupos** é exclusivo para o ADOX. Você pode:  
  
-   Adicione um novo grupo de segurança à coleção com o método **Append** .  
  
 As propriedades e os métodos restantes são standard para coleções de ADO. Você pode:  
  
-   Acesse um grupo na coleção com a propriedade [Item](../../../ado/reference/ado-api/item-property-ado.md) .  
  
-   Retorna o número de grupos contidos na coleção com a propriedade [Count](../../../ado/reference/ado-api/count-property-ado.md) .  
  
-   Remova um grupo da coleção com o método [delete](../../../ado/reference/adox-api/delete-method-adox-collections.md) .  
  
-   Atualize os objetos na coleção para refletir o esquema de banco de dados atual com o método de [atualização](../../../ado/reference/ado-api/refresh-method-ado.md) .  
  
> [!NOTE]
>  Antes de acrescentar um objeto de **grupo** à coleção de **grupos** de um objeto de **usuário** , um objeto de **grupo** com o mesmo [nome](../../../ado/reference/adox-api/name-property-adox.md) que aquele a ser anexado já deve existir na coleção de **grupos** do **Catálogo**.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos da coleção Groups](../../../ado/reference/adox-api/groups-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto de catálogo (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Objeto Group (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)
