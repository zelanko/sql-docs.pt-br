---
title: Objeto de coluna (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Column
helpviewer_keywords:
- Column object [ADOX]
ms.assetid: 6e772783-1bc8-4ea7-94b2-7d7a52ea5c47
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3d688a64630fbf22ad8efbe987e02d13bfdb07a5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="column-object-adox"></a>Objeto de coluna (ADOX)
Representa uma coluna de uma tabela, índice ou chave.  
  
## <a name="remarks"></a>Remarks  
 O código a seguir cria um novo **coluna**:  
  
 `Dim obj As New Column`  
  
 Com as propriedades e coleções de uma **coluna** do objeto, você pode:  
  
-   Identificar a coluna com o [nome de propriedade (ADOX)](../../../ado/reference/adox-api/name-property-adox.md) propriedade.  
  
-   Especifique o tipo de dados da coluna com o [a propriedade de tipo (chave) (ADOX)](../../../ado/reference/adox-api/type-property-key-adox.md) propriedade.  
  
-   Determinar se a coluna for de comprimento fixo, ou se ele pode conter valores null com o [atributos de propriedade (ADOX)](../../../ado/reference/adox-api/attributes-property-adox.md) propriedade.  
  
-   Especifique o tamanho máximo da coluna com o [propriedade DefinedSize (ADOX)](../../../ado/reference/adox-api/definedsize-property-adox.md) propriedade.  
  
-   Para valores numéricos, especificar a escala com o [NumericScale propriedade (ADOX)](../../../ado/reference/adox-api/numericscale-property-adox.md) propriedade.  
  
-   Para valor de dados numéricos, especifique a precisão máxima com o [propriedade precisão (ADOX)](../../../ado/reference/adox-api/precision-property-adox.md) propriedade.  
  
-   Especifique o [o objeto de catálogo (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md) que possui a coluna com o [ParentCatalog propriedade (ADOX)](../../../ado/reference/adox-api/parentcatalog-property-adox.md) propriedade.  
  
-   Para colunas de chave, especifique o nome da coluna relacionada na tabela relacionada com a [RelatedColumn propriedade (ADOX)](../../../ado/reference/adox-api/relatedcolumn-property-adox.md) propriedade.  
  
-   Para colunas de índice, especifique se a ordem de classificação é crescente ou decrescente com o [propriedade SortOrder (ADOX)](../../../ado/reference/adox-api/sortorder-property-adox.md) propriedade.  
  
-   Acessar as propriedades específicas do provedor com o [propriedades de coleção (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) coleção.  
  
> [!NOTE]
>  Nem todas as propriedades de **coluna** objetos podem ser aceitos pelo seu provedor de dados. Um erro ocorrerá se você tiver definido um valor para uma propriedade que o provedor não oferece suporte. Para o novo **coluna** objetos, ocorrerá um erro quando o objeto é acrescentado à coleção. Para objetos existentes, o erro ocorrerá quando a configuração da propriedade.  
>   
>  Ao criar **coluna** objetos, a existência de um valor padrão apropriado para uma propriedade opcional não garante que o provedor oferece suporte à propriedade. Para obter mais informações sobre quais propriedades o provedor oferece suporte, consulte a documentação do provedor.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto Column](../../../ado/reference/adox-api/column-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas e colunas acrescentar métodos, exemplo de nome de propriedade (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Método Close da Conexão, exemplo de propriedade de tipo de tabela (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Chaves de acrescentar o método, tipo de chave, RelatedColumn, RelatedTable e exemplo de propriedades de UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Exemplo de código ADOX: NumericScale e exemplo de propriedades de precisão (VB)](../../../ado/reference/adox-api/adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [Exemplo de propriedade ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Exemplo de propriedade SortOrder (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Coleção de colunas (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
