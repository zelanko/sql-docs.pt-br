---
title: Validação cruzada (SQL Server Data Mining Add-ins) | Microsoft Docs
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
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66086646"
---
# <a name="cross-validation-sql-server-data-mining-add-ins"></a>Validação cruzada (Suplementos de Mineração de Dados do SQL Server)
  ![Botão de validação cruzada, faixa de opções mineração de dados](media/dmc-xvalid.gif "botão validação cruzada, faixa de opções mineração de dados")  
  
 A validação cruzada é uma ferramenta padrão para análise e é um importante recurso para ajudar a desenvolver e ajustar os modelos de mineração de dados. Use a validação cruzada após criar um modelo de mineração para avaliar a validade do modelo e comparar seus resultados aos de outros modelos de mineração relacionados.  
  
 A validação cruzada consiste em duas fases: treinamento e geração de relatório. Você executará as seguintes etapas:  
  
-   Selecione uma estrutura ou um modelo de mineração de destino.  
  
-   Especifique o valor de destino, se aplicável.  
  
-   Especifique o número de seções cruzadas, ou *dobras*, nas qual dividir os dados da estrutura.  
  
 O **validação cruzada** assistente e em seguida, cria um novo modelo em cada uma das partições, testa o modelo nas outras partições e, em seguida, reporta a precisão do modelo. Após a conclusão, o **validação cruzada** assistente cria um relatório que mostra as métricas para cada dobra e fornece um resumo do modelo na agregação. Essas informações podem ser usadas para determinar o quão bons são os dados subjacentes de um modelo ou comparar modelos diferentes criados com base nos mesmos dados.  
  
## <a name="using-the-cross-validation-wizard"></a>Usando o assistente de validação cruzada  
 Use a validação cruzada em relação a modelos temporários e modelos armazenados em uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
#### <a name="to-create-a-cross-validation-report"></a>Para criar um relatório de validação cruzada  
  
1.  No **precisão e validação** grupo da **mineração de dados** faixa de opções, clique em **validação cruzada**.  
  
2.  No **selecionar estrutura ou modelo** caixa de diálogo, selecione uma estrutura de mineração existente ou modelo de mineração. Se você selecionar uma estrutura, o assistente usará a validação cruzada em relação a todos os modelos com base na estrutura que têm o mesmo atributo de previsão. Se você selecionar um modelo, o assistente usará validação cruzada em relação apenas a esse modelo.  
  
3.  No **especificar parâmetros de validação cruzada** na caixa de **número de partições** , escolha o número de partições entre os quais dividir o conjunto de dados. Uma partição é uma seção cruzada de dados selecionada aleatoriamente.  
  
4.  Opcionalmente, defina o número máximo de linhas a serem usadas na validação cruzada digitando um número na **máximo de linhas** caixa de texto.  
  
    > [!NOTE]  
    >  Quanto mais linhas você usar, mais precisos serão os resultados. No entanto, o tempo de processamento também pode aumentar significativamente. O número escolhido depende dos dados, mas em geral, você deve escolher o número mais alto possível sem sacrificar o desempenho. Para melhorar o desempenho, também é possível especificar menos partições.  
  
5.  Selecione uma coluna a partir de **atributo de destino** lista suspensa. A lista exibe apenas as colunas configuradas como atributos previsíveis durante a criação original do modelo. O modelo pode conter vários atributos previsíveis, mas você pode escolher apenas um.  
  
6.  Selecione um valor de **estado de destino** lista suspensa.  
  
     Se a coluna previsível contiver dados numéricos contínuos, essa opção não estará disponível.  
  
7.  Opcionalmente, especifique um valor a ser usado como o **limite de destino** ao considerar previsões como precisas. Esse valor é expresso como uma probabilidade, que é um número entre 0 e 1, onde 1 é garantia da previsão da precisão, 0 significa que não há nenhuma possibilidade de a previsão estar correta e .5 corresponde a uma previsão aleatória.  
  
     Se a coluna previsível contiver dados numéricos contínuos, essa opção não estará disponível.  
  
