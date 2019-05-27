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
manager: craigg
ms.openlocfilehash: dc620811209d854af5a9c874956847236819f462
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66081053"
---
# <a name="forecast-table-analysis-tools-for-excel"></a>Previsão (Ferramentas de Análise de Tabela para Excel)
  ![Botão previsão na análise de tabela da faixa de opções de ferramentas](media/tat-forecast.gif "botão previsão na faixa de opções de ferramentas de análise de tabela")  
  
 O **previsão** ferramenta ajuda você a fazer previsões com base nos dados em uma tabela de dados do Excel ou outra fonte de dados e, opcionalmente, exibir as probabilidades associadas a cada valor previsto. Por exemplo, se os dados contiverem uma coluna de data e uma coluna que mostre o total de vendas de cada dia do mês, você poderá prever as vendas dos dias futuros. Também é possível especificar o número de previsões a serem feitas. Por exemplo, você pode prever cinco ou trinta dias.  
  
 Quando a ferramenta for concluída, ela anexará as novas previsões ao final da tabela da fonte de dados e realçará os novos valores. Novos valores de série temporal não são anexados; isso lhe permite examinar as previsões primeiro.  
  
 A ferramenta também cria uma nova planilha denominada **relatório de previsão**. Esta planilha reporta se o assistente criou a previsão com êxito. A nova planilha também contém um gráfico de linha que mostra as tendências históricas.  
  
 Quando você estende a série temporal para incluir as novas previsões, os valores previstos são adicionados ao gráfico de linha. Os valores históricos são mostrados como uma linha sólida e as previsões são mostradas como uma linha pontilhada.  
  
## <a name="using-the-forecast-tool"></a>Usando a ferramenta Previsão  
  
1.  Abra uma tabela do Excel que contenha dados numéricos previsíveis.  
  
2.  Clique em **previsão** sobre o **analisar** guia.  
  
