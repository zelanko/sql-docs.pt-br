---
title: Objeto Procedure (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Procedure
helpviewer_keywords:
- Procedure object [ADOX]
ms.assetid: 927bcf3e-32f5-4a80-98d3-600779f0732e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1681001dd42026c1a1fce04814b094047a475a0f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67965483"
---
# <a name="procedure-object-adox"></a>Objeto Procedure (ADOX)
Representa um procedimento armazenado. Quando usado em conjunto com o ADO [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto, o **procedimento** objeto pode ser usado para adicionar, excluir ou modificar procedimentos armazenados.  
  
## <a name="remarks"></a>Comentários  
 O **procedimento** objeto permite que você crie um procedimento armazenado sem precisar saber ou usar a sintaxe de "CREATE PROCEDURE" do provedor.  
  
 Com as propriedades de um **procedimento** do objeto, você pode:  
  
-   Identificar o procedimento com o [nome](../../../ado/reference/adox-api/name-property-adox.md) propriedade.  
  
-   Especifique o ADO **comando** objeto que pode ser usado para criar ou executar o procedimento com o [comando](../../../ado/reference/adox-api/command-property-adox.md) propriedade.  
  
-   Retornar informações de data com o [DateCreated](../../../ado/reference/adox-api/datecreated-property-adox.md) e [DateModified](../../../ado/reference/adox-api/datemodified-property-adox.md) propriedades.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto Procedure](../../../ado/reference/adox-api/procedure-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo Command e CommandText propriedades (VB)](../../../ado/reference/adox-api/command-and-commandtext-properties-example-vb.md)   
 [Coleção de parâmetros de exemplo da propriedade Command (VB)](../../../ado/reference/adox-api/parameters-collection-command-property-example-vb.md)   
 [Append de procedimentos de exemplo do método (VB)](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [Delete de procedimentos de exemplo do método (VB)](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [Coleção Procedures (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)
