---
title: Cálculos | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d1da69c09768d7a8cecedd683f629a4837c5e5e8
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34039312"
---
# <a name="calculations"></a>Cálculos 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Depois de importar dados para o modelo, será possível adicionar cálculos para agregar, filtrar, estender, combinar e proteger esses dados. Os modelos tabulares usam o DAX (Data Analysis Expressions), uma linguagem de fórmula para criar cálculos personalizados. Nos modelos de tabela, os cálculos que você cria usando fórmulas DAX são usados em *Colunas Calculadas*, *Medidas*e *Filtros de Linha*.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Noções básicas sobre DAX em modelos de tabela](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md)|Descreve a linguagem de fórmula DAX usada para criar cálculos para colunas calculadas, medidas e filtros de linha em modelos de tabela.|  
|[Compatibilidade de fórmula do DAX no modo DirectQuery](http://msdn.microsoft.com/en-us/981b6a68-434d-4db6-964e-d92f8eb3ee3e)|Descreve as diferenças, lista as funções que não têm suporte no modo DirectQuery e lista as funções com suporte, mas que poderiam retornar resultados diferentes.|  
|[Referência de DAX (Data Analysis Expressions)](http://msdn.microsoft.com/en-us/70a82136-0926-4a91-bcb3-e18e82593b0d)|Esta seção fornece descrições detalhadas de sintaxe DAX, operadores e funções.|  
  
> [!NOTE]  
>  Esta seção não contém tarefas passo a passo para criar cálculos. Como os cálculos são especificados em colunas calculadas, medidas e filtros de linha (em funções), as instruções sobre onde criar fórmulas DAX são fornecidas em tarefas relacionadas a esses recursos. Para obter mais informações, consulte [criar uma coluna calculada](../../analysis-services/tabular-models/ssas-calculated-columns-create-a-calculated-column.md), [criar e gerenciar medidas](../../analysis-services/tabular-models/create-and-manage-measures-ssas-tabular.md), e [criar e gerenciar funções](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md).  
  
> [!NOTE]  
>  Apesar de o DAX também poder ser usado para consultar um modelo de tabela, tópicos desta seção destacam especificamente o uso de fórmulas DAX para criar cálculos.  
  
  
