---
description: Coleção Tables (ADOX)
title: Coleção Tables (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 0b6d580dd6f56f78947ff1a881db1bff28c3e2b8
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983257"
---
# <a name="tables-collection-adox"></a>Coleção Tables (ADOX)
Contém todos os objetos de [tabela](./table-object-adox.md) de um catálogo.  
  
## <a name="remarks"></a>Comentários  
 O método [Append](./append-method-adox-tables.md) para uma coleção **Tables** é exclusivo para o ADOX. Você pode:  
  
-   Adicione uma nova tabela à coleção com o método **Append** .  
  
 As propriedades e os métodos restantes são standard para coleções de ADO. Você pode:  
  
-   Acesse uma tabela na coleção com a propriedade [Item](../ado-api/item-property-ado.md) .  
  
-   Retorna o número de tabelas contidas na coleção com a propriedade [Count](../ado-api/count-property-ado.md) .  
  
-   Remova uma tabela da coleção com o método [delete](./delete-method-adox-collections.md) .  
  
-   Atualize os objetos na coleção para refletir o esquema de banco de dados atual com o método de [atualização](../ado-api/refresh-method-ado.md) .  
  
 Alguns provedores podem retornar outros objetos de esquema, como uma exibição, na coleção **Tables** . Portanto, algumas coleções do ADOX podem conter várias referências ao mesmo objeto. Se você excluir o objeto de uma coleção, a alteração não será visível em outra coleção que referencie o objeto excluído até que o método de **atualização** seja chamado na coleção. Por exemplo, com o provedor de OLE DB para Microsoft Jet, as exibições são retornadas com a coleção **Tables** . Se você soltar uma exibição, deverá atualizar a coleção de **tabelas** antes que a coleção reflita a alteração.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos da coleção Tables](./tables-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade ActiveConnection do catálogo (VB)](./catalog-activeconnection-property-example-vb.md)   
 [Exemplo da propriedade Name e métodos de acréscimo de colunas e tabelas (VB)](./columns-and-tables-append-methods-name-property-example-vb.md)   
 [Método Connection Close, exemplo da propriedade de tipo Table (VB)](./connection-close-method-table-type-property-example-vb.md)   
 [Exemplo das propriedades método, tipo de chave, RelatedColumn, RELATEDTABLE e UpdateRule da tecla Append (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Objeto de catálogo (ADOX)](./catalog-object-adox.md)   
 [Objeto Table (ADOX)](./table-object-adox.md)