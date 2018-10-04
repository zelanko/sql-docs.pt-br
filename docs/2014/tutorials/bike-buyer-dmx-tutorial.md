---
title: Tutorial DMX comprador de bicicleta | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- DMX [Analysis Services], tutorials
- data mining [Analysis Services], tutorials
- statements [DMX], tutorials
- Data Mining Extensions [Analysis Services], tutorials
- tutorials [Data Mining]
ms.assetid: 4b634cc1-86dc-42ec-9804-a19292fe8448
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2d5b77952cd3476adddcdf0a528c2e12ab30cc2b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48074956"
---
# <a name="bike-buyer-dmx-tutorial"></a>Tutorial DMX Comprador de bicicleta
  Nesse tutorial, você aprenderá a criar, treinar e explorar modelos de mineração de dados com o uso da linguagem de consulta DMX (Extensões de Mineração de Dados). Você então utilizará esses modelos de mineração de dados para criar previsões que determinem se um cliente comprará uma bicicleta.  
  
 Os modelos de mineração serão criados a partir dos dados contidos no banco de dados de exemplo [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)], que armazena dados para a empresa fictícia [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]. [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] é uma grande empresa industrial e multinacional. A empresa fabrica e vende bicicletas de metal e compostas para os mercados norte-americano, europeu e asiático. A central de operações está situada em Bothell, Washington, com 290 funcionários, e possui várias equipes regionais de vendas distribuídas por toda a sua base de mercado internacional.  
  
## <a name="tutorial-scenario"></a>Cenário do tutorial  
 A [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] decidiu estender a análise de dados, criando um aplicativo personalizado que usa a funcionalidade de data mining. Sua meta para o aplicativo personalizado é ser capaz de:  
  
-   Usar como entrada as características específicas sobre um cliente potencial e prever se eles comprarão uma bicicleta.  
  
-   Usar como entrada uma lista de cliente potenciais, assim como características sobre clientes e prever quais comprarão uma bicicleta.  
  
 No primeiro caso, os dados de cliente são fornecidos por uma página de registro de cliente e, no segundo caso, uma lista de clientes potenciais é fornecida pelo departamento de marketing da [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)].  
  
 Além disso, o departamento de marketing solicitou a capacidade de agrupar clientes existentes em categorias com base em características como onde eles vivem, o número de filhos que possuem e a distância do trabalho. Eles querem consultar se esses agrupamentos podem ser usados para ajudar a estabelecer como meta tipos específicos de clientes. Isso irá requerer um modelo de mineração adicional.  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] fornece várias ferramentas que podem ser usadas para realizar essas tarefas:  
  
-   A linguagem de consulta DMX  
  
-   O [algoritmo árvores de decisão da Microsoft](../../2014/analysis-services/data-mining/microsoft-decision-trees-algorithm.md) e o [algoritmo Microsoft Clustering](../../2014/analysis-services/data-mining/microsoft-clustering-algorithm.md)  
  
