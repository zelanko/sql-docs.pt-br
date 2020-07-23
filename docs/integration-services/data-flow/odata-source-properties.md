---
title: Propriedades do OData Source | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4fde5bb0-6d78-4ec4-8f0b-67f91c53fe99
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fe4a3c3d1375095a4766186e1b854ea038b54ac9
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86920762"
---
# <a name="odata-source-properties"></a>Propriedades da origem do OData

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


Ao clicar com o botão direito do mouse em **OData Source** no fluxo de dados e clicar em **Propriedades**, você verá as propriedades do componente de **OData Source** na janela **Propriedades**.  

## <a name="properties"></a>Propriedades 

|Propriedade|DESCRIÇÃO|  
|-|-|  
|CollectionName|Nome da coleção que você deseja recuperar do serviço OData. A propriedade **CollectionName** é usada quando **UseResourcePath** é falso.<br /><br /> Esta propriedade pode ser definida via expressão, o que permite que você defina o valor em runtime. No entanto, se os metadados da coleção não corresponderem aos metadados que existiam em tempo de design, um erro de validação ocorrerá, fazendo com que a execução do fluxo de dados falhe.|  
|DefaultStringLength|Este valor especifica o comprimento padrão para as colunas de cadeia de caracteres que não têm nenhum comprimento máximo.<br /><br /> **Padrão:** 4000|  
|Consulta|Os parâmetros de consulta do OData. Esta propriedade pode ser definida via expressão e em runtime.|  
|ResourcePath|Use essa propriedade quando precisar especificar um caminho completo de recurso, em vez de apenas selecionar um nome de coleção. Esta propriedade é usada quando **UseResourcePath** é verdadeiro.|  
|UseResourcePath|Quando definido como verdadeiro, o valor de **ResourcePath** é anexado à URL de base para determinar o local do feed de OData. Quando definido como falso, o valor de **CollectionName** é usado.<br /><br /> **Padrão:** Falso|  
  
## <a name="see-also"></a>Consulte Também
[Origem OData](odata-source.md)
