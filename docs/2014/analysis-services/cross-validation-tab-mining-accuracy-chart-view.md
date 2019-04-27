---
title: Guia validação cruzada (exibição de gráfico de precisão de mineração) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.accuracychart.crossvalidation.f1
ms.assetid: bd215a68-1ad7-4046-9c44-ec8e2be13a64
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d49e80d01a83f2ffad43178fa987010cd4f76b01
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62679744"
---
# <a name="cross-validation-tab-mining-accuracy-chart-view"></a>Guia da validação cruzada (Exibição do gráfico de precisão de mineração)
  A validação cruzada permite dividir uma estrutura de mineração em seções cruzadas e interativamente treinar e testar modelos com cada seção cruzada. Você especifica um número de partições para dividir e colocar os dados; cada partição, por sua vez, é usada como dados de teste, enquanto os dados restantes são usados para treinar o novo modelo. O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] gera um conjunto de métricas de precisão padrão para cada modelo. Comparando as métricas dos modelos geradas para cada seção cruzada, é possível obter uma boa noção da confiabilidade do modelo em relação a todo conjunto de dados.  
  
 Para obter mais informações, consulte [Cross-Validation &#40;Analysis Services - Data Mining&#41;](data-mining/cross-validation-analysis-services-data-mining.md).  
  
> [!NOTE]  
>  A validação cruzada não pode ser usada com modelos que foram criados usando os algoritmos [!INCLUDE[msCoName](../includes/msconame-md.md)] MTS ou o [!INCLUDE[msCoName](../includes/msconame-md.md)] MSC. Se você executar o relatório em uma estrutura de mineração que contenha estes tipos de modelos, os modelos não serão incluídos no relatório.  
  
## <a name="task-list"></a>Lista de Tarefas  
  
-   Especificar o número de dobras.  
  
-   Especificar o número máximo de casos para usar para validação cruzada.  
  
-   Especificar a coluna previsível.  
  
-   Opcionalmente, especificar um estado previsível.  
  
-   Opcionalmente, ajuste os parâmetros que controlam como a exatidão da previsão é avaliada.  
  
-   Clique em **Obter Resultados** para exibir os resultados de validação cruzada.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Número de partições**  
 Especifique o número de dobras ou partições para criar. O valor mínimo é 2, significando que a metade do conjunto de dados é usada para testar e metade para treinar.  
  
 O valor máximo é 10 para estruturas de mineração da sessão.  
  
 O valor máximo será 256 se a estrutura de mineração for armazenada em uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
> [!NOTE]  
>  À medida que você aumenta o número de partições, o tempo necessário para realizar a validação cruzada também aumenta em n. Você poderá enfrentar problemas de desempenho se o número de casos for grande e o valor de **Número de Partições** também for alto.  
  
 **Máx. de casos**  
 Especificar o número máximo de casos para usar para validação cruzada. O número de casos em qualquer dobra em particular é igual ao valor de **Máx. de Casos** dividido pelo valor de **Número de Partições** .  
  
 Se você usar **0**, todas os casos nos dados de origem serão usados para validação cruzada.  
  
 Não há valor padrão.  
  
> [!NOTE]  
>  Ao aumentar o número de casos, o tempo de processamento também aumentara.  
  
 **Atributo de destino**  
 Selecione uma coluna da lista de colunas previsíveis encontradas em todos os modelos. Você só pode selecionar uma coluna previsível toda vez que executar a validação cruzada.  
  
 Para testar somente modelos de clustering, selecione **Cluster**.  
  
 **Estado de destino**  
 Digite um valor ou selecione um valor de destino de uma listagem suspensa de valores.  
  
 O valor padrão é `null`, indicando que todos os estados serão testados.  
  
 Desabilitado para modelos de clustering.  
  
 **Limite**  **de Destino**  
 Especifique um valor entre 0 e 1 que indica a condição acima do estado previsível em que a probabilidade da previsão é considerada para estar correta. O valor pode ser definido em acréscimos de 0,1.  
  
 O padrão é `null`, indicando que a previsão mais provável é contada como correta.  
  
> [!NOTE]  
>  Embora você possa definir o valor como 0,0, usando este valor ira aumentar o tempo de processamento sem resultados significativos de rendimento.  
  
 **Obter resultados**  
 Clique para começar a validação cruzada do modelo usando os parâmetros especificados.  
  
 O modelo é dividido no número especificado de dobras e um modelo separado é testado para cada dobra. Portanto, pode levar algum tempo para a validação cruzada retornar os resultados.  
  
 Para obter mais informações sobre como interpretar os resultados do relatório de validação cruzada, consulte [Medidas no relatório de validação cruzada](data-mining/measures-in-the-cross-validation-report.md).  
  
## <a name="setting-the-accuracy-threshold"></a>Definir o limite de precisão  
 Você pode controlar o padrão para medir a precisão da previsão definindo um valor para **Limite** **de Destino**. Um limite representa um tipo de barra de precisão. Para cada previsão é atribuída uma probabilidade de que o valor previsto está correto. Portanto, ao definir o valor **Limite** **de Destino** próximo de 1, você está requerendo que a probabilidade de qualquer predição em particular seja razoavelmente alta para ser considerada como uma boa previsão. Por outro lado, se você definir o **Limite** **de Destino** próximo de 0, mesmo as previsões com baixos valores de probabilidade serão contadas como “boas”.  
  
 Não existe um valor de limite recomendado porque a probabilidade de qualquer previsão depende da quantidade de dados e do tipo de previsão que você esta fazendo. Você deve analisar algumas previsões a níveis de probabilidades diferentes para determinar uma barra de precisão apropriada para seus dados. É importante que se faça isto, porque o valor que você define para o **Limite** **de Destino** afeta a precisão medida do modelo.  
  
 Por exemplo, suponha que três previsões são feitas para um determinado estado de destino, e as probabilidades de cada previsão são 0,05, 0,15 e 0,8. Se você definir o limite de 0,5, só uma previsão será contada como estando correta. Se você definir o **Limite** **do Destino** como 0,10, serão contadas duas previsões como estando corretas.  
  
 Quando **alvo** **limite** está definido como `null`, que é o valor padrão, a previsão mais provável para cada caso é contada como correta. No exemplo a pouco citado, 0,05, 0,15 e 0,8 são as probabilidades para previsões em três casos diferentes. Embora as probabilidades sejam muito diferentes, cada previsão será contada como correta, porque cada caso gera somente uma previsão e essas são as melhores previsões para esses casos.  
  
## <a name="see-also"></a>Consulte também  
 [Teste e validação &#40;Mineração de dados&#41;](data-mining/testing-and-validation-data-mining.md)   
 [Validação cruzada &#40;Analysis Services – Data Mining&#41;](data-mining/cross-validation-analysis-services-data-mining.md)   
 [Medidas no relatório de validação cruzada](data-mining/measures-in-the-cross-validation-report.md)   
 [Procedimentos armazenados da mineração de dados &#40;Analysis Services – Mineração de dados&#41;](/sql/analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining)  
  
  
