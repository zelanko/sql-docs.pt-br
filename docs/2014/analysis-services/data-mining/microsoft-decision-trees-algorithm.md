---
title: Algoritmo árvores de decisão da Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- predictions [Analysis Services], discrete attributes
- predictions [Analysis Services], continuous attributes
- algorithms [data mining]
- discrete attributes [Analysis Services]
- classification algorithms [Analysis Services]
- discrete columns [Analysis Services]
- decision tree algorithms [Analysis Services]
- decision trees [Analysis Services]
- continuous columns
- regression algorithms [Analysis Services]
ms.assetid: 95ffe66f-c261-4dc5-ad57-14d2d73205ff
author: minewiskan
ms.author: owend
ms.openlocfilehash: fd55af5914bcc6409a3e5d6c899cbfd8b7f939f5
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84522142"
---
# <a name="microsoft-decision-trees-algorithm"></a>Algoritmo Árvores de Decisão da Microsoft
  O [!INCLUDE[msCoName](../../includes/msconame-md.md)] algoritmo árvores de decisão é um algoritmo de classificação e regressão fornecido pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para uso em modelagem preditiva de atributos discretos e contínuos.

 No caso dos atributos discretos, o algoritmo faz previsões fundadas nas relações entre colunas de entrada em um conjunto de dados. Ele usa os valores, conhecidos como estados, dessas colunas para prever os estados de uma coluna que você define como previsível. Especificamente, o algoritmo identifica as colunas de entrada que são correlacionadas com a coluna previsível. Por exemplo, em um cenário em que se deseja prever a tendência dos clientes em adquirir uma bicicleta, se 9 de 10 clientes jovens comprarem uma bicicleta, mas apenas 2 de 10 clientes mais velhos fizerem o mesmo, o algoritmo infere que idade é um bom indicador para a compra de bicicletas. A árvore de decisão faz previsões com base nesta tendência para obter um resultado específico.

 No caso de atributos contínuos, o algoritmo usa a regressão linear para determinar onde uma árvore de decisão se divide.

 Se mais de uma coluna for definida como previsível, ou se os dados de entrada tiverem uma tabela aninhada configurada como previsível, o algoritmo criará uma árvore de decisão separada para cada coluna previsível.

## <a name="example"></a>Exemplo
 O departamento de marketing da empresa [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] deseja identificar as características dos clientes antigos que possam indicar se há chance de eles realizarem compras futuramente. O banco de dados da [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] armazena informações demográficas que descrevem clientes antigos. Usando o algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] para analisar essas informações, o departamento de marketing pode criar um modelo que prevê se um cliente específico comprará ou não produtos com base nos estados de colunas conhecidas sobre aquele cliente, como padrões demográficos ou compras já efetuadas.

## <a name="how-the-algorithm-works"></a>Como o algoritmo funciona
 O algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] gera um modelo de mineração de dados criando uma série de divisões na árvore. Essas divisões são representadas como *nós*. O algoritmo adiciona um nó ao modelo toda vez que uma coluna de entrada é considerada significativamente correlacionada a uma coluna previsível. A forma que o algoritmo determina uma divisão depende do fato de ele estar prevendo uma coluna contínua ou discreta.

 O algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] usa a *seleção de recurso* para guiar a seleção dos atributos mais úteis. A seleção de recurso é usada por todos os algoritmos de mineração de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para melhorar o desempenho e a qualidade da análise. A seleção de recurso é importante para impedir que atributos sem-importância usem tempo do processador. Se você usar muitas entradas ou atributos previsíveis ao criar um modelo de mineração de dados, o modelo poderá demorar muito tempo para processar ou ainda esgotar a memória. Os métodos usados para determinar a divisão da árvore incluem medidas padrão da indústria para *entropia* e redes Bayesianas *.* Para obter mais informações sobre os métodos usados para selecionar atributos significativos e depois classificá-los, consulte [Seleção de recursos &#40;Mineração de dados&#41;](feature-selection-data-mining.md).

 Um problema comum nos modelos de Data Mining é que o modelo se torna muito sensível a pequenas diferenças nos dados de treinamento. nesse caso, disse-se que ele é *superajustado* ou *supertreinado*. Um modelo sobrecarregado não pode ser generalizado para outros conjuntos de dados. Para evitar a superajuste de um determinado conjunto de dados, o algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] usa técnicas para controlar o crescimento da árvore. Para obter uma explicação mais detalhada de como funciona o algoritmo de Árvores de Decisão [!INCLUDE[msCoName](../../includes/msconame-md.md)] , consulte [Referência técnica do algoritmo Árvores de Decisão da Microsoft](microsoft-decision-trees-algorithm-technical-reference.md).

### <a name="predicting-discrete-columns"></a>Prevendo colunas discretas
 A forma como o algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] cria uma árvore para uma coluna previsível discreta pode ser mostrada usando um histograma. O diagrama a seguir mostra um histograma que esboça uma coluna previsível, Compradores de bicicleta, em comparação com uma coluna de entrada, Idade. O histograma mostra que a idade de uma pessoa ajuda a distinguir se ela comprará uma bicicleta.

 ![Histograma do algoritmo Árvores de Decisão da Microsoft](../media/dt-histogram.gif "Histograma do algoritmo Árvores de Decisão da Microsoft")

 A correlação que é mostrada no diagrama faz com que o algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] crie um novo nó no modelo.

 ![Nó da árvore de decisão](../media/dt-tree.gif "Nó da árvore de decisão")

 À medida que o algoritmo acrescenta novos nós em um modelo, uma estrutura de árvore é formada. O nó superior da árvore indica a divisão da coluna previsível para a média da população de clientes. Como o modelo continua crescendo, o algoritmo considera todas as colunas.

