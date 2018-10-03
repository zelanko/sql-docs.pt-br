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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9249cac94f2e066d0502e16e40656de4e8b8bdc0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47848314"
---
# <a name="odata-source-properties"></a>Propriedades da origem do OData
Ao clicar com o botão direito do mouse em **OData Source** no fluxo de dados e clicar em **Propriedades**, você verá as propriedades do componente de **OData Source** na janela **Propriedades**.  

## <a name="properties"></a>Propriedades 
|Propriedade|Descrição|  
|-|-|  
|CollectionName|Nome da coleção que você deseja recuperar do serviço OData. A propriedade **CollectionName** é usada quando **UseResourcePath** é falso.<br /><br /> Esta propriedade pode ser definida via expressão, o que permite que você defina o valor em tempo de execução. No entanto, se os metadados da coleção não corresponderem aos metadados que existiam em tempo de design, um erro de validação ocorrerá, fazendo com que a execução do fluxo de dados falhe.|  
|DefaultStringLength|Este valor especifica o comprimento padrão para as colunas de cadeia de caracteres que não têm nenhum comprimento máximo.<br /><br /> **Padrão:** 4000|  
|Consulta|Os parâmetros de consulta do OData. Esta propriedade pode ser definida via expressão e em tempo de execução.|  
|ResourcePath|Use essa propriedade quando precisar especificar um caminho completo de recurso, em vez de apenas selecionar um nome de coleção. Esta propriedade é usada quando **UseResourcePath** é verdadeiro.|  
|UseResourcePath|Quando definido como verdadeiro, o valor de **ResourcePath** é anexado à URL de base para determinar o local do feed de OData. Quando definido como falso, o valor de **CollectionName** é usado.<br /><br /> **Padrão:** Falso|  
  
## <a name="see-also"></a>Consulte Também
[Origem OData](odata-source.md)
