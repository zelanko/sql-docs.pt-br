---
title: "Escolher um tipo de gr&#225;fico de precis&#227;o e definir op&#231;&#245;es de gr&#225;fico | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Gráfico de precisão de mineração [Analysis Services]"
  - "modelos de mineração [Analysis Services], validando"
  - "precisão de classificação [mineração de dados]"
  - "teste de precisão [mineração de dados]"
ms.assetid: bd24dd4a-624f-478a-9c94-b1361e857680
caps.latest.revision: 24
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 24
---
# Escolher um tipo de gr&#225;fico de precis&#227;o e definir op&#231;&#245;es de gr&#225;fico
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornece vários métodos para determinar a validade de seus modelos de mineração. O tipo de gráfico de precisão que você pode criar para cada modelo ou estrutura depende destes fatores:  
  
-   O tipo de algoritmo que foi usado na criação do modelo  
  
-   O tipo de dados do atributo previsível.  
  
-   O número de atributos previsíveis para medir  
  
 Este tópico fornece uma visão geral dos diferentes gráficos de precisão.  
  
 **Observação** os gráficos e suas definição não são salvos. Se você fechar a janela que contém um gráfico, terá que criá-lo novamente.  
  
## Tipos de gráfico de precisão  
 Dependendo do tipo de gráfico escolhido, você tem a possibilidade de configurar mais as opções, navegar pelo gráfico, copiar o gráfico na área de transferência e trabalhar com os dados no Excel.  
  
#### Gráfico de comparação de precisão  
 Depois de configurar as opções para os modelos e os dados de teste, clique na guia **Gráfico de Comparação de Precisão** para exibir os resultados. Você também pode copiar o gráfico na área de transferência ou exibir os detalhes das linhas de tendência individuais ou pontos de dados na Legenda de Mineração.  
  
#### Gráfico de ganho  
 Depois de configurar as opções para os modelos e os dados de teste, clique na guia **Gráfico de Comparação de Precisão**, selecione **Gráfico de Ganho** na lista **Tipo de Gráfico** para definir as opções do gráfico de ganho e, em seguida, clique em **OK** para exibir os resultados.  
  
 Você pode usar a caixa de diálogo **Configurações do Gráfico de Ganho** quantas vezes desejar para testar diferentes opções de custo e exibir novamente o gráfico. O Legenda de Mineração contém informações detalhadas sobre o ganho estimado para cada modelo. Você também pode copiar o gráfico e seus conteúdo da Legenda de Mineração para a área de transferência para trabalhar com eles no Excel.  
  
#### Dispersão  
 Se tiver selecionado o tipo de modelo apropriado, ao clicar na guia **Gráfico de Comparação de Precisão**, o tipo do gráfico será definido automaticamente como **Dispersão** e uma dispersão será exibida. Não é possível fazer nenhuma configuração adicional. Você também pode copiar o gráfico para a área de transferência e colar o gráfico no Excel ou em outro aplicativo.  
  
#### Matriz de classificação  
 Para obter uma matriz de classificação, use a guia **Seleção de Entrada** para selecionar os modelos e os dados de teste. Depois, clique na guia **Matriz de Classificação** para exibir os resultados.  
  
 Os conteúdos de uma matriz de classificação são os mesmos para todos os tipos de modelo e não podem ser configurados. Você pode copiar os dados no gráfico para a área de transferência e então trabalhar com eles no Excel.  
  
#### Relatório de validação cruzada  
 Para obter um relatório de validação cruzada, depois de selecionar uma estrutura ou um modelo de mineração no Gerenciador de Soluções, clique na guia **Validação Cruzada**, configure as opções relevantes e depois clique em **Obter Resultados** para gerar o relatório. Não é possível fazer nenhuma configuração adicional.  
  
 O formato do relatório de validação cruzada é o mesmo para todos os tipos de modelo e não pode ser configurado. Entretanto, o conteúdo do relatório difere dependendo do tipo de modelo que você está analisando e do tipo de dados do atributo previsível. Também é possível copiar os resultados do relatório para a área de transferência e trabalhar com os dados no Excel.  
  
  