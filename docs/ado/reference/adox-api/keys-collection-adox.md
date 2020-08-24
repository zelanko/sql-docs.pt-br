---
description: Coleção Keys (ADOX)
title: Coleção Keys (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Table::Keys
- Keys
helpviewer_keywords:
- Keys collection [ADOX]
ms.assetid: cdb31c76-e559-475c-b33a-aac24f73e70e
author: rothja
ms.author: jroth
ms.openlocfilehash: 95d1b5b927f03a0592f25cc4cc79c0ffe78cee74
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770055"
---
# <a name="keys-collection-adox"></a>Coleção Keys (ADOX)
Contém todos os objetos de [chave](./key-object-adox.md) de uma [tabela](./table-object-adox.md).  
  
## <a name="remarks"></a>Comentários  
 O método [Append](./append-method-adox-keys.md) para uma [coleção de chaves]() é exclusivo para o ADOX. Você pode:  
  
-   Adicione uma nova chave à coleção com o método [Append](./append-method-adox-keys.md) .  
  
 As propriedades e os métodos restantes são standard para coleções de ADO. Você pode:  
  
-   Acesse uma chave na coleção com a propriedade [Item](../ado-api/item-property-ado.md) .  
  
-   Retorna o número de chaves contidas na coleção com a propriedade [Count](../ado-api/count-property-ado.md) .  
  
-   Remova uma chave da coleção com o método [delete](./delete-method-adox-collections.md) .  
  
-   Atualize os objetos na coleção para refletir o esquema do banco de dados atual com o método [Refresh](../ado-api/refresh-method-ado.md) .  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos da coleção Indexes](./indexes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades método, tipo de chave, RelatedColumn, RELATEDTABLE e UpdateRule da tecla Append (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Propriedades, métodos e eventos da coleção Keys](./keys-collection-properties-methods-and-events.md)   
 [Objeto Key (ADOX)](./key-object-adox.md)