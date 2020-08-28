---
description: Coleção Procedures (ADOX)
title: Coleção de procedimentos (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Procedures
- Catalog::Procedures
helpviewer_keywords:
- Procedures collection [ADOX]
ms.assetid: dc7a38e1-93b9-4034-9af2-ff419e8fb2a3
author: rothja
ms.author: jroth
ms.openlocfilehash: b3f98420fc85cabd2ccc584817ac6ca9a9203081
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983567"
---
# <a name="procedures-collection-adox"></a>Coleção Procedures (ADOX)
Contém todos os objetos de [procedimento](./procedure-object-adox.md) de um catálogo.  
  
## <a name="remarks"></a>Comentários  
 O método [Append](./append-method-adox-procedures.md) para uma coleção de **procedimentos** é exclusivo para o ADOX. Você pode:  
  
-   Adicione um novo procedimento à coleção com o método **Append** .  
  
 As propriedades e os métodos restantes são standard para coleções de ADO. Você pode:  
  
-   Acesse um procedimento na coleção com a propriedade [Item](../ado-api/item-property-ado.md) .  
  
-   Retorna o número de procedimentos contidos na coleção com a propriedade [Count](../ado-api/count-property-ado.md) .  
  
-   Remova um procedimento da coleção com o método [delete](./delete-method-adox-collections.md) .  
  
-   Atualize os objetos na coleção para refletir o esquema de banco de dados atual com o método de [atualização](../ado-api/refresh-method-ado.md) .  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos da coleção Indexes](./indexes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades Command e CommandText (VB)](./command-and-commandtext-properties-example-vb.md)   
 [Coleção Parameters, exemplo da Propriedade Command (VB)](./parameters-collection-command-property-example-vb.md)   
 [Exemplo do método Append Procedures (VB)](./procedures-append-method-example-vb.md)   
 [Exemplo do método Delete de procedimentos (VB)](./procedures-delete-method-example-vb.md)   
 [Exemplo do método Refresh de procedimentos (VB)](./procedures-refresh-method-example-vb.md)   
 [Propriedades, métodos e eventos da coleção procedures](./procedures-collection-properties-methods-and-events.md)   
 [Objeto de catálogo (ADOX)](./catalog-object-adox.md)   
 [Objeto Procedure (ADOX)](./procedure-object-adox.md)