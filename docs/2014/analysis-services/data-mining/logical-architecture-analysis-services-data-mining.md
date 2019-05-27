---
title: Arquitetura lógica (Analysis Services - mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], about mining structures
- logical architecture [Data Mining]
- architecture [Analysis Services], mining models
- mining models [Analysis Services], about data mining models
- architecture [Analysis Services]
ms.assetid: 4e0cbf46-cc60-4e91-a292-9a69f29746f0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5702e3e2e5b12edecff4dd6d6f46b632575d211d
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66084273"
---
# <a name="logical-architecture-analysis-services---data-mining"></a>Arquitetura lógica (Analysis Services – Mineração de Dados)
  A mineração de dados é um processo que envolve a interação de vários componentes.  
  
-   Você acessa fontes de dados em um banco de dados SQL Server ou em qualquer outra fonte de dados para usá-los para treinamento, teste e previsão.  
  
-   Você define estruturas de mineração de dados e modelos usando o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ou o Visual Studio.  
  
-   É possível gerenciar objetos de mineração de dados e criar previsões e consultas usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
-   Quando a solução estiver completa, você a implanta em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 O processo de criar estes objetos de solução já foi descrito em outro lugar. Para obter mais informações, consulte [Soluções de mineração de dados](data-mining-solutions.md).  
  

  
##  <a name="bkmk_SourceData"></a> Dados de origem da mineração de dados  
 Os dados usados na mineração de dados não são armazenados na solução de mineração de dados. Apenas as associações são armazenadas. Além disso, os dados podem residir em um banco de dados criado em uma versão anterior do SQL Server, sistema CRM ou mesmo em um arquivo simples. Quando você treina a estrutura ou modelo por processamento, um resumo estatístico dos dados é criado e armazenado em um cache que pode ser persistido para uso em operações subsequentes ou excluídas depois do processamento. Para obter mais informações, consulte [Estruturas de mineração &#40;Analysis Services – Mineração de dados&#41;](mining-structures-analysis-services-data-mining.md).  
  
 Você combina dados discrepantes dentro do objeto de DSV (exibição da fonte de dados) do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que fornece uma camada de abstração sobre sua fonte de dados. Você pode especificar junções entre tabelas ou adicionar as tabelas que têm uma relação muitos para um para criar colunas de tabelas aninhadas. A definição destes objetos, a fonte de dados e a exibição da fonte de dados, é armazenada dentro da solução com as extensões de nome de arquivo *.ds e \*.dsv. Para obter mais informações sobre como criar e usar [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fontes de dados e exibições da fonte de dados, consulte [fontes de dados com suporte &#40;Multidimensional do SSAS&#41;](../multidimensional-models/supported-data-sources-ssas-multidimensional.md).  
  
 Também é possível definir e alterar fontes de dados e exibições de fontes de dados usando AMO ou XMLA. Para obter mais informações sobre como trabalhar com esses objetos programaticamente, consulte [Visão geral da arquitetura lógica &#40;Analysis Services – Dados multidimensionais&#41;](../multidimensional-models/olap-logical/logical-architecture-overview-analysis-services-multidimensional-data.md).  
  

  
##  <a name="bkmk_Structures"></a> Mining Structures  
 Uma estrutura de mineração de dados é um contêiner de dados lógicos que define o domínio de dados do qual modelos de mineração são criados. Uma única estrutura de mineração pode dar suporte a diversos modelos de mineração.  
  
 Quando precisar usar os dados na solução de mineração de dados, o Analysis Services lerá os dados da origem e gerará um cache com agregações e outras informações. Por padrão, este cache é persistido para que os dados de treinamento possam ser reutilizado para dar suporte a modelos adicionais. Se você precisar excluir o cache, altere a propriedade `CacheMode` no objeto da estrutura de mineração para o valor `ClearAfterProcessing`. Para obter mais informações, consulte [Classes de mineração de dados AMO](https://docs.microsoft.com/bi-reference/amo/amo-data-mining-classes).  
  
 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] também fornece a capacidade de separar seus dados em conjuntos de dados treinamento e de teste. Com isso, você pode testar seus modelos de mineração em um conjunto de dados representativo, selecionado aleatoriamente. Os dados não são de fato armazenados separadamente; em vez disso, os dados de caso no cache da estrutura são marcados com uma propriedade que indica se esse caso em particular é usado para treinamento ou teste. Se o cache for excluído, essas informações não poderão ser recuperadas.  
  
 Para obter mais informações, consulte [Estruturas de mineração &#40;Analysis Services – Mineração de dados&#41;](mining-structures-analysis-services-data-mining.md).  
  
 Uma estrutura de mineração de dados pode conter tabelas aninhadas. Uma tabela aninhada fornece detalhes adicionais sobre o caso modelado na tabela de dados primários. Para obter mais informações, consulte [Tabelas aninhadas &#40;Analysis Services – Mineração de dados&#41;](nested-tables-analysis-services-data-mining.md)  
  
 
  
##  <a name="bkmk_Models"></a> Mining Models  
 Antes de processar, um modelo de mineração de dados é somente uma combinação de propriedades de metadados. Essas propriedades especificam uma estrutura de mineração, especificam um algoritmo de mineração de dados e definem uma coleção de configurações de parâmetros e filtros que afetam o modo como os dados são processados. Para obter mais informações, consulte [Modelos de mineração &#40;Analysis Services – Mineração de dados&#41;](mining-models-analysis-services-data-mining.md).  
  
 Quando você processar o modelo, os dados de treinamento que foram armazenados no cache da estrutura de mineração serão usados para gerar padrões, com base nas propriedades estatísticas dos dados e na heurística definida pelo algoritmo e seus parâmetros. Isso é conhecido como *training* do modelo.  
  
 O resultado do treinamento é um conjunto de dados de resumo, contidos dentro do *conteúdo de modelo*, que descreve os padrões encontrados e fornece regras pelas quais gerar previsões. Para obter mais informações, consulte [Conteúdo do modelo de mineração &#40;Analysis Services – Mineração de dados&#41;](mining-model-content-analysis-services-data-mining.md).  
  
 Em casos limitados, a estrutura lógica do modelo também pode ser exportada para um arquivo que representa fórmulas de modelo e associações de dados de acordo com um formato padrão, a PMML (Predictive Model Markup Language). Esta estrutura lógica pode ser importada em outros sistemas que utilizam PMML e esse modelo descrito poderá ser usado para previsão. Para obter mais informações, consulte [Noções básicas sobre a instrução DMX Select](/sql/dmx/understanding-the-dmx-select-statement).  
  

  
##  <a name="bkmk_CustomObjects"></a> Objetos personalizados de mineração de dados  
 Outros objetos que você usa no contexto de um projeto de mineração de dados, como gráficos de exatidão ou consultas de previsão, não são persistidos dentro da solução, mas podem ter o script criado usando ASSL ou criados usando AMO.  
  
 Além disso, você pode estender os serviços e os recursos disponíveis em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] adicionando estes objetos personalizados:  
  
 **Assemblies personalizados**  
 Os assemblies de .NET podem ser definidos usando qualquer linguagem compatível com CLR ou COM e, em seguida, registrados com uma instância do SQL Server. Os arquivos assembly são carregados do local definido pelo aplicativo e uma cópia é gravada no servidor com os dados. A cópia do arquivo assembly é usada para carregar o assembly sempre que o serviço é iniciado.  
  
 Para obter mais informações, consulte [Gerenciamento de assemblies de modelo multidimensional](../multidimensional-models/multidimensional-model-assemblies-management.md).  
  
 **Procedimentos armazenados personalizados**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] A mineração de dados dá suporte ao uso de procedimentos armazenados para trabalhar com objetos de mineração de dados. Você pode criar seus próprios procedimentos armazenados para estender a funcionalidade e trabalhar mais facilmente com dados retornados por consultas de previsão e consultas de conteúdo.  
  
 [Definindo procedimentos armazenados](../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
 Os procedimentos armazenados a seguir têm suporte para uso ao realizar validação cruzada.  
  
 [Procedimentos armazenados da mineração de dados &#40;Analysis Services – Mineração de dados&#41;](/sql/analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining)  
  
 Além disso, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] contém muitos procedimentos armazenados do sistema que são usados internamente para mineração de dados. Embora os procedimentos armazenados do sistema sejam para uso interno, você pode achá-los atalhos úteis. A Microsoft reserva-se o direito de alterar estes procedimentos armazenados conforme o necessário; portanto, para uso de produção, nós recomendamos que você crie consultas usando DMX, AMO ou XMLA.  
  
 **Algoritmos de plug-in personalizado**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornece um mecanismo para criar seus próprios algoritmos e, em seguida, adicioná-los como um novo serviço de mineração de dados à instância de servidor.  
  
 O Analysis Services usa interfaces COM para se comunicar com algoritmos de plugin. Para saber mais sobre como implementar novos algoritmos, consulte [Algoritmos de plug-in](plugin-algorithms.md).  
  
 É necessário registrar cada novo algoritmo antes de poder usá-los. Para registrar um algoritmo, você adiciona os metadados necessários para os algoritmos no arquivo .ini da instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Você deve adicionar as informações a cada instância onde planeja usar o novo algoritmo. Depois de adicionar o algoritmo, você poderá reiniciar a instância e usar o conjunto de linhas de esquema MINING_SERVICES para exibir o novo algoritmo, inclusive as opções e os provedores ao qual o algoritmo dá suporte.  
  

  
## <a name="see-also"></a>Consulte também  
 [Processamento de objetos de modelo multidimensional](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Referência de DMX &#40;extensões DMX&#41;](/sql/dmx/data-mining-extensions-dmx-reference)  
  
  
