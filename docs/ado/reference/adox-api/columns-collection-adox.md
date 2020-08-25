---
description: Coleção Columns (ADOX)
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
ms.openlocfilehash: 4c0e37715077af500e0c5cc023021765a9e4978d
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770975"
---
# <a name="columns-collection-adox"></a>Coleção Columns (ADOX)
Contém todos os objetos de [coluna](./column-object-adox.md) de uma tabela, índice ou chave.  
  
## <a name="remarks"></a>Comentários  
 O método [Append](./append-method-adox-columns.md) para uma coleção **Columns** é exclusivo para o ADOX. Você pode:  
  
-   Adicione uma nova coluna à coleção com o método **Append** .  
  
 As propriedades e os métodos restantes são standard para coleções de ADO. Você pode:  
  
-   Acesse uma coluna na coleção com a propriedade [Item](../ado-api/item-property-ado.md) .  
  
-   Retorna o número de colunas contidas na coleção com a propriedade [Count](../ado-api/count-property-ado.md) .  
  
-   Remova uma coluna da coleção com o método [delete](./delete-method-adox-collections.md) .  
  
-   Atualize os objetos na coleção para refletir o esquema do banco de dados atual com o método [Refresh](../ado-api/refresh-method-ado.md) .  
  
> [!NOTE]
>  Ocorrerá um erro ao acrescentar uma **coluna** à coleção de **colunas** de um [índice](./index-object-adox.md) se a **coluna** não existir em uma [tabela](./table-object-adox.md) que já esteja anexada à coleção de [tabelas](./tables-collection-adox.md) .  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos da coleção Columns](./columns-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade Name e métodos de acréscimo de colunas e tabelas (VB)](./columns-and-tables-append-methods-name-property-example-vb.md)   
 [Método Connection Close, exemplo da propriedade de tipo Table (VB)](./connection-close-method-table-type-property-example-vb.md)   
 [Exemplo das propriedades método, tipo de chave, RelatedColumn, RELATEDTABLE e UpdateRule da tecla Append (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Exemplo da propriedade ParentCatalog (VB)](./parentcatalog-property-example-vb.md)   
 [Exemplo da propriedade SortOrder (VB)](./sortorder-property-example-vb.md)   
 [Objeto Column (ADOX)](./column-object-adox.md)