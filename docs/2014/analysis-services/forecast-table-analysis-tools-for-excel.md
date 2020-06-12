---
title: Previsão (ferramentas de análise de tabela para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- forecasting
- mining model, time series
- time series [data mining]
ms.assetid: 22bb0b5e-78f5-484e-883d-2b5985a12749
author: minewiskan
ms.author: owend
ms.openlocfilehash: a08cdf759ad3accd1f3c1405cefff9cde6b5319f
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544471"
---
# <a name="forecast-table-analysis-tools-for-excel"></a>Previsão (Ferramentas de Análise de Tabela para Excel)
  ![Botão Previsão na faixa de opções Ferramentas de Análise de Tabela](media/tat-forecast.gif "Botão Previsão na faixa de opções Ferramentas de Análise de Tabela")  
  
 A ferramenta de **previsão** ajuda você a fazer previsões com base em dados em uma tabela de dados do Excel ou em outra fonte de dados e, opcionalmente, exibir as probabilidades associadas a cada valor previsto. Por exemplo, se os dados contiverem uma coluna de data e uma coluna que mostre o total de vendas de cada dia do mês, você poderá prever as vendas dos dias futuros. Também é possível especificar o número de previsões a serem feitas. Por exemplo, você pode prever cinco ou trinta dias.  
  
 Quando a ferramenta for concluída, ela anexará as novas previsões ao final da tabela da fonte de dados e realçará os novos valores. Novos valores de série temporal não são anexados; isso lhe permite examinar as previsões primeiro.  
  
 A ferramenta também cria uma nova planilha chamada **relatório de previsão**. Esta planilha reporta se o assistente criou a previsão com êxito. A nova planilha também contém um gráfico de linha que mostra as tendências históricas.  
  
 Quando você estende a série temporal para incluir as novas previsões, os valores previstos são adicionados ao gráfico de linha. Os valores históricos são mostrados como uma linha sólida e as previsões são mostradas como uma linha pontilhada.  
  
## <a name="using-the-forecast-tool"></a>Usando a ferramenta Previsão  
  
1.  Abra uma tabela do Excel que contenha dados numéricos previsíveis.  
  
2.  Clique em **previsão** na guia **analisar** .  
  
3.  Especifique as colunas a serem previstas. A ferramenta seleciona automaticamente colunas nos dados que têm um tipo de dados previsível – ou seja, dados numéricos contínuos. Talvez a ferramenta não selecione algumas colunas que tenham dados numéricos contínuos caso elas contenham muitos valores de zero ou nulos, porque os dados ausentes podem afetar os resultados. Se isso acontecer, você poderá corrigir os dados usando a ferramenta [rerotular &#40;SQL Server suplementos de mineração de dados&#41;](relabel-sql-server-data-mining-add-ins.md) .  
  
4.  Especifique a coluna que contém um identificador de data, tempo ou outra série. Se você selecionar a opção, **\<no time stamp>** a ferramenta criará uma série com base na sequência de linhas nos dados de origem.  
  
5.  Especifique o número de previsões a serem feitas.  
  
6.  Se desejar, forneça uma dica ao algoritmo para informar se você espera que os dados sejam repetidos semanalmente, mensalmente ou em outros períodos. Se os dados não couberem em nenhum dos padrões determinados, ou se você não estiver ciente de quaisquer padrões, selecione **\<detect automatically>** para que a ferramenta Localize os períodos de tempo de repetição.  
  
7.  O assistente adiciona as previsões à tabela de origem e cria um relatório de previsão em uma nova planilha.  
  
8.  Para adicionar os novos valores ao gráfico de previsão, estenda a série temporal para incluir os valores previstos.  
  
### <a name="requirements"></a>Requisitos  
 As colunas previstas devem conter dados numéricos contínuos, como moeda ou outros números.  
  
 Se possível, os dados também devem incluir uma coluna que contenha uma série de horários ou datas. Você pode usar uma série numérica (1, 2, 3...) em vez de dados de data e hora. No entanto, os valores na coluna da série devem ser exclusivos. Ocorrerá um erro se a ferramenta de **previsão** encontrar valores duplicados na coluna série.  
  
 Você não pode prever uma data usando a ferramenta de **previsão** . Embora talvez não ocorra um erro, esse algoritmo não foi projetado para usar datas como valores previsíveis.  
  
### <a name="understanding-time-stamps"></a>Entendendo carimbos de data/hora  
 Você deve identificar uma coluna a ser usada como *carimbo de data/hora*. O carimbo de data/hora serve para duas finalidades. Primeiro, identifica exclusivamente um valor em uma série temporal. Por exemplo, se você estiver rastreando vendas diariamente, deverá ter apenas um valor de vendas para cada dia. A data do calendário poderá ser usada como carimbo de data/hora. Segundo, a coluna de carimbo de data/hora indica a unidade para realização de previsões. Se você estiver rastreando vendas diárias, suas previsões também serão feitas em unidades de dias.  
  
 Se os dados não incluírem uma coluna de data ou hora, a ferramenta criará automaticamente uma chave de série temporal, denominada _RowIndex. A chave será baseada na ordem das linhas no conjunto de dados.  
  
 Quando você especificar o número de previsões, digite um número inteiro que indique a contagem de etapas. As unidades dessas etapas dependerão das unidades usadas nas séries temporal e de data nos seus dados. Se os dados listarem resultados de vendas por mês, a previsão será feita para uma série de meses. Não será possível alterar as unidades de tempo, a menos que você altere os dados de origem.  
  
### <a name="understanding-periodicity"></a>Entendendo a periodicidade  
 Uma previsão se baseia na repetição de padrões durante um período de tempo. Assim, o algoritmo MTS executa cálculos para determinar os períodos de tempo que têm os padrões mais intensos. *Periodicidade* refere-se a esses períodos de tempo.  
  
 Uma série temporal pode conter vários padrões potenciais. Se você tiver certeza de que os dados contêm um certo padrão, talvez possa melhorar a qualidade da previsão fornecendo uma dica ao algoritmo.  
  
 Por exemplo, se você esperar que os dados se repitam semanalmente, selecione Semanalmente para indicar que o algoritmo deve procurar padrões semanais. No entanto, se nenhum padrão semanal intenso for encontrado, o algoritmo ignorará a dica.  
  
## <a name="understanding-the-forecasting-report"></a>Compreendendo o relatório de previsão  
 Neste gráfico, os valores históricos da tabela de dados aparecem como uma linha escura. Os valores previstos aparecem como linhas pontilhadas. Você pode clicar em um ponto na linha para visualizar o valor previsto.  
  
> [!NOTE]  
>  Se você não vir rótulos no eixo de tempo para os valores previstos no grafo, abra a planilha que contém os valores previstos e use a função de **série Fill** no Excel para estender a coluna de carimbo de data/hora para incluir os valores previstos.  
  
 Em alguns casos, talvez a previsão não tenha o número necessário de frações de tempo. Em geral, isso significa que os dados não eram suficientes para permitir ao algoritmo prever tão adiante no futuro. A ferramenta de **previsão** fará apenas previsões que atendam a um limite de probabilidade mínimo.  
  
## <a name="related-tools"></a>Ferramentas relacionadas  
 O Cliente de Mineração de Dados para Excel, um suplemento separado que fornece funções de mineração de dados mais avançadas, também contém um assistente para previsão.  
  
 A ferramenta de **previsão** (nas ferramentas de análise de tabela para Excel) e o assistente de **previsão** (no cliente de mineração de dados para Excel) usam o [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo Time Series.  
  
-   A ferramenta de **previsão** é mais fácil de usar porque configura automaticamente o algoritmo para usar as configurações mais adequadas para seus dados.  
  
-   O assistente de **previsão** no cliente de mineração de dados para Excel fornece a capacidade de personalizar os parâmetros.  
  
 Para obter mais informações sobre o assistente de **previsão** , consulte [assistente de previsão &#40;suplementos de mineração de dados para Excel&#41;](forecast-wizard-data-mining-add-ins-for-excel.md). Para obter mais informações sobre o algoritmo usado para previsão, consulte o tópico "Algoritmo MTS" nos Manuais Online do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Ferramentas de Análise de Tabela para Excel](table-analysis-tools-for-excel.md)  
  
  
