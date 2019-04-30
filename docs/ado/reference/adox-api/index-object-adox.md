---
title: Índice do objeto (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Index
helpviewer_keywords:
- Index object [ADOX]
ms.assetid: 6b9578c0-bc94-46b9-b801-c18e14b04b31
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0b6fca30201a93b84f59e9356c5201e1070053d5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63311785"
---
# <a name="index-object-adox"></a>Objeto Index (ADOX)
Representa um índice de uma tabela de banco de dados.  
  
## <a name="remarks"></a>Comentários  
 O código a seguir cria um novo **índice**:  
  
```  
Dim obj As New Index  
```  
  
 Com as propriedades e coleções de uma **índice** do objeto, você pode:  
  
-   Identificar o índice com o [nome](../../../ado/reference/adox-api/name-property-adox.md) propriedade.  
  
-   Acessar as colunas de banco de dados do índice com o [colunas](../../../ado/reference/adox-api/columns-collection-adox.md) coleção.  
  
-   Especifique se as chaves de índice devem ser exclusivas com o [Unique](../../../ado/reference/adox-api/unique-property-adox.md) propriedade.  
  
-   Especifique se o índice é a chave primária para uma tabela com o [PrimaryKey](../../../ado/reference/adox-api/primarykey-property-adox.md) propriedade.  
  
-   Especifique se os registros que têm valores nulos em seus campos de índice têm entradas de índice com o [IndexNulls](../../../ado/reference/adox-api/indexnulls-property-adox.md) propriedade.  
  
-   Especifique se o índice é clusterizado com o [Clustered](../../../ado/reference/adox-api/clustered-property-adox.md) propriedade.  
  
-   Acessar as propriedades de índice específica do provedor com o [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção.  
  
> [!NOTE]
>  Ocorrerá um erro ao anexar um [coluna](../../../ado/reference/adox-api/column-object-adox.md) para o **colunas** coleção de um **índice** se o **coluna** não existe em um [Tabela](../../../ado/reference/adox-api/table-object-adox.md) objeto já foi acrescentado para o [tabelas](../../../ado/reference/adox-api/tables-collection-adox.md) coleção.  
  
> [!NOTE]
>  Seu provedor de dados não pode dar suporte a todas as propriedades de **índice** objetos. Se você tiver definido um valor para uma propriedade que não é suportado pelo provedor, ocorrerá um erro. Para o novo **índice** objetos, ocorrerá um erro quando o objeto é acrescentado à coleção. Para objetos existentes, o erro ocorrerá quando a configuração da propriedade.  
  
> [!NOTE]
>  Ao criar **índice** objetos, a existência de um valor padrão adequado para uma propriedade opcional não garante que o provedor oferece suporte à propriedade. Para obter mais informações sobre as propriedades que o provedor oferece suporte, consulte a documentação do provedor.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto Index](../../../ado/reference/adox-api/index-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo (VB) do método Indexes Append](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [Exemplo da propriedade IndexNulls (VB)](../../../ado/reference/adox-api/indexnulls-property-example-vb.md)   
 [PrimaryKey e propriedades exclusivas (VB)](../../../ado/reference/adox-api/primarykey-and-unique-properties-example-vb.md)   
 [Exemplo da propriedade SortOrder (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Coleção Columns (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Coleção Indexes (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
