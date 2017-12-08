---
title: "Valores ausentes (Analysis Services – mineração de dados) | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- attributes [data mining]
- MISSING_VALUE_SUBSTITUTION
- MissingValueSubstitution property
- MISSING_VALUE_SUBSTITUTION parameter
- null values [Analysis Services]
- coding [Data Mining]
ms.assetid: 2b34abdc-7ed4-4ec1-8780-052a704d6dbe
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b1c2b1b598989965af2be43ad62c02ae4017fd42
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="missing-values-analysis-services---data-mining"></a>Valores ausentes (Analysis Services - Mineração de dados)
  Tratar  *valores ausentes values* corretamente é uma parte importante da modelagem efetiva. Esta seção explica o que são valores ausentes, e descreve os recursos fornecidos no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para trabalhar com valores ausentes ao criar estruturas de mineração de dados e modelos de mineração.  
  
## <a name="definition-of-missing-values-in-data-mining"></a>Definição de valores ausentes em Mineração de Dados  
 Um valor ausente pode significar várias coisas diferentes. Talvez o campo não fosse aplicável, o evento não aconteceu ou os dados não estavam disponíveis. Pode ser que a pessoa que inseriu os dados não sabia o valor certo, ou não se preocupou que um campo não foi preenchido.  
  
 No entanto, há muitos cenários de mineração de dados nos quais os valores ausentes fornecem informações importantes. O significado dos valores ausentes depende em grande parte do contexto. Por exemplo, um valor ausente para a data em uma lista de faturas tem um significado substancialmente diferente da falta de uma data na coluna que indica uma data de admissão de funcionário. Geralmente, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] trata valores ausentes como informativos e ajusta as probabilidades para incorporá-los a seus cálculos. Dessa forma, é possível assegurar o equilíbrio dos modelos e que eles não atribuem um peso excessivo aos casos existentes.  
  
 Portanto, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornece dois mecanismos diferentes para gerenciar e calcular valores ausentes. O primeiro método controla o tratamento de nulos no nível da estrutura de mineração. O segundo método difere na implementação para cada algoritmo, mas geralmente define como valores ausentes são processados e contabilizados em modelos que permitem valores nulos.  
  
## <a name="specifying-handling-of-nulls"></a>Especificando tratamento de nulos  
 Em sua fonte de dados, os valores ausentes podem ser representados de muitas maneiras: como nulos, como células vazias em uma planilha, como o valor N/A ou algum outro código, ou como um valor artificial como 9999. Porém, para fins de mineração de dados, somente nulos são considerados valores ausentes. Se seus dados contiverem valores de espaço reservado em vez de nulos, eles poderão afetar os resultados do modelo, de modo que você deve substituí-los por nulos ou inferir valores corretos, se possível. Existem diversas ferramentas que você pode usar para deduzir e preencher os valores apropriados, como a transformação Pesquisa ou a tarefa Criador de Perfil do SQL Server Integration Services ou a ferramenta Preencher do Exemplo fornecida com os Suplementos de Mineração de Dados do Excel.  
  
 Se a tarefa que você está modelando especifica que uma coluna jamais deve ficar sem valores, aplique o sinalizador de modelagem **NOT_NULL** à coluna ao definir a estrutura de mineração. Esse sinalizador indica que poderá haver uma falha no processamento se um caso não tiver um valor apropriado. Se ocorrer esse erro ao processar um modelo, você poderá registrar o erro em log e tomar as medidas necessárias para corrigir os dados fornecidos ao modelo.  
  
