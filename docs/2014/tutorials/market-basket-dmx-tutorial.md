---
title: Tutorial do DMX de cesta de mercado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- DMX [Analysis Services], tutorials
- data mining [Analysis Services], tutorials
- statements [DMX], tutorials
- Data Mining Extensions [Analysis Services], tutorials
- market basket analysis [Analysis Services]
- tutorials [Data Mining]
- tutorials [DMX]
ms.assetid: 6e262a1d-c89e-4033-8368-46cf25168ef5
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: fe12f1c4ca1c0946572c61e89f4f4edb8ba9a762
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63185645"
---
# <a name="market-basket-dmx-tutorial"></a>Tutorial de DMX do Market Basket
  Nesse tutorial, você aprenderá como criar, treinar e explorar modelos de mineração de dados, utilizando a linguagem de consulta DMX. Você então utilizará esses modelos de mineração de dados para criar previsões que descrevem quais produtos tendem a ser adquiridos ao mesmo tempo.  
  
 Os modelos de mineração serão criados a partir dos dados contidos no banco de dados de exemplo [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] , que armazena dados para a empresa fictícia [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]. 
  [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] é uma grande empresa industrial e multinacional. A empresa fabrica e vende bicicletas de metal e compostas para os mercados norte-americano, europeu e asiático. Suas operações principais estão situadas em Bothell, Washington, com 290 funcionários, e tem várias equipes regionais de vendas distribuídas por toda a sua base de mercado internacional.  
  
## <a name="tutorial-scenario"></a>Cenário do tutorial  
 
  [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] decidiu criar um aplicativo personalizado que utilize a funcionalidade de mineração de dados para prever que tipos de produtos seus clientes tendem a comprar ao mesmo tempo. A meta do aplicativo personalizado é poder especificar um conjunto de produtos e prever quais produtos adicionais serão adquiridos com os produtos especificados. O [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] usará essas informações para adicionar um recurso de "sugestão" a seu site, e também para organizar melhor a maneira como as informações são apresentadas a seus clientes.  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] fornece várias ferramentas que podem ser usadas para realizar essa [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] tarefa:  
  
-   A linguagem de consulta DMX  
  
-   O [algoritmo de associação da Microsoft](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md)  
  
