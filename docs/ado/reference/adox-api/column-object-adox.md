---
description: Objeto Column (ADOX)
title: Objeto Column (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: b6cc15e82091da2161a01c1c0a468e86095dd0d6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985097"
---
# <a name="column-object-adox"></a>Objeto Column (ADOX)
Representa uma coluna de uma tabela, índice ou chave.  
  
## <a name="remarks"></a>Comentários  
 O código a seguir cria uma nova **coluna**:  
  
 `Dim obj As New Column`  
  
 Com as propriedades e coleções de um objeto de **coluna** , você pode:  
  
-   Identifique a coluna com a propriedade [Name (ADOX)](./name-property-adox.md) .  
  
-   Especifique o tipo de dados da coluna com a propriedade [(chave) do tipo Propriedade (ADOX)](./type-property-key-adox.md) .  
  
-   Determine se a coluna tem comprimento fixo ou se ela pode conter valores nulos com a propriedade de [propriedade Attributes (ADOX)](./attributes-property-adox.md) .  
  
-   Especifique o tamanho máximo da coluna com a propriedade da [Propriedade DefinedSize (ADOX)](./definedsize-property-adox.md) .  
  
-   Para valores de dados numéricos, especifique a escala com a propriedade da [Propriedade NumericScale (ADOX)](./numericscale-property-adox.md) .  
  
-   Para valor de dados numéricos, especifique a precisão máxima com a propriedade de [propriedade de precisão (ADOX)](./precision-property-adox.md) .  
  
-   Especifique o [objeto de catálogo (ADOX)](./catalog-object-adox.md) que possui a coluna com a propriedade [ParentCatalog (ADOX)](./parentcatalog-property-adox.md) .  
  
-   Para colunas de chave, especifique o nome da coluna relacionada na tabela relacionada com a propriedade [RelatedColumn (ADOX)](./relatedcolumn-property-adox.md) .  
  
-   Para colunas de índice, especifique se a ordem de classificação é crescente ou decrescente com a propriedade [OrdemDeClassificação (Propriedade SortOrder)](./sortorder-property-adox.md) .  
  
-   Acesse propriedades específicas do provedor com a coleção de [Propriedades Collection (ADO)](../ado-api/properties-collection-ado.md) .  
  
> [!NOTE]
>  Nem todas as propriedades de objetos de **coluna** podem ser suportadas pelo seu provedor de dados. Ocorrerá um erro se você tiver definido um valor para uma propriedade para a qual o provedor não oferece suporte. Para novos objetos de **coluna** , o erro ocorrerá quando o objeto for anexado à coleção. Para objetos existentes, o erro ocorrerá ao definir a propriedade.  
>   
>  Ao criar objetos de **coluna** , a existência de um valor padrão apropriado para uma propriedade opcional não garante que seu provedor dê suporte à propriedade. Para obter mais informações sobre quais propriedades seu provedor dá suporte, consulte a documentação do provedor.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto Column](./column-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade Name e métodos de acréscimo de colunas e tabelas (VB)](./columns-and-tables-append-methods-name-property-example-vb.md)   
 [Método Connection Close, exemplo da propriedade de tipo Table (VB)](./connection-close-method-table-type-property-example-vb.md)   
 [Exemplo das propriedades método, tipo de chave, RelatedColumn, RELATEDTABLE e UpdateRule da tecla Append (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Exemplo de código ADOX: exemplo de propriedades NumericScale e Precision (VB)](./adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [Exemplo da propriedade ParentCatalog (VB)](./parentcatalog-property-example-vb.md)   
 [Exemplo da propriedade SortOrder (VB)](./sortorder-property-example-vb.md)   
 [Coleção Columns (ADOX)](./columns-collection-adox.md)   
 [Coleção Properties (ADO)](../ado-api/properties-collection-ado.md)