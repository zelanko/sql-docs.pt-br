---
title: Guia matriz de classificação (exibição de gráfico de precisão de mineração) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.accuracychart.confusionmatrix.f1
ms.assetid: 85d5a047-d656-41e0-8a31-400271c2a620
caps.latest.revision: 22
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 58df3c6d14edb8bfddbd53db0c110475d2a983bd
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37251508"
---
# <a name="classification-matrix-tab-mining-accuracy-chart-view"></a>Guia Matriz de Classificação (Exibição do Gráfico de Precisão de Mineração)
  A guia de **Matriz de Classificação** exibe uma matriz de classificação para cada modelo selecionado na grade de modelos da guia do **Mapeamento de Colunas** . A matriz de classificação só estará disponível se a coluna previsível que for selecionada na guia **Mapeamento de Colunas** não for contínua. Para obter uma descrição mais detalhada da guia **Matriz de Classificação** , consulte [Testing and Validation &#40;Data Mining&#41;](data-mining/testing-and-validation-data-mining.md).  
  
## <a name="options"></a>Opções  
 **Copiar**  
 Copia o conteúdo de cada matriz de classificação para a área de transferência.  
  
 **Contagens de \<modelo > em \< coluna previsível >**  
 Exibe uma matriz de classificação para cada modelo de mineração na estrutura de mineração. A matriz contém as seguintes colunas:  
  
|Valor|Description|  
|-----------|-----------------|  
|**Previsto**|Contém uma linha para cada estado da coluna previsível.|  
|**\<estados > (real)**|Uma coluna para cada estado da coluna previsível. Se o estado da linha e da coluna forem correspondentes, a célula representará o número real de vezes em que o estado aparece no banco de dados. Se não corresponderem, a célula representará o erro da previsão.|  
  
## <a name="see-also"></a>Consulte também  
 [Designer do gráfico de precisão de mineração &#40;mineração de dados&#41;](mining-accuracy-chart-designer-data-mining.md)   
 [Teste e validação de tarefas e instruções &#40;mineração de dados&#41;](data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)   
 [Teste e validação &#40;mineração de dados&#41;](data-mining/testing-and-validation-data-mining.md)  
  
  
