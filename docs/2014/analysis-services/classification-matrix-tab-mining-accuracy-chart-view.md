---
title: Guia matriz de classificação (exibição de gráfico de precisão de mineração) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.accuracychart.confusionmatrix.f1
ms.assetid: 85d5a047-d656-41e0-8a31-400271c2a620
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ca3471a96a2ad171255f488b255deee55f73e2e0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66087945"
---
# <a name="classification-matrix-tab-mining-accuracy-chart-view"></a>Guia Matriz de Classificação (Exibição do Gráfico de Precisão de Mineração)
  A guia **matriz de classificação** exibe uma matriz de classificação para cada modelo selecionado na grade modelos na guia mapeamento de **coluna** . A matriz de classificação só estará disponível se a coluna previsível selecionada na guia **mapeamento de coluna** não for contínua. Para obter uma descrição mais detalhada da guia **Matriz de Classificação** , consulte [Testing and Validation &#40;Data Mining&#41;](data-mining/testing-and-validation-data-mining.md).  
  
## <a name="options"></a>Opções  
 **Copy**  
 Copia o conteúdo de cada matriz de classificação para a área de transferência.  
  
 **Contagens de \<modelo> na \< coluna previsível>**  
 Exibe uma matriz de classificação para cada modelo de mineração na estrutura de mineração. A matriz contém as seguintes colunas:  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**Previsto**|Contém uma linha para cada estado da coluna previsível.|  
|**\<> de Estados (real)**|Uma coluna para cada estado da coluna previsível. Se o estado da linha e da coluna forem correspondentes, a célula representará o número real de vezes em que o estado aparece no banco de dados. Se não corresponderem, a célula representará o erro da previsão.|  
  
## <a name="see-also"></a>Consulte Também  
 [Designer de gráfico de precisão de mineração &#40;mineração de dados&#41;](mining-accuracy-chart-designer-data-mining.md)   
 [Tarefas de teste e validação e instruções &#40;mineração de dados&#41;](data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)   
 [Teste e validação &#40;mineração de dados&#41;](data-mining/testing-and-validation-data-mining.md)  
  
  
