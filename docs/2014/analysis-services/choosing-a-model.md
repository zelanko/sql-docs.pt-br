---
title: Escolhendo um modelo | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining algorithms
- mining models
- mining structures
- data mining models
- data mining structures
ms.assetid: 444bbf9c-cec8-460e-881d-38784fb146fa
author: minewiskan
ms.author: owend
ms.openlocfilehash: 0f3b1e504b7e027e888458b8cc2eaee169ca272f
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527532"
---
# <a name="choosing-a-model"></a>Escolhendo um modelo
  **Algoritmo de mineração:** O *algoritmo* Data Mining é o mecanismo que cria padrões a partir de dados. Esse algoritmo define o modo como os dados são contados, como as relações são derivadas e como os padrões são armazenados. A seleção de um algoritmo depende parcialmente do tipo de dados que você deseja analisar. Por exemplo, alguns algoritmos só podem funcionar com números contínuos, enquanto que outros funcionam melhor com um número limitado de valores distintos.  
  
 **Modelo de mineração:** O resultado da análise de dados por um algoritmo é salvo em um *modelo de mineração*. Um modelo de mineração é uma coleção de regras, estatísticas e padrões. O *conteúdo* do modelo de mineração depende do algoritmo que você usou para processar os dados, mas pode incluir o seguinte:  
  
-   Regras Se-então que descrevem como são agrupados produtos em uma transação.  
  
-   Uma árvore de decisão que rastreia os caminhos que levam a um resultado, com probabilidades para a ocorrência de cada caminho.  
  
-   Um modelo matemático com equações para o modelo como um todo ou para segmentos do modelo.  
  
-   Coleções de itens semelhantes (chamados de *clusters* ou *segmentos*) que são definidos pelas características que eles compartilham e por uma pontuação de similaridade.  
  
-   *Nós* em uma rede, conectados por *bordas*. Os nós representam itens ou grupos de itens. As bordas são pontuadas de acordo com a intensidade das relações entre os nós.  
  
 **Usando o modelo:** Depois de criar um modelo, você pode usar os visualizadores fornecidos para explorá-lo ou pode criar uma consulta no modelo. As consultas podem ser usadas para:  
  
-   Prever valores futuros.  
  
-   Gerar um conjunto de produtos relacionados ou recomendados.  
  
-   Retornar regras, padrões ou fórmulas no modelo.  
  
-   Obter metadados do modelo.  
  
-   Fornecer a probabilidade e dar suporte a pontuações para todas ou algumas previsões.  
  
## <a name="types-of-machine-learning-algorithms"></a>Tipos de algoritmos de Machine Learning  
 Como tipos diferentes de algoritmos usam os dados de maneiras diferentes, você deve selecionar o algoritmo apropriado para suas metas e para os dados que deseja analisar ao criar um modelo.  
  
 Os Suplementos de Mineração de Dados para Excel incluem os tipos abrangentes de algoritmos a seguir:  
  
-   *Algoritmos de classificação*.  
  
     Preveem uma ou mais variáveis discretas, com base nos outros atributos do conjunto de dados.  
  
-   *Algoritmos de regressão*  
  
     Preveem uma ou mais variáveis contínuas, como lucro ou perda, com base nos outros atributos do conjunto de dados.  
  
-   *Algoritmos de segmentação*  
  
     Dividem dados em grupos ou clusters de itens que têm propriedades semelhantes.  
  
-   *Algoritmos de associação*  
  
     Encontram correlações entre atributos diferentes em um conjunto de dados. Esse tipo de algoritmo é mais comumente usado para criar regras de associação. As regras de associação podem ser usadas em uma análise da cesta de compras.  
  
-   *Algoritmos de análise de sequência*  
  
     Resumem sequências frequentes ou episódios em dados, como os caminhos que os usuários seguem quando navegam em um site.  
  
 Os algoritmos usados pelos Suplementos de Mineração de Dados do SQL Server para Office se baseiam nos algoritmos fornecidos pelo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Você também pode usar algoritmos de terceiros que estão em conformidade com a OLE DB para especificação de mineração de dados, se a instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] à qual você está conectado tiver sido configurada para permitir algoritmos de terceiros.  
  
## <a name="requirements"></a>Requisitos  
 Cada algoritmo difere no tipo de dados com os quais pode trabalhar.  
  