-   Editor de Consultas do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]  
  
 DMX (Extensões de Mineração de Dados) é uma linguagem de consulta fornecida por [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que pode ser usada para criar e trabalhar com modelos de mineração. O algoritmo Árvores de Decisão da [!INCLUDE[msCoName](../includes/msconame-md.md)] cria modelos que podem ser usados para prever se alguém comprará uma bicicleta. O modelo resultante pode usar cliente individual ou uma tabela de clientes como uma entrada. O algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Clustering pode criar agrupamentos de clientes com base em características compartilhadas. O objetivo deste tutorial é fornecer os scripts DMX que serão usados no aplicativo personalizado.  
  
 **Para obter mais informações:** [soluções de mineração de dados](../../2014/analysis-services/data-mining/data-mining-solutions.md)  
  
## <a name="mining-structure-and-mining-models"></a>Estrutura de mineração e modelos de mineração  
 Antes de começar a criar instruções DMX, é importante compreender os objetos principais que o  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usa para criar modelos de mineração. A estrutura de mineração é uma estrutura de dados que define o domínio de dados do qual modelos de mineração são criados. Uma única estrutura de mineração pode conter vários modelos de mineração que compartilham o mesmo domínio. Um modelo de mineração aplica um algoritmo de modelo de mineração aos dados que são representados por uma estrutura de mineração.  
  
 Os blocos de construção da estrutura de mineração são as colunas da estrutura de mineração, que descrevem os dados que a fonte de dados contém. Essas colunas contêm informações como tipo de dados, tipo de conteúdo e como os dados são distribuídos.  
  
 Os modelos de mineração devem conter a coluna de chave descrita na estrutura de mineração, bem como um subconjunto das colunas restantes. O modelo de mineração define o uso para cada coluna e define o algoritmo que é utilizado para criar o modelo de mineração. Por exemplo, em DMX você pode especificar que uma coluna é uma coluna de chave ou uma coluna PREDICT. Se uma coluna não for especificada, será assumido que é uma coluna de entrada.  
  
 Em DMX, há dois modos para criar modelos de mineração. Você pode criar a estrutura de mineração e o modelo de mineração associado juntos utilizando a instrução CREATE MINING MODEL, ou pode criar primeiro uma estrutura de mineração utilizando a instrução CREATE MINING STRUCTURE e, em seguida, adicionar um modelo de mineração à estrutura utilizando a instrução ALTER STRUCTURE. Esses métodos são descritos na tabela a seguir.  
  
 CREATE MINING MODEL  
 Use esta instrução para criar juntos uma estrutura de mineração e um modelo de mineração associado que usa o mesmo nome. O nome de modelo de mineração é acrescentado com "Structure" para diferenciá-lo da estrutura de mineração. Esta instrução será útil se você estiver criando uma estrutura de mineração que conterá um único modelo de mineração.  
  
 Para obter mais informações, consulte [CREATE MINING MODEL &#40;DMX&#41;](/sql/dmx/create-mining-model-dmx).  
  
 ALTER MINING STRUCTURE  
 Use esta instrução para acrescentar um modelo de mineração a uma estrutura de mineração que já existe no servidor. Essa instrução será útil se você quiser criar uma estrutura de mineração que contenha vários modelos de mineração diferentes. Há várias razões pelas quais você deseja adicionar mais de um modelo de mineração em uma única estrutura de mineração. Por exemplo, é possível criar vários modelos de mineração que usam algoritmos diferentes para verificar qual algoritmo funciona melhor. Você pode criar vários modelos de mineração que usam o mesmo algoritmo, mas com um parâmetro definido de modo diferente para cada modelo de mineração a fim de encontrar a melhor definição para o parâmetro.  
  
 Para obter mais informações, consulte [ALTER MINING STRUCTURE &#40;DMX&#41;] ((~/dmx/alter-mining-structure-dmx.md).  
  
 Como você criará uma estrutura que contém vários modelos de mineração, utilizará o método secundário neste tutorial.  
  
 **Para obter mais informações**  
  
 [Extensões de mineração de dados &#40;DMX&#41; referência](/sql/dmx/data-mining-extensions-dmx-reference), [Noções básicas sobre o DMX instrução Select](/sql/dmx/understanding-the-dmx-select-statement), [estrutura e uso de consultas de previsão DMX](/sql/dmx/structure-and-usage-of-dmx-prediction-queries)  
  
## <a name="what-you-will-learn"></a>O que você aprenderá  
 Ele se divide nas lições a seguir:  
  
 [Lição 1: Criando a estrutura de mineração de Comprador de Bicicleta](../../2014/tutorials/lesson-1-creating-the-bike-buyer-mining-structure.md)  
 Nesta lição, você aprenderá a usar a instrução `CREATE` para criar estruturas de mineração.  
  
 [Lição 2: Adicionando modelos de mineração à estrutura de mineração de Comprador de Bicicleta](../../2014/tutorials/lesson-2-adding-mining-models-to-the-bike-buyer-mining-structure.md)  
 Nesta lição, você aprenderá a usar a instrução `ALTER` para adicionar modelos de mineração a uma estrutura de mineração.  
  
 [Lição 3: Processando a estrutura de mineração Comprador de Bicicleta](../../2014/tutorials/lesson-3-processing-the-bike-buyer-mining-structure.md)  
 Nesta lição, você aprenderá a usar a instrução `INSERT INTO` para processar estruturas de mineração e seus modelos de mineração associados.  
  
 [Lição 4: Explorando modelos de mineração Comprador de Bicicleta](../../2014/tutorials/lesson-4-browsing-the-bike-buyer-mining-models.md)  
 Nesta lição, você aprenderá a usar a instrução `SELECT` para explorar o conteúdo dos modelos de mineração.  
  
 [Lição 5: Executando previsão de consultas](../../2014/tutorials/lesson-5-executing-prediction-queries.md)  
 Nesta lição, você aprenderá a usar a instrução `PREDICTION JOIN` para criar previsões em relação aos modelos de mineração.  
  
## <a name="requirements"></a>Requisitos  
 Antes de fazer este tutorial, verifique se os seguintes itens estão instalados:  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)], [!INCLUDE[ssASversion10](../includes/ssasversion10-md.md)], [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)], ou [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   O banco de dados [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]. Por padrão, e para reforçar a segurança, os bancos de dados de exemplo não são instalados. Para instalar os bancos de dados de exemplo oficiais do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], visite o [Microsoft SQL Sample Databases](http://go.microsoft.com/fwlink/?LinkId=88417) página e selecione os bancos de dados que você deseja instalar...  
  
> [!NOTE]  
>  Ao examinar os tutoriais, recomendamos que você adicione os botões **Próximo Tópico** e **Tópico Anterior** à barra de ferramentas do visualizador de documentos.  
  
## <a name="see-also"></a>Consulte também  
 [Tutorial DMX do Market Basket](../../2014/tutorials/market-basket-dmx-tutorial.md)   
 [Tutorial de mineração de dados básico](../../2014/tutorials/basic-data-mining-tutorial.md)  
  
  
