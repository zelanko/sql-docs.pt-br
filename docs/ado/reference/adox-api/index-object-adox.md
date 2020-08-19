---
description: Objeto Index (ADOX)
title: Objeto Index (ADOX) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 81f0bf8d07bbb89105a0ceab421d8433d52f1672
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439938"
---
# <a name="index-object-adox"></a>Objeto Index (ADOX)
Representa um índice de uma tabela de banco de dados.  
  
## <a name="remarks"></a>Comentários  
 O código a seguir cria um novo **índice**:  
  
```  
Dim obj As New Index  
```  
  
 Com as propriedades e coleções de um objeto de **índice** , você pode:  
  
-   Identifique o índice com a propriedade [Name](../../../ado/reference/adox-api/name-property-adox.md) .  
  
-   Acesse as colunas de banco de dados do índice com a coleção de [colunas](../../../ado/reference/adox-api/columns-collection-adox.md) .  
  
-   Especifique se as chaves de índice devem ser exclusivas com a propriedade [Unique](../../../ado/reference/adox-api/unique-property-adox.md) .  
  
-   Especifique se o índice é a chave primária para uma tabela com a propriedade [PrimaryKey](../../../ado/reference/adox-api/primarykey-property-adox.md) .  
  
-   Especifique se os registros que têm valores nulos em seus campos de índice têm entradas de índice com a propriedade [IndexNulls](../../../ado/reference/adox-api/indexnulls-property-adox.md) .  
  
-   Especifique se o índice é clusterizado com a propriedade [clusterizada](../../../ado/reference/adox-api/clustered-property-adox.md) .  
  
-   Acesse Propriedades de índice específicas do provedor com a coleção [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) .  
  
> [!NOTE]
>  Ocorrerá um erro ao acrescentar uma [coluna](../../../ado/reference/adox-api/column-object-adox.md) à coleção de **colunas** de um **índice** se a **coluna** não existir em um objeto de [tabela](../../../ado/reference/adox-api/table-object-adox.md) já acrescentado à coleção de [tabelas](../../../ado/reference/adox-api/tables-collection-adox.md) .  
  
> [!NOTE]
>  Seu provedor de dados pode não dar suporte a todas as propriedades de objetos de **índice** . Ocorrerá um erro se você tiver definido um valor para uma propriedade sem suporte pelo provedor. Para novos objetos de **índice** , o erro ocorrerá quando o objeto for anexado à coleção. Para objetos existentes, o erro ocorrerá ao definir a propriedade.  
  
> [!NOTE]
>  Ao criar objetos de **índice** , a existência de um valor padrão apropriado para uma propriedade opcional não garante que seu provedor dê suporte à propriedade. Para obter mais informações sobre quais propriedades seu provedor dá suporte, consulte a documentação do provedor.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto Index](../../../ado/reference/adox-api/index-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método Indexes Append (VB)](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [Exemplo da propriedade IndexNulls (VB)](../../../ado/reference/adox-api/indexnulls-property-example-vb.md)   
 [Exemplo de PrimaryKey e propriedades exclusivas (VB)](../../../ado/reference/adox-api/primarykey-and-unique-properties-example-vb.md)   
 [Exemplo da propriedade SortOrder (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Coleção Columns (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Coleção de índices (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
