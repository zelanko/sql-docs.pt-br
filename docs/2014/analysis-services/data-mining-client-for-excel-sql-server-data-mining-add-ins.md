---
title: Cliente de mineração de dados para Excel (SQL Server Data Mining Add-ins) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Data Mining Client
- wizards
- getting started
ms.assetid: e075e2de-11cc-4f71-9603-0b161bca8a24
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e61ae53ee78574351545109f75cebd88827c404b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62692016"
---
# <a name="data-mining-client-for-excel-sql-server-data-mining-add-ins"></a>Cliente de Mineração de Dados para Excel (Suplementos de Mineração de Dados do SQL Server)
  O Cliente de Mineração de Dados para Excel é um conjunto de ferramentas que permite realizar tarefas comuns de mineração de dados, desde a limpeza de dados até a criação de modelos e de consultas de previsão. Você pode usar dados nas tabelas ou nos intervalos do Excel, ou acessar fontes de dados externas.  
  
 ![DM](media/dm-tabletools.gif "DM")  
  
-   [Trabalhar com dados](#bkmk_Data)  
  
     Carregue os dados no Excel, limpe-os, verifique se há exceções e crie resumos estatísticos. Você também pode executar tipos diferentes de amostragem, criar o perfil dos dados e testar os modelos usando dados externos. O Cliente de Mineração de Dados é a maneira mais fácil de preparar os dados para análise sem scripts complexos ou processos ETL.  
  
-   [Criar modelos e analisar](#bkmk_Model)  
  
     Essas ferramentas oferecem interfaces de assistente a algoritmos de mineração de dados conhecidos e testados empiricamente, incluindo clustering (K-means e EM), análise de associação, análise de séries temporais e árvores de decisão. As opções avançadas de modelagem para cada assistente permitem escolher algoritmos diferentes, como Naïve Bayes ou redes neurais, e personalizar o comportamento como a semente de cluster ou o tamanho de amostragem inicial.  
  
     Todos os algoritmos de mineração de dados são hospedados em uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], oferecendo maior capacidade para a criação de modelos complexos.  
  
-   [Testar, consultar e validar modelos](#bkmk_Validate)  
  
     O Cliente de Mineração de Dados fornece ferramentas padrão do setor para testar modelos, incluindo gráficos de comparação de precisão e validação cruzada. Os assistentes fornecidos facilitam o teste da validade do conjunto de dados e sua precisão. O assistente de consulta cria consultas para usar os modelos para previsão e pontuação.  
  
-   [Modelos de exibição](#bkmk_ViewModels)  
  
     Os gráficos são gerados pela maioria das ferramentas podem ser salvos diretamente no Excel. Use o [procurando modelos no Excel &#40;SQL Server Data Mining Add-ins&#41; ](browsing-models-in-excel-sql-server-data-mining-add-ins.md) ferramenta para explorar os modelos.  
  
-   [Gerenciar, documentar e implantar](#bkmk_UsageMgmt)  
  
     O Cliente de Mineração de Dados para Excel mantém uma conexão ativa com o servidor, para que você possa salvar o modelo de mineração de dados no servidor, para usar em mais testes ou para implantar em um servidor de produção para maior escalabilidade.  
  
##  <a name="bkmk_Data"></a> Trabalhar com dados  
 O **preparação de dados** grupo contém os seguintes assistentes que ajudam você a examinar e limpar dados em preparação para tarefas de mineração de dados. A maioria dos assistentes também permite que você separe dados em conjuntos de treinamento e de testes.  
  
 [Explorar dados &#40;suplementos de mineração de dados do SQL Server&#41;](explore-data-sql-server-data-mining-add-ins.md)  
 Para criar e armazenar modelos, os suplementos dão suporte a estas conexões de dados:  
  
-   Conexão a um servidor [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], para armazenamento e processamento dos modelos.  
  
-   Conexões opcional a fontes de dados externas. Você pode criar seu modelo usando qualquer tipo de dados que possa ser definido como uma fonte de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ou usar apenas os dados que já estejam no Excel.  
  
 [Explorar dados &#40;suplementos de mineração de dados do SQL Server&#41;](explore-data-sql-server-data-mining-add-ins.md)  
 O **explorar dados** assistente o ajudará a entender o tipo e a quantidade de dados na tabela de dados representando graficamente a distribuição e os valores das colunas selecionadas, um de cada vez.  
  
 [Dados de exemplo &#40;suplementos de mineração de dados do SQL Server&#41;](sample-data-sql-server-data-mining-add-ins.md)  
 Criar o tipo certo de dados para treinar e testar seus modelos é uma parte importante da mineração de dados, mas também é uma parte que pode ser tediosa sem as ferramentas corretas. O **dados de exemplo** assistente facilita a divisão dos dados usados para um modelo em dois grupos, um para criar o modelo e outro para testá-lo. Você pode usar amostragem ou sobreamostragem aleatórias.  
  
 [Cálculo de previsão &#40;ferramentas de análise de tabela para Excel&#41;](prediction-calculator-table-analysis-tools-for-excel.md)  
 O **remover exceções** assistente oferece várias ferramentas para identificar e lidar adequadamente com exceções. Mostra para você a distribuição dos valores e a relação das exceções para outros dados, além de permitir que você decida se remove ou altera exceções.  
  
 [Cálculo de previsão &#40;ferramentas de análise de tabela para Excel&#41;](prediction-calculator-table-analysis-tools-for-excel.md)  
 O **rotular novamente** assistente o ajuda a criar novos rótulos para os dados para torná-lo mais fácil de entender os resultados da análise. Por exemplo, você pode renomear um intervalo de dados com um nome mais descritivo ou pode escolher um valor representativo na lista.  
  
##  <a name="bkmk_Model"></a> Criar modelos e analisar  
 As opções de **modelagem de dados** seção da barra de ferramentas lhe permitem derivar padrões dos dados; agrupar linhas de dados com base nos atributos ou explorar associações. Os assistentes na faixa de opções da ferramenta se baseiam nos algoritmos de mineração de dados avançados disponíveis no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Diferentemente de ferramentas semelhantes nas Ferramentas de Análise de Tabela para Excel, esses assistentes lhe permitem personalizar o comportamento do algoritmo e usar várias fontes de dados.  
  
 [Assistente para classificar &#40;Data Mining Add-ins para Excel&#41;](classify-wizard-data-mining-add-ins-for-excel.md)  
 O **classificar** assistente o ajuda a criar um modelo de classificação com base nos dados existentes em uma tabela do Excel, um intervalo do Excel ou uma fonte de dados externa. Um modelo de classificação extrai padrões nos dados que indicam similaridades e o ajudam a fazer previsões com base nos agrupamentos de valores. Por exemplo, um modelo de classificação talvez seja usado para prever o risco com base em padrões de renda ou gastos.  
  
 O **classificar** Assistente suporta o uso desses algoritmos de mineração de dados da Microsoft: Algoritmo de árvores, Regressão logística, Naïve Bayesiana, redes neurais de decisão.  
  
 [Assistente de estimativa &#40;Data Mining Add-ins para Excel&#41;](estimate-wizard-data-mining-add-ins-for-excel.md)  
 O **estimativa** assistente o ajuda a criar um modelo de estimativa. Um modelo de estimativa extrai padrões de dados e usa esses padrões para prever um resultado numérico, como moeda, quantidade de vendas, data ou hora.  
  
 O **estimativa** assistente usa esses algoritmos de mineração de dados da Microsoft: Árvores de decisão, Regressão Linear, Regressão logística e redes neurais.  
  
 [Analisar os influenciadores principais &#40;ferramentas de análise de tabela para Excel&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)  
 O assistente para Cluster ajuda você a criar um modelo de cluster. Um modelo de clustering detecta grupos de linhas que compartilham características semelhantes. Esse assistente é útil para explorar padrões em todos os tipos de dados.  
  
 O **Cluster** assistente usa o algoritmo Microsoft Clustering, que inclui K-means e EME.  
  
 [Assistente para associação &#40;cliente de mineração de dados para Excel&#41;](associate-wizard-data-mining-client-for-excel.md)  
 O **associar** assistente o ajuda a criar um modelo de mineração de dados usando o algoritmo regras de associação da Microsoft, que detecta itens concomitante frequente ou eventos. Esses modelos de associação são particularmente úteis para fazer recomendações.  
  
 O **associar** assistente usa o algoritmo regras de associação da Microsoft.  
  
 [Assistente de previsão &#40;Data Mining Add-ins para Excel&#41;](forecast-wizard-data-mining-add-ins-for-excel.md)  
 O **previsão** assistente o ajuda a prever valores em uma série de tempo. Tipicamente, os dados usados em uma previsão contêm algum tipo de série temporal, um carimbo de data/hora ou alguma ID de sequência, e você os utiliza para derivar padrões para uso em valores de previsões futuras.  
  
 O **previsão** assistente usa o algoritmo Microsoft Time Series.  
  
 [Avançadas de modelagem &#40;Data Mining Add-ins para Excel&#41;](advanced-modeling-data-mining-add-ins-for-excel.md)  
 Já conhece a mineração de dados? Você pode usar o **avançado** opções para criar estruturas de dados e criar modelos usando personalizações não incluídas nas outras ferramentas e assistentes de modelagem de dados.  
  
##  <a name="bkmk_Validate"></a> Testar, consultar e validar modelos  
 Use os assistentes o **precisão e validação** barra de ferramentas para usar testes padrão da indústria para validar a precisão dos modelos de e para avaliar a viabilidade do conjunto de dados para a criação de modelos.  
  
 [Analisar os influenciadores principais &#40;ferramentas de análise de tabela para Excel&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)  
 Avalia o desempenho de um modelo de mineração de dados gerando um gráfico de comparação de precisão ou gráfico de dispersão.  
  
 [Matriz de classificação &#40;suplementos de mineração de dados do SQL Server&#41;](classification-matrix-sql-server-data-mining-add-ins.md)  
 Ajuda você a avaliar o desempenho de um modelo de classificação criando um gráfico que resume previsões precisas e imprecisas feitas pelo modelo.  
  
 [Gráfico de ganho &#40;suplementos de mineração de dados do SQL Server&#41;](profit-chart-sql-server-data-mining-add-ins.md)  
 Ajuda você a entender o impacto de um modelo de mineração de dados colocando em um gráfico a precisão das previsões junto com os custos e os benefícios de executar uma ação com base na previsão.  
  
 [A validação cruzada &#40;suplementos de mineração de dados do SQL Server&#41;](cross-validation-sql-server-data-mining-add-ins.md)  
 Cria um relatório que resume a precisão do modelo em muitos subconjuntos do conjunto de dados, para que você possa determinar a estabilidade do modelo.  
  
 Também é possível usar dados em uma tabela do Excel como entrada para uma consulta de previsão em relação a um modelo de mineração armazenado no servidor.  
  
 [Consulta &#40;suplementos de mineração de dados do SQL Server&#41;](query-sql-server-data-mining-add-ins.md)  
 O **consulta** assistente o ajuda a criar previsões em um modelo de mineração de dados existente.  
  
 [Editor de Consulta Avançada de Mineração de Dados](advanced-data-mining-query-editor.md)  
 Para usuários avançados, essa ferramenta oferece uma interface arrastar e soltar ao DMX. Você pode criar consultas de previsão ou novos modelos com facilidade, sem precisar se preocupar com a sintaxe.  
  
##  <a name="bkmk_ViewModels"></a> Modelos de exibição  
 Os modelos que você cria são abertos automaticamente para procurar. No entanto, você também pode procurar modelos no servidor e gerar novas visualizações. Use o [formas do Visio](viewing-data-mining-models-in-visio-data-mining-add-ins.md) exportar diagramas de modelo para uma tela personalizável.  
  
 [Procurando modelos no Excel &#40;suplementos de mineração de dados do SQL Server&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
 Exiba os modelos que você criou, usando gráficos interativos personalizados para cada tipo de modelo.  
  
 [Documentando modelos de mineração &#40;Data Mining Add-ins para Excel&#41;](documenting-mining-models-data-mining-add-ins-for-excel.md)  
 Esse assistente cria relatórios que oferecem um resumo estatístico do conjunto de dados e dos metadados sobre o modelo, para auxiliar na investigação e na interpretação.  
  
##  <a name="bkmk_UsageMgmt"></a> Gerenciar, documentar e implantar  
 Essas ferramentas ajudam você a se conectar a um servidor de mineração de dados, além de gerenciar e exportar modelos e monitorar a atividade de mineração de dados.  
  
 [Gerenciar modelos de &#40;suplementos de mineração de dados do SQL Server&#41;](manage-models-sql-server-data-mining-add-ins.md)  
 Se você tiver as permissões necessárias, poderá excluir, modificar, renomear ou processar as estruturas e os modelos de mineração existentes, sem sair do Excel.  
  
 [Rastreamento &#40;cliente de mineração de dados para Excel&#41;](trace-data-mining-client-for-excel.md)  
 Clique em **rastreamento** para exibir uma captura contínua da interação entre o cliente do Excel e o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] server. Toda a atividade é armazenada como instruções DMX ou XMLA, para que você possa solucionar problemas da sessão de mineração de dados ou salvar as informações para uso posterior.  
  
 [Conectar a um servidor de mineração de dados](connect-to-a-data-mining-server.md)  
 Para usar o Excel como um cliente de mineração de dados, você deve estabelecer uma conexão com uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. A conexão proporciona acesso ao mecanismo do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Se você tiver permissões, a conexão também lhe permitirá armazenar padrões que você tenha descoberto e modificar objetos de mineração de dados existentes.  
  
 O **conexões** barra de ferramentas fornece assistentes para gerenciar conexões a uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. É necessário definir uma conexão com uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para usar as ferramentas e os algoritmos de mineração de dados. Você pode criar a conexão quando instala o suplemento ou pode adicionar uma conexão depois.  
  
 **Introdução**  
 Clique o **guia de Introdução** botão para iniciar um Assistente de configuração que orienta você durante o processo de criação de uma conexão a uma instância de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]e obter as permissões necessárias para fazer mineração de dados.  
  
 **Ajuda**  
 O **ajudar** menu suspenso fornece links para a Ajuda online, sites da Web e um Assistente de configuração para ajudar você a concluir a instalação e a mineração de dados de início.  
  
 A página Ajuda também vincula a recursos online, incluindo a Ajuda do suplemento e vídeos, demonstrações e amostras adicionais.  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas de análise de tabela para Excel](table-analysis-tools-for-excel.md)   
 [Solução de problemas de diagramas de mineração de dados do Visio &#40;suplementos de mineração de dados do SQL Server&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