-   Editor de Consultas do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]  
  
 DMX (Extensões de Mineração de Dados) é uma linguagem de consulta fornecida por [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que pode ser usada para criar e trabalhar com modelos de mineração. O [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo de associação cria modelos que podem prever os produtos que provavelmente serão comprados juntos.  
  
 O objetivo deste tutorial é fornecer as consultas DMX que serão usadas no aplicativo personalizado.  
  
 **Para obter mais informações: soluções de mineração de** [dados](../../2014/analysis-services/data-mining/data-mining-solutions.md)  
  
## <a name="mining-structure-and-mining-models"></a>Estrutura de mineração e modelos de mineração  
 Antes de começar a criar instruções DMX, é importante compreender os objetos principais que o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usa para criar modelos de mineração. A *estrutura de mineração* é uma estrutura de dados que define o domínio de dados do qual os modelos de mineração são criados. Uma única estrutura de mineração pode conter vários *modelos de mineração* que compartilham o mesmo domínio. Um modelo de mineração aplica um algoritmo de modelo de mineração aos dados que são representados por uma estrutura de mineração.  
  
 Os blocos de construção da estrutura de mineração são as colunas da estrutura de mineração, que descrevem os dados que a fonte de dados contém. Essas colunas contêm informações como tipo de dados, tipo de conteúdo e como os dados são distribuídos.  
  
 Os modelos de mineração devem conter a coluna de chave descrita na estrutura de mineração, bem como um subconjunto das colunas restantes. O modelo de mineração define o uso para cada coluna e define o algoritmo que é utilizado para criar o modelo de mineração. Por exemplo, em DMX você pode especificar que uma coluna é uma coluna de chave ou uma coluna PREDICT. Se uma coluna não for especificada, será assumido que é uma coluna de entrada.  
  
 Em DMX, há dois modos para criar modelos de mineração. Você pode criar a estrutura de mineração e o modelo de mineração associado juntos utilizando a instrução `CREATE MINING MODEL`, ou pode criar primeiro uma estrutura de mineração utilizando a instrução `CREATE MINING STRUCTURE` e, em seguida, adicionar um modelo de mineração à estrutura utilizando a instrução `ALTER STRUCTURE`. Estes métodos são descritos abaixo.  
  
 `CREATE MINING MODEL`  
 Use esta instrução para criar juntos uma estrutura de mineração e um modelo de mineração associado que usa o mesmo nome. O nome de modelo de mineração é acrescentado com "Structure" para diferenciá-lo da estrutura de mineração.  
  
 Esta instrução será útil se você estiver criando uma estrutura de mineração que conterá um único modelo de mineração.  
  
 Para obter mais informações, consulte [CREATE MINING MODEL &#40;DMX&#41;](/sql/dmx/create-mining-model-dmx).  
  
 CRIAR UMA ESTRUTURA DE MINERAÇÃO  
 Use essa declaração para criar uma nova estrutura de mineração sem-modelos.  
  
 Ao usar CREATE MINING STRUCTURE, você também poderá criar um conjunto de dados de validação que poderá ser usado para teste de modelos baseados na mesma estrutura de mineração.  
  
 Para obter mais informações, consulte [CREATE MINING STRUCTURE &#40;DMX&#41;](/sql/dmx/create-mining-structure-dmx).  
  
 `ALTER MINING STRUCTURE`  
 Use esta instrução para acrescentar um modelo de mineração a uma estrutura de mineração que já existe no servidor.  
  
 Há várias razões pelas quais você deseja adicionar mais de um modelo de mineração em uma única estrutura de mineração. Por exemplo, você poderia criar vários modelos de mineração utilizando algoritmos diferentes para ver qual trabalha melhor. Como alternativa, você poderia criar vários modelos de mineração usando o mesmo algoritmo, mas com um conjunto de parâmetros definido de modo diferente para cada modelo de mineração a fim de encontrar a melhor definição para o parâmetro.  
  
 Para obter mais informações, consulte [ALTER MINING STRUCTURE &#40;DMX&#41;](/sql/dmx/alter-mining-structure-dmx?view=sql-server-2016).  
  
 Como você criará uma estrutura que contém vários modelos de mineração, utilizará o método secundário neste tutorial.  
  
 **Para obter mais informações**  
  
 [As extensões de mineração de dados &#40;referência&#41; DMX](/sql/dmx/data-mining-extensions-dmx-reference), [compreendendo a instrução DMX SELECT](/sql/dmx/understanding-the-dmx-select-statement), a [estrutura e o uso de consultas de previsão DMX](/sql/dmx/structure-and-usage-of-dmx-prediction-queries)  
  
## <a name="what-you-will-learn"></a>O que você aprenderá  
 Ele se divide nas lições a seguir:  
  
 [Lição 1: Criando a estrutura de mineração do Market Basket](../../2014/tutorials/lesson-1-creating-the-market-basket-mining-structure.md)  
 Nesta lição, você aprenderá a usar a instrução `CREATE` para criar estruturas de mineração.  
  
 [Lição 2: Adicionando modelos de mineração à estrutura de mineração do Market Basket](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md)  
 Nesta lição, você aprenderá a usar a instrução `ALTER` para adicionar modelos de mineração a uma estrutura de mineração.  
  
 [Lição 3: Processando a estrutura de mineração do Market Basket](../../2014/tutorials/lesson-3-processing-the-market-basket-mining-structure.md)  
 Nesta lição, você aprenderá a usar a instrução `INSERT INTO` para processar estruturas de mineração e seus modelos de mineração associados.  
  
 [Lição 4: Executando previsões de Market Basket](../../2014/tutorials/lesson-4-executing-market-basket-predictions.md)  
 Nesta lição, você aprenderá a usar a instrução `PREDICTION JOIN` para criar previsões em relação aos modelos de mineração.  
  
## <a name="requirements"></a>Requisitos  
 Antes de fazer este tutorial, verifique se os seguintes itens estão instalados:  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   O banco de dados [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]  
  
 Por padrão, e para reforçar a segurança, os bancos de dados de exemplo não são instalados. Para instalar os bancos de dados de exemplo oficiais [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]do, vá [http://www.CodePlex.com/MSFTDBProdSamples](https://go.microsoft.com/fwlink/?LinkId=88417) para ou no Microsoft SQL Server exemplos e projetos da Comunidade home page na seção Microsoft SQL Server exemplos de produto. Clique em **Bancos de Dados**e, em seguida, clique na guia **Releases** e selecione o banco de dados desejado.  
  
> [!NOTE]  
>  Ao examinar os tutoriais, recomendamos que você adicione os botões **Próximo Tópico** e **Tópico Anterior** à barra de ferramentas do visualizador de documentos.  
  
## <a name="see-also"></a>Consulte Também  
 [Tutorial DMX do comprador de bicicletas](../../2014/tutorials/bike-buyer-dmx-tutorial.md)   
 [Tutorial de mineração de dados básico](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [Lição 3: Criando um cenário de cesta de mercado &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
  
  
