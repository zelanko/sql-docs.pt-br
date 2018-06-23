---
title: Lista de verificação de preparação para mineração de dados | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0e056c95-ba06-413e-8dc1-4d411a447c3b
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 4f7429dd799a1081bd1a03e985a8772b04498129
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122286"
---
# <a name="checklist-of-preparation-for-data-mining"></a>Lista de verificação de preparação para mineração de dados
  Embora os suplementos de mineração de dados tornem as experiências com modelos algo fácil e divertido, quando você precisar obter resultados repetíveis e acionáveis, deverá aguardar um tempo suficiente para formular requisitos empresariais básicos e para obter e preparar dados. Esta seção fornece uma lista de verificação para ajudá-lo a planejar sua investigação e descreve os problemas comuns.  
  
## <a name="checklist-of-data-preparation"></a>Lista de verificação de preparação de dados  
 **Eu identifiquei uma saída claramente definida.**  
 Ter um plano para como você usará os resultados. Tipos de modelos diferentes têm saídas diferentes. Um modelo de série temporal gera valores para uma série no futuro, que são fáceis de entender e utilizar. Outros modelos geram conjuntos complexos que devem ser analisados por especialistas no assunto para produzir um valor maior.  
  
-   Qual saída você deseja?  
  
-   Você pode definir a saída como uma única coluna ou valor ou outro resultado acionável?  
  
-   Quais são os critérios para saber que o modelo foi útil?  
  
-   Como você usará e interpretará esses resultados?  
  
-   Você pode mapear novos dados de entrada para os resultados esperados?  
  
 **Eu sei o significado, tipos de dados e a distribuição dos dados de entrada.**  
 Dedique algum tempo para explorar e entender os dados de origem. É importante que as pessoas que examinam o modelo entendam o tipo de dados de entrada que foi usado e saibam como interpretar os tipos de dados e a variabilidade, bem como o equilíbrio e a qualidade.  
  
-   Qual é a quantidade de dados que você tem? Há dados suficientes para modelar?  
  
     Não precisa ser uma quantidade enorme – é melhor que seja menor e equilibrada.  
  
-   Os dados são de várias origens ou uma única origem?  
  
-   Os dados já foram processados e limpos? Existem mais dados de entrada disponíveis?  
  
-   Você sabe como eles foram manipulados antes de você os receber – como os dados podem ter sido truncados, resumidos ou convertidos?  
  
-   Os dados de entrada têm alguns resultados de exemplo que podem ser usados para treinamento?  
  
 **Entendo que o nível de integridade de dados, que temos e o nível que precisamos.**  
 Dados incorretos podem afetar a qualidade do modelo ou impedir que o modelo seja até mesmo criado. Você deve ter um bom entendimento da distribuição e do significado dos dados, e como eles chegaram a esse estado. Você precisará compreender se é possível ou apropriado simplificar os dados rotulando, truncando tipos de dados numéricos ou resumindo.  
  
-   Rótulos de dados: estão claros e corretos?  
  
-   Tipos de dados: são apropriados e foram modificados?  
  
-   Você classificou, limpou ou descartou os dados errados?  
  
     Você verificou se não há nenhuma duplicata?  
  
-   Como você administrará valores ausentes? Os valores ausentes têm um significado?  
  
-   Você verificou as fontes para ver se algum erro pode ter sido introduzido no processo de importação?  
  
     Onde a entrada está armazenada? Quanto tempo ele permanece disponível?  
  
     Há um dicionário de dados? Você pode criar um?  
  
-   Se você combinou conjuntos de dados, verificou se há várias colunas que representam os mesmos dados?  
  
 **Eu sei onde os dados de origem estão armazenados, de onde vieram e como são processados. O processo pode facilmente ser repetido se necessário.**  
 Os conjuntos de dados únicos são bons para experiências, mas, se você quiser mover o modelo para produção, vai querer planejar como o processo de limpeza pode ser aplicado aos dados operacionais. Além disso, se você tiver dados operacionais, precisará saber como eles podem ter sido alterados antes de você os obter; precisará certamente saber como eles foram arredondados ou resumidos.  
  
-   Você deseja ser capaz de repetir a experiência?  
  
-   Quais ferramentas você usará para preparar dados em um formato que dá suporte à análise de dados? Isso pode ser automatizado ou precisa que alguém examine e limpe no Excel?  
  
-   Se você estiver fornecendo dados de outro sistema, poderá capturar e rastrear os filtros que foram aplicados?  
  
-   Sua estrutura de processamento de dados também pode aplicar algoritmos de aprendizagem de máquina, executar testes e visualizar os resultados?  
  
 **Nós concordamos a granularidade desejada das previsões e nossos dados foram modificados para produzir essas unidades.**  
 Decida sobre a granularidade dos resultados desejados antes de preparar dados. Por exemplo, você deseja as previsões de vendas por dia ou por trimestre? Você deverá considerar estruturas de dados diferentes para os mesmos dados, para tratar níveis diferentes de resumo.  
  
-   Qual é a unidade de medida ou unidade de tempo atual?  
  
     Qual unidade você deseja usar nos resultados?  
  
-   É possível definir uma unidade básica (por exemplo, dia / hora / min / instrução de chamada) para todos os dados de entrada?  
  
     Você deseja fazer rollup para unidades maiores?  
  
-   As categorias são rotuladas consistentemente? É fácil adicionar ou remover categorias?  
  
 **Nosso design de avaliação é repetível e reprodutível.**  
 Considere estratégias para analisar e validar seus resultados e planeje capturar um instantâneo dos dados, para garantir você possa rastrear os efeitos para os dados. Se uma semente aleatória é usada, os resultados poderão variar um pouco. Isso pode dificultar a comparação e a validação de modelos.  
  
-   Se você fizer muitas alterações personalizadas nos dados, o que acontecerá na próxima vez que quiser criar o modelo?  
  
-   Já foi definido um procedimento manual ou um processo aprovado que você deverá usar para processar a entrada e obter os resultados desejados?  
  
-   Você decidiu usar uma semente para o modelo?  
  
 **Podemos ter conhecimento do domínio para validar os resultados ou ter acesso aos especialistas no assunto que podem aconselhar.**  
 Reserve um tempo para validar as variáveis, o modelo e os resultados. Obtenha a ajuda de especialistas para avaliar as interações e os resultados. No entanto, não deixe suposições substituírem a evidência. Esteja aberto a novas e inesperadas descobertas.  
  
-   O conhecimento de domínio está disponível para ajudar a filtrar dados e reduzir o ruído de entrada?  
  
-   Os especialistas de domínio podem ajudar a entender e interpretar os resultados e sugerir melhorias?  
  
## <a name="see-also"></a>Consulte também  
 [Escolhendo os dados para a mineração de dados](choosing-data-for-data-mining.md)  
  
  