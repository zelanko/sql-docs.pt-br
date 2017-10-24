---
title: "Tabelas de coleção (ADOX) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Catalog::Tables
- Tables
helpviewer_keywords:
- Tables collection [ADOX]
ms.assetid: 38d750e7-f3fb-426e-b4b4-55eea4f1a654
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1489bb1716cb29116e385158e6f05dcc3d028431
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="tables-collection-adox"></a>Coleção de tabelas (ADOX)
Contém todos os [tabela](../../../ado/reference/adox-api/table-object-adox.md) objetos de um catálogo.  
  
## <a name="remarks"></a>Comentários  
 O [Append](../../../ado/reference/adox-api/append-method-adox-tables.md) método para um **tabelas** coleção é exclusiva para ADOX. Você pode:  
  
-   Adicionar uma nova tabela à coleção com o **Append** método.  
  
 As propriedades e os métodos restantes são padrão para coleções de ADO. Você pode:  
  
-   Acesso a uma tabela na coleção com o [Item](../../../ado/reference/ado-api/item-property-ado.md) propriedade.  
  
-   Retorna o número de tabelas contidas na coleção com o [contagem](../../../ado/reference/ado-api/count-property-ado.md) propriedade.  
  
-   Remover uma tabela da coleção com o [excluir](../../../ado/reference/adox-api/delete-method-adox-collections.md) método.  
  
-   Atualizar os objetos na coleção para refletir o esquema de banco de dados atual com o [atualização](../../../ado/reference/ado-api/refresh-method-ado.md) método.  
  
 Alguns provedores podem retornar outros objetos de esquema, como um modo de exibição no **tabelas** coleção. Portanto, algumas coleções ADOX podem conter várias referências ao mesmo objeto. Você deve excluir o objeto de uma coleção, a alteração não será visível em outra coleção que faz referência ao objeto excluído até que o **atualização** método é chamado na coleção. Por exemplo, com o OLE DB Provider for Microsoft Jet, modos de exibição são retornados com o **tabelas** coleção. Se você remover um modo de exibição, você deve atualizar o **tabelas** coleção antes da coleção refletirão a alteração.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos da coleção Tables](../../../ado/reference/adox-api/tables-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de propriedade ActiveConnection do catálogo (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Tabelas e colunas acrescentar métodos, exemplo de nome de propriedade (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Método Close da Conexão, exemplo de propriedade de tipo de tabela (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Chaves de acrescentar o método, tipo de chave, RelatedColumn, RelatedTable e exemplo de propriedades de UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Objeto de catálogo (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Objeto Table (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)

