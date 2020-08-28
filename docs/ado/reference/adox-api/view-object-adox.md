---
description: Objeto View (ADOX)
title: Objeto View (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: eefc7c259d12f20ada1676a6518fa357719abe63
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88982987"
---
# <a name="view-object-adox"></a>Objeto View (ADOX)
Representa um conjunto filtrado de registros ou uma tabela virtual. Quando usado em conjunto com o objeto de [comando](../ado-api/command-object-ado.md) ADO, o objeto **View** pode ser usado para adicionar, excluir ou modificar exibições.  
  
## <a name="remarks"></a>Comentários  
 Uma exibição é uma tabela virtual, criada a partir de outras tabelas ou exibições de banco de dados. O objeto **View** permite que você crie uma exibição sem precisar saber ou usar a sintaxe "Create View" do provedor.  
  
 Com as propriedades de um objeto **View** , você pode:  
  
-   Identifique o modo de exibição com a propriedade [Name](./name-property-adox.md) .  
  
-   Especifique o objeto de **comando** ADO que pode ser usado para adicionar, excluir ou modificar exibições com a propriedade [Command](./command-property-adox.md) .  
  
-   Retornar informações de data com as propriedades [DateCreated](./datecreated-property-adox.md) e [DateModified](./datemodified-property-adox.md) .  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto View](./view-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de coleções de exibições e campos (VB)](./views-and-fields-collections-example-vb.md)   
 [Exemplo do método Append views (VB)](./views-append-method-example-vb.md)   
 [Coleção views, exemplo da propriedade CommandText (VB)](./views-collection-commandtext-property-example-vb.md)   
 [Exemplo do método Delete de views (VB)](./views-delete-method-example-vb.md)   
 [Coleção Views (ADOX)](./views-collection-adox.md)