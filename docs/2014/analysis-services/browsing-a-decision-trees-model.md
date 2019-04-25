---
title: Modelo de árvore de navegação de uma decisão | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, browsing
- mining models, viewing
- tree viewer
- mining model, decision tree
- decision tree [data mining]
- dependency network
ms.assetid: 6b3dd1ae-caff-41c3-817b-802dc020ff88
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 257d193c84420a0c70ea99ef2a8cadfa9e11eec5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62468708"
---
# <a name="browsing-a-decision-trees-model"></a>Procurando um modelo de árvores de decisão
  Quando você abre um modelo de classificação usando **navegue**, o modelo é exibido em um visualizador de árvore de decisão, semelhante do [!INCLUDE[msCoName](../includes/msconame-md.md)] Visualizador de árvores de decisão no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. O visualizador exibe os resultados da classificação como um gráfico que foi criado para realçar os critérios que diferenciam um grupo de dados do outro. Você também pode analisar subconjuntos individuais da árvore e recuperar os dados subjacentes.  
  
##  <a name="bkmk_Top"></a> Explorar o modelo  
 Os modelos baseados no algoritmo Árvores de Decisão têm várias informações interessantes para explorar. O **procurar** janela inclui as guias e painéis para ajudá-lo a aprender os padrões e prever resultados usando o gráfico a seguir:  
  
