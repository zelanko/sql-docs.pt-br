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
ms.openlocfilehash: 75ceef103f3f0e6a3e1c789206887e3044da8854
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770305"
---
# <a name="index-object-adox"></a>Objeto Index (ADOX)
Representa um índice de uma tabela de banco de dados.  
  
## <a name="remarks"></a>Comentários  
 O código a seguir cria um novo **índice**:  
  
```  
Dim obj As New Index  
```  
  
 Com as propriedades e coleções de um objeto de **índice** , você pode:  
  
-   Identifique o índice com a propriedade [Name](./name-property-adox.md) .  
  
-   Acesse as colunas de banco de dados do índice com a coleção de [colunas](./columns-collection-adox.md) .  
  
-   Especifique se as chaves de índice devem ser exclusivas com a propriedade [Unique](./unique-property-adox.md) .  
  
-   Especifique se o índice é a chave primária para uma tabela com a propriedade [PrimaryKey](./primarykey-property-adox.md) .  
  
-   Especifique se os registros que têm valores nulos em seus campos de índice têm entradas de índice com a propriedade [IndexNulls](./indexnulls-property-adox.md) .  
  
-   Especifique se o índice é clusterizado com a propriedade [clusterizada](./clustered-property-adox.md) .  
  
-   Acesse Propriedades de índice específicas do provedor com a coleção [Properties](../ado-api/properties-collection-ado.md) .  
  
> [!NOTE]
>  Ocorrerá um erro ao acrescentar uma [coluna](./column-object-adox.md) à coleção de **colunas** de um **índice** se a **coluna** não existir em um objeto de [tabela](./table-object-adox.md) já acrescentado à coleção de [tabelas](./tables-collection-adox.md) .  
  
> [!NOTE]
>  Seu provedor de dados pode não dar suporte a todas as propriedades de objetos de **índice** . Ocorrerá um erro se você tiver definido um valor para uma propriedade sem suporte pelo provedor. Para novos objetos de **índice** , o erro ocorrerá quando o objeto for anexado à coleção. Para objetos existentes, o erro ocorrerá ao definir a propriedade.  
  
> [!NOTE]
>  Ao criar objetos de **índice** , a existência de um valor padrão apropriado para uma propriedade opcional não garante que seu provedor dê suporte à propriedade. Para obter mais informações sobre quais propriedades seu provedor dá suporte, consulte a documentação do provedor.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto Index](./index-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método Indexes Append (VB)](./indexes-append-method-example-vb.md)   
 [Exemplo da propriedade IndexNulls (VB)](./indexnulls-property-example-vb.md)   
 [Exemplo de PrimaryKey e propriedades exclusivas (VB)](./primarykey-and-unique-properties-example-vb.md)   
 [Exemplo da propriedade SortOrder (VB)](./sortorder-property-example-vb.md)   
 [Coleção Columns (ADOX)](./columns-collection-adox.md)   
 [Coleção de índices (ADOX)](./indexes-collection-adox.md)   
 [Coleção Properties (ADO)](../ado-api/properties-collection-ado.md)