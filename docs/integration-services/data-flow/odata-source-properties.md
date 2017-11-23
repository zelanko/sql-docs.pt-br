---
title: Propriedades da fonte OData | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4fde5bb0-6d78-4ec4-8f0b-67f91c53fe99
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ee79d0f1b31963b7d13aa07bf4603246139c3a7c
ms.openlocfilehash: 64e297a37c3b6449551968b5788f8c2c0ddd4ab6
ms.contentlocale: pt-br
ms.lasthandoff: 08/23/2017

---
# <a name="odata-source-properties"></a>Propriedades da origem do OData
Quando você clica **fonte OData** no fluxo de dados e clique em **propriedades**, consulte Propriedades para o **fonte OData** componente no **propriedades** janela.  

## <a name="properties"></a>Propriedades 
|Propriedade|Description|  
|-|-|  
|CollectionName|Nome da coleção para recuperar do serviço OData. A propriedade **CollectionName** é usada quando **UseResourcePath** é falso.<br /><br /> Esta propriedade é expressionable, que permite que você defina o valor em tempo de execução. No entanto, se os metadados da coleção não coincide com os metadados que existiam em tempo de design, um erro de validação ocorrerá, fazendo com que a execução de fluxo de dados falhar.|  
|DefaultStringLength|Este valor especifica o comprimento padrão para as colunas de cadeia de caracteres que não têm nenhum comprimento máximo.<br /><br /> **Padrão:** 4000|  
|Consulta|Os parâmetros de consulta do OData. Essa propriedade é expressionable e pode ser definida em tempo de execução.|  
|ResourcePath|Use essa propriedade quando precisar especificar um caminho completo de recurso, em vez de apenas selecionar um nome de coleção. Esta propriedade é usada quando **UseResourcePath** é verdadeiro.|  
|UseResourcePath|Quando definido como verdadeiro, o valor de **ResourcePath** é anexado à URL de base para determinar o local do feed de OData. Quando definido como falso, o valor de **CollectionName** é usado.<br /><br /> **Padrão:** Falso|  
  
## <a name="see-also"></a>Consulte também
[Origem OData](odata-source.md)

