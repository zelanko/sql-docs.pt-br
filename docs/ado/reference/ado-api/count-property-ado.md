---
title: Propriedade Count (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Collection::Count
helpviewer_keywords:
- Count property [ADO]
ms.assetid: da9ccd1f-d402-41a2-940c-45556fc5340d
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2f9ae68eda44e92834ca54613aca0a68afffc979
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="count-property-ado"></a>Propriedade Count (ADO)
Indica o número de objetos em uma coleção.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um **longo** valor.  
  
## <a name="remarks"></a>Remarks  
 Use o **contagem** propriedade para determinar quantos objetos estão em uma determinada coleção.  
  
 Como a numeração de membros de uma coleção começa com zero, você sempre deve codificar loops iniciando com zero membro e terminando com o valor da **contagem** propriedade menos 1. Se você estiver usando o Microsoft Visual Basic e deseja executar um loop através dos membros de uma coleção sem verificar o **contagem** propriedade, use o **para cada um... Próxima** comando.  
  
 Se o **contagem** é zero, não existem objetos na coleção.  
  
## <a name="applies-to"></a>Aplica-se a  
  
||||  
|-|-|-|  
|[Coleção Axes (ADO MD)](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)|[Coleção Columns (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)|[Coleção CubeDefs (ADO MD)](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)|  
|[Coleção Dimensions (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)|[Coleção Errors (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)|[Coleção Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|  
|[Coleção Groups (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)|[Coleção Hierarchies (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)|[Coleção Indexes (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[Coleção Keys (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)|[Coleção Levels (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)|[Coleção Members (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)|  
|[Coleção Parameters (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)|[Coleção Positions (ADO MD)](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)|[Coleção Procedures (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)|  
|[Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)|[Coleção Tables (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)|[Coleção Users (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)|  
|[Coleção Views (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)|||  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de propriedade Count (VB)](../../../ado/reference/ado-api/count-property-example-vb.md)   
 [Exemplo de propriedade Count (VC + +)](../../../ado/reference/ado-api/count-property-example-vc.md)   
 [Método Refresh (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)
