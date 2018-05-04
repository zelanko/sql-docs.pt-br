---
title: Projetos de mineração de dados | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e01ea2027e95d3bb6e2635e48488df6b471bf238
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="data-mining-projects"></a>Projetos de mineração de dados
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Um projeto de mineração de dados faz parte de uma solução do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Durante o processo de design, os objetos que você cria neste projeto estão disponíveis para teste e consulta como parte de um banco de dados de espaço de trabalho. Quando você quiser que os usuários possam consultar ou procurar os objetos no projeto, deverá implantar o projeto em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] executado em modo multidimensional.  
  
 Este tópico fornece as informações básicas necessárias para entender e criar projetos de mineração de dados.  
  
 [Criando projetos de mineração de dados](#bkmk_Overview)  
  
 [Objetos em projetos de mineração de dados](#bkmk_Objects)  
  
-   [Fontes de dados](#bkmk_DataSources)  
  
-   [Exibições da fonte de dados](#bkmk_DSV)  
  
-   [Estruturas de mineração](#bkmk_Structures)  
  
-   [Modelos de mineração](#bkmk_Models)  
  
 [Usando um projeto concluído de mineração de dados](#bkmk_Complete)  
  
-   [Exibir e explorar modelos](#bkmk_ViewExplore)  
  
-   [Testar e validar modelos](#bkmk_Validate)  
  
-   [Criar previsões](#bkmk_Predict)  
  
 [Acesso programático a projetos de mineração de dados](#bkmk_API)  
  
##  <a name="bkmk_Overview"></a> Criando projetos de mineração de dados  
 No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], você cria projetos de mineração de dados usando o modelo **Projeto OLAP e de Mineração de Dados**. Você também pode criar projetos de mineração de dados programaticamente, usando o AMO. É possível gerar o script dos objetos de mineração de dados individuais com a linguagem ASSL (Analysis Services Scripting Language). Para obter mais informações, consulte [Acesso a dados de modelo multidimensional &#40;Analysis Services – dados multidimensionais&#41;](../../analysis-services/multidimensional-models/mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md).  
  
 Se você criar um projeto de mineração de dados dentro de uma solução existente, por padrão os objetos de mineração de dados serão implantados em um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] com o mesmo nome do arquivo de solução. Você pode alterar este nome e o servidor de destino usando a caixa de diálogo **Propriedades do Projeto** . Para obter mais informações, consulte [Configurar propriedades do projeto do Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/configure-analysis-services-project-properties-ssdt.md).  
  
> [!WARNING]  
>  Para criar e implantar seu projeto com êxito, você deverá ter acesso a uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que esteja sendo executada no modo OLAP/Mineração de dados. Você não pode desenvolver ou implantar soluções de mineração de dados em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que dá suporte a modelos de tabela, nem pode usar dados diretamente de uma pasta de trabalho [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ou de um modelo de tabela que usa o armazenamento de dados na memória. Para determinar se a instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que você tem dá suporte à mineração de dados, consulte [Determinar o Modo de Servidor de uma Instância do Analysis Services](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md).  
  
 Dentro de cada projeto de mineração de dados que você cria, você seguirá estas etapas:  
  
1.  Escolha uma *fonte de dados*, como um cubo, banco de dados ou arquivos de texto ou do Excel, que contém os dados brutos que você usará para criar modelos.  
  
2.  Defina um subconjunto dos dados na fonte de dados para usar para análise, e salve-o como uma *exibição da fonte de dados*.  
  
3.  Defina uma *estrutura de mineração* para dar suporte à modelagem.  
  
4.  Adicione *modelos de mineração* à estrutura de mineração, escolhendo um *algoritmo* e especificando como ele tratará os dados.  
  
5.  Treine os modelos populando-os com os dados selecionados ou um subconjunto filtrado dos dados.  
  
6.  Explore, teste e recrie modelos.  
  
 Quando o projeto estiver concluído, você poderá implantá-lo para os usuários navegarem ou consultarem, ou poderá fornecer acesso programático aos modelos de mineração em um aplicativo, para dar suporte a previsões e análises.  
  
  
##  <a name="bkmk_Objects"></a> Objetos em projetos de mineração de dados  
 Todos os projetos de mineração de dados contêm os quatro tipos de objetos a seguir. Você pode ter vários objetos de todos os tipos.  
  
-   Fontes de dados  
  
-   Exibições da fonte de dados  
  
-   Estruturas de mineração  
  
-   Modelos de mineração  
  
 Por exemplo, um único projeto de mineração de dados pode conter uma referência a várias fontes de dados, com cada fonte de dados dando suporte a várias exibições das fontes de dados. Em troca, cada exibição da fonte de dados pode dar suporte a várias estruturas de mineração, cada uma com muitos modelos de mineração relacionados.  
  
 Além disso, seu projeto pode incluir algoritmos de plug-in, assemblies personalizados ou procedimentos armazenados personalizados; porém, estes objetos não são descritos aqui. Para obter mais informações, consulte [Documentação do desenvolvedor do Analysis Services](../../analysis-services/analysis-services-developer-documentation.md).  
  
  
###  <a name="bkmk_DataSources"></a> Data Sources  
 A fonte de dados define a cadeia de conexão e as informações de autenticação que o servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usará para se conectar com a fonte de dados. A fonte de dados pode conter várias tabelas ou exibições; pode ser simples como uma única pasta de trabalho do Excel ou arquivo de texto, ou complexa como um banco de dados OLAP (processamento analítico online) ou banco de dados relacional grande.  
  
 Um único projeto de mineração de dados pode fazer referência a diversas fontes de dados. Embora um modelo de mineração possa usar somente uma fonte de dados de cada vez, o projeto pode ter vários desenhos de modelos em diferentes fontes de dados.  
  
 O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dá suporte a dados de muitos provedores externos, e a Mineração de Dados do SQL Server pode usar dados relacionais e de cubo como uma fonte de dados. Porém, se você desenvolver ambos os tipos de projetos — modelos baseados em fontes relacionais e modelos baseados em cubos OLAP — poderá querer desenvolvê-los e gerenciá-los em projetos separados.  
  
-   Geralmente, os modelos que são baseados em um cubo OLAP devem ser desenvolvidos dentro da solução de design OLAP. Uma razão é que os modelos baseados em um cubo devem processá-lo para atualizar os dados. Geralmente, você só deverá usar dados de cubo quando esse for o meio principal de armazenamento de dados e acesso, ou quando precisar das agregações, dimensões e atributos criados pelo projeto multidimensional.  
  
-   Se seu projeto somente usar dados relacionais, você deverá criar os modelos relacionais dentro de um projeto separado, de forma que não reprocesse outros objetos desnecessariamente. Em muitos casos, o banco de dados de preparo ou data warehouse usado para dar suporte à criação de cubo já contém as exibições que são necessárias para executar a mineração de dados, e você pode usar essas exibições para mineração de dados em vez de usar as agregações e as dimensões no cubo.  
  
-   Você não pode usar na memória ou dados [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] diretamente para criar modelos de mineração de dados.  
  
 A fonte de dados somente identifica o servidor ou provedor e o tipo geral de dados. Se você precisar alterar a formatação de dados e as agregações, use o objeto de exibição da fonte de dados.  
  
 Para controlar o modo como os dados da fonte de dados são tratados, você poderá adicionar colunas derivadas ou cálculo, modificar agregações ou renomear colunas nos dados na exibição da fonte de dados. (Você também pode trabalhar com dados downstream, modificando as colunas da estrutura de mineração, ou usando sinalizadores de modelagem e filtros no nível da coluna do modelo de mineração.)  
  
 Se a limpeza de dados for necessária, ou os dados no data warehouse tiverem que ser modificados para criar variáveis adicionais, alterar os tipos de dados ou criar agregação alternativa, você poderá precisar criar tipos de projetos adicionais para dar suporte à mineração de dados. Para obter mais informações sobre esses projetos relacionados, consulte [Projetos relacionados a soluções de mineração de dados](../../analysis-services/data-mining/related-projects-for-data-mining-solutions.md).  
  
  
###  <a name="bkmk_DSV"></a> Data Source Views  
 Depois de definir essa conexão a uma fonte de dados, você cria uma exibição que identifica os dados específicos que são relevantes para seu modelo.  
  
 A exibição da fonte de dados também permite que você personalize a forma como os dados na fonte de dados são fornecidos para o modelo de mineração. É possível modificar a estrutura dos dados para torná-la mais relevante para o seu projeto ou selecionar apenas determinados tipos de dados.  
  
 Por exemplo, usando a Exibição da Fonte de Dados, você pode:  
  
-   Criar colunas derivadas, como dateparts, subcadeia de caracteres etc.  
  
-   Agregar valores usando instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] , como GROUP BY  
  
-   Restringir dados temporariamente ou dados de exemplo  
  
 Para obter mais informações sobre como modificar dados em uma exibição de fonte de dados, consulte [Exibições de Fonte de Dados em Modelos Multidimensionais](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md).  
  
> [!WARNING]  
>  Se quiser filtrar dados, poderá fazê-lo na exibição da fonte de dados, mas também poderá criar filtros nos dados no nível do modelo de mineração. Como a definição de filtro está armazenada com o modelo de mineração, usar filtros de modelo facilita a determinação dos dados que foram usados para treinar o modelo. Além disso, você pode criar diversos modelos relacionados, com critérios de filtro diferentes. Para obter mais informações, consulte [Filtros para modelos de mineração &#40;Analysis Services – Mineração de dados&#41;](../../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md).  
  
 Observe que a exibição da fonte de dados que você cria pode conter dados adicionais que não são usados diretamente para análise. Por exemplo, é possível adicionar à sua exibição da fonte de dados os dados que são usados para teste, previsões ou detalhamento. Para obter mais informações sobre esses usos, consulte [Testing e Validation &#40;Data Mining&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md) e [Detalhamento](../../analysis-services/data-mining/drillthrough-queries-data-mining.md).  
  
  
###  <a name="bkmk_Structures"></a> Mining Structures  
 Quando tiver criado sua fonte de dados e a exibição da fonte de dados, você deverá selecionar as colunas de dados que são mais relevantes a seu problema dos negócios, definindo as *estruturas de mineração* dentro do projeto. Uma estrutura de mineração diz ao projeto quais colunas da exibição da fonte de dados devem ser de fato usadas para modelagem, treino e teste.  
  
 Para adicionar uma nova estrutura de mineração, inicie o Assistente de Mineração de Dados. O assistente automaticamente define a estrutura de mineração, acompanha você pelo processo de escolher os dados e, como opção, permite adicionar um modelo de mineração inicial à estrutura. Dentro da estrutura de mineração, você escolhe tabelas e colunas da exibição da fonte de dados ou de um cubo OLAP, e define relacionamentos entre tabelas, se os seus dados incluírem tabelas aninhadas.  
  
 Sua escolha de dados será muito diferente no Assistente de Mineração de Dados, dependendo se você usar fontes de dados relacionais ou OLAP (processamento analítico online).  
  
-   Quando você escolhe dados de uma fonte de dados relacional, configurar uma estrutura de mineração é fácil: você escolhe colunas dos dados na exibição da fonte de dados e define personalizações adicionais como aliases, ou define como os valores na coluna devem ser agrupados ou guardados. Para obter mais informações, consulte [Criar uma estrutura de mineração relacional](../../analysis-services/data-mining/create-a-relational-mining-structure.md).  
  
-   Quando você usa dados de um cubo OLAP, a estrutura de mineração deve estar no mesmo banco de dados que a solução OLAP.  Para criar uma estrutura de mineração, selecione atributos das dimensões e medidas relacionadas em sua solução OLAP. Os valores numéricos são geralmente encontrados em medidas e as variáveis categóricas em dimensões. Para obter mais informações, consulte [Criar uma estrutura de mineração OLAP](../../analysis-services/data-mining/create-an-olap-mining-structure.md).  
  
-   Também é possível definir estruturas de mineração usando DMX. Para obter mais informações, consulte [Instruções de definição de dados de extensões DMX &#40;Data Mining Extensions&#41;](../../dmx/dmx-statements-data-definition.md).  
  
 Após ter criado a estrutura de mineração inicial, é possível copiar, modificar e criar um alias das colunas da estrutura.  
  
 Cada estrutura de mineração pode conter diversos modelos de mineração. No entanto, depois de concluir, você poderá abrir novamente a estrutura de mineração e usar [Data Mining Designer](../../analysis-services/data-mining/data-mining-designer.md) para adicionar mais modelos de mineração à estrutura.  
  
 Você também tem a opção de separar seus dados em um conjunto de dados de treinamento, usado para criar modelos, e um conjunto de dados de controle para usar em teste ou validação de seus modelos de mineração.  
  
> [!WARNING]  
>  Alguns tipos de modelo, como modelos de série temporais, não dão suporte à criação de conjuntos de dados de controle, porque eles exigem uma série contínua de dados para treinamento. Para obter mais informações, consulte [Training and Testing Data Sets](../../analysis-services/data-mining/training-and-testing-data-sets.md).  
  
  
###  <a name="bkmk_Models"></a> Mining Models  
 O modelo de mineração define o algoritmo ou o método de análise que você usará nos dados. Para cada estrutura de mineração, é possível adicionar um ou mais modelos de mineração.  
  
 Dependendo de suas necessidades, você pode combinar muitos modelos em um único projeto ou criar projetos separados para cada tipo de modelo ou tarefa analítica.  
  
 Depois de ter criado uma estrutura e um modelo, você *processa* cada modelo ao executar os dados em uma exibição de fonte de dados através do algoritmo, o que gera um modelo matemático de dados. Esse processo também é conhecido como *treinamento de modelo*. Para obter mais informações, consulte [Requisitos e considerações sobre processamento &#40;Mineração de dados&#41;](../../analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md).  
  
 Depois que o modelo foi processado, você pode explorá-lo visualmente e criar consultas de previsão usando esse modelo de mineração. Se os dados do processo de treinamento tiverem sido armazenados em cache, você poderá usar consultas de *detalhamento* para retornar informações detalhadas sobre os casos usados no modelo.  
  
 Quando você quiser usar um modelo para produção (por exemplo, para fazer previsões, ou para ser explorado por usuários gerais), você poderá implantar o modelo para um servidor diferente. Se você precisar reprocessar o modelo no futuro, também terá que exportar a definição da estrutura de mineração subjacente (e, necessariamente, a definição da fonte de dados e exibição da fonte de dados) ao mesmo tempo.  
  
 Quando você implantar um modelo, também terá que assegurar que as opções de processamento corretas sejam definidas na estrutura e no modelo, e que os usuários em potencial tenham as permissões necessárias para executar consultas, exibir modelos ou detalhar para estruturar os dados do modelo. Para obter mais informações, consulte [Visão geral de segurança &#40;Mineração de Dados&#41;](../../analysis-services/data-mining/security-overview-data-mining.md).  
  
  
##  <a name="bkmk_Complete"></a> Usando um projeto concluído de mineração de dados  
 Esta seção resume as maneiras como você pode usar o projeto de mineração de dados concluído. Você pode criar gráficos de exatidão, explorar e validar os dados, e tornar os padrões de mineração de dados disponíveis para os usuários.  
  
> [!WARNING]  
>  Os gráficos, as consultas e as visualizações que você usa com os modelos de mineração de dados não são salvos como parte do projeto de mineração de dados e não podem ser implantados. Se você precisar persistir estes objetos, deverá salvar o conteúdo que é apresentado ou criar um script disto conforme descrito para cada objeto.  
  
  
###  <a name="bkmk_ViewExplore"></a> View and Explore Models  
 Depois de criar um modelo, você pode usar ferramentas visuais e consultas para explorar os padrões no modelo e saber mais sobre os padrões e estatísticas subjacentes. Na guia **Visualizador do Modelo de Mineração** do Designer de Mineração de Dados, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornece visualizadores para cada tipo de modelo de mineração, que podem ser usados para explorar os modelos de mineração.  
  
 Estas visualizações são temporárias e são fechadas sem salvar quando você encerra a sessão com o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Portanto, se você precisar exportar estas visualizações para outro aplicativo para apresentação ou análise adicional, use os comandos **Copiar** fornecidos em cada guia ou painel da interface do visualizador.  
  
 Os Suplementos de Mineração de dados para o Excel também fornecem um modelo de Visio que você pode usar para representar seus modelos em um diagrama de Visio, e anotar e modificar o diagrama usando as ferramentas do Visio. Para obter mais informações, consulte [Suplementos de mineração de dados do Microsoft SQL Server 2008 SP2 do Microsoft Office 2007](http://go.microsoft.com/fwlink/?LinkID=123146).  
  
  
###  <a name="bkmk_Validate"></a> Test and Validate Models  
 Depois de criar um modelo, será possível investigar os resultados e tomar decisões sobre quais modelos apresentam o melhor desempenho.  
  
 O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornece diversos gráficos que você pode usar para fornecer ferramentas que podem ser usadas para comparar diretamente modelos de mineração e escolher o mais preciso ou útil. Essas ferramentas incluem um gráfico de comparação de precisão, um gráfico de ganho e uma matriz de classificação. Você pode gerar estes gráficos usando a guia **Gráfico de precisão de mineração** do Designer de Mineração de Dados.  
  
 Você também pode usar um relatório de validação cruzada para realizar subamostragens interativas dos dados para determinar se o modelo é mais adequado para um conjunto de dados específico. As estatísticas fornecidas pelo relatório podem ser usadas para comparar objetivamente modelos e avaliar a qualidade dos seus dados de treinamento.  
  
 Observe que estes relatórios e gráficos não são armazenados com o projeto ou no banco de dados do ssASnoversion. Portanto, se você precisar preservar ou duplicar os resultados, salve-os ou gere um script com os objetos usando DMX ou AMO. Também é possível usar os procedimentos armazenados para validação cruzada.  
  
 Para obter mais informações, consulte [Teste e validação &#40;Mineração de dados&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md).  
  
  
###  <a name="bkmk_Predict"></a> Create Predictions  
 O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornece uma linguagem de consulta chamada DMX (Data Mining Extensions) que é a base para a criação de previsões e de fácil criação de scripts. Para ajudá-lo a criar consultas de previsão DMX, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece um construtor de consultas, disponível no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Também há muitos modelos DMX para o editor de consultas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Se você for iniciante em consultas de previsão, recomendamos usar o construtor de consultas que é fornecido no Designer de Mineração de Dados e no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações, consulte [Data Mining Tools](../../analysis-services/data-mining/data-mining-tools.md).  
  
 As previsões que você cria no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ou no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] não são persistidas. Portanto, se suas consultas forem complexas, ou se você precisa reproduzir os resultados, recomendamos salvar suas consultas de previsão em arquivos de consulta DMX, criar script deles ou inserir as consultas como parte de um pacote do Integration Services.  
  
  
##  <a name="bkmk_API"></a> Acesso programático a objetos de mineração de dados  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]fornece várias ferramentas que você pode usar para trabalhar programaticamente com projetos de mineração de dados e os objetos neles. A linguagem DMX fornece instruções que você pode usar para criar fontes de dados e exibições da fonte de dados, e para criar, treinar e usar a estrutura e os modelos de mineração de dados. Para obter mais informações, consulte [Referência de DMX &#40;extensões DMX&#41;](../../dmx/data-mining-extensions-dmx-reference.md).  
  
 É possível executar essas tarefas usando ASSL (Analysis Services Scripting Language), ou AMO (Objetos de Gerenciamento de Análise). Para obter mais informações, consulte [Desenvolvendo com XMLA no Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md).  
  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
 Os tópicos a seguir descrevem o uso do Assistente de Mineração de Dados para criar um projeto de mineração de dados e os objetos associados.  
  
|Tarefas|Tópicos|  
|-----------|------------|  
|Descreve como trabalhar com colunas de estrutura de mineração|[Criar uma estrutura de mineração relacional](../../analysis-services/data-mining/create-a-relational-mining-structure.md)|  
|Fornece mais informações sobre como adicionar novos modelos de mineração e processar uma estrutura e modelos|[Adicionar modelos de mineração para uma estrutura de & #40; Analysis Services – mineração de dados & #41;](../../analysis-services/data-mining/add-mining-models-to-a-structure-analysis-services-data-mining.md)|  
|Fornece links para recursos que ajudam a personalizar os algoritmos que criam modelos de mineração|[Personalizar a estrutura e modelos de mineração](../../analysis-services/data-mining/customize-mining-models-and-structure.md)|  
|Fornece links para informações sobre cada um dos visualizadores de modelo de mineração|[Visualizadores do modelo de mineração de dados](../../analysis-services/data-mining/data-mining-model-viewers.md)|  
|Saiba criar um gráfico de comparação de precisão, gráfico de ganho ou matriz de classificação ou testar uma estrutura de mineração|[Teste e validação &#40;Data Mining&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)|  
|Saiba sobre como processar opções e permissões|[Processar objetos de mineração de dados](../../analysis-services/data-mining/processing-data-mining-objects.md)|  
|Fornece mais informações sobre Analysis Services|[Bancos de dados de modelo multidimensional ](../../analysis-services/multidimensional-models/multidimensional-model-databases-ssas.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Designer de mineração de dados](../../analysis-services/data-mining/data-mining-designer.md)   
 [Criando modelos multidimensionais usando o SQL Server Data Tools & #40; SSDT & #41;](../../analysis-services/multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)   
 [Banco de dados do espaço de trabalho](../../analysis-services/tabular-models/workspace-database-ssas-tabular.md)  
  
  
