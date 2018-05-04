---
title: Escolha um tipo de gráfico de precisão e definir opções de gráfico | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 94116047b98ca0def155f1fad5557857c3a317b0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="choose-an-accuracy-chart-type-and-set-chart-options"></a>Escolher um tipo de gráfico de precisão e definir opções de gráfico
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornece vários métodos para determinar a validade dos modelos de mineração. O tipo de gráfico de precisão que você pode criar para cada modelo ou estrutura depende destes fatores:  
  
-   O tipo de algoritmo que foi usado na criação do modelo  
  
-   O tipo de dados do atributo previsível.  
  
-   O número de atributos previsíveis para medir  
  
 Este tópico fornece uma visão geral dos diferentes gráficos de precisão.  
  
 **Observação** os gráficos e suas definição não são salvos. Se você fechar a janela que contém um gráfico, terá que criá-lo novamente.  
  
## <a name="accuracy-chart-types"></a>Tipos de gráfico de precisão  
 Dependendo do tipo de gráfico escolhido, você tem a possibilidade de configurar mais as opções, navegar pelo gráfico, copiar o gráfico na área de transferência e trabalhar com os dados no Excel.  
  
#### <a name="lift-chart"></a>Gráfico de comparação de precisão  
 Depois de configurar as opções para os modelos e os dados de teste, clique na guia **Gráfico de Comparação de Precisão** para exibir os resultados. Você também pode copiar o gráfico na área de transferência ou exibir os detalhes das linhas de tendência individuais ou pontos de dados na Legenda de Mineração.  
  
#### <a name="profit-chart"></a>Gráfico de ganho  
 Depois de configurar as opções para os modelos e os dados de teste, clique na guia **Gráfico de Comparação de Precisão** , selecione **Gráfico de Ganho** na lista **Tipo de Gráfico** para definir as opções do gráfico de ganho e, em seguida, clique em **OK** para exibir os resultados.  
  
 Você pode usar a caixa de diálogo **Configurações do Gráfico de Ganho** quantas vezes desejar para testar diferentes opções de custo e exibir novamente o gráfico. O Legenda de Mineração contém informações detalhadas sobre o ganho estimado para cada modelo. Você também pode copiar o gráfico e seus conteúdo da Legenda de Mineração para a área de transferência para trabalhar com eles no Excel.  
  
#### <a name="scatter-plot"></a>Dispersão  
 Se tiver selecionado o tipo de modelo apropriado, ao clicar na guia **Gráfico de Comparação de Precisão** , o tipo do gráfico será definido automaticamente como **Dispersão** e uma dispersão será exibida. Não é possível fazer nenhuma configuração adicional. Você também pode copiar o gráfico para a área de transferência e colar o gráfico no Excel ou em outro aplicativo.  
  
#### <a name="classification-matrix"></a>Matriz de classificação  
 Para obter uma matriz de classificação, use a guia **Seleção de Entrada** para selecionar os modelos e os dados de teste. Depois, clique na guia **Matriz de Classificação** para exibir os resultados.  
  
 Os conteúdos de uma matriz de classificação são os mesmos para todos os tipos de modelo e não podem ser configurados. Você pode copiar os dados no gráfico para a área de transferência e então trabalhar com eles no Excel.  
  
#### <a name="cross-validation-report"></a>Relatório de validação cruzada  
 Para obter um relatório de validação cruzada, depois de selecionar uma estrutura ou um modelo de mineração no Gerenciador de Soluções, clique na guia **Validação Cruzada** , configure as opções relevantes e depois clique em **Obter Resultados** para gerar o relatório. Não é possível fazer nenhuma configuração adicional.  
  
 O formato do relatório de validação cruzada é o mesmo para todos os tipos de modelo e não pode ser configurado. Entretanto, o conteúdo do relatório difere dependendo do tipo de modelo que você está analisando e do tipo de dados do atributo previsível. Também é possível copiar os resultados do relatório para a área de transferência e trabalhar com os dados no Excel.  
  
  
