---
title: Propriedade DateCreated (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Table::get_DateCreated
- _Table::DateCreated
- _Table::GetDateCreated
helpviewer_keywords:
- DateCreated property [ADOX]
ms.assetid: 2bf4b00d-045c-444e-8af7-8af6297ed418
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d3b29411e3f1fff9213bdc9bbdfb61c06c78c3e0
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="datecreated-property-adox"></a>Propriedade DateCreated (ADOX)
Indica a data em que o objeto foi criado.  
  
## <a name="return-values"></a>Valores de retorno  
 Retorna um **Variant** valor que especifica a data de criação. O valor será nulo se **DateCreated** não é suportado pelo provedor.  
  
## <a name="remarks"></a>Remarks  
 O **DateCreated** propriedade é nula para objetos recentemente adicionados. Depois de anexar um novo [exibição](../../../ado/reference/adox-api/view-object-adox.md) ou [procedimento](../../../ado/reference/adox-api/procedure-object-adox.md), você deve chamar o [atualizar](../../../ado/reference/ado-api/refresh-method-ado.md) método o [exibições](../../../ado/reference/adox-api/views-collection-adox.md) ou [procedimentos ](../../../ado/reference/adox-api/procedures-collection-adox.md) coleção para obter valores para o **DateCreated** propriedade.  
  
## <a name="applies-to"></a>Aplica-se a  
  
||||  
|-|-|-|  
|[Objeto Procedure (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)|[Objeto Table (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|[Objeto View (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)|  
  
## <a name="see-also"></a>Consulte também  
 [DateCreated e DateModified propriedades exemplo (VB)](../../../ado/reference/adox-api/datecreated-and-datemodified-properties-example-vb.md)   
 [Propriedade DateModified (ADOX)](../../../ado/reference/adox-api/datemodified-property-adox.md)
