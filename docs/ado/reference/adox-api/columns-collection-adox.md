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
author: rothja
ms.author: jroth
ms.openlocfilehash: 46168e694f87c4a8a827420f8b395b843da1d29b
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759332"
---
# <a name="columns-collection-adox"></a>Coleção Columns (ADOX)
Contém todos os objetos de [coluna](../../../ado/reference/adox-api/column-object-adox.md) de uma tabela, índice ou chave.  
  
## <a name="remarks"></a>Comentários  
 O método [Append](../../../ado/reference/adox-api/append-method-adox-columns.md) para uma coleção **Columns** é exclusivo para o ADOX. Você pode:  
  
-   Adicione uma nova coluna à coleção com o método **Append** .  
  
 As propriedades e os métodos restantes são standard para coleções de ADO. Você pode:  
  
-   Acesse uma coluna na coleção com a propriedade [Item](../../../ado/reference/ado-api/item-property-ado.md) .  
  
-   Retorna o número de colunas contidas na coleção com a propriedade [Count](../../../ado/reference/ado-api/count-property-ado.md) .  
  
-   Remova uma coluna da coleção com o método [delete](../../../ado/reference/adox-api/delete-method-adox-collections.md) .  
  
-   Atualize os objetos na coleção para refletir o esquema do banco de dados atual com o método [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) .  
  
> [!NOTE]
>  Ocorrerá um erro ao acrescentar uma **coluna** à coleção de **colunas** de um [índice](../../../ado/reference/adox-api/index-object-adox.md) se a **coluna** não existir em uma [tabela](../../../ado/reference/adox-api/table-object-adox.md) que já esteja anexada à coleção de [tabelas](../../../ado/reference/adox-api/tables-collection-adox.md) .  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos da coleção Columns](../../../ado/reference/adox-api/columns-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade Name e métodos de acréscimo de colunas e tabelas (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Método Connection Close, exemplo da propriedade de tipo Table (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Exemplo das propriedades método, tipo de chave, RelatedColumn, RELATEDTABLE e UpdateRule da tecla Append (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Exemplo da propriedade ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Exemplo da propriedade SortOrder (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Objeto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)
