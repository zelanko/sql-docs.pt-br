---
title: Exibir objeto (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- View
helpviewer_keywords:
- View object [ADOX]
ms.assetid: 653421ce-7b94-43d0-9bc6-4900f8f2af45
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2980c92b7980fe2fa6ec16f82bc4d8f7d3aff585
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35287435"
---
# <a name="view-object-adox"></a>Objeto de exibição (ADOX)
Representa um conjunto de registros ou uma tabela virtual filtrado. Quando usado em conjunto com o ADO [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto, o **exibição** objeto pode ser usado para adicionar, excluir ou modificar os modos de exibição.  
  
## <a name="remarks"></a>Remarks  
 Uma exibição é uma tabela virtual, criada a partir de outras tabelas de banco de dados ou exibições. O **exibição** objeto permite que você crie um modo de exibição sem precisar saber ou usar a sintaxe de "Criar exibição" do provedor.  
  
 Com as propriedades de um **exibição** do objeto, você pode:  
  
-   Identificar a exibição com o [nome](../../../ado/reference/adox-api/name-property-adox.md) propriedade.  
  
-   Especifique o ADO **comando** objeto que pode ser usado para adicionar, excluir ou modificar os modos de exibição com o [comando](../../../ado/reference/adox-api/command-property-adox.md) propriedade.  
  
-   Retornar informações de data com o [DateCreated](../../../ado/reference/adox-api/datecreated-property-adox.md) e [DateModified](../../../ado/reference/adox-api/datemodified-property-adox.md) propriedades.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto View](../../../ado/reference/adox-api/view-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de coleções de campos (VB) e modos de exibição](../../../ado/reference/adox-api/views-and-fields-collections-example-vb.md)   
 [Exibições de acrescentar o exemplo de método (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Coleção de modos de exibição, o exemplo da propriedade CommandText (VB)](../../../ado/reference/adox-api/views-collection-commandtext-property-example-vb.md)   
 [Exemplo de método (VB)-excluir exibições](../../../ado/reference/adox-api/views-delete-method-example-vb.md)   
 [Coleção Views (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
