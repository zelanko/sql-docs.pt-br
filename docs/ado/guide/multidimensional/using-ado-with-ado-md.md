---
description: Usar o ADO com ADO MD
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 6314ae9a0682e1c10b1ecd45c8f8d5217e7d6426
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452398"
---
# <a name="using-ado-with-ado-md"></a>Usar o ADO com ADO MD
O ADO e o ADO MD estão relacionados, mas modelos de objeto separados. O ADO fornece objetos para se conectar a fontes de dados, executar comandos, recuperar dados tabulares e metadados de esquema em um formato tabular e exibir informações de erro do provedor. ADO MD fornece objetos para recuperar dados multidimensionais e exibir metadados de esquema multidimensional.  
  
 Ao trabalhar com um MDP, você pode optar por usar o ADO, ADO MD ou ambos com seu aplicativo. Ao referenciar as duas bibliotecas em seu projeto, você terá acesso completo à funcionalidade fornecida pelo seu MDP.  
  
 Geralmente, é útil para os consumidores obter uma exibição de tabela achatada de um conjunto de uma multidimensional. Você pode fazer isso usando o objeto ADO [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) . Especifique a origem de seu [células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) como o parâmetro de ***origem*** para o método [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) de um **conjunto de registros**, em vez de como a origem de um ADO MD **células**.  
  
 Também pode ser útil exibir os metadados do esquema em uma exibição tabular em vez de como uma hierarquia de objetos. O método ADO [OpenSchema](../../../ado/reference/ado-api/openschema-method.md) no objeto [Connection](../../../ado/reference/ado-api/connection-object-ado.md) permite que o usuário abra um **conjunto de registros** que contém informações de esquema. O parâmetro ***QueryType*** do método **OpenSchema** tem vários valores [SchemaEnum](../../../ado/reference/ado-api/schemaenum.md) relacionados especificamente a MDPs. Esses valores são:  
  
-   **adSchemaCubes**  
  
-   **adSchemaDimensions**  
  
-   **adSchemaHierarchies**  
  
-   **adSchemaLevels**  
  
-   **adSchemaMeasures**  
  
-   **adSchemaMembers**  
  
 Para usar valores de enumeração do ADO com ADO MD Propriedades ou métodos, seu projeto deve referenciar as bibliotecas ADO e ADO MD. Por exemplo, você pode usar os valores de enumeração ADO **adState** com a propriedade [State](../../../ado/reference/ado-md-api/state-property-ado-md.md) ADO MD. Para obter mais informações sobre como estabelecer referências a bibliotecas, consulte a documentação da sua ferramenta de desenvolvimento.  
  
 Para obter mais informações sobre os objetos e métodos do ADO, consulte a [referência da API do ADO](../../../ado/reference/ado-api/ado-api-reference.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Modelo de objeto ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (Multidimensional) (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [Visão geral de esquemas multidimensionais e dados](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [Programando com ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [Manipular dados multidimensionais](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
