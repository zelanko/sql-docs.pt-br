---
title: Chaves de coleção (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Table::Keys
- Keys
helpviewer_keywords:
- Keys collection [ADOX]
ms.assetid: cdb31c76-e559-475c-b33a-aac24f73e70e
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 803c105d0d91a6826a4c8fbf096d059bbf5070d8
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="keys-collection-adox"></a>Coleção de chaves (ADOX)
Contém todos os [chave](../../../ado/reference/adox-api/key-object-adox.md) objetos de um [tabela](../../../ado/reference/adox-api/table-object-adox.md).  
  
## <a name="remarks"></a>Remarks  
 O [Append](../../../ado/reference/adox-api/append-method-adox-keys.md) método para um [chaves coleção](../../../ado/reference/adox-api/keys-collection-adox.md) é exclusivo para ADOX. Você pode:  
  
-   Adicione uma nova chave para a coleção com o [Append](../../../ado/reference/adox-api/append-method-adox-keys.md) método.  
  
 As propriedades e os métodos restantes são padrão para coleções de ADO. Você pode:  
  
-   Acessar uma chave da coleção com o [Item](../../../ado/reference/ado-api/item-property-ado.md) propriedade.  
  
-   Retorna o número de chaves contidas na coleção com o [contagem](../../../ado/reference/ado-api/count-property-ado.md) propriedade.  
  
-   Remover uma chave da coleção com o [excluir](../../../ado/reference/adox-api/delete-method-adox-collections.md) método.  
  
-   Atualizar os objetos na coleção para refletir o esquema do banco de dados atual com o [atualização](../../../ado/reference/ado-api/refresh-method-ado.md) método.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos da coleção Indexes](../../../ado/reference/adox-api/indexes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Chaves de acrescentar o método, tipo de chave, RelatedColumn, RelatedTable e exemplo de propriedades de UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Propriedades de coleção de chaves, métodos e eventos](../../../ado/reference/adox-api/keys-collection-properties-methods-and-events.md)   
 [Objeto Key (ADOX)](../../../ado/reference/adox-api/key-object-adox.md)
