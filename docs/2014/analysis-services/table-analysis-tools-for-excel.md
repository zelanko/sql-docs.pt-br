---
title: Ferramentas de análise de tabela para Excel | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- getting started
ms.assetid: 6d9d1481-18e4-4108-9efa-68152b0940c9
author: minewiskan
ms.author: owend
ms.openlocfilehash: 7c8610fd3ac9ee92d6e08084c48f14298cb3203f
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940187"
---
# <a name="table-analysis-tools-for-excel"></a>Ferramentas de Análise de Tabela para Excel
  As ferramentas de Data Mining na barra de ferramentas de **análise** são a maneira mais fácil de começar a usar o Data Mining. Cada ferramenta analisa automaticamente a distribuição e o tipo de dados, e define os parâmetros para garantir que os resultados sejam válidos. Não é necessário selecionar um algoritmo ou configurar parâmetros complexos.  
  
 ![DM](media/dm-tabletoolsanalyze.gif "DM")  
  
 A faixa de opções de **análise** inclui as seguintes ferramentas:  
  
 [Analisar os influenciadores principais &#40;ferramentas de análise de tabela para Excel&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)  
 Você escolhe uma coluna ou um valor de saída e então o algoritmo analisa todos os dados de saída para identificar os fatores com mais influência no destino. Opcionalmente, você pode criar um relatório que compara quaisquer dois valores, de forma que você possa ver como os influenciadores são alterados.  
  
 A ferramenta **analisar influenciadores principais** usa o algoritmo Bayes simples da Microsoft.  
  
 [Detectar categorias &#40;ferramentas de análise de tabela para Excel&#41;](detect-categories-table-analysis-tools-for-excel.md)  
 Essa ferramenta permite que você adicione qualquer conjunto de dados e aplique clustering para localizar agrupamentos de dados. É útil para encontrar semelhanças e para criar grupos para analisar ainda mais.  
  
 A ferramenta **detectar categorias** usa o algoritmo Microsoft Clustering.  
  
 [Preencha com o exemplo &#40;ferramentas de análise de tabela para Excel&#41;](fill-from-example-table-analysis-tools-for-excel.md)  
 Essa ferramenta ajuda a imputar valores ausentes. Você fornece alguns exemplos de como deverão ser os valores ausentes e a ferramenta cria padrões com base em todos os dados da tabela, e então recomenda novos valores com base em padrões dos dados.  
  
 A ferramenta **preencher com exemplo** usa o algoritmo regressão logística da Microsoft.  
  
 [Previsão de &#40;ferramentas de análise de tabela para Excel&#41;](forecast-table-analysis-tools-for-excel.md)  
 Essa ferramenta obtém dados que são alterados ao longo do tempo e prevê valores futuros.  
  
 A ferramenta de **previsão** usa o algoritmo Microsoft Time Series.  
  
 [Realçar exceções &#40;ferramentas de análise de tabela para Excel&#41;](highlight-exceptions-table-analysis-tools-for-excel.md)  
 Essa ferramenta analisa padrões em uma tabela de dados e localiza linhas e valores que não se ajustam ao padrão. Então, você poderá examiná-los e corrigi-los e executar o modelo novamente, ou sinalizar valores para ação posterior.  
  
 A ferramenta **realçar exceções** usa o algoritmo Microsoft Clustering.  
  
 [Cenário de busca de meta &#40;ferramentas de análise de tabela para Excel&#41;](goal-seek-scenario-table-analysis-tools-for-excel.md)  
 Na ferramenta **meta Seek** , você especifica um valor de destino e a ferramenta identifica os fatores subjacentes que devem ser alterados para atender a esse destino. Por exemplo, se você sabe que deve aumentar a satisfação da chamada em 20%, poderá solicitar ao modelo que preveja os fatores que devem mudar para que essa meta seja produzida.  
  
 A ferramenta **meta Seek** usa o algoritmo regressão logística da Microsoft.  
  
 [Cenário de hipóteses &#40;ferramentas de análise de tabela para Excel&#41;](what-if-scenario-table-analysis-tools-for-excel.md)  
 A ferramenta de **análise** de hipóteses complementa a ferramenta de **meta Seek** . Com essa ferramenta, você inseriu o valor que deseja alterar, e o modelo prevê se essa alteração será suficiente para obtenção do resultado desejado. Por exemplo, você poderia perguntar ao modelo para inferir se a adição de um operador de chamada extra poderia aumentar a satisfação do cliente em um ponto.  
  
 A ferramenta **What-If** usa o algoritmo de regressão logística da Microsoft.  
  
 [Cálculo de Previsão &#40;ferramentas de análise de tabela para Excel&#41;](prediction-calculator-table-analysis-tools-for-excel.md)  
 Essa ferramenta cria um modelo que analisa os fatores que levam ao resultado de meta e, depois, prevê um resultado para todas as novas entradas, com base nas regras de pontuação dos dados. Essa ferramenta também gera uma planilha interativa de tomada de decisão que permite atribuir facilmente uma pontuação às novas entradas. Você também pode criar uma versão impressa da planilha de pontuação para uso offline.  
  
 A ferramenta de **cálculo de previsão** usa o algoritmo regressão logística da Microsoft.  
  
 [Análise de cesta de compras &#40;tabela AnalysisTools para Excel&#41;](shopping-basket-analysis-table-analysistools-for-excel.md)  
 Essa ferramenta identifica os padrões que podem ser usados na venda cruzada ou na venda adicional. Ela identifica grupos de produtos comprados juntos com frequência, além de gerenciar relatórios com base no preço e no custo dos pacotes de produtos relacionados, para ajudar na tomada de decisões.  
  
 A ferramenta não se limita à análise da cesta de compras; é possível aplicá-la a qualquer problema que se preste à análise de associação. Por exemplo, você poderia procurar eventos que ocorrem juntos com frequência, fatores que levam a um diagnóstico ou qualquer outro conjunto de causas e resultados potenciais.  
  
 A ferramenta de **análise de cesta de compras** usa o algoritmo de associação da Microsoft.  
  
## <a name="requirements-for-the-table-analysis-tools-for-excel"></a>Requisitos das Ferramentas de Análise de Tabela para Excel  
 Para usar as Ferramentas de Análise de Tabela para Excel, primeiro você deve criar uma conexão com uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Essa conexão lhe fornece acesso aos algoritmos de mineração de dados da Microsoft que são usados para analisar os dados. Se você não tiver acesso a uma instância do, é recomendável solicitar que o administrador configure uma instância que você possa usar para fazer experiências com a mineração de dados. Para obter mais informações, consulte [conectar-se a dados de origem &#40;cliente de mineração de dados para Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md).  
  
 Para trabalhar com dados utilizando as Ferramentas de Análise de Tabela, você deve converter o intervalo de dados a ser usado em tabelas do Excel.  
  
 Se você não conseguir ver a faixa de quadro de **análise** , tente clicar dentro de uma tabela de dados primeiro. O menu não será ativado até que uma tabela de dados seja selecionada.  
  
## <a name="see-also"></a>Consulte Também  
 [O cliente de mineração de dados para Excel &#40;SQL Server suplementos de mineração de dados&#41;](data-mining-client-for-excel-sql-server-data-mining-add-ins.md)   
 [Solução de problemas de diagramas de mineração de dados do Visio &#40;SQL Server suplementos de mineração de dados&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)   
 [O que está incluído nos Suplementos de Mineração de Dados para o Office](what-s-included-in-the-data-mining-add-ins-for-office.md)  
  
  
