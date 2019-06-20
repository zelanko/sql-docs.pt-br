---
title: Coleção Columns (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Index::Columns
- Table::Columns
- Key::Columns
- Columns
helpviewer_keywords:
- Columns collection [ADOX]
ms.assetid: 23b9fea8-4f76-4a51-95ce-1a6ce4560b34
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 4bdb60a6d174ab82df7529b6e26d8d5b2c031107
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66703953"
---
# <a name="columns-collection-adox"></a>Coleção Columns (ADOX)
Contém todos os [coluna](../../../ado/reference/adox-api/column-object-adox.md) objetos de uma tabela, índice ou chave.  
  
## <a name="remarks"></a>Comentários  
 O [Append](../../../ado/reference/adox-api/append-method-adox-columns.md) método para um **colunas** coleção é exclusiva para ADOX. Você pode:  
  
-   Adicionar uma nova coluna à coleção com o **Append** método.  
  
 As propriedades e os métodos restantes são padrão para coleções do ADO. Você pode:  
  
-   Acessar uma coluna na coleção com o [Item](../../../ado/reference/ado-api/item-property-ado.md) propriedade.  
  
-   Retornar o número de colunas contidas na coleção com o [contagem](../../../ado/reference/ado-api/count-property-ado.md) propriedade.  
  
-   Remover uma coluna da coleção com o [excluir](../../../ado/reference/adox-api/delete-method-adox-collections.md) método.  
  
-   Atualizar os objetos na coleção para refletir o esquema do banco de dados atual com o [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) método.  
  
> [!NOTE]
>  Ocorrerá um erro ao anexar um **coluna** para o **colunas** coleção de um [índice](../../../ado/reference/adox-api/index-object-adox.md) se o **coluna** não existe em um [Tabela](../../../ado/reference/adox-api/table-object-adox.md) que já é acrescentado para o [tabelas](../../../ado/reference/adox-api/tables-collection-adox.md) coleção.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos da coleção Columns](../../../ado/reference/adox-api/columns-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Columns and Tables Append métodos, exemplo da propriedade Name (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Método Close da Conexão, exemplo da propriedade Table Type (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Chaves de acrescentar o método, tipo de chave, RelatedColumn, RelatedTable e exemplo das propriedades UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Exemplo da propriedade ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Exemplo da propriedade SortOrder (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Objeto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)