8.  Clique em **Concluir**. É criada uma nova planilha, denominada **validação cruzada**.  
  
    > [!NOTE]  
    >  O Microsoft Excel poderá não responder temporariamente enquanto o modelo estiver sendo particionado em partições e cada partição for testada.  
  
### <a name="requirements"></a>Requisitos  
 Para criar um relatório de validação cruzada, é necessário já ter criado uma estrutura de mineração de dados e os modelos relacionados. O assistente fornece uma caixa de diálogo para ajudá-lo a escolher entre a estrutura e os modelos existentes.  
  
 Se você escolher uma estrutura de mineração com suporte para vários modelos de mineração, e os modelos usarem atributos de previsão diferentes, o assistente de Validação Cruzada testará apenas os modelos que compartilham o mesmo atributo previsível.  
  
 Se você escolher uma estrutura com suporte para modelos de clustering e outros tipos de modelos, os modelos de clustering não serão testados.  
  
## <a name="understanding-cross-validation-results"></a>Entendendo os resultados de validação cruzada  
 Os resultados da validação cruzada são exibidos em uma nova planilha, denominada **relatório de validação cruzada para \<nome do atributo >**. A nova planilha contém várias seções: a primeira é um resumo que fornece metadados importantes sobre o modelo testado, para que você possa saber para qual modelo ou estrutura os resultados são.  
  
 A segunda seção no relatório fornece um resumo estatístico que indica o quão bom é o modelo original. Resumindo, as diferenças entre os modelos criados para cada partição são analisadas para três medidas principais: *erro de raiz quadrada média*, *erro absoluto médio*, e *log pontuar*. Essas são medidas estatísticas padrão usadas não só na mineração de dados, como também na maioria dos tipos de análise estatística.  
  
 Para cada uma dessas medidas, o assistente de Validação Cruzada calcula a média e o desvio padrão do modelo como um todo. Isso informa o quão consistente é o modelo durante a previsão em subconjuntos diferentes dos dados. Por exemplo, se o desvio padrão for muito grande, isso indica que os modelos criados para cada partição terão resultados muito diferentes e, portanto, talvez o modelo tenha treinado muito perto de um determinado grupo de dados e não seja aplicável a outros conjuntos de dados.  
  
 A seção a seguir explica as medidas usadas para avaliar os modelos.  
  
### <a name="tests-and-measures"></a>Testes e medidas  
 Além de algumas informações básicas sobre o numero de partições nos dados, e a quantidade de dados em cada partição, a planilha exibe um conjunto de métricas sobre cada modelo, categorizadas por tipo de teste. Por exemplo, a precisão de um modelo de clustering é avaliada por testes diferentes dos que você usaria para um modelo de precisão.  
  
 A tabela a seguir lista os testes e a métrica, com uma explanação sobre o que a métrica significa.  
  
#### <a name="aggregates-and-general-statistical-measures"></a>Medidas estatísticas gerais e agregadas  
 As medidas agregadas fornecidas no relatório indicam como as partições criadas nos dados são diferentes.  
  
-   Desvio padrão e médio  
  
-   Média do desvio da média para uma medida específica, através de todas as partições em um modelo.  
  
#### <a name="classification-passfail"></a>Classificação: Aprovação/reprovação  
 Essa medida é usada em modelos de classificação quando você não especifica um valor de destino para o atributo previsível. Por exemplo, se você criar um modelo que preveja várias possibilidades, essa medida informará quão bem o modelo se saiu na previsão de todos os valores possíveis.  
  
 Aprovado/reprovado é calculado pela contagem de casos que atendem as condições a seguir: **passar** se o estado previsto com a mais alta probabilidade é o mesmo que o estado de entrada e a probabilidade é maior que o valor especificado para o **Limiar de estado**; caso contrário, **falhar**.  
  
#### <a name="classification-true-or-false-positives-and-negatives"></a>Classificação: VERDADEIRO ou falsos positivos e negativos  
 Este teste é usado para todos os modelos de classificação que têm um destino especificado. A medida indica como cada caso é classificado em resposta a essas questões: o que o modelo prevê e qual foi o resultado real.  
  
