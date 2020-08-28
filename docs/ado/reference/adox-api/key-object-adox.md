---
description: Objeto Key (ADOX)
title: Objeto de chave (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: d8b2f37dd12f7243f2c5fcb8e577dc35e350c6a9
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984047"
---
# <a name="key-object-adox"></a>Objeto Key (ADOX)
Representa um campo de chave primária, estrangeira ou exclusiva de uma tabela de banco de dados.  
  
## <a name="remarks"></a>Comentários  
 O código a seguir cria uma nova **chave**:  
  
```  
Dim obj As New Key  
```  
  
 Com as propriedades e coleções de um objeto de **chave** , você pode:  
  
-   Identifique a chave com a propriedade [Name](./name-property-adox.md) .  
  
-   Determine se a chave é primária, estrangeira ou exclusiva com a propriedade [Type](./type-property-key-adox.md) .  
  
-   Acesse as colunas de banco de dados da chave com a coleção de [colunas](./columns-collection-adox.md) .  
  
-   Especifique o nome da tabela relacionada com a propriedade [RELATEDTABLE](./relatedtable-property-adox.md) .  
  
-   Determine a ação executada na exclusão ou atualização de uma chave primária com as propriedades [DeleteRule](./deleterule-property-adox.md) e [UpdateRule](./updaterule-property-adox.md) .  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto Key](./key-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades método, tipo de chave, RelatedColumn, RELATEDTABLE e UpdateRule da tecla Append (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Coleção Columns (ADOX)](./columns-collection-adox.md)   
 [Coleção Keys (ADOX)](./keys-collection-adox.md)