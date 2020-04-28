---
title: Objeto Column (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Column
helpviewer_keywords:
- Column object [ADOX]
ms.assetid: 6e772783-1bc8-4ea7-94b2-7d7a52ea5c47
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db2c2dbe6af2a50fc2507a9ade92d83e0502f2ee
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67966916"
---
# <a name="column-object-adox"></a>Objeto Column (ADOX)
Representa uma coluna de uma tabela, índice ou chave.  
  
## <a name="remarks"></a>Comentários  
 O código a seguir cria uma nova **coluna**:  
  
 `Dim obj As New Column`  
  
 Com as propriedades e coleções de um objeto de **coluna** , você pode:  
  
-   Identifique a coluna com a propriedade [Name (ADOX)](../../../ado/reference/adox-api/name-property-adox.md) .  
  
-   Especifique o tipo de dados da coluna com a propriedade [(chave) do tipo Propriedade (ADOX)](../../../ado/reference/adox-api/type-property-key-adox.md) .  
  
-   Determine se a coluna tem comprimento fixo ou se ela pode conter valores nulos com a propriedade de [propriedade Attributes (ADOX)](../../../ado/reference/adox-api/attributes-property-adox.md) .  
  
-   Especifique o tamanho máximo da coluna com a propriedade da [Propriedade DefinedSize (ADOX)](../../../ado/reference/adox-api/definedsize-property-adox.md) .  
  
-   Para valores de dados numéricos, especifique a escala com a propriedade da [Propriedade NumericScale (ADOX)](../../../ado/reference/adox-api/numericscale-property-adox.md) .  
  
-   Para valor de dados numéricos, especifique a precisão máxima com a propriedade de [propriedade de precisão (ADOX)](../../../ado/reference/adox-api/precision-property-adox.md) .  
  
-   Especifique o [objeto de catálogo (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md) que possui a coluna com a propriedade [ParentCatalog (ADOX)](../../../ado/reference/adox-api/parentcatalog-property-adox.md) .  
  
-   Para colunas de chave, especifique o nome da coluna relacionada na tabela relacionada com a propriedade [RelatedColumn (ADOX)](../../../ado/reference/adox-api/relatedcolumn-property-adox.md) .  
  
-   Para colunas de índice, especifique se a ordem de classificação é crescente ou decrescente com a propriedade [OrdemDeClassificação (Propriedade SortOrder)](../../../ado/reference/adox-api/sortorder-property-adox.md) .  
  
-   Acesse propriedades específicas do provedor com a coleção de [Propriedades Collection (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) .  
  
> [!NOTE]
>  Nem todas as propriedades de objetos de **coluna** podem ser suportadas pelo seu provedor de dados. Ocorrerá um erro se você tiver definido um valor para uma propriedade para a qual o provedor não oferece suporte. Para novos objetos de **coluna** , o erro ocorrerá quando o objeto for anexado à coleção. Para objetos existentes, o erro ocorrerá ao definir a propriedade.  
>   
>  Ao criar objetos de **coluna** , a existência de um valor padrão apropriado para uma propriedade opcional não garante que seu provedor dê suporte à propriedade. Para obter mais informações sobre quais propriedades seu provedor dá suporte, consulte a documentação do provedor.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto Column](../../../ado/reference/adox-api/column-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade Name e métodos de acréscimo de colunas e tabelas (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Método Connection Close, exemplo da propriedade de tipo Table (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Exemplo das propriedades método, tipo de chave, RelatedColumn, RELATEDTABLE e UpdateRule da tecla Append (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Exemplo de código ADOX: exemplo de propriedades NumericScale e Precision (VB)](../../../ado/reference/adox-api/adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [Exemplo da propriedade ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Exemplo da propriedade SortOrder (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Coleção Columns (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
