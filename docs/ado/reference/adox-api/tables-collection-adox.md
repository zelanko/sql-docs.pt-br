---
title: Tabelas de coleção (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Catalog::Tables
- Tables
helpviewer_keywords:
- Tables collection [ADOX]
ms.assetid: 38d750e7-f3fb-426e-b4b4-55eea4f1a654
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1ba06c10b3f890f08abac371346c3d03a0278aa8
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66705729"
---
# <a name="tables-collection-adox"></a>Coleção Tables (ADOX)
Contém todos os [tabela](../../../ado/reference/adox-api/table-object-adox.md) objetos de um catálogo.  
  
## <a name="remarks"></a>Comentários  
 O [Append](../../../ado/reference/adox-api/append-method-adox-tables.md) método para um **tabelas** coleção é exclusiva para ADOX. Você pode:  
  
-   Adicionar uma nova tabela à coleção com o **Append** método.  
  
 As propriedades e os métodos restantes são padrão para coleções do ADO. Você pode:  
  
-   Acesso a uma tabela na coleção com o [Item](../../../ado/reference/ado-api/item-property-ado.md) propriedade.  
  
-   Retornar o número de tabelas contidas na coleção com o [contagem](../../../ado/reference/ado-api/count-property-ado.md) propriedade.  
  
-   Remover uma tabela da coleção com o [excluir](../../../ado/reference/adox-api/delete-method-adox-collections.md) método.  
  
-   Atualizar os objetos na coleção para refletir o esquema de banco de dados atual com o [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) método.  
  
 Alguns provedores podem retornar outros objetos de esquema, como um modo de exibição na **tabelas** coleção. Portanto, algumas coleções ADOX podem conter várias referências ao mesmo objeto. Você deve excluir o objeto de uma coleção, a alteração não será visível em outra coleção que faz referência ao objeto excluído até que o **Refresh** método é chamado na coleção. Por exemplo, com o OLE DB Provider para Microsoft Jet, as exibições são retornadas com o **tabelas** coleção. Se você soltar um modo de exibição, você deve atualizar o **tabelas** coleção antes que a coleção refletirão a alteração.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos da coleção Tables](../../../ado/reference/adox-api/tables-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo da propriedade ActiveConnection de catálogo (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Columns and Tables Append métodos, exemplo da propriedade Name (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Método Close da Conexão, exemplo da propriedade Table Type (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Chaves de acrescentar o método, tipo de chave, RelatedColumn, RelatedTable e exemplo das propriedades UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Objeto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Objeto Table (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)
