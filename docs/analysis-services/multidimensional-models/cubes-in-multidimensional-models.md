---
title: Cubos em modelos multidimensionais | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5962889f38043e675b70558e7561bfc3f63b39ce
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209052"
---
# <a name="cubes-in-multidimensional-models"></a>Cubos em modelos multidimensionais
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Um cubo é uma estrutura multidimensional que contém informações para fins analíticos; os principais elementos constituintes de um cubo são dimensões e medidas. As dimensões definem a estrutura do cubo que você usa para fazer divisões, e as medidas fornecem valores numéricos agregados de interesse do usuário final. Como é uma estrutura lógica, um cubo permite a um aplicativo cliente recuperar valores, de medidas, como se estivessem contidos em células no cubo; as células são definidas para cada valor resumido possível. Uma célula, no cubo, é definida pela interseção de membros de dimensão e contém os valores agregados das medidas nessa interseção específica.  
  
## <a name="benefits-of-using-cubes"></a>Benefícios do uso de cubos  
 Um cubo oferece um único local onde todos os dados relacionados são armazenados para análise.  
  
## <a name="components-of-cubes"></a>Componentes de cubos  
 Um cubo é constituído de:  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|Dimensões|[Dimensões em modelos multidimensionais](../../analysis-services/multidimensional-models/dimensions-in-multidimensional-models.md)|  
|Medidas e Grupos de Medidas|[Criar medidas e grupos de medidas em modelos multidimensionais](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md)|  
|Partições|[Partições em modelos multidimensionais](../../analysis-services/multidimensional-models/partitions-in-multidimensional-models.md)|  
|perspectivas|[Perspectivas em modelos multidimensionais](../../analysis-services/multidimensional-models/perspectives-in-multidimensional-models.md)|  
|Hierarquias|[Criar hierarquias definidas pelo usuário](../../analysis-services/multidimensional-models/user-defined-hierarchies-create.md)|  
|Ações|[Ações em modelos multidimensionais](../../analysis-services/multidimensional-models/actions-in-multidimensional-models.md)|  
|KPI (indicadores de desempenho chave)|[Indicadores Chave de Desempenho &#40;KPIs&#41; em Modelos Multidimensionais](../../analysis-services/multidimensional-models/key-performance-indicators-kpis-in-multidimensional-models.md)|  
|Cálculos|[Cálculos em modelos multidimensionais](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)|  
|Translations|[Traduções em modelos multidimensionais &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/translations-in-multidimensional-models-analysis-services.md)|  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Criar um cubo usando o Assistente para Cubos](../../analysis-services/multidimensional-models/create-a-cube-using-the-cube-wizard.md)|Descreve como usar o Assistente para Cubos para definir um cubo, as dimensões, os atributos de dimensão e as hierarquias definidas pelo usuário.|  
|[Criar medidas e grupos de medidas em modelos multidimensionais](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md)|Descreve como definir os grupos de medidas.|  
|[Cálculos em modelos multidimensionais](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)|Descreve como definir e configurar um cálculo em um script MDX.|  
|[Ações em modelos multidimensionais](../../analysis-services/multidimensional-models/actions-in-multidimensional-models.md)|Descreve como definir e configurar uma ação.|  
|[Perspectivas em modelos multidimensionais](../../analysis-services/multidimensional-models/perspectives-in-multidimensional-models.md)|Descreve como definir e configurar uma perspectiva.|  
|[Definindo procedimentos armazenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)|Descreve como trabalhar com procedimentos armazenados.|  
  
  
