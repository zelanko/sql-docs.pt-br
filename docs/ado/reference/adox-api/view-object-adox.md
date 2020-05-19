---
title: Objeto View (ADOX) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: b468ccc3edc4cc5453b4f08371cd2b4b962f0c72
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82753189"
---
# <a name="view-object-adox"></a>Objeto View (ADOX)
Representa um conjunto filtrado de registros ou uma tabela virtual. Quando usado em conjunto com o objeto de [comando](../../../ado/reference/ado-api/command-object-ado.md) ADO, o objeto **View** pode ser usado para adicionar, excluir ou modificar exibições.  
  
## <a name="remarks"></a>Comentários  
 Uma exibição é uma tabela virtual, criada a partir de outras tabelas ou exibições de banco de dados. O objeto **View** permite que você crie uma exibição sem precisar saber ou usar a sintaxe "Create View" do provedor.  
  
 Com as propriedades de um objeto **View** , você pode:  
  
-   Identifique o modo de exibição com a propriedade [Name](../../../ado/reference/adox-api/name-property-adox.md) .  
  
-   Especifique o objeto de **comando** ADO que pode ser usado para adicionar, excluir ou modificar exibições com a propriedade [Command](../../../ado/reference/adox-api/command-property-adox.md) .  
  
-   Retornar informações de data com as propriedades [DateCreated](../../../ado/reference/adox-api/datecreated-property-adox.md) e [DateModified](../../../ado/reference/adox-api/datemodified-property-adox.md) .  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto View](../../../ado/reference/adox-api/view-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de coleções de exibições e campos (VB)](../../../ado/reference/adox-api/views-and-fields-collections-example-vb.md)   
 [Exemplo do método Append views (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Coleção views, exemplo da propriedade CommandText (VB)](../../../ado/reference/adox-api/views-collection-commandtext-property-example-vb.md)   
 [Exemplo do método Delete de views (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)   
 [Coleção Views (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
