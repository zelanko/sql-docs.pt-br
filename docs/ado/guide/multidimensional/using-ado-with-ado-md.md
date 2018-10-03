---
title: Usando o ADO com ADO MD | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, using with ADO MD
ms.assetid: cfae435e-2ac3-4312-8c1e-9ca4a74cd875
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 69707e5026497a1f98ab168d71b4e6b286520fbe
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47790414"
---
# <a name="using-ado-with-ado-md"></a>Usar o ADO com ADO MD
ADO e o ADO MD são modelos de objeto relacionado, mas separado. O ADO oferece objetos para se conectar a fontes de dados, execução de comandos, recuperando dados tabulares e metadados de esquema em um formato tabular e exibindo informações de erro do provedor. ADO MD oferece objetos para recuperar dados multidimensionais e exibição de metadados de esquema multidimensional.  
  
 Quando você trabalha com um MDP, você pode optar por usar o ADO, o ADO MD ou ambos com o seu aplicativo. Referenciando as duas bibliotecas dentro de seu projeto, você terá acesso completo à funcionalidade fornecida pelo seu MDP.  
  
 Geralmente é útil para os consumidores obter uma exibição tabular bidimensional de um conjunto de dados multidimensional. Você pode fazer isso usando o ADO [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto. Especificar a origem para seu [conjunto de células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) como o ***fonte*** parâmetro para o [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md) método de um **Recordset**, em vez de como a fonte para um ADO MD **conjunto de células**.  
  
 Ele também pode ser útil exibir os metadados de esquema em uma exibição tabular em vez de uma hierarquia de objetos. O ADO [OpenSchema](../../../ado/reference/ado-api/openschema-method.md) método o [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto permite que o usuário abra um **conjunto de registros** que contém informações de esquema. O ***QueryType*** parâmetro do **OpenSchema** método tem várias [SchemaEnum](../../../ado/reference/ado-api/schemaenum.md) valores relacionados especificamente ao MDPs. Esses valores são da seguinte maneira:  
  
-   **adSchemaCubes**  
  
-   **adSchemaDimensions**  
  
-   **adSchemaHierarchies**  
  
-   **adSchemaLevels**  
  
-   **adSchemaMeasures**  
  
-   **adSchemaMembers**  
  
 Para usar valores de enumeração do ADO com ADO MD propriedades ou métodos, seu projeto deve fazer referência a bibliotecas de ADO e o ADO MD. Por exemplo, você pode usar o ADO **adState** valores de enumeração com o ADO MD [estado](../../../ado/reference/ado-md-api/state-property-ado-md.md) propriedade. Para obter mais informações sobre como estabelecer referências a bibliotecas, consulte a documentação da sua ferramenta de desenvolvimento.  
  
 Para obter mais informações sobre os objetos do ADO e métodos, consulte o [referência da API ADO](../../../ado/reference/ado-api/ado-api-reference.md).  
  
## <a name="see-also"></a>Consulte também  
 [Modelo de objeto do ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (Multidimensional) (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [Visão geral de esquemas Multidimensional e de dados](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [Programando com ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [Manipular dados multidimensionais](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
