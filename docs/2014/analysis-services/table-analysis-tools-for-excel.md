---
title: Ferramentas de análise de tabela para Excel | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- getting started
ms.assetid: 6d9d1481-18e4-4108-9efa-68152b0940c9
caps.latest.revision: 17
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dde976376aa356a0b349e769821b0137eb0be29c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37312336"
---
# <a name="table-analysis-tools-for-excel"></a>Ferramentas de Análise de Tabela para Excel
  As ferramentas de mineração de dados das **analisar** barra de ferramentas são a maneira mais fácil para começar com a mineração de dados. Cada ferramenta analisa automaticamente a distribuição e o tipo de dados, e define os parâmetros para garantir que os resultados sejam válidos. Não é necessário selecionar um algoritmo ou configurar parâmetros complexos.  
  
 ![DM](media/dm-tabletoolsanalyze.gif "DM")  
  
 O **analisar** faixa de opções inclui as seguintes ferramentas:  
  
 [Analisar os influenciadores principais &#40;ferramentas de análise de tabela para Excel&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)  
 Você escolhe uma coluna ou um valor de saída e então o algoritmo analisa todos os dados de saída para identificar os fatores com mais influência no destino. Opcionalmente, você pode criar um relatório que compara quaisquer dois valores, de forma que você possa ver como os influenciadores são alterados.  
  
 O **analisar os influenciadores principais** ferramenta usa o algoritmo Microsoft Naïve Bayes.  
  
 [Detectar categorias &#40;ferramentas de análise de tabela para Excel&#41;](detect-categories-table-analysis-tools-for-excel.md)  
 Essa ferramenta permite que você adicione qualquer conjunto de dados e aplique clustering para localizar agrupamentos de dados. É útil para encontrar semelhanças e para criar grupos para mais análise.  
  
 O **detectar categorias** ferramenta usa o algoritmo Microsoft Clustering.  
  
 [Preencher com base no exemplo &#40;ferramentas de análise de tabela para Excel&#41;](fill-from-example-table-analysis-tools-for-excel.md)  
 Essa ferramenta ajuda a imputar valores ausentes. Você fornece alguns exemplos de como deverão ser os valores ausentes e a ferramenta cria padrões com base em todos os dados da tabela, e então recomenda novos valores com base em padrões dos dados.  
  
 O **preencher do exemplo** ferramenta usa o algoritmo de regressão logística da Microsoft.  
  
 [Previsão &#40;ferramentas de análise de tabela para Excel&#41;](forecast-table-analysis-tools-for-excel.md)  
 Essa ferramenta obtém dados que são alterados ao longo do tempo e prevê valores futuros.  
  
 O **previsão** ferramenta usa o algoritmo Microsoft Time Series.  
  
 [Realçar exceções &#40;ferramentas de análise de tabela para Excel&#41;](highlight-exceptions-table-analysis-tools-for-excel.md)  
 Essa ferramenta analisa padrões em uma tabela de dados e localiza linhas e valores que não se ajustam ao padrão. Então, você poderá examiná-los e corrigi-los e executar o modelo novamente, ou sinalizar valores para ação posterior.  
  
 O **realçar exceções** ferramenta usa o algoritmo Microsoft Clustering.  
  
 [Cenário de metas a atingir &#40;ferramentas de análise de tabela para Excel&#41;](goal-seek-scenario-table-analysis-tools-for-excel.md)  
 No **meta a atingir** ferramenta, você especifica um valor de destino e a ferramenta identificará os fatores subjacentes que devem ser alterados para alcançar a meta. Por exemplo, se você sabe que deve aumentar a satisfação da chamada em 20%, poderá solicitar ao modelo que preveja os fatores que devem mudar para que essa meta seja produzida.  
  
 O **meta a atingir** ferramenta usa o algoritmo de regressão logística da Microsoft.  
  
 [Cenário e-se &#40;ferramentas de análise de tabela para Excel&#41;](what-if-scenario-table-analysis-tools-for-excel.md)  
 O **hipóteses** ferramenta complementa o **meta a atingir** ferramenta. Com essa ferramenta, você inseriu o valor que deseja alterar, e o modelo prevê se essa alteração será suficiente para obtenção do resultado desejado. Por exemplo, você poderia perguntar ao modelo para inferir se a adição de um operador de chamada extra poderia aumentar a satisfação do cliente em um ponto.  
  
 O **hipotética** ferramenta usa o algoritmo de regressão logística da Microsoft.  
  
 [Cálculo de previsão &#40;ferramentas de análise de tabela para Excel&#41;](prediction-calculator-table-analysis-tools-for-excel.md)  
 Essa ferramenta cria um modelo que analisa os fatores que levam ao resultado de meta e, depois, prevê um resultado para todas as novas entradas, com base nas regras de pontuação dos dados. Essa ferramenta também gera uma planilha interativa de tomada de decisão que permite atribuir facilmente uma pontuação às novas entradas. Você também pode criar uma versão impressa da planilha de pontuação para uso offline.  
  
 O **cálculo de previsão** ferramenta usa o algoritmo de regressão logística da Microsoft.  
  
 [Análise da cesta de compras &#40;ferramentas de análise de tabela para Excel&#41;](shopping-basket-analysis-table-analysistools-for-excel.md)  
 Essa ferramenta identifica os padrões que podem ser usados na venda cruzada ou na venda adicional. Ela identifica grupos de produtos comprados juntos com frequência, além de gerenciar relatórios com base no preço e no custo dos pacotes de produtos relacionados, para ajudar na tomada de decisões.  
  
 A ferramenta não se limita à análise da cesta de compras; é possível aplicá-la a qualquer problema que se preste à análise de associação. Por exemplo, você poderia procurar eventos que ocorrem juntos com frequência, fatores que levam a um diagnóstico ou qualquer outro conjunto de causas e resultados potenciais.  
  
 O **análise da cesta de compras** ferramenta usa o algoritmo Microsoft Association.  
  
## <a name="requirements-for-the-table-analysis-tools-for-excel"></a>Requisitos das Ferramentas de Análise de Tabela para Excel  
 Para usar as Ferramentas de Análise de Tabela para Excel, primeiro você deve criar uma conexão com uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Essa conexão lhe fornece acesso aos algoritmos de mineração de dados da Microsoft que são usados para analisar os dados. Se você não tiver acesso a uma instância do, é recomendável solicitar que o administrador configure uma instância que você possa usar para fazer experiências com a mineração de dados. Para obter mais informações, consulte [conectar-se a fonte de dados &#40;cliente de mineração de dados para Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md).  
  
 Para trabalhar com dados utilizando as Ferramentas de Análise de Tabela, você deve converter o intervalo de dados a ser usado em tabelas do Excel.  
  
 Se você não conseguir ver a **analisar** faixa de opções, tente clicar em uma tabela de dados pela primeira vez. O menu não será ativado até que uma tabela de dados seja selecionada.  
  
## <a name="see-also"></a>Consulte também  
 [Cliente de mineração de dados para Excel &#40;suplementos de mineração de dados do SQL Server&#41;](data-mining-client-for-excel-sql-server-data-mining-add-ins.md)   
 [Solução de problemas de diagramas de mineração de dados do Visio &#40;suplementos de mineração de dados do SQL Server&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)   
 [O que está incluído nos Suplementos de Mineração de Dados para o Office](what-s-included-in-the-data-mining-add-ins-for-office.md)  
  
  
