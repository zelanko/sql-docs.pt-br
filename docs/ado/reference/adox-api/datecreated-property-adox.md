---
description: Propriedade DateCreated (ADOX)
title: Propriedade DateCreated (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Table::get_DateCreated
- _Table::DateCreated
- _Table::GetDateCreated
helpviewer_keywords:
- DateCreated property [ADOX]
ms.assetid: 2bf4b00d-045c-444e-8af7-8af6297ed418
author: rothja
ms.author: jroth
ms.openlocfilehash: 7ae2c0fcfdc164906f0216abb45f98f705de9cd4
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770735"
---
# <a name="datecreated-property-adox"></a>Propriedade DateCreated (ADOX)
Indica a data em que o objeto foi criado.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um valor **Variant** que especifica a data de criação. O valor será NULL se **DateCreated** não for suportado pelo provedor.  
  
## <a name="remarks"></a>Comentários  
 A propriedade **DateCreated** é nula para objetos acrescentados recentemente. Depois de acrescentar uma nova [exibição](./view-object-adox.md) ou [procedimento](./procedure-object-adox.md), você deve chamar o método [Refresh](../ado-api/refresh-method-ado.md) da coleção [views](./views-collection-adox.md) ou [procedures](./procedures-collection-adox.md) para obter valores para a propriedade **DateCreated** .  
  
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
 [Propriedade DateModified (ADOX)](./datemodified-property-adox.md)