### <a name="predicting-continuous-columns"></a>Prevendo colunas contínuas
 Quando o algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)] cria uma árvore com base em uma coluna previsível contínua, cada nó contém uma fórmula de regressão. Uma divisão ocorre em um ponto de não linearidade na fórmula de regressão. Por exemplo, considere o seguinte diagrama:

 ![Várias linhas de regressão mostrando não linearidade](../media/regression-tree1.gif "Várias linhas de regressão mostrando não linearidade")

 O diagrama contém dados que podem ser modelados usando uma única linha ou usando duas linhas conectadas. Porém, uma única linha não representaria os dados de forma satisfatória. Mas, se você usar duas linhas, o modelo terá um desempenho muito melhor ao aproximar dados. O ponto onde duas linhas se encontram é o ponto de não linearidade e é onde o nó de um modelo de árvore de decisão se dividiria. Por exemplo, o nó que corresponde ao ponto de não linearidade no gráfico anterior poderia ser representado pelo diagrama a seguir. As duas equações representam as equações de regressão para as duas linhas.

 ![Equação que representa um ponto de não linearidade](../media/regression-tree2.gif "Equação que representa um ponto de não linearidade")

## <a name="data-required-for-decision-tree-models"></a>Dados necessários para modelos de árvore de decisão
 Ao preparar dados para usar em um modelo de árvore de decisão, você deve saber os requisitos do algoritmo específico, incluindo a quantidade de dados necessária e como eles são usados.

 Os requisitos para um modelo de árvore de decisão são os seguintes:

-   **Uma única coluna de chave** Cada modelo deve conter uma coluna de texto ou numérica que identifique unicamente cada registro. Não são permitidas chaves compostas.

-   **Uma coluna previsível** Requer, pelo menos, uma coluna previsível. Você pode incluir vários atributos previsíveis em um modelo, e o atributo previsível pode ser de diferentes tipos, tanto numérico como discreto. Porém, o aumento no número de atributos previsíveis pode aumentar o tempo de processamento.

-   **Colunas de entrada** Requer colunas de entrada que podem ser discretas ou contínuas. O aumento no número de atributos de entrada afeta o tempo de processamento.

 Para obter informações mais detalhadas sobre os tipos de conteúdo e de dados com suporte pelos modelos de árvore de decisão, consulte a seção Requisitos de [Referência técnica do algoritmo de árvore de decisão da Microsoft](microsoft-decision-trees-algorithm-technical-reference.md).

## <a name="viewing-a-decision-trees-model"></a>Exibindo um modelo de árvore de decisão
 Para explorar o modelo, você pode usar o **Visualizador de Árvores da Microsoft**. Caso seu modelo gere várias árvores, é possível selecionar uma árvore e o visualizador mostrará uma divisão de como os casos são categorizados para cada atributo previsível. Você também pode exibir a interação das árvores usando o visualizador de rede de dependência. Para obter mais informações, consulte [Procurar um modelo usando o Visualizador de Árvores da Microsoft](browse-a-model-using-the-microsoft-tree-viewer.md).

 Se quiser obter mais detalhes sobre qualquer ramificação ou nó da árvore, você também pode explorar o modelo usando o [Visualizador de Árvore de Conteúdo Genérica da Microsoft](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md). O conteúdo armazenado para o modelo inclui a distribuição de todos os valores em cada nó, as probabilidades em cada nível da árvore e as fórmulas de regressão dos atributos contínuos. Para obter mais informações, consulte [Conteúdo do modelo de mineração para modelos de árvore de decisão &#40;Analysis Services – Data Mining&#41;](mining-model-content-for-decision-tree-models-analysis-services-data-mining.md).

## <a name="creating-predictions"></a>Criando previsões
 Depois que o modelo foi processado, os resultados são armazenados como um conjunto de padrões e estatísticas. Esse conjunto pode ser usado para explorar relações e fazer previsões.

 Para obter exemplos de consultas a usar com um modelo de árvores de decisão, consulte [Exemplos de consulta de modelo de árvores de decisão](decision-trees-model-query-examples.md).

 Para obter informações gerais sobre como criar consultas com base em modelos de mineração, consulte [Consultas de mineração de dados](data-mining-queries.md).

## <a name="remarks"></a>Comentários

-   Suporta o uso de PMML (Predictive Model Markup Language) para criar modelos de mineração.

-   Dá suporte ao detalhamento.

-   Dá suporte ao uso de modelos de mineração OLAP e à criação de dimensões de mineração de dados.

## <a name="see-also"></a>Consulte Também
 [Algoritmos de mineração de dados &#40;mineração de dados de Analysis Services&#41;](data-mining-algorithms-analysis-services-data-mining.md) [algoritmo árvores de decisão de referência técnica](microsoft-decision-trees-algorithm-technical-reference.md) [modelo](decision-trees-model-query-examples.md) [de árvores de decisão Analysis Services &#40;do](mining-model-content-for-decision-tree-models-analysis-services-data-mining.md) Microsoft


