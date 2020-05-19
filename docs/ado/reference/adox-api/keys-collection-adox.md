---
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
ms.openlocfilehash: 1a7bebc1c05ab195d3b23c5c0894d4fcce967625
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82746547"
---
# <a name="keys-collection-adox"></a>Coleção Keys (ADOX)
Contém todos os objetos de [chave](../../../ado/reference/adox-api/key-object-adox.md) de uma [tabela](../../../ado/reference/adox-api/table-object-adox.md).  
  
## <a name="remarks"></a>Comentários  
 O método [Append](../../../ado/reference/adox-api/append-method-adox-keys.md) para uma [coleção de chaves](../../../ado/reference/adox-api/keys-collection-adox.md) é exclusivo para o ADOX. Você pode:  
  
-   Adicione uma nova chave à coleção com o método [Append](../../../ado/reference/adox-api/append-method-adox-keys.md) .  
  
 As propriedades e os métodos restantes são standard para coleções de ADO. Você pode:  
  
-   Acesse uma chave na coleção com a propriedade [Item](../../../ado/reference/ado-api/item-property-ado.md) .  
  
-   Retorna o número de chaves contidas na coleção com a propriedade [Count](../../../ado/reference/ado-api/count-property-ado.md) .  
  
-   Remova uma chave da coleção com o método [delete](../../../ado/reference/adox-api/delete-method-adox-collections.md) .  
  
-   Atualize os objetos na coleção para refletir o esquema do banco de dados atual com o método [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) .  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos da coleção Indexes](../../../ado/reference/adox-api/indexes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades método, tipo de chave, RelatedColumn, RELATEDTABLE e UpdateRule da tecla Append (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Propriedades, métodos e eventos da coleção Keys](../../../ado/reference/adox-api/keys-collection-properties-methods-and-events.md)   
 [Objeto Key (ADOX)](../../../ado/reference/adox-api/key-object-adox.md)
