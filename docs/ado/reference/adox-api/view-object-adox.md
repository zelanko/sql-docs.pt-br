---
title: Exibir objeto (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- View
helpviewer_keywords:
- View object [ADOX]
ms.assetid: 653421ce-7b94-43d0-9bc6-4900f8f2af45
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d87b56716ed1876acc6ac139e7804036d5cdfb86
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718804"
---
# <a name="view-object-adox"></a>Objeto View (ADOX)
Representa um conjunto filtrado de registros ou uma tabela virtual. Quando usado em conjunto com o ADO [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto, o **exibição** objeto pode ser usado para adicionar, excluir ou modificar os modos de exibição.  
  
## <a name="remarks"></a>Comentários  
 Uma exibição é uma tabela virtual, criada a partir de outras tabelas de banco de dados ou exibições. O **exibição** objeto permite que você crie um modo de exibição sem precisar saber ou usar a sintaxe de "CREATE VIEW" do provedor.  
  
 Com as propriedades de um **exibição** do objeto, você pode:  
  
-   Identificar a exibição com o [nome](../../../ado/reference/adox-api/name-property-adox.md) propriedade.  
  
-   Especifique o ADO **comando** objeto que pode ser usado para adicionar, excluir ou modificar os modos de exibição com o [comando](../../../ado/reference/adox-api/command-property-adox.md) propriedade.  
  
-   Retornar informações de data com o [DateCreated](../../../ado/reference/adox-api/datecreated-property-adox.md) e [DateModified](../../../ado/reference/adox-api/datemodified-property-adox.md) propriedades.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto View](../../../ado/reference/adox-api/view-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Modos de exibição e o exemplo de coleções de campos (VB)](../../../ado/reference/adox-api/views-and-fields-collections-example-vb.md)   
 [Append de exibições de exemplo do método (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Coleção Views, exemplo da propriedade CommandText (VB)](../../../ado/reference/adox-api/views-collection-commandtext-property-example-vb.md)   
 [Modos de exibição excluir exemplo de método (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)   
 [Coleção Views (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
