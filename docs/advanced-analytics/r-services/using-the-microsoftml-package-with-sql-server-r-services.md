---
title: "Usando o pacote MicrosoftML com o SQL Server R Services | Microsoft Docs"
ms.custom: ""
ms.date: "01/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 1c377717-e281-431e-8171-3924dcce1cdd
caps.latest.revision: 12
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# Usando o pacote MicrosoftML com o SQL Server R Services
O pacote **MicrosoftML** que é fornecido com o Microsoft R Server e SQL Server vNext CTP 1.0 inclui vários algoritmos de aprendizado de máquina desenvolvidos pela Microsoft, que oferecem suporte a streaming rápido de dados e processamento de vários núcleos. O pacote também inclui transformações para processamento de texto e personalização.

### <a name="new-machine-learning-algorithms"></a>Novos algoritmos de aprendizado de máquina


-  **Fast Linear.** Um aprendiz linear com base em ascendente de coordenada dupla alheatória que pode ser usada para classificação binária ou regressão. O modelo dá suporte a regularização L1 e L2.

- **Fast Tree.** Um algoritmo de árvore de decisão ampliado, originalmente conhecido como FastRank, que foi desenvolvido para uso no Bing. É um dos aprendizes mais rápidos e mais populares. Dá suporte a regressão e classificação binária.

- **Fast Forest.** Um modelo de regressão logística com base no método de floresta aleatória. É semelhante à função `rxLogit` do RevoScaleR, mas dá suporte à regularização L1 e L2. Dá suporte a regressão e classificação binária.

- **Logistic Regression.** Um modelo de regressão logística semelhante à função `rxLogit` do RevoScaleR, com suporte adicional para a regularização L1 e L2. Dá suporte à classificação multiclasse ou binária.

- **Neural Net.** Um modelo de rede neural para classificação binária, classificação multiclasse e regressão. Dá suporte à aceleração de GPU e redes complicadas personalizáveis.

- **One-Class SVM.** Um modelo de detecção de anomalias com base no método SVM que pode ser usado para classificação binária em conjuntos de dados desbalanceados.

## <a name="transformation-functions"></a>Funções de transformação

O pacote **MicrosoftML** também inclui as seguintes funções, que podem ser usadas para transformar os dados e extrair recursos.

- `featurizeText()`
 
  Gera as contagens de ngrams em uma cadeia de caracteres de texto especificada. 

  A função inclui as opções para detectar o idioma usado, executar a normalização e a geração de tokens de texto, remover palavras irrelevantes e gerar recursos do texto. 

- `categorical()`

  Cria um dicionário de categorias e transforma cada categoria em um vetor de indicador. 
 
- `categoricalHash()`

  Converte valores categóricos em uma matriz de indicador, transformando o valor em um hash e usando o hash como um índice no multiconjunto.  

- `selectFeatures()` 

  Seleciona um subconjunto de recursos da variável determinada, tanto pela contagem de valores não padrão quanto pela computação de uma pontuação de informações mútuas em relação ao rótulo. 

Para obter informações detalhadas sobre esses novos recursos, consulte as [funções MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml).

## <a name="support-for-microsoftml-in-r-services"></a>Suporte para o MicrosoftML no R Services

O pacote **MicrosoftML** está totalmente integrado com o pipeline de processamento de dados usado pelo pacote **RevoScaleR**. No momento, você pode usar o pacote **MicrosoftML** em qualquer contexto de computação baseado em Windows, incluindo o SQL Server R Services.



## <a name="see-also"></a>Consulte também


[Referência de função RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler)

