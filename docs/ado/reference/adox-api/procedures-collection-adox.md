---
description: Coleção Procedures (ADOX)
title: Coleção de procedimentos (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: 97421c9020750627dcd27f6188ae5cda72a2d90c
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769623"
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