-   Um modelo de regressão linear somente pode modelar valores numéricos. As suas variáveis de entrada e os resultados de destino devem ser tipos numéricos contínuos. Use um modelo de estimativa ou de árvore de decisão se quiser misturar variáveis discretas e contínuas.  
  
-   Um modelo Naïve Bayes exige que todos os números sejam compartimentados. Se você usar um dos assistentes baseados neste algoritmo, a compartimentalização será executada automaticamente para você.  
  
-   Um modelo de árvore de decisão pode conter variáveis discretas e contínuas. No entanto, os números serão compartimentados automaticamente conforme o necessário para divisões na árvore.  
  
-   As redes neurais e os modelos de regressão logística automaticamente compartimentam números usados como resultados ou variáveis de entrada. Se você quiser agrupar os números de acordo com outros critérios, deverá usar a ferramenta Rotular Novamente para criar os agrupamentos antes da modelagem. Por exemplo, talvez você queira agrupar valores em uma coluna de **idade** por decis (10-20, 21-30 e assim por diante), em vez dos agrupamentos estatisticamente significativos encontrados pelo modelo (um exemplo pode ser 35.6-41.8 anos).  
  
-   Um modelo de associação exige que os dados sejam agrupados em transações, cada uma fazendo referência a vários itens ou linhas. Se você estiver usando o [Assistente de associação &#40;o assistente de&#41;do cliente de mineração de dados para Excel](associate-wizard-data-mining-client-for-excel.md) ou a [análise da cesta de compras &#40;tabela AnalysisTools para a ferramenta de&#41;do Excel](shopping-basket-analysis-table-analysistools-for-excel.md) , os dados deverão ser dispostos conforme mostrado na guia **associar** da pasta de trabalho de exemplo.  
  
     Se você quiser usar tabelas aninhadas em uma fonte de dados externa, deverá usar a [modelagem avançada &#40;suplementos de mineração de dados para&#41;](advanced-modeling-data-mining-add-ins-for-excel.md) opções de modelagem do Excel para criar uma estrutura de mineração e um modelo de mineração que é salvo no servidor. O Excel não dá suporte a tabelas aninhadas.  
  
## <a name="feature-selection"></a>Seleção de recursos  
 Dependendo do conjunto de dados, o algoritmo pode aplicar a *seleção de recursos*, eliminar colunas que não são úteis e determinar quais colunas de dados são estatisticamente significativas em relação ao resultado.  
  
 Cada algoritmo usa métodos ligeiramente diferentes da seleção de recursos (como entropia ou várias pontuações de informações) para determinar quais tendências são importantes e quais diferenças podem ser descartadas.  
  
 Nos suplementos de mineração de dados para Excel, a seleção de recursos é aplicada automaticamente, usando o método de pontuação adequado para cada algoritmo. Se você quiser afetar os resultados da seleção de recursos, use os assistentes na faixa de opção **mineração de dados** e clique em **avançado** para definir os parâmetros usando a caixa de diálogo **parâmetros de algoritmo** .  
  
 Para obter uma lista dos métodos de seleção de recursos usados por cada algoritmo, consulte o tópico sobre [seleção de recursos &#40;mineração de dados&#41;](data-mining/feature-selection-data-mining.md) em manuais online do SQL Server.  
  
## <a name="list-of-supported-algorithms"></a>Lista de algoritmos com suporte  
 Os seguintes algoritmos são fornecidos por padrão.  
  
|Nome do algoritmo|Description|Usado em|  
|--------------------|-----------------|-------------|  
|Regras de Associação da Microsoft|Cria regras que descrevem quais itens provavelmente aparecem juntos em uma transação.|[Assistente para associar &#40;cliente de mineração de dados para Excel&#41;](associate-wizard-data-mining-client-for-excel.md)<br /><br /> [Análise de cesta de compras &#40;tabela AnalysisTools para Excel&#41;](shopping-basket-analysis-table-analysistools-for-excel.md)|  
|Microsoft Clustering|Identifica relações em um conjunto de dados que talvez não sejam derivadas de forma lógica por meio de observação casual. Usa técnicas iterativas para agrupar registros em clusters que contenham características semelhantes.|[Detectar categorias &#40;ferramentas de análise de tabela para Excel&#41;](detect-categories-table-analysis-tools-for-excel.md)<br /><br /> [Assistente de cluster &#40;suplementos de mineração de dados para Excel&#41;](cluster-wizard-data-mining-add-ins-for-excel.md)|  
|Árvores de Decisão da Microsoft|Faz previsões com base nas relações entre colunas no conjunto de dados e modela as relações como uma série de divisões semelhantes a uma árvore aplicadas a valores específicos.<br /><br /> Dá suporte à previsão de atributos discretos e contínuos.|[Assistente de classificação &#40;suplementos de mineração de dados para Excel&#41;](classify-wizard-data-mining-add-ins-for-excel.md)<br /><br /> [Assistente de estimativa &#40;suplementos de mineração de dados para Excel&#41;](estimate-wizard-data-mining-add-ins-for-excel.md)|  
|Regressão Linear da Microsoft|Se houver uma dependência linear entre a variável de destino e as variáveis sendo examinadas, encontra a relação mais eficiente entre o destino e suas entradas.<br /><br /> Dá suporte à previsão de atributos contínuos.|Esse algoritmo está disponível no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Nos Suplementos de Mineração de Dados para Office, você pode criar um modelo que use esse algoritmo criando uma estrutura e adicionando um modelo manualmente.<br /><br /> Para obter mais informações, consulte [modelagem avançada &#40;suplementos de mineração de dados para Excel&#41;](advanced-modeling-data-mining-add-ins-for-excel.md).|  
|Regressão Logística da Microsoft|Analisa os fatores que contribuem para um resultado, em que o resultado fica restrito a dois valores, geralmente a ocorrência ou não de um evento.<br /><br /> Dá suporte à previsão de atributos discretos e contínuos.|[Preencha com o exemplo &#40;ferramentas de análise de tabela para Excel&#41;](fill-from-example-table-analysis-tools-for-excel.md)<br /><br /> [Cenário de busca de meta &#40;ferramentas de análise de tabela para Excel&#41;](goal-seek-scenario-table-analysis-tools-for-excel.md)<br /><br /> [Cenário de hipóteses &#40;ferramentas de análise de tabela para Excel&#41;](what-if-scenario-table-analysis-tools-for-excel.md)<br /><br /> [Cálculo de Previsão &#40;ferramentas de análise de tabela para Excel&#41;](prediction-calculator-table-analysis-tools-for-excel.md)|  
|Microsoft Naïve Bayes|Encontra a probabilidade da relação entre todas as colunas de entrada e previsíveis. Esse algoritmo é útil para gerar rapidamente modelos de mineração para descobrir relações.<br /><br /> Dá suporte apenas a atributos discretos ou discretizados.<br /><br /> Trata todos os atributos de entrada como independentes.|[Analisar os influenciadores principais &#40;ferramentas de análise de tabela para Excel&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)|  
|Rede Neural da Microsoft|Analisa dados de entrada complexos ou problemas comerciais para os quais uma quantidade significativa de dados de treinamento está disponível, mas para os quais também não é possível derivar regras facilmente usando outros algoritmos.<br /><br /> Pode prever vários atributos.<br /><br /> Pode ser usado para classificar atributos discretos e regressão de atributos contínuos.|Esse algoritmo está disponível no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Nos Suplementos de Mineração de Dados para Office, você pode criar um modelo que use esse algoritmo criando uma estrutura e adicionando um modelo manualmente.<br /><br /> Para obter mais informações, consulte [modelagem avançada &#40;suplementos de mineração de dados para Excel&#41;](advanced-modeling-data-mining-add-ins-for-excel.md).|  
|Microsoft Sequence Clustering|Identifica clusters de eventos ordenados similarmente em uma sequência.<br /><br /> Fornece uma combinação de análise de sequência e clustering.|Este algoritmo está disponível apenas no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. No entanto, nos Suplementos de Mineração de Dados para Office, você pode criar um modelo que use esse algoritmo criando uma estrutura e adicionando um modelo manualmente.<br /><br /> Para obter mais informações, consulte [modelagem avançada &#40;suplementos de mineração de dados para Excel&#41;](advanced-modeling-data-mining-add-ins-for-excel.md).|  
|Microsoft Time Series|Analisa dados relacionados ao tempo usando uma árvore de decisão linear.<br /><br /> Os padrões podem ser usados para prever valores futuros na série temporal.|[Previsão de &#40;ferramentas de análise de tabela para Excel&#41;](forecast-table-analysis-tools-for-excel.md)<br /><br /> [Assistente de previsão &#40;suplementos de mineração de dados para Excel&#41;](forecast-wizard-data-mining-add-ins-for-excel.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [O que está incluído nos Suplementos de Mineração de Dados para o Office](what-s-included-in-the-data-mining-add-ins-for-office.md)  
  
  
