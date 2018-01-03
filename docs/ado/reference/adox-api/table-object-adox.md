---
title: Tabela de objeto (ADOX) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Table
helpviewer_keywords: Table object [ADOX]
ms.assetid: a6d74000-0828-49ba-850a-63da865f8802
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cd6d351f97d2b6357b8d4156c3208fb4f32a4805
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="table-object-adox"></a>Objeto de tabela (ADOX)
Representa uma tabela de banco de dados, incluindo colunas, índices e chaves.  
  
## <a name="remarks"></a>Remarks  
 O código a seguir cria um novo **tabela**:  
  
```  
Dim obj As New Table  
```  
  
 Com as propriedades e coleções de uma **tabela** do objeto, você pode:  
  
-   Identifique a tabela com o [nome de propriedade (ADOX)](../../../ado/reference/adox-api/name-property-adox.md) propriedade.  
  
-   Determinar o tipo de tabela com o [a propriedade de tipo (tabela) (ADOX)](../../../ado/reference/adox-api/type-property-table-adox.md) propriedade.  
  
-   Acessar as colunas de banco de dados da tabela com a [coleção de colunas (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md) coleção.  
  
-   Acessar os índices da tabela com a [coleção de índices (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md).  
  
-   Acessar as chaves da tabela com a [coleção de chaves (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md).  
  
-   Especifique o catálogo que possui a tabela com o [ParentCatalog propriedade (ADOX)](../../../ado/reference/adox-api/parentcatalog-property-adox.md) propriedade.  
  
-   Retornar informações de data com o [propriedade DateCreated (ADOX)](../../../ado/reference/adox-api/datecreated-property-adox.md) e [propriedade DateModified (ADOX)](../../../ado/reference/adox-api/datemodified-property-adox.md) propriedades.  
  
-   Acessar as propriedades específicas do provedor de tabela com o [propriedades de coleção (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) coleção.  
  
> [!NOTE]
>  O provedor de dados pode não oferecer suporte a todas as propriedades de **tabela** objetos. Um erro ocorrerá se você tiver definido um valor para uma propriedade que o provedor não oferece suporte. Para o novo **tabela** objetos, ocorrerá um erro quando o objeto é acrescentado à coleção. Para objetos existentes, o erro ocorrerá quando a configuração da propriedade.  
>   
>  Ao criar **tabela** objetos, a existência de um valor padrão apropriado para uma propriedade opcional não garante que o provedor oferece suporte à propriedade. Para obter mais informações sobre quais propriedades o provedor oferece suporte, consulte a documentação do provedor.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto Table](../../../ado/reference/adox-api/table-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de propriedade ActiveConnection do catálogo (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Tabelas e colunas acrescentar métodos, exemplo de nome de propriedade (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Método Close da Conexão, exemplo de propriedade de tipo de tabela (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Chaves de acrescentar o método, tipo de chave, RelatedColumn, RelatedTable e exemplo de propriedades de UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Exemplo de propriedade ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Coleção de colunas (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Coleção de índices (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [Coleção de chaves (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)   
 [Coleção de propriedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Coleção Tables (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)
