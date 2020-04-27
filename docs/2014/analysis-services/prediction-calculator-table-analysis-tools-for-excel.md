---
title: Cálculo de Previsão (ferramentas de análise de tabela para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining model, regression
- Table Analysis tools
- scorecard
- logistic regression
- prediction calculator
ms.assetid: 8bb8c318-e85f-4fd6-b32b-4cdfb13ca1b5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e57aee7142da5c256a213ddd2eb0390a0f3b042a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66070854"
---
# <a name="prediction-calculator-table-analysis-tools-for-excel"></a>Cálculo de Previsão (Ferramentas de Análise de Tabela para Excel)
  ![Ferramenta Cálculo de Previsão](media/tat-predcal.gif "Ferramenta Cálculo de Previsão")  
  
 A ferramenta **cálculo de previsão** ajuda a criar um scorecard que pode ser usado para analisar novos dados e avaliar opções ou riscos. Por exemplo, se você tiver dados históricos e demográficos sobre os clientes, a ferramenta **cálculo de previsão** poderá ajudá-lo com duas tarefas principais:  
  
-   Gerar uma análise subjacente da demografia, do comportamento de compra e de vários outros fatores.  
  
-   Criar um scorecard de trabalho que ajude a avaliar os membros e fazer as recomendações para ofertas de novos produtos ou serviços.  
  
 O assistente também cria uma planilha que armazena todos os cálculos subjacentes, para que você possa interagir com o modelo e ver como valores de entrada diferentes afetam a pontuação final.  
  
 Se você quiser, o assistente também poderá criar uma versão impressa da planilha que poderá ser usada para pontuação offline. Não é possível interagir com o modelo como você faz com a pasta de trabalho online do Excel, mas a versão impressa fornece todos os cálculos necessários para inserir valores e calcular uma pontuação final.  
  
## <a name="using-the-prediction-calculator-tool"></a>Usando a ferramenta Cálculo de Previsão  
  
1.  Abra uma tabela do Excel que contenha os dados que você deseja analisar.  
  
2.  Clique **cálculo de previsão** na guia **analisar** .  
  
3.  Na caixa de diálogo **cálculo de previsão** , para destino, escolha a coluna que você deseja prever, como comportamento de compra.  
  
4.  Especifique o valor de destino. Se o valor for numérico, use a opção **no intervalo**e, em seguida, digite os valores mínimo e máximo para o intervalo desejado. Se o valor for discreto, selecione a opção **exatamente** e, em seguida, selecione o valor na lista suspensa.  
  
5.  Clique em **escolher colunas para usar para análise**.  
  
6.  Na caixa de diálogo **seleção de coluna avançada** , selecione as colunas que têm informações úteis. Remova as colunas que não forem relevantes para a análise. Clique em **OK**.  
  
     Para não prejudicar os resultados, você também deve remover colunas que tenham informações duplicadas. Por exemplo, se houver uma coluna Entrada que contenha dados numéricos, e uma coluna Grupo de Entrada que contenha os rótulos Alto, Médio e Baixo, não inclua as duas colunas no mesmo modelo. Crie um modelo separado para cada coluna.  
  
7.  Na seção **Opções de saída** , selecione **calculadora operacional** para criar a análise e o Scorecard em uma pasta de trabalho do Excel. Selecione **calculadora pronta para impressão** para criar a análise e gerar também um relatório que pode ser impresso e usado para classificação manual.  
  
8.  Clique em **Executar**.  
  
     A ferramenta cria novas planilhas que contêm os relatórios e os scorecards.  
  
### <a name="requirements"></a>Requisitos  
 A ferramenta de **cálculo de previsão** usa o algoritmo regressão logística da Microsoft, que pode funcionar com valores discretos, bem como discretizado e dados numéricos contínuos.  
  
## <a name="understanding-the-scoring-reports"></a>Compreendendo os relatórios de pontuação  
 Se você selecionar opções de saída, o Cálculo de Previsão criará as seguintes planilhas novas na pasta de trabalho atual:  
  
-   Um **relatório de previsão**que contém os resultados da análise, completo com tabelas interativas e grafos que ajudam você a experimentar interações e lucros.  
  
-   Um **cálculo de previsão** interativo que ajuda a criar pontuações.  
  
-   Uma **calculadora imprimível** com instruções e coeficientes a serem usadas na pontuação.  
  
-   Esta seção descreve as informações em cada relatório e como usar as várias opções de relatório.  
  
### <a name="prediction-report-with-graphs"></a>Relatório de previsão com elementos gráficos  
 O primeiro relatório de previsão é intitulado **cálculo de previsão relatório para o \<estado de destino> do \<atributo de destino>**. Ele contém uma tabela de fatores derivados da análise, junto com ferramentas para ajudá-lo a avaliar o impacto financeiro de uma determinada análise.  
  
#### <a name="table-for-specifying-costs-and-profits"></a>Tabela para especificar custos e lucros  
 A primeira ferramenta neste relatório, no lado superior esquerdo, é uma tabela na qual é possível especificar os custos e os lucros associados à previsão correta e incorreta de um valor.  Esses custos e lucros são necessários para calcular o limite de pontuação ideal para o cálculo.  
  
|Item|Descrição e exemplo|  
|----------|-----------------------------|  
|Custo do Falso Positivo|Custo de assumir que o modelo previu um resultado positivo corretamente quando na verdade a previsão estava errada.<br /><br /> Por exemplo, o modelo prevê que um cliente comprará algo e, com base nisso, você desenvolve uma campanha voltada para esse cliente. Você pode inserir o custo do atendimento ao cliente aqui.|  
|Custo do Falso Negativo|Custo de assumir que o modelo previu um resultado negativo corretamente quando na verdade a previsão estava errada.<br /><br /> Por exemplo, o modelo pode prever que os clientes mais antigos provavelmente não comprarão uma bicicleta, mas você pode descobrir que o modelo estava distorcido e, por isso, perdeu uma oportunidade de alcançar esses clientes. É possível atribuir aqui um custo à unidade perdida.|  
|Lucro do Verdadeiro Positivo|O lucro de prever corretamente um resultado positivo. Por exemplo, se você buscar os clientes e os resultados de atendimento certos em uma venda, poderá inserir o lucro-por-cliente aqui.|  
|Lucro do Verdadeiro Negativo|O lucro de prever corretamente um resultado negativo.<br /><br /> Por exemplo, se você puder identificar corretamente os clientes que não deverão ser procurados, poderá inserir um número X de custo de publicidade por cliente aqui.|  
  
#### <a name="chart-for-viewing-maximum-profit"></a>Gráfico para exibição do lucro máximo  
 À medida que você insere valores na tabela, os elementos gráficos relacionados são atualizados automaticamente para mostrar o melhor ponto para maximizar o lucro atribuído ao modelo atual. O elemento gráfico de linha à direita desta tabela exibe o lucro para os vários limites de pontuação. O lucro é estimado com o uso dos números de lucro e custo digitados na tabela, com base nas previsões e probabilidades do modelo.  
  
 Por exemplo, se, na tabela superior esquerda, a célula do **limite sugerido para maximizar o lucro** mostrar o valor 500, o gráfico no lado direito mostrará 500 como o ponto mais alto no grafo de linha. Esse valor de 500 significa que, para maximizar os lucros, você deve seguir as 500 recomendações principais do modelo de mineração, ordenado por probabilidade.  
  
#### <a name="table-listing-scores-for-each-attribute-and-value"></a>Pontuações de listagem de tabela para cada atributo e valor  
 A tabela no lado inferior esquerdo do relatório mostra uma análise detalhada dos valores detectados e como cada valor afeta o resultado. Você não pode alterar os valores nesta tabela; eles são exibidos para ajudá-lo a entender a previsão.  
  
 A tabela a seguir mostra um exemplo dos resultados quando o resultado de destino é o de um cliente comprar uma bicicleta. A tabela lista cada coluna de entrada usada no modelo, quer a entrada tenha afetado ou não o modelo. A tabela também listará os valores discretos e os valores discretizados se a coluna de entrada continha dados numéricos contínuos.  
  
 Os valores na coluna **impacto relativo** são probabilidades, representadas como porcentagens. A célula é sombreada para representar visualmente o impacto desse valor nos resultados.  
  
|Atributo|Valor|Impacto relativo|  
|---------------|-----------|---------------------|  
|Estado Civil|Married|0|  
|Estado Civil|Single|71|  
|Gênero|Feminino|13|  
|Gênero|Masculino|0|  
  
 Você pode interpretar esses fatores da seguinte forma:  
  
-   Ser casado não afeta a probabilidade de um cliente comprar uma bicicleta.  
  
-   No entanto, ser solteiro é um indicador sólido (70%) da probabilidade de um cliente comprar uma bicicleta.  
  
-   O sexo do cliente tem apenas um efeito secundário (13%) na previsão do comportamento de compra de bicicleta se o cliente for mulher, e não tem efeito na previsão do comportamento de compra de bicicleta se o cliente for um homem.  
  
#### <a name="chart-of-cumulative-misclassification-cost"></a>Gráfico de custo acumulado da classificação incorreta  
 O gráfico de área no lado inferior direito do relatório mostra o custo acumulado da classificação incorreta para vários limites de pontuação. Este gráfico também usa os números de custo e lucro inseridos para falsos positivos, verdadeiros positivos, falsos negativos e falsos positivos.  
  
 Diferentemente do gráfico na parte superior direita do relatório, que enfatiza a maximização do lucro, esse gráfico incorpora o custo de fazer a previsão errada. Este gráfico é especialmente útil em cenários como de prevenção, nos quais o custo de tomar a decisão errada supera significativamente o custo de prever corretamente.  
  
 Por exemplo, embora o primeiro gráfico sugira que buscar os 500 clientes principais previstos pelo modelo é um modo de maximizar os lucros, talvez você decida após examinar este segundo gráfico que os custos de buscar clientes incorretamente é muito grande e prefira cortar a campanha de marketing nos primeiros 400 clientes.  
  
### <a name="interactive-prediction-calculator"></a>Cálculo de Previsão Interativo  
 A segunda planilha criada pela ferramenta de Cálculo de Previsão é intitulada **cálculo de previsão para \<o estado de destino \<> do atributo de destino>**. Trata-se de uma planilha interativa que você pode usar para calcular pontuações individuais. Como essa planilha usa estatísticas e padrões armazenados no modelo, você pode fazer experiências com valores diferentes e verificar como eles afetam a pontuação prevista. Esse relatório também tem duas seções: uma é interativa e a outra é fornecida como referência.  
  
#### <a name="first-table"></a>Primeira tabela  
 Você pode selecionar ou digitar um novo valor na coluna **valor** da tabela para ver como a alteração do valor afeta a pontuação.  
  
 Por exemplo, se o relatório contiver os valores a seguir, diminua o valor de Carros para 1 e depois para 0 para verificar como isso afeta o comportamento de compra dos clientes. À medida que você altera o valor de **carros** para 0, a previsão na parte inferior muda para verdadeiro.  
  
|Atributo|Valor|Impacto relativo|  
|---------------|-----------|---------------------|  
|Estado Civil|Married|0|  
|Gênero|Masculino|0|  
|Receita|39050-71062|117|  
|Children|0|157|  
|Educação|Bachelors|22|  
|Occupation|Skilled Manual|33|  
|Home Owner|Sim|8|  
|Cars|2|50|  
|Distância do Trabalho|0-1 Miles|99|  
|Região|América do Norte|0|  
|Idade|37-46|5|  
|Total||491|  
|Previsão para 'Sim'||FALSE|  
  
 Quando você digita o novo valor, a pontuação exibida na célula, Previsão para Sim, muda para verdadeiro e as pontuações de **impacto relativo** para os vários atributos também são atualizadas.  
  
> [!NOTE]  
>  Mesmo que você altere apenas um valor, como o número de carros, os valores e os impactos de outros atributos talvez sejam alterados quando isso for feito. Isso ocorre porque os modelos de mineração de dados com frequência encontram relações complexas entre os dados, e alterar qualquer variável pode ter efeitos imprevisíveis. Por isso, é recomendável usar o cálculo de previsão interativa para fazer experiências com valores diferentes ou procurar o modelo de mineração para entender melhor as interações. Para obter mais informações, consulte [procurar modelos](prediction-calculator-table-analysis-tools-for-excel.md).  
  
#### <a name="score-breakdown"></a>Análise da pontuação  
 Esta tabela mostra as pontuações individuais para cada estado possível das colunas de entrada e o impacto relativo que a pontuação terá nos resultados. Esta tabela é estática e apenas para referência.  
  
### <a name="printable-prediction-calculator"></a>Cálculo de Previsão Imprimível  
 A terceira planilha criada pela ferramenta de Cálculo de Previsão é intitulada **PrintablePrediction Calculator para \<o estado de destino \<> do atributo de destino>**. Este scorecard deve ser impresso para que você possa calcular manualmente pontuações quando estiver longe do computador.  
  
##### <a name="to-print-and-use-the-scoring-report-generated-by-the-prediction-calculator"></a>Para imprimir e usar o relatório de pontuação gerado pelo Cálculo de Previsão  
  
1.  Clique na guia que é chamada **de cálculo de previsão imprimível para \<>de atributo **.  
  
2.  No menu arquivo do Excel, selecione **visualização de impressão**.  
  
3.  Altere a orientação da página, as margens e outras opções de impressão até que o scorecard se ajuste à página da maneira desejada.  
  
     Este scorecard não é dinâmico e não está conectado ao modelo de nenhuma forma, portanto, você pode mover colunas ou linhas para melhorar a formatação sem afetar os dados subjacentes.  
  
4.  Imprima o scorecard.  
  
5.  Escolha apenas um valor para cada atributo. Para o valor escolhido, coloque uma marca de seleção na caixa e escreva o número correspondente na coluna **Pontuação** .  
  
6.  Preencha o máximo possível de atributos para assegurar a precisão.  
  
7.  Calcule a soma das pontuações de cada atributo e insira esse número na linha de **total** .  
  
8.  Converta a pontuação em um resultado previsto usando os critérios impressos na planilha imediatamente após a linha de **total** .  
  
## <a name="related-tools"></a>Ferramentas relacionadas  
 O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] fornece o algoritmo Regressão Logística da Microsoft para uso nesse tipo de análise. Se você já estiver familiarizado com a regressão logística, poderá criar facilmente modelos de regressão logística usando a opção **avançada** do cliente de mineração de dados para Excel. Para obter mais informações, consulte [modelagem avançada &#40;suplementos de mineração de dados para Excel&#41;](advanced-modeling-data-mining-add-ins-for-excel.md). Para obter mais informações sobre as opções e parâmetros para modelos de regressão logística, consulte o tópico "algoritmo de regressão logística [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] da Microsoft" nos manuais online do.  
  
## <a name="see-also"></a>Consulte Também  
 [Ferramentas de Análise de Tabela para Excel](table-analysis-tools-for-excel.md)  
  
  
