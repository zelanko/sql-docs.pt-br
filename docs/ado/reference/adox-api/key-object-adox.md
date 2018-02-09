---
title: Chave de objeto (ADOX) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Key
helpviewer_keywords:
- Key object [ADOX]
ms.assetid: 55f116fe-4d56-4892-bffe-0cdd6fc727c9
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9a1f971c07571c54cc74e4a750fde505e60af2f2
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="key-object-adox"></a>Objeto de chave (ADOX)
Representa um campo de chave estrangeiro, exclusivo ou primário de uma tabela de banco de dados.  
  
## <a name="remarks"></a>Remarks  
 O código a seguir cria um novo **chave**:  
  
```  
Dim obj As New Key  
```  
  
 Com as propriedades e coleções de uma **chave** do objeto, você pode:  
  
-   Identifique a chave com o [nome](../../../ado/reference/adox-api/name-property-adox.md) propriedade.  
  
-   Determinar se a chave é primária, externa ou exclusivo com o [tipo](../../../ado/reference/adox-api/type-property-key-adox.md) propriedade.  
  
-   Acessar as colunas de banco de dados da chave com o [colunas](../../../ado/reference/adox-api/columns-collection-adox.md) coleção.  
  
-   Especifique o nome da tabela relacionada com a [RelatedTable](../../../ado/reference/adox-api/relatedtable-property-adox.md) propriedade.  
  
-   Determinar a ação executada na exclusão ou atualização de uma chave primária com o [DeleteRule](../../../ado/reference/adox-api/deleterule-property-adox.md) e [UpdateRule](../../../ado/reference/adox-api/updaterule-property-adox.md) propriedades.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto Key](../../../ado/reference/adox-api/key-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Chaves de acrescentar o método, tipo de chave, RelatedColumn, RelatedTable e exemplo de propriedades de UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Coleção de colunas (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Coleção Keys (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)
