---
title: "Programação de modelo de propriedades de cubo - multidimensionais | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
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
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0d22d6fd46939b435cc0a8a6f25268aea0a192d6
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
---
# <a name="cube-properties---multidimensional-model-programming"></a>Programação de modelo de propriedades de cubo - Multidimensional
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Os cubos têm várias propriedades que você pode definir para afetar o comportamento de todo o cubo. Essas propriedades são resumidas na tabela a seguir.  
  
> [!NOTE]  
>  Algumas propriedades são definidas automaticamente na criação do cubo e não podem ser alteradas.  
  
 Para obter mais informações sobre como definir propriedades de cubo, consulte [Designer de cubo &#40; Analysis Services - dados multidimensionais &#41; ](http://msdn.microsoft.com/library/a6692467-da88-4312-8b03-d812f2ae5a96).  
  
|Propriedade|Description|  
|--------------|-----------------|  
|**AggregationPrefix**|Especifica o prefixo comum usado para nomes de agregação.|  
|**Agrupamento**|Especifica o identificador de localidade (LCID) e o sinalizador de comparação, separados por um sublinhado: por exemplo, Latin1_General_C1_AS.|  
|**DefaultMeasure**|Contém uma linguagem MDX que define a medida padrão para o cubo.|  
|**Descrição**|Fornece uma descrição do cubo que pode ser exposta em aplicativos cliente.|  
|**ErrorConfiguration**|Contêm configurações de tratamento de erros que podem ser definidas para tratar chaves duplicadas, chaves desconhecidas, limites de erros, ação devido à detecção de erros, arquivo de log de erros e tratamento de chaves nulas.|  
|**EstimatedRows**|Especifica o número de linhas estimadas no cubo.|  
|**ID**|Contém o identificador exclusivo (ID) do cubo.|  
|**Idioma**|Especifica o identificador de idioma padrão do cubo.|  
|**Nome**|Especifica o nome amigável do cubo.|  
|**ProactiveCaching**|Define configurações de cache pró-ativas para o cubo.|  
|**ProcessingMode**|Indica se a indexação e a agregação devem ocorrer durante ou após o processamento. Opções são **regular** ou **lento**.|  
|**ProcessingPriority**|Determina a prioridade de processamento do cubo durante as operações em segundo plano, como agregações lentas e indexação. O valor padrão é **0**.|  
|**ScriptCacheProcessingMode**|Indica se o cache de script deve ser criado durante ou após o processamento. Opções são **regular** e **lento**.|  
|**ScriptErrorHandlingMode**|Determina o tratamento de erros. Opções são **IgnoreNone** ou **IgnoreAll**|  
|**Origem**|Mostra a exibição da fonte de dados usada para o cubo.|  
|**StorageLocation**|Especifica o local de armazenamento do sistema de arquivos para o cubo. Se nenhum for especificado, o local será herdado do banco de dados que contém o objeto de cubo.|  
|**StorageMode**|Especifica o modo de armazenamento para o cubo. Os valores são **MOLAP**, **ROLAP**, ou **HOLAP**.|  
|**Visível**|Determina a visibilidade do cubo.|  
  
> [!NOTE]  
>  Para obter mais informações sobre como definir valores para a propriedade ErrorConfiguration ao trabalhar com valores nulos e outros problemas de integridade de dados, consulte [Handling Data Integrity Issues in Analysis Services 2005](http://go.microsoft.com/fwlink/?LinkId=81891).  
  
## <a name="see-also"></a>Consulte também  
 [O cache pró-ativo &#40; Partições &#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)  
  
  
