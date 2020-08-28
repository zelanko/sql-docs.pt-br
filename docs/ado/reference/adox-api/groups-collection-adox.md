---
description: Coleção Groups (ADOX)
title: Coleção groups (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 9624a30970e5a6f6a0186d2cb9e2390c98968d9e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984367"
---
# <a name="groups-collection-adox"></a>Coleção Groups (ADOX)
Contém todos os objetos de [grupo](./group-object-adox.md) armazenados de um catálogo ou usuário.  
  
## <a name="remarks"></a>Comentários  
 A coleção de **grupos** de um [Catálogo](./catalog-object-adox.md) representa todas as contas de grupo do catálogo. A coleção de **grupos** de um [usuário](./user-object-adox.md) representa apenas o grupo ao qual o usuário pertence.  
  
 O método [Append](./append-method-adox-groups.md) para uma coleção de **grupos** é exclusivo para o ADOX. Você pode:  
  
-   Adicione um novo grupo de segurança à coleção com o método **Append** .  
  
 As propriedades e os métodos restantes são standard para coleções de ADO. Você pode:  
  
-   Acesse um grupo na coleção com a propriedade [Item](../ado-api/item-property-ado.md) .  
  
-   Retorna o número de grupos contidos na coleção com a propriedade [Count](../ado-api/count-property-ado.md) .  
  
-   Remova um grupo da coleção com o método [delete](./delete-method-adox-collections.md) .  
  
-   Atualize os objetos na coleção para refletir o esquema de banco de dados atual com o método de [atualização](../ado-api/refresh-method-ado.md) .  
  
> [!NOTE]
>  Antes de acrescentar um objeto de **grupo** à coleção de **grupos** de um objeto de **usuário** , um objeto de **grupo** com o mesmo [nome](./name-property-adox.md) que aquele a ser anexado já deve existir na coleção de **grupos** do **Catálogo**.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos da coleção Groups](./groups-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto de catálogo (ADOX)](./catalog-object-adox.md)   
 [Objeto Group (ADOX)](./group-object-adox.md)