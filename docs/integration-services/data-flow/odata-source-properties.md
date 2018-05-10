---
title: Propriedades do OData Source | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4fde5bb0-6d78-4ec4-8f0b-67f91c53fe99
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6c1035a694f53c274e47a89b45fc7b62022a7b21
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="odata-source-properties"></a>Propriedades da origem do OData
Ao clicar com o botão direito do mouse em **OData Source** no fluxo de dados e clicar em **Propriedades**, você verá as propriedades do componente de **OData Source** na janela **Propriedades**.  

## <a name="properties"></a>Propriedades 
|Propriedade|Description|  
|-|-|  
|CollectionName|Nome da coleção que você deseja recuperar do serviço OData. A propriedade **CollectionName** é usada quando **UseResourcePath** é falso.<br /><br /> Esta propriedade pode ser definida via expressão, o que permite que você defina o valor em tempo de execução. No entanto, se os metadados da coleção não corresponderem aos metadados que existiam em tempo de design, um erro de validação ocorrerá, fazendo com que a execução do fluxo de dados falhe.|  
|DefaultStringLength|Este valor especifica o comprimento padrão para as colunas de cadeia de caracteres que não têm nenhum comprimento máximo.<br /><br /> **Padrão:** 4000|  
|Consulta|Os parâmetros de consulta do OData. Esta propriedade pode ser definida via expressão e em tempo de execução.|  
|ResourcePath|Use essa propriedade quando precisar especificar um caminho completo de recurso, em vez de apenas selecionar um nome de coleção. Esta propriedade é usada quando **UseResourcePath** é verdadeiro.|  
|UseResourcePath|Quando definido como verdadeiro, o valor de **ResourcePath** é anexado à URL de base para determinar o local do feed de OData. Quando definido como falso, o valor de **CollectionName** é usado.<br /><br /> **Padrão:** Falso|  
  
## <a name="see-also"></a>Consulte Também
[Origem OData](odata-source.md)
