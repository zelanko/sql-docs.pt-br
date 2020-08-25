---
description: Propriedade Count (ADO)
title: Propriedade Count (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Collection::Count
helpviewer_keywords:
- Count property [ADO]
ms.assetid: da9ccd1f-d402-41a2-940c-45556fc5340d
author: rothja
ms.author: jroth
ms.openlocfilehash: 3f821642915bdb01e67f673fab871df0541c63ad
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775685"
---
# <a name="count-property-ado"></a>Propriedade Count (ADO)
Indica o número de objetos em uma coleção.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um valor **longo** .  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **Count** para determinar quantos objetos estão em uma determinada coleção.  
  
 Como a numeração de membros de uma coleção começa com zero, você deve sempre codificar loops começando com o membro zero e terminando com o valor da propriedade **Count** menos 1. Se você estiver usando o Microsoft Visual Basic e quiser executar um loop pelos membros de uma coleção sem verificar a propriedade **Count** , use o **para cada... Próximo** comando.  
  
 Se a propriedade **Count** for zero, não haverá nenhum objeto na coleção.  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Coleção Axes (ADO MD)](../ado-md-api/axes-collection-ado-md.md)  
        [Coleção Columns (ADOX)](../adox-api/columns-collection-adox.md)  
        [Coleção CubeDefs (ADO MD)](../ado-md-api/cubedefs-collection-ado-md.md)  
        [Coleção Dimensions (ADO MD)](../ado-md-api/dimensions-collection-ado-md.md)  
        [Coleção Errors (ADO)](./errors-collection-ado.md)  
        [Coleção Fields (ADO)](./fields-collection-ado.md)  
        [Coleção Groups (ADOX)](../adox-api/groups-collection-adox.md)  
    :::column-end:::
    :::column:::
        [Coleção Hierarchies (ADO MD)](../ado-md-api/hierarchies-collection-ado-md.md)  
        [Coleção Indexes (ADOX)](../adox-api/indexes-collection-adox.md)  
        [Coleção Keys (ADOX)](../adox-api/keys-collection-adox.md)  
        [Coleção Levels (ADO MD)](../ado-md-api/levels-collection-ado-md.md)  
        [Coleção Members (ADO MD)](../ado-md-api/members-collection-ado-md.md)  
        [Coleção Parameters (ADO)](./parameters-collection-ado.md)  
    :::column-end:::
    :::column:::
        [Coleção Positions (ADO MD)](../ado-md-api/positions-collection-ado-md.md)  
        [Coleção Procedures (ADOX)](../adox-api/procedures-collection-adox.md)  
        [Coleção Properties (ADO)](./properties-collection-ado.md)  
        [Coleção Tables (ADOX)](../adox-api/tables-collection-adox.md)  
        [Coleção Users (ADOX)](../adox-api/users-collection-adox.md)  
        [Coleção Views (ADOX)](../adox-api/views-collection-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade Count (VB)](./count-property-example-vb.md)   
 [Exemplo da propriedade Count (VC + +)](./count-property-example-vc.md)   
 [Método Refresh (ADO)](./refresh-method-ado.md)