## <a name="calculation-of-the-missing-state"></a>Cálculo do estado ausente  
 Para o algoritmo de mineração de dados, os valores ausentes são informativos. No caso de tabelas, **Ausente** é um estado válido como qualquer outro. Além disso, um modelo de mineração de dados pode usar outros valores para prever se um valor está ausente. Em outras palavras, o fato de um valor estar ausente não é um erro.  
  
 Quando você criar um modelo de mineração, um estado **Ausente** será adicionado automaticamente ao modelo para todas as colunas discretas. Por exemplo, se a coluna de entrada de [Gênero] tiver dois valores possíveis, Masculino e Feminino, um terceiro valor será adicionado automaticamente para representar o valor **Ausente** , e o histograma que mostra a distribuição de todos os valores da coluna sempre incluirá a contagem de casos com valores **Ausentes** . Se não houver valores ausentes na coluna Gênero, o histograma mostrará que o estado Ausente foi encontrado em 0 casos.  
  
 O raciocínio para incluir o estado **Ausente** por padrão é claro se você considerar que os dados podem não ter exemplos de todos os valores possíveis e que não convém excluir uma possibilidade simplesmente porque não há um exemplo nos dados. Se, por exemplo, os dados de vendas de uma loja mostrarem que todos os clientes que compraram um determinado produto foram mulheres, não convém criar um modelo que prevê que somente mulheres comprariam esse produto. Em vez disso, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] adiciona um espaço reservado para um valor extra desconhecido, chamado **Ausente**, como uma forma de acomodar outros estados possíveis.  
  
 Por exemplo, a tabela a seguir mostra a distribuição de valores do nó (All) no modelo de árvore de decisão criado para o tutorial Bike Buyer. No cenário do exemplo, a coluna [Bike Buyer] é um atributo previsível, em que 1 indica "Sim" e 0 indica "Não".  
  
|Value|Casos|  
|-----------|-----------|  
|0|9296|  
|1|9098|  
|Ausente|0|  
  
 Essa distribuição mostra que cerca de metade dos clientes comprou uma bicicleta e metade não. Esse conjunto de dados em particular é bem simples; portanto, cada caso tem um valor na coluna [Bike Buyer] e a contagem de valores **Ausentes** é 0. Contudo, se algum caso tivesse um nulo no campo [Bike Buyer], o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] contaria essa linha como um caso com valor **Ausente** .  
  
 Se a entrada for uma coluna contínua, o modelo tabulará dois estados possíveis para o atributo: **Existente** e **Ausente**. Em outras palavras, ou a coluna contém um valor de algum tipo de dados numérico ou não contém valor algum. Nos casos que têm um valor, o modelo calculará o desvio médio padrão e outras estatísticas significativas. Para casos que não têm nenhum valor, o modelo fornecerá uma contagem dos valores **Ausentes** e ajustará as previsões de acordo. O método usado para ajustar a previsão varia dependendo do algoritmo e é descrito na próxima seção.  
  
> [!NOTE]  
>  Para atributos em uma tabela aninhada, os valores ausentes não são informativos. Por exemplo, se um cliente não tivesse comprado um produto, a tabela **Produtos** aninhada não teria a linha correspondente a esse produto e o modelo de mineração não criaria um atributo para o produto ausente. No entanto, se você estiver interessado nos clientes que não compraram certos produtos, poderá criar um modelo que seja filtrado pela não existência dos produtos na tabela aninhada usando uma instrução NOT EXISTS no filtro do modelo. Para obter mais informações, consulte [Aplicar um filtro a um modelo de mineração](../../analysis-services/data-mining/apply-a-filter-to-a-mining-model.md).  
  
## <a name="adjusting-probability-for-missing-states"></a>Ajustando a probabilidade para valores ausentes  
 Além de contar valores, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] calcula a probabilidade de qualquer valor em todo o conjunto de dados. O mesmo é válido para o valor **Ausente** . Por exemplo, a tabela a seguir mostra as probabilidades para os casos do exemplo anterior:  
  
|Value|Casos|Probabilidade|  
|-----------|-----------|-----------------|  
|0|9296|50.55%|  
|1|9098|49.42%|  
|Ausente|0|0.03%|  
  
 Pode parecer estanho que a probabilidade do valor **Ausente** tenha sido calculada como 0,03% quando o número de casos é 0. Na realidade, esse é o comportamento padrão e representa um ajuste que permite ao modelo lidar bem com valores desconhecidos.  
  
 Em geral, o cálculo da probabilidade é feito ao dividir o número de casos favoráveis por todos os casos possíveis. Nesse exemplo, o algoritmo computa a soma dos casos que satisfazem um determinado critério ([Bike Buyer] = 1, ou [Bike Buyer] = 0) e divide esse número pela contagem total de linhas. Entretanto, para considerar os casos **Ausentes** , 1 é somado ao número de todos os casos possíveis. Como resultado, a probabilidade do caso desconhecido não é mais zero, mas um número bem pequeno, indicando simplesmente que o estado é improvável, mas não impossível.  
  
 A adição do valor **Ausente** baixo não altera o resultado do indicador. Entretanto, ela permite uma melhor modelagem em cenários nos quais os dados históricos não incluem todos os resultados possíveis.  
  
