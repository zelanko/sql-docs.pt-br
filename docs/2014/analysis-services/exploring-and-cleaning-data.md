---
title: Explorando e limpando dados | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7c888c95-8986-461e-9f11-2395044b9d97
caps.latest.revision: 7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0200bb66afa6728f3bd5587774dc9f80fb10c5fd
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37304716"
---
# <a name="exploring-and-cleaning-data"></a>Explorando e limpando dados
  A preparação dos dados é muito mais do que limpeza de dados. Lembre-se de que o modo como os dados são preparados também afeta como os resultados são interpretados no final. A preparação dos dados envolve as seguintes tarefas:  
  
-   Exploração e verificação da distribuição dos dados.  
  
-   Limpeza de registros incorretos e escolha das colunas para a mineração de dados.  
  
-   Tratamento incorreto de nulos.  
  
-   Compartimentalização ou agregação de valores por diferentes partes de tempo.  
  
-   Adição de rótulos para aumentar a usabilidade dos resultados.  
  
-   Conversão dos tipos de dados ou categorização de valores se necessário para análise.  
  
 Se você for novo para a modelagem de dados, é recomendável que você leia o tópico relacionado, [lista de verificação de preparação para mineração de dados](checklist-of-preparation-for-data-mining.md).  
  
## <a name="data-preparation-tools"></a>Ferramentas de preparação de dados  
 Os Suplementos de Mineração de Dados para Office incluem as seguintes ferramentas para limpeza e preparação dos dados:  
  
### <a name="explore-data"></a>Explorar Dados  
 Use o **explorar dados** Assistente para essas tarefas de preparação de dados:  
  
-   Visualize seus dados e identifique erros que devem ser corrigidos antes da análise.  
  
-   Colete informações estatísticas úteis para entender o equilíbrio dos dados e as tarefas de limpeza necessárias.  
  
-   Identifique colunas que sejam úteis para análise e planeje a fase de modelagem de dados.  
  
 [Explorar dados &#40;suplementos de mineração de dados do SQL Server&#41;](explore-data-sql-server-data-mining-add-ins.md).  
  
### <a name="detect-and-handle-outliers"></a>Detectar exceções e lidar com elas  
 O **exceções** Assistente representa graficamente a distribuição dos valores de seus dados e ajuda a remover valores extremos. Use o **exceções** ferramenta para as seguintes tarefas de preparação de dados:  
  
-   Determine se valores individuais são confiáveis, com base em padrões encontrados nos dados.  
  
-   Examine os valores incomuns e tome uma ação ao excluí-los ou substituí-los.  
  
-   Faça um escopo de um modelo para um intervalo de valores específicos. Por exemplo, se você souber que tem exceções em um armazenamento em particular, poderá eliminar esse valor e obter um modelo que preveja melhor outros armazenamentos.  
  
 [Exceções &#40;suplementos de mineração de dados do SQL Server&#41;](outliers-sql-server-data-mining-add-ins.md).  
  
### <a name="relabel-and-bin-data"></a>Rotular Novamente e Guardar Dados  
 O **rotular novamente** Assistente agrupa dados por valores para que você possa alterar os rótulos nos dados. Use a ferramenta Rotular Novamente para estas tarefas de preparação de dados:  
  
-   Altere códigos numéricos usados nos resultados da pesquisa para uma descrição textual do significado do código numérico.  
  
     Por exemplo, você pode substituir entradas de dados como Sexo = 1 por Sexo = Feminino.  
  
-   Guarde os dados, criando grupos que representam intervalos de número.  
  
     Por exemplo, você talvez queira substituir uma coluna de receita de números por rótulos como **renda – moderada** e **renda – alta**.  
  
-   Recolher valores discretos em categorias.  
  
     Por exemplo, se você tiver muitos produtos individuais para detectar um padrão entre compras, poderá tentar atribuir produtos em categorias mais amplas.  
  
 [Rotular novamente &#40;suplementos de mineração de dados do SQL Server&#41;](relabel-sql-server-data-mining-add-ins.md)  
  
### <a name="cleanse-data"></a>Limpar dados  
 A limpeza de dados inclui uma ampla gama de atividades, a maioria das quais têm suporte pelos suplementos  
  
-   Identificar nulos e determinar se devem ser alterados para um valor real ou se devem ser tratados como valores `Missing`.  
  
-   Detecte valores ausentes e remova-os ou impute um valor adequado, como um valor médio, nulo ou outro.  
  
 [Explorar dados &#40;suplementos de mineração de dados do SQL Server&#41;](explore-data-sql-server-data-mining-add-ins.md)  
  
 [Rotular novamente &#40;suplementos de mineração de dados do SQL Server&#41;](relabel-sql-server-data-mining-add-ins.md)  
  
 [Preencher com Base no Exemplo](fill-from-example-table-analysis-tools-for-excel.md)  
  
### <a name="sample-data"></a>Dados de Amostra  
 O assistente de Dados de Amostra fornece dois métodos para criar conjuntos de dados balanceados para modelos de treinamento e teste.  
  
-   **Amostragem aleatória.** Use esta opção para extrair um conjunto representativo de dados de um conjunto de dados maior, para usar em treinamento ou teste. Usam os suplementos de mineração de dados *estratificado* para garantir que um conjunto de valores balanceado é obtido para cada variável de exemplo.  
  
-   **Sobreamostragem.** Use essa opção quando você tiver menos dados do que desejar para um resultado de destino, e precisar pesar esses dados de maneira mais pesada. Por exemplo, a fraude pode ser relativamente rara, mas você pode sobreamostrar os casos que envolvem fraude para obter dados suficientes para modelagem.  
  
 [Dados de exemplo &#40;suplementos de mineração de dados do SQL Server&#41;](sample-data-sql-server-data-mining-add-ins.md).  
  
## <a name="see-also"></a>Consulte também  
 [Criar um modelo de mineração de dados](creating-a-data-mining-model.md)   
 [Validando modelos e usando modelos para previsão &#40;Data Mining Add-ins para Excel&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)   
 [Implantando e dimensionando modelos de mineração &#40;Data Mining Add-ins para Excel&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
