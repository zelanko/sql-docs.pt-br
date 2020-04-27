---
title: Validação cruzada (SQL Server suplementos de mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- cross-validation
- partitioning data [data mining]
- mining models, testing
ms.assetid: bf9483b3-4099-41c4-bbc5-da7005e07bcd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0cc3a132792cca8ecdf5a33a2fe4e4d40116c497
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66086646"
---
# <a name="cross-validation-sql-server-data-mining-add-ins"></a>Validação cruzada (Suplementos de Mineração de Dados do SQL Server)
  ![Botão Validação Cruzada, faixa de opções Mineração de Dados](media/dmc-xvalid.gif "Botão Validação Cruzada, faixa de opções Mineração de Dados")  
  
 A validação cruzada é uma ferramenta padrão para análise e é um importante recurso para ajudar a desenvolver e ajustar os modelos de mineração de dados. Use a validação cruzada após criar um modelo de mineração para avaliar a validade do modelo e comparar seus resultados aos de outros modelos de mineração relacionados.  
  
 A validação cruzada consiste em duas fases: treinamento e geração de relatório. Você executará as seguintes etapas:  
  
-   Selecione uma estrutura ou um modelo de mineração de destino.  
  
-   Especifique o valor de destino, se aplicável.  
  
-   Especifique o número de seções cruzadas ou *dobras*para particionar os dados da estrutura.  
  
 Em seguida, o assistente de **validação cruzada** cria um novo modelo em cada uma das dobras, testa o modelo nas outras dobras e, em seguida, relata a precisão do modelo. Após a conclusão, o assistente de **validação cruzada** cria um relatório que mostra as métricas para cada dobra e fornece um resumo do modelo em agregação. Essas informações podem ser usadas para determinar o quão bons são os dados subjacentes de um modelo ou comparar modelos diferentes criados com base nos mesmos dados.  
  
## <a name="using-the-cross-validation-wizard"></a>Usando o assistente de validação cruzada  
 Use a validação cruzada em relação a modelos temporários e modelos armazenados em uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
#### <a name="to-create-a-cross-validation-report"></a>Para criar um relatório de validação cruzada  
  
1.  No grupo de **precisão e validação** da faixa de de **mineração de dados** , clique em **validação cruzada**.  
  
2.  Na caixa de diálogo **selecionar estrutura ou modelo** , selecione uma estrutura de mineração ou modelo de mineração existente. Se você selecionar uma estrutura, o assistente usará a validação cruzada em relação a todos os modelos com base na estrutura que têm o mesmo atributo de previsão. Se você selecionar um modelo, o assistente usará validação cruzada em relação apenas a esse modelo.  
  
3.  Na caixa de diálogo **especificar parâmetros de validação cruzada** , na caixa **contagem de partições** , escolha o número de dobras entre os quais dividir o conjunto de dados. Uma partição é uma seção cruzada de dados selecionada aleatoriamente.  
  
4.  Opcionalmente, defina o número máximo de linhas a serem usadas na validação cruzada digitando um número na caixa de texto **máximo de linhas** .  
  
    > [!NOTE]  
    >  Quanto mais linhas você usar, mais precisos serão os resultados. No entanto, o tempo de processamento também pode aumentar significativamente. O número escolhido depende dos dados, mas em geral, você deve escolher o número mais alto possível sem sacrificar o desempenho. Para melhorar o desempenho, também é possível especificar menos partições.  
  
5.  Selecione uma coluna na lista suspensa **atributo de destino** . A lista exibe apenas as colunas configuradas como atributos previsíveis durante a criação original do modelo. O modelo pode conter vários atributos previsíveis, mas você pode escolher apenas um.  
  
6.  Selecione um valor na lista suspensa **estado de destino** .  
  
     Se a coluna previsível contiver dados numéricos contínuos, essa opção não estará disponível.  
  
7.  Opcionalmente, especifique um valor a ser usado como o **limite de destino** para contar previsões como precisas. Esse valor é expresso como uma probabilidade, que é um número entre 0 e 1, onde 1 é garantia da previsão da precisão, 0 significa que não há nenhuma possibilidade de a previsão estar correta e .5 corresponde a uma previsão aleatória.  
  
     Se a coluna previsível contiver dados numéricos contínuos, essa opção não estará disponível.  
  
8.  Clique em **Concluir**. Uma nova planilha é criada, chamada **validação cruzada**.  
  
    > [!NOTE]  
    >  O Microsoft Excel poderá não responder temporariamente enquanto o modelo estiver sendo particionado em partições e cada partição for testada.  
  
### <a name="requirements"></a>Requisitos  
 Para criar um relatório de validação cruzada, é necessário já ter criado uma estrutura de mineração de dados e os modelos relacionados. O assistente fornece uma caixa de diálogo para ajudá-lo a escolher entre a estrutura e os modelos existentes.  
  
 Se você escolher uma estrutura de mineração com suporte para vários modelos de mineração, e os modelos usarem atributos de previsão diferentes, o assistente de Validação Cruzada testará apenas os modelos que compartilham o mesmo atributo previsível.  
  
 Se você escolher uma estrutura com suporte para modelos de clustering e outros tipos de modelos, os modelos de clustering não serão testados.  
  
## <a name="understanding-cross-validation-results"></a>Entendendo os resultados de validação cruzada  
 Os resultados da validação cruzada são exibidos em uma nova planilha, intitulado **relatório de validação cruzada para \<o nome do atributo>**. A nova planilha contém várias seções: a primeira é um resumo que fornece metadados importantes sobre o modelo testado, para que você possa saber para qual modelo ou estrutura os resultados são.  
  
 A segunda seção no relatório fornece um resumo estatístico que indica o quão bom é o modelo original. Neste resumo, as diferenças entre os modelos criados para cada dobra são analisadas para três medidas principais: *erro de raiz quadrada média*, *erro absoluto médio*e *Pontuação de log*. Essas são medidas estatísticas padrão usadas não só na mineração de dados, como também na maioria dos tipos de análise estatística.  
  
 Para cada uma dessas medidas, o assistente de Validação Cruzada calcula a média e o desvio padrão do modelo como um todo. Isso informa o quão consistente é o modelo durante a previsão em subconjuntos diferentes dos dados. Por exemplo, se o desvio padrão for muito grande, isso indica que os modelos criados para cada partição terão resultados muito diferentes e, portanto, talvez o modelo tenha treinado muito perto de um determinado grupo de dados e não seja aplicável a outros conjuntos de dados.  
  
 A seção a seguir explica as medidas usadas para avaliar os modelos.  
  
### <a name="tests-and-measures"></a>Testes e medidas  
 Além de algumas informações básicas sobre o numero de partições nos dados, e a quantidade de dados em cada partição, a planilha exibe um conjunto de métricas sobre cada modelo, categorizadas por tipo de teste. Por exemplo, a precisão de um modelo de clustering é avaliada por testes diferentes dos que você usaria para um modelo de precisão.  
  
 A tabela a seguir lista os testes e a métrica, com uma explanação sobre o que a métrica significa.  
  
#### <a name="aggregates-and-general-statistical-measures"></a>Medidas estatísticas gerais e agregadas  
 As medidas agregadas fornecidas no relatório indicam como as partições criadas nos dados são diferentes.  
  
-   Desvio padrão e médio  
  
-   Média do desvio da média para uma medida específica, através de todas as partições em um modelo.  
  
#### <a name="classification-passfail"></a>Classificação: aprovado/reprovado  
 Essa medida é usada em modelos de classificação quando você não especifica um valor de destino para o atributo previsível. Por exemplo, se você criar um modelo que preveja várias possibilidades, essa medida informará quão bem o modelo se saiu na previsão de todos os valores possíveis.  
  
 A passagem/falha é calculada pela contagem de casos que atendem às seguintes condições: **Pass** se o estado previsto com a probabilidade mais alta for igual ao estado de entrada e a probabilidade for maior do que o valor especificado para o **limite de estado**; caso contrário, **falha**.  
  
#### <a name="classification-true-or-false-positives-and-negatives"></a>Classificação: verdadeiro ou falsos positivos e negativos  
 Este teste é usado para todos os modelos de classificação que têm um destino especificado. A medida indica como cada caso é classificado em resposta a essas questões: o que o modelo prevê e qual foi o resultado real.  
  
|Medida|Descrição|  
|-------------|-----------------|  
|Verdadeiro positivo|Contagem de casos que atendem estas condições:<br /><br /> Casos que contém o valor de destino.<br /><br /> O modelo previu que o caso contém o valor de destino.|  
|Falso positivo|Contagem de casos que atendem estas condições:<br /><br /> O valor atual é igual ao valor de destino.<br /><br /> O modelo previu que o caso contém o valor de destino.|  
|Verdadeiro negativo|Contagem de casos que atendem estas condições:<br /><br /> Caso não contém o valor de destino.<br /><br /> O modelo previu que o caso não contém o valor de destino.|  
|Falso negativo|Contagem de casos que atendem estas condições:<br /><br /> O valor atual não é igual ao valor de destino.<br /><br /> O modelo previu que o caso não contém o valor de destino.|  
  
#### <a name="lift"></a>Comparação de Precisão  
 A comparação de *precisão* é uma medida associada à probabilidade. Se um resultado for mais provável quando você usar o modelo do que quando fizer uma estimativa aleatória, o modelo será considerado para fornecer uma *elevação positiva*. No entanto, se o modelo fizer previsões que sejam menos prováveis do que a probabilidade aleatória, a pontuação de comparação será *negativa*. Assim, essa métrica indica a quantidade de aperfeiçoamento que pode ser obtida com o uso do modelo, no qual uma pontuação mais alta é melhor.  
  
 A comparação de precisão é calculada como a proporção de probabilidade da previsão atual para a probabilidade marginal nos casos de teste.  
  
#### <a name="log-score"></a>Pontuação de log  
 A *Pontuação de log*, também chamada de *Pontuação de probabilidade de log* para a previsão, representa a proporção entre duas probabilidades, convertida em uma escala logarítmica. Como a probabilidade é representada como uma fração decimal, as pontuações de log são sempre números negativos. Uma pontuação próxima de 0 é melhor.  
  
 Visto que contagens brutas podem ter distribuições muito irregulares ou distorcidas, uma contagem de log é semelhante a uma porcentagem.  
  
#### <a name="root-mean-square-error"></a>Erro de Raiz Quadrada Média  
 *Erro de raiz quadrada média* (RMSE) é um método padrão em estatísticas para observar como os conjuntos de dados diferentes são comparados e suavizar as diferenças que podem ser introduzidas pela escala das entradas.  
  
 RMSE representa o erro médio do valor previsto quando comparado ao valor real. Ele é calculado como a raiz quadrada do erro médio para todos os casos de partição, dividida pelo número de casos na partição, excluindo as linhas com valores ausentes para os atributos de destino.  
  
#### <a name="mean-absolute-error"></a>Erro de Média Absoluta  
 O *erro* de média absoluta é o erro médio do valor previsto para o valor real. Ele é calculado pela obtenção da soma absoluta dos erros e descoberta da média desses erros.  
  
 Esse valor o ajuda a entender o quanto as pontuações variam da média.  
  
#### <a name="case-likelihood"></a>Probabilidade de caso  
 Essa medida é usada apenas para modelos de clustering e indica qual o grau de probabilidade de um novo caso pertencer a um determinado cluster.  
  
 Em modelos de clustering, há dois tipos de associação ao cluster, dependendo do método usado para criação do modelo. Em alguns modelos, com base no algoritmo de médias K, espera-se que um novo caso pertença a apenas um cluster. No entanto, por padrão, o algoritmo Microsoft Clustering usa o método Maximização da Expectativa, que assume que um novo caso pode pertencer a qualquer cluster. Assim, nesses modelos um caso pode ter vários valores `CaseLikelihood`, mas aquele que será reportado por padrão será a probabilidade de o caso pertencer ao cluster que melhor corresponder ao novo caso.  
  
## <a name="see-also"></a>Consulte Também  
 [Validando modelos e usando modelos para previsão &#40;suplementos de mineração de dados para Excel&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)  
  
  