> [!NOTE]  
>  A mineração de dados difere na maneira como lida com valores ausentes. Por exemplo, alguns provedores assumem que os dados ausentes em uma coluna aninhada são uma representação esparsa, mas que os dados ausentes em uma coluna não aninhada estão ausentes ao acaso.  
  
 Se você tiver certeza de que todos os resultados foram especificados nos dados e quiser evitar o ajuste das probabilidades, defina o sinalizador de modelagem NOT_NULL na coluna da estrutura de mineração.  
  
> [!NOTE]  
>  Cada algoritmo pode controlar os valores ausentes de maneiras diferentes, inclusive algoritmos personalizados que você pode ter obtido de um plug-in de terceiros.  
  
### <a name="special-handling-of-missing-values-in-decision-tree-models"></a>Tratamento especial de valores ausentes em modelos de árvore de decisão  
 O algoritmo Árvores de Decisão da Microsoft calcula probabilidades para valores ausentes de formas diferentes em outros algoritmos. Em vez de apenas adicionar 1 ao número total de casos, o algoritmo de árvore de decisão ajusta o estado **Ausente** usando uma fórmula um pouco diferente.  
  
 Em um modelo de árvore de decisão, a probabilidade do estado **Ausente** é calculado como segue:  
  
 StateProbability = (NodePriorProbability) * (StateSupport + 1) / (NodeSupport + TotalStates)  
  
O algoritmo de árvores de decisão faz um ajuste adicional que ajuda o algoritmo a compensar a presença de filtros no modelo, o que pode resultar em vários estados durante o treinamento.  
  
 No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], se houver um estado durante o treinamento, mas não tiver suporte em determinado nó, o ajuste padrão será feito. Porém, se um estado nunca for encontrado durante o treinamento, o algoritmo definirá a probabilidade exatamente como zero. Esse ajuste é válido não só para o estado **Ausente** , mas também para outros estados que existem nos dados de treinamento, mas com suporte para zero como resultado da filtragem do modelo.  
  
 Esse ajuste adicional resulta na seguinte fórmula:  
  
 StateProbability = 0,0 se esse estado tiver 0 suporte no treinamento definido  
  
 ELSE StateProbability = (NodePriorProbability)* (StateSupport + 1) / (NodeSupport + TotalStatesWithNonZeroSupport)  
  
 O efeito desse ajuste é manter a estabilidade da árvore.  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
 Os tópicos a seguir fornecem mais informações sobre como tratar valores ausentes.  
  
|Tarefas|Links|  
|-----------|-----------|  
|Adicione sinalizadores a colunas de modelo individuais para controlar o tratamento de valores ausentes|[Exibir ou alterar sinalizadores de modelagem &#40;Mineração de dados&#41;](../../analysis-services/data-mining/view-or-change-modeling-flags-data-mining.md)|  
|Defina as propriedades em um modelo de mineração para controlar o tratamento de valores ausentes|[Alterar as propriedades de um modelo de mineração](../../analysis-services/data-mining/change-the-properties-of-a-mining-model.md)|  
|Saiba como especificar sinalizadores de modelagem no DMX|[Sinalizadores de modelagem &#40;DMX&#41;](../../dmx/modeling-flags-dmx.md)|  
|Altere o modo como a estrutura de mineração trata valores ausentes|[Alterar as propriedades de uma estrutura de mineração](../../analysis-services/data-mining/change-the-properties-of-a-mining-structure.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Conteúdo do modelo de mineração &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)   
 [Sinalizadores de modelagem &#40;Mineração de dados&#41;](../../analysis-services/data-mining/modeling-flags-data-mining.md)  
  
  
