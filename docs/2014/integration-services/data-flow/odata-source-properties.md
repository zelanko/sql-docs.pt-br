---
title: Propriedades do OData Source | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4fde5bb0-6d78-4ec4-8f0b-67f91c53fe99
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 26be406c26c362f1bd7fc5880e7c889fbd450ad6
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84915180"
---
# <a name="odata-source-properties"></a>Propriedades da origem do OData
  Ao clicar com o botão direito do mouse em **Origem OData** no fluxo de dados e clicar em **Propriedades**, você verá as propriedades do componente de **Origem OData** na janela **Propriedades** .  
  
|||  
|-|-|  
|Propriedade|Descrição|  
|CollectionName|Nome da coleção que você deseja recuperar do serviço OData. A propriedade **CollectionName** é usada quando **UseResourcePath** é falso.<br /><br /> Esta propriedade pode receber expressão, permitindo que o valor seja definido em runtime. No entanto, se os metadados da coleção não corresponderem aos metadados usados em tempo de design, um erro de validação ocorrerá, fazendo com que a execução do fluxo de dados falhe.|  
|DefaultStringLength|Este valor especifica o comprimento padrão para as colunas de cadeia de caracteres que não têm nenhum comprimento máximo.<br /><br /> **Padrão:** 4000|  
|Consulta|Os parâmetros de consulta do OData. Esta propriedade pode receber expressão e pode ser definida em runtime.|  
|ResourcePath|Use essa propriedade quando precisar especificar um caminho completo de recurso, em vez de apenas selecionar um nome de coleção. Esta propriedade é usada quando **UseResourcePath** é verdadeiro.|  
|UseResourcePath|Quando definido como verdadeiro, o valor de **ResourcePath** é anexado à URL de base para determinar o local do feed de OData. Quando definido como falso, o valor de **CollectionName** é usado.<br /><br /> **Padrão:** For|  
  
  
