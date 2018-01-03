---
title: "Índice do objeto (ADOX) | Microsoft Docs"
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
f1_keywords: Index
helpviewer_keywords: Index object [ADOX]
ms.assetid: 6b9578c0-bc94-46b9-b801-c18e14b04b31
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: faeb92dd8c63fb5850da5970df0cc58430f23725
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="index-object-adox"></a>Objeto de índice (ADOX)
Representa um índice de uma tabela de banco de dados.  
  
## <a name="remarks"></a>Remarks  
 O código a seguir cria um novo **índice**:  
  
```  
Dim obj As New Index  
```  
  
 Com as propriedades e coleções de uma **índice** do objeto, você pode:  
  
-   Identificar o índice com o [nome](../../../ado/reference/adox-api/name-property-adox.md) propriedade.  
  
-   Acessar as colunas de banco de dados do índice com o [colunas](../../../ado/reference/adox-api/columns-collection-adox.md) coleção.  
  
-   Especifique se as chaves de índice devem ser exclusivas com o [Unique](../../../ado/reference/adox-api/unique-property-adox.md) propriedade.  
  
-   Especifique se o índice é a chave primária para uma tabela com o [PrimaryKey](../../../ado/reference/adox-api/primarykey-property-adox.md) propriedade.  
  
-   Especifique se os registros com valores nulos em seus campos de índice têm entradas de índice com o [IndexNulls](../../../ado/reference/adox-api/indexnulls-property-adox.md) propriedade.  
  
-   Especifique se o índice é clusterizado com o [Clustered](../../../ado/reference/adox-api/clustered-property-adox.md) propriedade.  
  
-   Acessar as propriedades específicas do provedor de índice com o [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção.  
  
> [!NOTE]
>  Ocorrerá um erro ao anexar um [coluna](../../../ado/reference/adox-api/column-object-adox.md) para o **colunas** coleção de um **índice** se o **coluna** não existe em um [Tabela](../../../ado/reference/adox-api/table-object-adox.md) objeto já está anexado ao [tabelas](../../../ado/reference/adox-api/tables-collection-adox.md) coleção.  
  
> [!NOTE]
>  O provedor de dados pode não oferecer suporte a todas as propriedades de **índice** objetos. Um erro ocorrerá se você tiver definido um valor para uma propriedade que não é suportada pelo provedor. Para o novo **índice** objetos, ocorrerá um erro quando o objeto é acrescentado à coleção. Para objetos existentes, o erro ocorrerá quando a configuração da propriedade.  
  
> [!NOTE]
>  Ao criar **índice** objetos, a existência de um valor padrão apropriado para uma propriedade opcional não garante que o provedor oferece suporte à propriedade. Para obter mais informações sobre quais propriedades o provedor oferece suporte, consulte a documentação do provedor.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto Index](../../../ado/reference/adox-api/index-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Índices de acrescentar o exemplo de método (VB)](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [Exemplo de propriedade IndexNulls (VB)](../../../ado/reference/adox-api/indexnulls-property-example-vb.md)   
 [PrimaryKey e exemplo de propriedades exclusivas (VB)](../../../ado/reference/adox-api/primarykey-and-unique-properties-example-vb.md)   
 [Exemplo de propriedade SortOrder (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Coleção de colunas (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Coleção de índices (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
