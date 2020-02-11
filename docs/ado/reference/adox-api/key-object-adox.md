---
title: Objeto de chave (ADOX) | Microsoft Docs
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
ms.openlocfilehash: f7e405cfdde86a4f19590a87035ff574e1d255c9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67965909"
---
# <a name="key-object-adox"></a>Objeto Key (ADOX)
Representa um campo de chave primária, estrangeira ou exclusiva de uma tabela de banco de dados.  
  
## <a name="remarks"></a>Comentários  
 O código a seguir cria uma nova **chave**:  
  
```  
Dim obj As New Key  
```  
  
 Com as propriedades e coleções de um objeto de **chave** , você pode:  
  
-   Identifique a chave com a propriedade [Name](../../../ado/reference/adox-api/name-property-adox.md) .  
  
-   Determine se a chave é primária, estrangeira ou exclusiva com a propriedade [Type](../../../ado/reference/adox-api/type-property-key-adox.md) .  
  
-   Acesse as colunas de banco de dados da chave com a coleção de [colunas](../../../ado/reference/adox-api/columns-collection-adox.md) .  
  
-   Especifique o nome da tabela relacionada com a propriedade [RELATEDTABLE](../../../ado/reference/adox-api/relatedtable-property-adox.md) .  
  
-   Determine a ação executada na exclusão ou atualização de uma chave primária com as propriedades [DeleteRule](../../../ado/reference/adox-api/deleterule-property-adox.md) e [UpdateRule](../../../ado/reference/adox-api/updaterule-property-adox.md) .  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto Key](../../../ado/reference/adox-api/key-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades método, tipo de chave, RelatedColumn, RELATEDTABLE e UpdateRule da tecla Append (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Coleção Columns (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Coleção Keys (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)
