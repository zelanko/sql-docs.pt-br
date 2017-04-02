---
title: "Criar uma dimens&#227;o de tipo de moeda | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "dimensões [Analysis Services], moeda"
  - "moeda [Analysis Services]"
  - "convertendo moeda"
  - "dimensões de moeda [Analysis Services]"
ms.assetid: b1f037d1-ce47-4e47-a1c2-5ec9e781cff6
caps.latest.revision: 16
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Criar uma dimens&#227;o de tipo de moeda
  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], uma dimensão de tipo de moeda é aquela cujos atributos representam uma lista de moedas para uso em relatórios financeiros.  
  
 Uma dimensão de moeda permite a inclusão de recursos de conversão de moeda em um cubo do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para adicionar a conversão de moeda a um cubo, use o Assistente de Business Intelligence para definir um comando de script MDX que converte medidas monetárias nos valores apropriados para a localidade do aplicativo cliente. Para criar esse script MDX, o Assistente de Business Intelligence precisa das seguintes informações:  
  
-   Uma dimensão de moeda que representa as moedas de origem. (Essa dimensão é a dimensão de moeda de origem.)  
  
-   Um grupo de medidas que representa as taxas de câmbio que serão usadas.  
  
 Com essas informações, o Assistente de Business Intelligence criará o processo de conversão de moedas que identificará a dimensão da moeda de destino apropriada (a dimensão de moeda que representa as moedas de destino). Dependendo do número de conversões de moeda que a solução de business intelligence precisar, o Assistente de Business Intelligence pode definir várias dimensões de moeda de destino. Para obter mais informações sobre como definir conversões de moeda, consulte [Conversões de moeda &#40;Analysis Services&#41;](../../analysis-services/currency-conversions-analysis-services.md).  
  
 Para identificar uma dimensão como dimensão de moeda, defina a propriedade **Type** da dimensão como **Currency**.  
  
## Estrutura da Dimensão  
 Uma dimensão de moeda contém, no mínimo, um atributo de chave que identifica cada moeda da tabela de dimensões da dimensão de moeda. O valor do atributo de chave é diferente nas dimensões de moeda de origem e destino:  
  
-   Para identificar um atributo como atributo de chave de uma dimensão de moeda de origem, defina a propriedade **Type** do atributo como **CurrencySource**.  
  
-   Para identificar um atributo como dimensão da moeda de destino, defina a propriedade **Type** do atributo como **CurrencyDestination**.  
  
 Para geração de relatório, tanto a dimensão de moeda de origem como a de destino podem conter, opcionalmente, os seguintes atributos:  
  
-   Um atributo de nome da moeda.  
  
     Para identificar um atributo como nome da moeda, defina a propriedade **Type** do atributo como **CurrencyName**.  
  
-   Um atributo de origem da moeda.  
  
     Para identificar um atributo como atributo de origem da moeda, defina a propriedade **Type** do atributo como **CurrencySource**.  
  
-   Um código de moeda da Organização de Padronização Internacional (ISO).  
  
     Para identificar um atributo como atributo de código ISO da moeda, defina a propriedade **Type** do atributo como **CurrencyIsoCode**.  
  
 Para obter mais informações sobre tipos de atributos, consulte [Configurar tipos de atributo](../../analysis-services/multidimensional-models/configure-attribute-types.md).  
  
## Definindo inteligência de conta com o Assistente de Business Intelligence  
 Depois de configurar a dimensão de conta e adicioná-la a um cubo, você pode usar o Assistente de Business Intelligence para adicionar à dimensão funcionalidades de inteligência de conta, como identificação e mapeamento de tipos de conta. Para obter mais informações, consulte [Adicionar inteligência de conta a uma dimensão](../../analysis-services/multidimensional-models/add-account-intelligence-to-a-dimension.md).  
  
## Consulte também  
 [Atributos e hierarquias de atributos](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Ajuda F1 do Assistente de Business Intelligence](../Topic/Business%20Intelligence%20Wizard%20F1%20Help.md)   
 [Tipos de dimensão](../Topic/Dimension%20Types.md)  
  
  