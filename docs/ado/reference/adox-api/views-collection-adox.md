---
description: Coleção Views (ADOX)
title: Coleção views (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Catalog::Views
- Views
helpviewer_keywords:
- Views collection [ADOX]
ms.assetid: a55d380c-2b7b-4b57-af74-8ba0b3de0db9
author: rothja
ms.author: jroth
ms.openlocfilehash: 26d61c1d2835d9dcabba82beb2a120330f8f2ead
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88982867"
---
# <a name="views-collection-adox"></a>Coleção Views (ADOX)
Contém todos os objetos de [exibição](./view-object-adox.md) de um catálogo.  
  
## <a name="remarks"></a>Comentários  
 O método [Append](./append-method-adox-views.md) para uma coleção **views** é exclusivo para o ADOX. Você pode:  
  
-   Adicione uma nova exibição à coleção com o método **Append** .  
  
 As propriedades e os métodos restantes são standard para coleções de ADO. Você pode:  
  
-   Acesse uma exibição na coleção com a propriedade [Item](../ado-api/item-property-ado.md) .  
  
-   Retorna o número de exibições contidas na coleção com a propriedade [Count](../ado-api/count-property-ado.md) .  
  
-   Remova uma exibição da coleção com o método [delete](./delete-method-adox-collections.md) .  
  
-   Atualize os objetos na coleção para refletir o esquema de banco de dados atual com o método de [atualização](../ado-api/refresh-method-ado.md) .  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos da coleção Views](./views-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de coleções de exibições e campos (VB)](./views-and-fields-collections-example-vb.md)   
 [Exemplo do método Append views (VB)](./views-append-method-example-vb.md)   
 [Coleção views, exemplo da propriedade CommandText (VB)](./views-collection-commandtext-property-example-vb.md)   
 [Exemplo do método Delete de views (VB)](./views-delete-method-example-vb.md)   
 [Exemplo do método Refresh de exibições (VB)](./views-refresh-method-example-vb.md)   
 [Objeto de catálogo (ADOX)](./catalog-object-adox.md)   
 [Objeto View (ADOX)](./view-object-adox.md)