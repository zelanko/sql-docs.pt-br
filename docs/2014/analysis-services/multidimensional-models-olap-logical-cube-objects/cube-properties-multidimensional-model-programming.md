---
title: Propriedades do cubo | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- Collation property
- ID property
- ErrorConfiguration property
- cubes [Analysis Services], properties
- Description property
- DefaultMeasure property
- ProcessingMode property
- AggregationPrefix property
- EstimatedRows property
- Visible property
- StorageLocation property
- StorageMode property
- ScriptErrorHandlingMode property
- Source property
- ScriptCacheProcessingMode property
- Language property
- Name property
- properties [Analysis Services], cubes
- ProcessingPriority property
- ProactiveCaching property
ms.assetid: 72ca3387-620d-4473-8e23-7fe1f2b3d5bf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4d2b99362f242ff7f815e9ceb9f67db9c80983c8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62727642"
---
# <a name="cube-properties"></a>Propriedades do cubo
  Os cubos têm várias propriedades que você pode definir para afetar o comportamento de todo o cubo. Essas propriedades são resumidas na tabela a seguir.  
  
> [!NOTE]  
>  Algumas propriedades são definidas automaticamente na criação do cubo e não podem ser alteradas.  
  
 Para obter mais informações sobre como definir propriedades de cubo, consulte [Designer de cubo &#40;Analysis Services&#41;de dados multidimensionais ](../cube-designer-analysis-services-multidimensional-data.md).  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|`AggregationPrefix`|Especifica o prefixo comum usado para nomes de agregação.|  
|`Collation`|Especifica o identificador de localidade (LCID) e o sinalizador de comparação, separados por um sublinhado: por exemplo, Latin1_General_C1_AS.|  
|`DefaultMeasure`|Contém uma linguagem MDX que define a medida padrão para o cubo.|  
|`Description`|Fornece uma descrição do cubo que pode ser exposta em aplicativos cliente.|  
|`ErrorConfiguration`|Contêm configurações de tratamento de erros que podem ser definidas para tratar chaves duplicadas, chaves desconhecidas, limites de erros, ação devido à detecção de erros, arquivo de log de erros e tratamento de chaves nulas.|  
|`EstimatedRows`|Especifica o número de linhas estimadas no cubo.|  
|`ID`|Contém o identificador exclusivo (ID) do cubo.|  
|`Language`|Especifica o identificador de idioma padrão do cubo.|  
|`Name`|Especifica o nome amigável do cubo.|  
|`ProactiveCaching`|Define configurações de cache pró-ativas para o cubo.|  
|`ProcessingMode`|Indica se a indexação e a agregação devem ocorrer durante ou após o processamento. As opções **regular** são regular `lazy`ou.|  
|`ProcessingPriority`|Determina a prioridade de processamento do cubo durante as operações em segundo plano, como agregações lentas e indexação. O valor padrão é **0**.|  
|`ScriptCacheProcessingMode`|Indica se o cache de script deve ser criado durante ou após o processamento. As opções **regular** são regular `lazy`e.|  
|`ScriptErrorHandlingMode`|Determina o tratamento de erros. As opções `IgnoreNone` são ou`IgnoreAll`|  
|`Source`|Mostra a exibição da fonte de dados usada para o cubo.|  
|`StorageLocation`|Especifica o local de armazenamento do sistema de arquivos para o cubo. Se nenhum for especificado, o local será herdado do banco de dados que contém o objeto de cubo.|  
|`StorageMode`|Especifica o modo de armazenamento para o cubo. Os valores `MOLAP`são `ROLAP`, ou`HOLAP``.`|  
|`Visible`|Determina a visibilidade do cubo.|  
  
> [!NOTE]  
>  Para obter mais informações sobre como definir valores para a Propriedade ErrorConfiguration ao trabalhar com valores nulos e outros problemas de integridade de dados, consulte [tratamento de problemas de integridade de dados no Analysis Services 2005](https://go.microsoft.com/fwlink/?LinkId=81891).  
  
## <a name="see-also"></a>Consulte Também  
 [Cache pró-ativo &#40;partições&#41;](partitions-proactive-caching.md)  
  
  
