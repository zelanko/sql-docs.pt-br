---
title: Explorando e limpando dados | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 7c888c95-8986-461e-9f11-2395044b9d97
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 79d356aa1b14ac30ba5bc9a8f579fc66ddebea92
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66081269"
---
# <a name="exploring-and-cleaning-data"></a>Explorando e limpando dados
  A preparação dos dados é muito mais do que limpeza de dados. Lembre-se de que o modo como os dados são preparados também afeta como os resultados são interpretados no final. A preparação dos dados envolve as seguintes tarefas:  
  
-   Exploração e verificação da distribuição dos dados.  
  
-   Limpeza de registros incorretos e escolha das colunas para a mineração de dados.  
  
-   Tratamento incorreto de nulos.  
  
-   Compartimentalização ou agregação de valores por diferentes partes de tempo.  
  
-   Adição de rótulos para aumentar a usabilidade dos resultados.  
  
-   Conversão dos tipos de dados ou categorização de valores se necessário para análise.  
  
 Se você for novo na modelagem de dados, é recomendável ler o tópico relacionado, [lista de verificação de preparação para mineração de dados](checklist-of-preparation-for-data-mining.md).  
  
## <a name="data-preparation-tools"></a>Ferramentas de preparação de dados  
 Os Suplementos de Mineração de Dados para Office incluem as seguintes ferramentas para limpeza e preparação dos dados:  
  
### <a name="explore-data"></a>Explorar Dados  
 Use o assistente para **explorar dados** para estas tarefas de preparação de dados:  
  
-   Visualize seus dados e identifique erros que devem ser corrigidos antes da análise.  
  
-   Colete informações estatísticas úteis para entender o equilíbrio dos dados e as tarefas de limpeza necessárias.  
  
-   Identifique colunas que sejam úteis para análise e planeje a fase de modelagem de dados.  
  
 [Explore os dados &#40;SQL Server suplementos de mineração de dados&#41;](explore-data-sql-server-data-mining-add-ins.md).  
  
### <a name="detect-and-handle-outliers"></a>Detectar exceções e lidar com elas  
 O assistente de **exceções** grafa a distribuição de valores em seus dados e ajuda você a remover valores extremos. Use a ferramenta de **exceções** para as seguintes tarefas de preparação de dados:  
  
-   Determine se valores individuais são confiáveis, com base em padrões encontrados nos dados.  
  
-   Examine os valores incomuns e tome uma ação ao excluí-los ou substituí-los.  
  
-   Faça um escopo de um modelo para um intervalo de valores específicos. Por exemplo, se você souber que tem exceções em um armazenamento em particular, poderá eliminar esse valor e obter um modelo que preveja melhor outros armazenamentos.  
  
 As [exceções &#40;SQL Server suplementos de mineração de dados&#41;](outliers-sql-server-data-mining-add-ins.md).  
  
### <a name="relabel-and-bin-data"></a>Rotular Novamente e Guardar Dados  
 O assistente de **rerotulação** agrupa dados por valores para que você possa alterar os rótulos nos dados. Use a ferramenta Rotular Novamente para estas tarefas de preparação de dados:  
  
-   Altere códigos numéricos usados nos resultados da pesquisa para uma descrição textual do significado do código numérico.  
  
     Por exemplo, você pode substituir entradas de dados como Sexo = 1 por Sexo = Feminino.  
  
-   Guarde os dados, criando grupos que representam intervalos de número.  
  
     Por exemplo, talvez você queira substituir uma coluna de renda de números por rótulos como **receita-moderada** e **renda alta**.  
  
-   Recolher valores discretos em categorias.  
  
     Por exemplo, se você tiver muitos produtos individuais para detectar um padrão entre compras, poderá tentar atribuir produtos em categorias mais amplas.  
  
 [Rerotular &#40;SQL Server os suplementos de mineração de dados&#41;](relabel-sql-server-data-mining-add-ins.md)  
  
### <a name="cleanse-data"></a>Limpar dados  
 A limpeza de dados inclui uma ampla gama de atividades, a maioria das quais têm suporte pelos suplementos  
  
-   Identificar nulos e determinar se devem ser alterados para um valor real ou se devem ser tratados como valores `Missing`.  
  
-   Detecte valores ausentes e remova-os ou impute um valor adequado, como um valor médio, nulo ou outro.  
  
 [Explorar dados &#40;SQL Server suplementos de mineração de dados&#41;](explore-data-sql-server-data-mining-add-ins.md)  
  
 [Rerotular &#40;SQL Server os suplementos de mineração de dados&#41;](relabel-sql-server-data-mining-add-ins.md)  
  
 [Preencher com Base no Exemplo](fill-from-example-table-analysis-tools-for-excel.md)  
  
### <a name="sample-data"></a>Dados de Amostra  
 O assistente de Dados de Amostra fornece dois métodos para criar conjuntos de dados balanceados para modelos de treinamento e teste.  
  
-   **Amostragem aleatória.** Use esta opção para extrair um conjunto representativo de dados de um conjunto de dados maior, para usar em treinamento ou teste. Os suplementos de mineração de dados usam a *amostragem de sobreratificação* para garantir que um conjunto equilibrado de valores seja obtido para cada variável amostrada.  
  
-   **Sobreamostragem.** Use essa opção quando você tiver menos dados do que desejar para um resultado de destino, e precisar pesar esses dados de maneira mais pesada. Por exemplo, a fraude pode ser relativamente rara, mas você pode sobreamostrar os casos que envolvem fraude para obter dados suficientes para modelagem.  
  
 [Dados de exemplo &#40;SQL Server suplementos de mineração de dados&#41;](sample-data-sql-server-data-mining-add-ins.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Criando um modelo de mineração de dados](creating-a-data-mining-model.md)   
 [Validando modelos e usando modelos para previsão &#40;suplementos de mineração de dados para Excel&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)   
 [Implantando e dimensionando modelos de mineração &#40;suplementos de mineração de dados para Excel&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