|Measure|Descrição|  
|-------------|-----------------|  
|Verdadeiro positivo|Contagem de casos que atendem estas condições:<br /><br /> Casos que contém o valor de destino.<br /><br /> O modelo previu que o caso contém o valor de destino.|  
|Falso positivo|Contagem de casos que atendem estas condições:<br /><br /> O valor atual é igual ao valor de destino.<br /><br /> O modelo previu que o caso contém o valor de destino.|  
|Verdadeiro negativo|Contagem de casos que atendem estas condições:<br /><br /> Caso não contém o valor de destino.<br /><br /> O modelo previu que o caso não contém o valor de destino.|  
|Falso negativo|Contagem de casos que atendem estas condições:<br /><br /> O valor atual não é igual ao valor de destino.<br /><br /> O modelo previu que o caso não contém o valor de destino.|  
  
#### <a name="lift"></a>Comparação de Precisão  
 *Comparação de precisão* é uma medida que é associada à probabilidade. Se um resultado mais provável é quando você usa o modelo do que quando você faz uma suposição aleatória, o modelo será considerado como fornecendo *comparação de precisão positiva*. No entanto, se o modelo faz previsões que têm menor probabilidade de que a possibilidade aleatória, a pontuação de comparação de precisão é *negativo*. Assim, essa métrica indica a quantidade de aperfeiçoamento que pode ser obtida com o uso do modelo, no qual uma pontuação mais alta é melhor.  
  
 A comparação de precisão é calculada como a proporção de probabilidade da previsão atual para a probabilidade marginal nos casos de teste.  
  
#### <a name="log-score"></a>Pontuação de log  
 O *pontuação de log*, também chamado de *pontuação de probabilidade de log* para a previsão, representa a relação entre duas probabilidades, convertida em uma escala logarítmica. Como a probabilidade é representada como uma fração decimal, as pontuações de log são sempre números negativos. Uma pontuação próxima de 0 é melhor.  
  
 Visto que contagens brutas podem ter distribuições muito irregulares ou distorcidas, uma contagem de log é semelhante a uma porcentagem.  
  
#### <a name="root-mean-square-error"></a>Erro de Raiz Quadrada Média  
 *Erro de raiz quadrada média* (RMSE) é um método padrão em estatísticas para examinar a comparação de diferentes conjuntos de dados e suavizar as diferenças que podem ser introduzidas pela escala das entradas.  
  
 RMSE representa o erro médio do valor previsto quando comparado ao valor real. Ele é calculado como a raiz quadrada do erro médio para todos os casos de partição, dividida pelo número de casos na partição, excluindo as linhas com valores ausentes para os atributos de destino.  
  
#### <a name="mean-absolute-error"></a>Erro de Média Absoluta  
 O *erro de média absoluta* é o erro médio do valor previsto para o valor real. Ele é calculado pela obtenção da soma absoluta dos erros e descoberta da média desses erros.  
  
 Esse valor o ajuda a entender o quanto as pontuações variam da média.  
  
#### <a name="case-likelihood"></a>Probabilidade de caso  
 Essa medida é usada apenas para modelos de clustering e indica qual o grau de probabilidade de um novo caso pertencer a um determinado cluster.  
  
 Em modelos de clustering, há dois tipos de associação ao cluster, dependendo do método usado para criação do modelo. Em alguns modelos, com base no algoritmo de médias K, espera-se que um novo caso pertença a apenas um cluster. No entanto, por padrão, o algoritmo Microsoft Clustering usa o método Maximização da Expectativa, que assume que um novo caso pode pertencer a qualquer cluster. Assim, nesses modelos um caso pode ter vários valores `CaseLikelihood`, mas aquele que será reportado por padrão será a probabilidade de o caso pertencer ao cluster que melhor corresponder ao novo caso.  
  
## <a name="see-also"></a>Consulte também  
 [Validando modelos e usando modelos para previsão &#40;Data Mining Add-ins para Excel&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)  
  
  