-   [Árvore de Decisão](#BKMK_DecisionTree)  
  
-   [Rede de Dependências](#BKMK_DNetwork)  
  
 Para experimentar um modelo de árvores de decisão, você poderá usar os dados de exemplo na guia Dados de Treinamento (ou os Dados de Origem) da pasta de trabalho de dados de exemplo e criar um modelo de árvore de decisão usando Bike Buyer como o atributo previsível.  
  
###  <a name="BKMK_DecisionTree"></a> Árvore de Decisão  
 Essa exibição pretende ajudá-lo a compreender e explorar os fatores que levam a um resultado.  
  
 O gráfico da árvore de decisão pode ser lido da esquerda para a direita da seguinte maneira:  
  
-   Os retângulos, que são denominados *nós*, contêm subconjuntos de dados. O rótulo no nó informa as características de definição desse subconjunto.  
  
-   O nó mais à esquerda, rotulado **todos os**, representa o conjunto de dados completo. Todos os nós subsequentes representam subconjuntos dos dados.  
  
-   Uma árvore de decisão contém muitas *divide*, ou locais onde os dados divergem e em vários conjuntos baseados em atributos.  
  
     Por exemplo, a primeira divisão no modelo de exemplo divide o conjunto de dados em três grupos por idade.  
  
-   A divisão imediatamente após o **todos os** nó é mais importante, pois mostra a condição primária que divide esse conjunto de dados.  
  
     Divisões adicionais ocorrem à direita. Portanto, ao analisar segmentos diferentes da árvore, você poderá saber quais atributos tinham mais influência sobre o comportamento de compra.  
  
 ![Gráfico de rede de dependência para um modelo de associação](media/dm13-dec-tree-split-definition.gif "grafo de rede de dependência para um modelo de associação")  
  
 Usando essas informações, você poderá concentrar uma campanha de marketing nos clientes que podem apenas precisar de incentivo para fazer uma compra.  
  
##### <a name="explore-the-decision-tree"></a>Explorar a árvore de decisão  
  
1.  Clique o **todos os** nó e examine o **legenda de mineração**.  
  
     Ela exibe a contagem exata dos casos no conjunto de dados de treinamento, assim como uma análise dos resultados.  
  
     Você poderá exibir as mesmas informações em uma dica de ferramenta se para o mouse sobre um nó.  
  
2.  Clique nos sinais de adição e subtração ao lado de cada nó para expandir ou recolher a árvore.  
  
     Você também pode usar o **Mostrar nível** controle deslizante para expandir ou recolher a árvore.  
  
3.  Observa que alguns nós são mais escuros do que outros?  
  
     Por padrão, **população** é usado como a variável de sombreamento, o que significa que a intensidade da cor mostra os nós que têm mais suporte.  
  
     Consequentemente, o nó mais à esquerda é o mais escuro, porque contém o conjunto de dados inteiro.  
  
4.  Altere o valor de **plano de fundo** partir **todos os casos** para **Sim**.  
  
     ![alteração gráfico da árvore de decisão para realçar compradores](media/dm13-dectreeshadedbuyer.gif "alterando o gráfico da árvore de decisão para realçar compradores")  
  
5.  Agora a intensidade da cor informa quantos clientes em cada nó compraram uma bicicleta, que é o comportamento no qual você está interessado.  
  
     Observe as barras coloridas em cada nó. Este é um histograma que mostra a distribuição de resultados nesse subconjunto de dados. Por exemplo, a árvore de decisão do comprador de bicicleta de exemplo, a barra colorida mostra a proporção de clientes que compraram Bicicletas (valores Sim) versus aqueles que não compraram (nenhum valor). Para obter os valores exatos, você pode clicar no nó e exiba os **legenda de mineração**.  
  
6.  Ao seguir o gráfico, você poderá ver como cada subconjunto de dados é decomposto em grupos menores, e quais os atributos são os mais úteis para prever um resultado.  
  
     Apenas examinar a intensidade do sombreamento, você poderá se concentrar em alguns grupos de interesse, e obter dados mais detalhados sobre eles para comparação. Por exemplo, esses grupos têm uma probabilidade consideravelmente mais alta de comprar bicicletas:  
  
    -   Idade > = 32 e \< 53 and Renda anual > = 26000 e filhos = 0  
  
         Total de casos: 1150  
  
         Probabilidade do comprador de bicicleta: 18%  
  
    -   Idade > = 32 e \< 53 and Renda anual > = 26000 e filhos não = 0 e estado civil = "Solteiro"  
  
         Total de casos: 402  
  
         Probabilidade do comprador de bicicleta: 16%  
  
7.  Altere o valor de **plano de fundo** de **Sim** para **não** e veja como o gráfico muda.  
  
     ![Gráfico de rede de dependência para um modelo de associação](media/dm13-dec-tree-background-no.gif "grafo de rede de dependência para um modelo de associação")  
  
 **Dicas**  
  
-   Se os dados puderem ser divididos em várias séries, um modelo diferente será criado para cada conjunto de dados que você quiser modelar.  
  
-   No modelo de dados de exemplo, há apenas um resultado previsível – comprador de bicicleta – mas suponha que você tenha informações sobre se o cliente comprou um plano de serviço e quisesse prever isso também. Nesse caso, você teria esses dados em uma coluna separada e incluiria dois atributos previsíveis no modelo.  
  
     Clique o **histograma** opção, no canto superior esquerdo do painel de árvore de decisão para alterar o número máximo de estados que podem aparecer nos histogramas na árvore. Isso será útil se o atributo previsível tiver muitos estados. Os estados aparecem em um histograma na ordem de popularidade da esquerda para a direita.  
  
-   Você também pode usar as opções sobre o **árvore de decisão** guia para afetar como a árvore é exibida, zoom ou dimensionando o gráfico para se ajustar à janela.  
  
-   Use a opção **Expansão Padrão** para definir o número padrão de níveis exibidos em todas as árvores no modelo.  
  
-   Selecione **Mostrar nome longo** para exibir o nome completo do atributo, inclusive a fonte de dados. Os nomes curtos e longos são iguais, a menos que seus casos sejam obtidos de uma fonte de dados diferente dos atributos para cada caso.  
  
 [Voltar ao início](#bkmk_Top)  
  
###  <a name="BKMK_DNetwork"></a> Rede de Dependências  
 O **rede de dependências** modo de exibição exibe as conexões entre os atributos de entrada e os atributos previsíveis no modelo.  
  
1.  Clique e arraste o controle deslizante à esquerda do visualizador  
  
     Na posição superior, todas as conexões são mostradas. Quando você arrasta o controle deslizante para baixo, apenas os links mais importantes são mostrados no visualizador.  
  
2.  Agora clique no nó Comprador de bicicleta.  
  
     ![Exibição de rede de dependência para árvores de decisão](media/dm13-dectree-depnet.gif "exibição de rede de dependência para árvores de decisão")  
  
     Quando você selecionar um nó, o visualizador destacará as dependências específicas ao nó. Nesse caso, o visualizador destacará cada nó que ajuda a prever o resultado.  
  
3.  Se o visualizador contiver muitos nós, você pode procurar nós específicos usando o **localizar nó** botão. Clicar em **Localizar Nó** faz com que a caixa de diálogo **Localizar Nó** seja aberta, na qual você pode usar um filtro para pesquisar e selecionar nós específicos.  
  
4.  A legenda na parte inferior do visualizador vincula os nós de cores ao tipo de dependência no gráfico. Por exemplo, quando você seleciona um nó previsível, ele fica sombreado na cor turquesa e os nós que preveem o nó selecionado são sombreados em laranja.  
  
 [Voltar ao início](#bkmk_Top)  
  
### <a name="drill-through-to-underlying-data"></a>Detalhar os dados subjacentes  
 A capacidade de dar suporte a vários tipos de modelos *drill-through* do modelo para os dados de caso subjacentes. Isso pode ser muito útil se você quiser contatar os clientes em um segmento específico ou retirar os dados para executar uma análise mais detalhada.  
  
##### <a name="get-case-data"></a>Obter dados de caso  
  
1.  Clique com o botão direito do mouse no nó na árvore que contém os dados desejados e selecione uma destas opções:  
  
    -   **Detalhar modelo**. Essa opção obtém os casos que pertencem ao nó selecionado e salva-os em uma tabela no Excel. Você obtém de volta apenas as colunas de dados que foram realmente usadas para criar o modelo.  
  
    -   **Detalhar colunas da estrutura**. Essa opção obtém os casos que pertencem ao nó selecionado e salva-os em uma tabela no Excel. Você obtém todas as informações que estavam disponíveis no subjacente quando você criou, até mesmo de uma coluna de dados não foi usados no modelo. Por exemplo, você pode ter excluído o endereço e o código postal do cliente porque esses campos não são úteis na análise, mas deixou-os na estrutura.  
  
     Retorne para o Excel para exibir seus dados. O visualizador Procurar executa uma consulta, salva os dados em uma tabela em uma nova planilha e rotula os resultados.  
  
     ![os resultados de detalhamento são salvos no Excel](media/dm13-dectree-drillthroughresults.gif "os resultados de detalhamento são salvos no Excel")  
  
## <a name="see-also"></a>Consulte também  
 [Procurando modelos no Excel &#40;suplementos de mineração de dados do SQL Server&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
