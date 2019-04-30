---
title: Tabela de objeto (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Table
helpviewer_keywords:
- Table object [ADOX]
ms.assetid: a6d74000-0828-49ba-850a-63da865f8802
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f5af59dbc50f6e1a2cd95cbdf99874d860eceeb1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63281598"
---
# <a name="table-object-adox"></a>Objeto Table (ADOX)
Representa uma tabela de banco de dados, incluindo colunas, índices e chaves.  
  
## <a name="remarks"></a>Comentários  
 O código a seguir cria um novo **tabela**:  
  
```  
Dim obj As New Table  
```  
  
 Com as propriedades e coleções de uma **tabela** do objeto, você pode:  
  
-   Identifique a tabela com o [nome da propriedade (ADOX)](../../../ado/reference/adox-api/name-property-adox.md) propriedade.  
  
-   Determinar o tipo de tabela com o [propriedade Type (Table) (ADOX)](../../../ado/reference/adox-api/type-property-table-adox.md) propriedade.  
  
-   Acessar as colunas de banco de dados da tabela com o [coleção de colunas (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md) coleção.  
  
-   Acessar os índices da tabela com o [coleção de índices (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md).  
  
-   Acessar as chaves da tabela com o [coleção de chaves (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md).  
  
-   Especifique o catálogo que possua a tabela com o [propriedade ParentCatalog (ADOX)](../../../ado/reference/adox-api/parentcatalog-property-adox.md) propriedade.  
  
-   Retornar informações de data com o [propriedade DateCreated (ADOX)](../../../ado/reference/adox-api/datecreated-property-adox.md) e [propriedade DateModified (ADOX)](../../../ado/reference/adox-api/datemodified-property-adox.md) propriedades.  
  
-   Acessar as propriedades de tabela específico do provedor com o [coleção de propriedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) coleção.  
  
> [!NOTE]
>  Seu provedor de dados não pode dar suporte a todas as propriedades de **tabela** objetos. Um erro ocorrerá se você tiver definido um valor para uma propriedade que o provedor não dá suporte. Para o novo **tabela** objetos, ocorrerá um erro quando o objeto é acrescentado à coleção. Para objetos existentes, o erro ocorrerá quando a configuração da propriedade.  
>   
>  Ao criar **tabela** objetos, a existência de um valor padrão adequado para uma propriedade opcional não garante que o provedor oferece suporte à propriedade. Para obter mais informações sobre as propriedades que o provedor oferece suporte, consulte a documentação do provedor.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto Table](../../../ado/reference/adox-api/table-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo da propriedade ActiveConnection de catálogo (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Columns and Tables Append métodos, exemplo da propriedade Name (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Método Close da Conexão, exemplo da propriedade Table Type (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Chaves de acrescentar o método, tipo de chave, RelatedColumn, RelatedTable e exemplo das propriedades UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Exemplo da propriedade ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Coleção Columns (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Coleção Indexes (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [Coleção Keys (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)   
 [Coleção de propriedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Coleção Tables (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)
