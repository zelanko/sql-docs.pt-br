---
description: Coleção Indexes (ADOX)
title: Coleção de índices (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Table::Indexes
- Indexes
helpviewer_keywords:
- Indexes collection [ADOX]
ms.assetid: 184cf536-455c-42be-bf1c-a5c25bade961
author: rothja
ms.author: jroth
ms.openlocfilehash: daea070c8bd39d6208404f119578773382078634
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984187"
---
# <a name="indexes-collection-adox"></a>Coleção Indexes (ADOX)
Contém todos os objetos de [índice](./index-object-adox.md) de uma tabela.  
  
## <a name="remarks"></a>Comentários  
 O método [Append](./append-method-adox-indexes.md) para uma coleção de **índices** é exclusivo para o ADOX. Você pode:  
  
-   Adicione um novo índice à coleção com o método **Append** .  
  
 As propriedades e os métodos restantes são standard para coleções de ADO. Você pode:  
  
-   Acesse um índice na coleção com a propriedade [Item](../ado-api/item-property-ado.md) .  
  
-   Retorna o número de índices contidos na coleção com a propriedade [Count](../ado-api/count-property-ado.md) .  
  
-   Remova um índice da coleção com o método [delete](./delete-method-adox-collections.md) .  
  
-   Atualize os objetos na coleção para refletir o esquema de banco de dados atual com o método de [atualização](../ado-api/refresh-method-ado.md) .  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos da coleção Indexes](./indexes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método Indexes Append (VB)](./indexes-append-method-example-vb.md)   
 [Objeto Index (ADOX)](./index-object-adox.md)