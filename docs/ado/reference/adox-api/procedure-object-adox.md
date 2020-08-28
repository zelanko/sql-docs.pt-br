---
description: Objeto Procedure (ADOX)
title: Objeto de procedimento (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: b41e83033ab86810c4e26ff3c15fa4d9d1ea97ae
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983627"
---
# <a name="procedure-object-adox"></a>Objeto Procedure (ADOX)
Representa um procedimento armazenado. Quando usado em conjunto com o objeto de [comando](../ado-api/command-object-ado.md) ADO, o objeto de **procedimento** pode ser usado para adicionar, excluir ou modificar procedimentos armazenados.  
  
## <a name="remarks"></a>Comentários  
 O objeto **Procedure** permite que você crie um procedimento armazenado sem precisar saber ou usar a sintaxe "criar procedimento" do provedor.  
  
 Com as propriedades de um objeto de **procedimento** , você pode:  
  
-   Identifique o procedimento com a propriedade [Name](./name-property-adox.md) .  
  
-   Especifique o objeto de **comando** ADO que pode ser usado para criar ou executar o procedimento com a propriedade [Command](./command-property-adox.md) .  
  
-   Retornar informações de data com as propriedades [DateCreated](./datecreated-property-adox.md) e [DateModified](./datemodified-property-adox.md) .  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto Procedure](./procedure-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades Command e CommandText (VB)](./command-and-commandtext-properties-example-vb.md)   
 [Coleção Parameters, exemplo da Propriedade Command (VB)](./parameters-collection-command-property-example-vb.md)   
 [Exemplo do método Append Procedures (VB)](./procedures-append-method-example-vb.md)   
 [Exemplo do método Delete de procedimentos (VB)](./procedures-delete-method-example-vb.md)   
 [Coleção Procedures (ADOX)](./procedures-collection-adox.md)