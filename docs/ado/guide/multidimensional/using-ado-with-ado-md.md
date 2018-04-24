---
title: Usando o ADO com ADO MD | Microsoft Docs
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
helpviewer_keywords:
- ADO, using with ADO MD
ms.assetid: cfae435e-2ac3-4312-8c1e-9ca4a74cd875
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4b99d78262909123157cdcd60cc14dc95e9115c0
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="using-ado-with-ado-md"></a>Usando o ADO com ADO MD
ADO e o ADO MD são modelos de objeto relacionado, mas separado. ADO fornece objetos para conectar-se a fontes de dados, executar comandos, recuperando dados de tabela e metadados de esquema em um formato tabular e exibindo informações de erro do provedor. ADO MD fornece objetos para recuperar dados multidimensionais e exibindo metadados do esquema multidimensional.  
  
 Quando você trabalha com um MDP, você pode optar por usar ADO, ADO MD ou com seu aplicativo. Consultando as duas bibliotecas dentro de seu projeto, você terá acesso completo para a funcionalidade fornecida pelo seu MDP.  
  
 É muito útil para os consumidores obter uma exibição tabular bidimensional de um conjunto de dados multidimensional. Você pode fazer isso usando o ADO [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto. Especificar a origem para sua [conjunto de células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) como o ***fonte*** parâmetro para o [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md) método de um **registros**, em vez de como a fonte de um ADO MD **conjunto de células**.  
  
 Ele também pode ser útil exibir os metadados de esquema em uma exibição tabular em vez de como uma hierarquia de objetos. O ADO [OpenSchema](../../../ado/reference/ado-api/openschema-method.md) método no [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto permite que o usuário abrir um **registros** que contém informações de esquema. O ***QueryType*** parâmetro o **OpenSchema** método tem várias [SchemaEnum](../../../ado/reference/ado-api/schemaenum.md) valores relacionadas especificamente aos MDPs. Esses valores são os seguintes:  
  
-   **adSchemaCubes**  
  
-   **adSchemaDimensions**  
  
-   **adSchemaHierarchies**  
  
-   **adSchemaLevels**  
  
-   **adSchemaMeasures**  
  
-   **adSchemaMembers**  
  
 Para usar valores de enumeração do ADO com ADO MD propriedades ou métodos, seu projeto deve fazer referência a bibliotecas o ADO e o ADO MD. Por exemplo, você pode usar o ADO **adState** valores de enumeração com o ADO MD [estado](../../../ado/reference/ado-md-api/state-property-ado-md.md) propriedade. Para obter mais informações sobre como estabelecer referências a bibliotecas, consulte a documentação da sua ferramenta de desenvolvimento.  
  
 Para obter mais informações sobre os objetos do ADO e métodos, consulte o [referência da API ADO](../../../ado/reference/ado-api/ado-api-reference.md).  
  
## <a name="see-also"></a>Consulte também  
 [Modelo de objeto ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (Multidimensional) (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [Visão geral de esquemas Multidimensional e de dados](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [Programando com ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [Manipular dados multidimensionais](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
