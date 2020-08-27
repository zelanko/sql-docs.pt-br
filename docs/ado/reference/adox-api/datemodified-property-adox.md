---
description: Propriedade DateModified (ADOX)
title: Propriedade DateModified (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Table::get_DateModified
- _Table::DateModified
- _Table::GetDateModified
helpviewer_keywords:
- DateModified property [ADOX]
ms.assetid: fed09266-1547-4bda-9088-c254d81cc738
author: rothja
ms.author: jroth
ms.openlocfilehash: 613dbf829009e4e471844b0d49285817d75316b6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984737"
---
# <a name="datemodified-property-adox"></a>Propriedade DateModified (ADOX)
Indica a data em que o objeto foi modificado pela última vez.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um valor **Variant** que especifica a data de modificação. O valor será NULL se **DateModified** não tiver suporte do provedor.  
  
## <a name="remarks"></a>Comentários  
 A propriedade **DateModified** é nula para objetos acrescentados recentemente. Depois de acrescentar uma nova [exibição](./view-object-adox.md) ou [procedimento](./procedure-object-adox.md), você deve chamar o método [Refresh](../ado-api/refresh-method-ado.md) da coleção [views](./views-collection-adox.md) ou [procedures](./procedures-collection-adox.md) para obter valores para a propriedade **DateModified** .  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Objeto Procedure (ADOX)](./procedure-object-adox.md)  
    :::column-end:::
    :::column:::
        [Objeto Table (ADOX)](./table-object-adox.md)  
    :::column-end:::
    :::column:::
        [Objeto View (ADOX)](./view-object-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades DateCreated e DateModified (VB)](./datecreated-and-datemodified-properties-example-vb.md)   
 [Propriedade DateCreated (ADOX)](./datecreated-property-adox.md)