3.  Especifique as colunas a serem previstas. A ferramenta seleciona automaticamente colunas nos dados que têm um tipo de dados previsível-ou seja, dados numéricos contínuos. Talvez a ferramenta não selecione algumas colunas que tenham dados numéricos contínuos caso elas contenham muitos valores de zero ou nulos, porque os dados ausentes podem afetar os resultados. Se isso acontecer, você poderá corrigir os dados usando o [rotular novamente &#40;SQL Server Data Mining Add-ins&#41; ](relabel-sql-server-data-mining-add-ins.md) ferramenta.  
  
4.  Especifique a coluna que contém um identificador de data, tempo ou outra série. Se você selecionar a opção  **\<nenhum carimbo de data / hora >** a ferramenta criará uma série com base na sequência de linhas na fonte de dados.  
  
5.  Especifique o número de previsões a serem feitas.  
  
6.  Se desejar, forneça uma dica ao algoritmo para informar se você espera que os dados sejam repetidos semanalmente, mensalmente ou em outros períodos. Se seus dados não se ajusta a qualquer um dos padrões determinados ou se você estiver ciente de nenhum padrão, selecione  **\<detectar automaticamente >** para que a ferramenta Encontre os períodos de tempo de repetição.  
  
7.  O assistente adiciona as previsões à tabela de origem e cria um relatório de previsão em uma nova planilha.  
  
8.  Para adicionar os novos valores ao gráfico de previsão, estenda a série temporal para incluir os valores previstos.  
  
### <a name="requirements"></a>Requisitos  
 As colunas previstas devem conter dados numéricos contínuos, como moeda ou outros números.  
  
 Se possível, os dados também devem incluir uma coluna que contenha uma série de horários ou datas. Você pode usar uma série numérica (1,2, 3...) em vez de dados de data e hora. No entanto, os valores na coluna da série devem ser exclusivos. Ocorrerá um erro se o **previsão** ferramenta encontrar valores duplicados na coluna da série.  
  
 Você não pode prever uma data usando o **previsão** ferramenta. Embora talvez não ocorra um erro, esse algoritmo não foi projetado para usar datas como valores previsíveis.  
  
### <a name="understanding-time-stamps"></a>Entendendo carimbos de data/hora  
 Você deve identificar uma coluna a ser usado como um *carimbo de data / hora*. O carimbo de data/hora serve para duas finalidades. Primeiro, identifica exclusivamente um valor em uma série temporal. Por exemplo, se você estiver rastreando vendas diariamente, deverá ter apenas um valor de vendas para cada dia. A data do calendário poderá ser usada como carimbo de data/hora. Segundo, a coluna de carimbo de data/hora indica a unidade para realização de previsões. Se você estiver rastreando vendas diárias, suas previsões também serão feitas em unidades de dias.  
  
 Se os dados não incluírem uma coluna de data ou hora, a ferramenta criará automaticamente uma chave de série temporal, denominada _RowIndex. A chave será baseada na ordem das linhas no conjunto de dados.  
  
 Quando você especificar o número de previsões, digite um número inteiro que indique a contagem de etapas. As unidades dessas etapas dependerão das unidades usadas nas séries temporal e de data nos seus dados. Se os dados listarem resultados de vendas por mês, a previsão será feita para uma série de meses. Não será possível alterar as unidades de tempo, a menos que você altere os dados de origem.  
  
### <a name="understanding-periodicity"></a>Entendendo a periodicidade  
 Uma previsão se baseia na repetição de padrões durante um período de tempo. Assim, o algoritmo MTS executa cálculos para determinar os períodos de tempo que têm os padrões mais intensos. *Periodicidade* refere-se a esses períodos de tempo.  
  
 Uma série temporal pode conter vários padrões potenciais. Se você tiver certeza de que os dados contêm um certo padrão, talvez possa melhorar a qualidade da previsão fornecendo uma dica ao algoritmo.  
  
 Por exemplo, se você esperar que os dados se repitam semanalmente, selecione Semanalmente para indicar que o algoritmo deve procurar padrões semanais. No entanto, se nenhum padrão semanal intenso for encontrado, o algoritmo ignorará a dica.  
  
## <a name="understanding-the-forecasting-report"></a>Compreendendo o relatório de previsão  
 Neste gráfico, os valores históricos da tabela de dados aparecem como uma linha escura. Os valores previstos aparecem como linhas pontilhadas. Você pode clicar em um ponto na linha para visualizar o valor previsto.  
  
> [!NOTE]  
>  Se você não vir rótulos no eixo de tempo para os valores previstos no gráfico, abra a planilha que contém os valores previstos e use o **preencher, série** função no Excel para estender a coluna de carimbo de data / hora para incluir o previsto valores.  
  
 Em alguns casos, talvez a previsão não tenha o número necessário de frações de tempo. Em geral, isso significa que os dados não eram suficientes para permitir ao algoritmo prever tão adiante no futuro. O **previsão** ferramenta somente fará previsões que cumpram um limite de probabilidade mínima.  
  
## <a name="related-tools"></a>Ferramentas relacionadas  
 O Cliente de Mineração de Dados para Excel, um suplemento separado que fornece funções de mineração de dados mais avançadas, também contém um assistente para previsão.  
  
 Os dois o **previsão** ferramenta (em ferramentas de análise de tabela para Excel) e o **previsão** uso do assistente (no cliente mineração de dados para Excel) o [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo MTS.  
  
-   O **previsão** ferramenta é mais fácil de usar porque configura automaticamente o algoritmo para usar as configurações que são melhores para seus dados.  
  
-   O **previsão** assistente no cliente de mineração de dados para Excel oferece a capacidade de personalizar os parâmetros.  
  
 Para obter mais informações sobre o **previsão** assistente, consulte [Assistente de previsão de &#40;Data Mining Add-ins para Excel&#41;](forecast-wizard-data-mining-add-ins-for-excel.md). Para obter mais informações sobre o algoritmo usado para previsão, consulte o tópico "Algoritmo MTS" nos Manuais Online do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas de Análise de Tabela para Excel](table-analysis-tools-for-excel.md)  
  
  
