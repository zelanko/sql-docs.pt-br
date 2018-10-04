---
title: Chave de objeto (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Key
helpviewer_keywords:
- Key object [ADOX]
ms.assetid: 55f116fe-4d56-4892-bffe-0cdd6fc727c9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7365b3ac33f215840a112089523f23e88697a433
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47626724"
---
# <a name="key-object-adox"></a>Objeto Key (ADOX)
Representa um campo de chave estrangeiro, exclusivo ou primário de uma tabela de banco de dados.  
  
## <a name="remarks"></a>Comentários  
 O código a seguir cria um novo **chave**:  
  
```  
Dim obj As New Key  
```  
  
 Com as propriedades e coleções de uma **chave** do objeto, você pode:  
  
-   Identificar a chave com o [nome](../../../ado/reference/adox-api/name-property-adox.md) propriedade.  
  
-   Determinar se a chave é, estrangeiras, exclusiva ou primária com a [tipo](../../../ado/reference/adox-api/type-property-key-adox.md) propriedade.  
  
-   Acessar as colunas de banco de dados da chave com o [colunas](../../../ado/reference/adox-api/columns-collection-adox.md) coleção.  
  
-   Especifique o nome da tabela relacionada com a [RelatedTable](../../../ado/reference/adox-api/relatedtable-property-adox.md) propriedade.  
  
-   Determinar a ação executada na exclusão ou atualização de uma chave primária com a [DeleteRule](../../../ado/reference/adox-api/deleterule-property-adox.md) e [UpdateRule](../../../ado/reference/adox-api/updaterule-property-adox.md) propriedades.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto Key](../../../ado/reference/adox-api/key-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Chaves de acrescentar o método, tipo de chave, RelatedColumn, RelatedTable e exemplo das propriedades UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Coleção Columns (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Coleção Keys (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)
