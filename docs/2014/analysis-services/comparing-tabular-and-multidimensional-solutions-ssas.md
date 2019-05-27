---
title: Comparando soluções tabulares e multidimensionais (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 76ee5e96-6a04-49af-a88e-cb5fe29f2e9a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1da4224387e70ccc76e069aa3ce411dddb79b805
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66087768"
---
# <a name="comparing-tabular-and-multidimensional-solutions-ssas"></a>Comparando soluções tabulares e multidimensionais (SSAS)
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] fornece dois métodos distintos para modelagem de dados: tabela e multidimensionais. Embora haja sobreposição significativa entre eles, também há diferenças importantes que informarão a sua decisão sobre como seguir em frente. Neste tópico, podemos oferecer comparações de recurso e explicar como cada abordagem trata os requisitos comuns de projeto. Por exemplo, se o suporte de uma fonte de dados específica é uma consideração importante, a seção sobre fontes de dados pode ajudar a orientar sua decisão sobre qual abordagem de modelagem utilizar.  
  
 Este tópico inclui as seguintes seções:  
  
-   [Visão geral de modelagem no Analysis Services](#bkmk_overview)  
  
-   [Suporte de fonte de dados por tipo de solução](#bkmk_ds)  
  
-   [Recursos de modelo](#bkmk_models)  
  
-   [Tamanho do modelo](#bkmk_modelsize)  
  
-   [Programação e experiência do desenvolvedor](#bkmk_ext)  
  
-   [Consulta e suporte de linguagem de scripts](#bkmk_lang)  
  
-   [Suporte ao recurso de segurança](#bkmk_sec)  
  
-   [Ferramentas de design](#bkmk_designer)  
  
-   [Cliente e aplicativos de relatório](#bkmk_client)  
  
-   [Plataformas de hospedagem](#bkmk_sharePoint)  
  
-   [Modos de implantação de servidor para soluções multidimensionais e tabulares](#bkmk_deploymentmode)  
  
-   [Próxima etapa: Criar uma solução](#bkmk_Next)  
  
 Informações adicionais podem ser encontradas neste artigo técnico no MSDN: [Escolhendo uma experiência de modelagem Tabular ou Multidimensional no SQL Server 2012 Analysis Services](https://go.microsoft.com/fwlink/?LinkId=251588).  
  
##  <a name="bkmk_overview"></a> Visão geral de modelagem no Analysis Services  
 O Analysis Services fornece uma experiência de desenvolvimento de modelo, bem como a implantação do modelo por meio da hospedagem de banco de dados em uma instância do Analysis Services. Os tipos de modelos incluem tabela e multidimensional. Como esperado, a hospedagem de banco de dados dá suporte às soluções de tabela e multidimensional que você cria, mas ela também inclui o PowerPivot para SharePoint.  
  
 O PowerPivot para SharePoint é o *Analysis Services no modo do SharePoint*, sendo que o Analysis Services funciona como um serviço complementar para o SharePoint, ajudando a hospedar e a gerenciar modelos de dados do Excel que foram criados anteriormente no Excel e, em seguida, salvos no SharePoint. A função do Analysis Services neste contexto é carregar o modelo de dados na memória, atualizar os dados de fontes de dados externas e executar consultas no modelo. Nessa configuração, o Analysis Services funciona nos bastidores. Todas as conexões e solicitações para o Analysis Services são feitas pelo SharePoint e somente quando uma pasta de trabalho do Excel contém um modelo de dados (modelos de dados são opcionais em pastas de trabalho do Excel). Se criar um modelo de dados no Excel e hospedá-lo no SharePoint, atende aos seus requisitos de projeto, consulte [Power Pivot: Análise de dados avançada e modelagem de dados no Excel](https://support.office.com/en-ie/article/Power-Pivot-Powerful-data-analysis-and-data-modeling-in-Excel-d7b119ed-1b3b-4f23-b634-445ab141b59b) e [PowerPivot para SharePoint &#40;SSAS&#41; ](power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md) para obter mais informações.  
  
> [!NOTE]  
>  Modelos de dados do Excel e modelos de tabelas são arquitetonicamente similares. É possível importar um modelo de dados do Excel para um modelo de tabela se for preciso dar suporte a grandes quantidades de dados ou utilizar outros recursos de modelo não disponíveis no Excel.  
  
 As soluções tabulares e multidimensionais são criadas usando o [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] e são destinadas para projetos de BI corporativo que são executados em uma instância autônoma do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Ambas as soluções rendem bancos de dados analíticos de alto desempenho que são integrados facilmente com o Excel, os relatórios do Reporting Services e outros aplicativos de BI da Microsoft e aplicativos de terceiros. Ambas as soluções resultam em bancos de dados independentes que podem ser utilizados por qualquer aplicativo cliente que dê suporte ao Analysis Services.  
  
 Em um nível alto, as diferenças entre modelos de tabela e multidimensional podem ser caracterizadas como a seguir:  
  
-   As soluções multidimensionais e de mineração de dados utilizam construções de modelagem OLAP (cubos e dimensões) e o armazenamento MOLAP, ROLAP ou HOLAP que utiliza o disco como o armazenamento de dados primário para os dados agregados previamente.  
  
-   Soluções tabulares usam construções de modelagem relacionais como tabelas e relações para modelar dados e o mecanismo de análise de memória para armazenar e calcular dados. A maior parte do modelo, se não ele todo, é armazenada na RAM e, geralmente, é muito mais rápida do que a contraparte multidimensional.  
  
 Para novos projetos, utilize primeiro a abordagem de tabela. Será mais rápido de criar, testar e implantar; e funcionará melhor com os aplicativos de autoatendimento de BI mais recentes da Microsoft.  
  
##  <a name="bkmk_ds"></a> Suporte de fonte de dados por tipo de solução  
 Modelos multidimensionais e de tabela usam dados importados de fontes externas. A maioria dos desenvolvedores utiliza um data warehouse, projetado para oferecer suporte a estruturas de dados de relatório, como a fonte de dados principal por trás de um modelo. O data warehouse é normalmente baseado em um esquema estrela ou floco de neve e o SSIS é utilizado para carregar os dados de soluções OLTP no data warehouse. A modelagem é mais simples ao utilizar um data warehouse como a fonte de dados de back-end.  
  
|**Link**|**Resumo das opções com suporte**|  
|--------------|--------------------------------------|  
|[Fontes de dados com suporte no &#40;Multidimensional do SSAS&#41;](multidimensional-models/supported-data-sources-ssas-multidimensional.md)|Modelos multidimensionais utilizam os dados de fontes de dados relacionais.|  
|[Fontes de dados com suporte &#40;SSAS de Tabela&#41;](tabular-models/data-sources-supported-ssas-tabular.md)|Modelos de tabela oferecem suporte a uma maior variedade de fontes de dados, incluindo arquivos simples, feeds de dados e fontes de dados que são acessadas por meio de provedores de dados ODBC.|  
  
 Ambas as abordagens de modelagem podem utilizar dados de várias fontes de dados no mesmo modelo.  
  
 Se sua solução exige o armazenamento de dados de modelo fora do modelo no banco de dados relacional (uma técnica utilizada quando o tamanho dos dados requisitados é especialmente grande), o tipo de fonte de dados deve ser um banco de dados relacional do SQL Server. Tanto o armazenamento ROLAP para modelos multidimensionais e o DirectQuery para modelos de tabela têm esse requisito.  
  
 **Tamanho dos dados**  
  
 As soluções tabular e multidimensionais usam compactação de dados que reduz o tamanho do banco de dados do Analysis Services referente ao data warehouse do qual você está importando dados. Como a compactação real variará com base nas características dos dados subjacentes, não há nenhum modo de saber precisamente quanto disco e memória será exigida por uma solução depois que os dados forem processados e usados em consultas. Uma estimativa usada por muitos desenvolvedores do Analysis Services é que o armazenamento primário de um banco de dados multidimensional será aproximadamente um terço do tamanho dos dados originais.  
  
 Os bancos de dados tabulares podem muitas vezes obter quantidades maiores de compactação, cerca de um décimo do tamanho, principalmente se a maioria dos dados for importada de tabelas de fatos. Para tabular, os requisitos de memória serão maiores que o tamanho dos dados em disco devido a estruturas de dados adicionais que são criadas quando o banco de dados tabular é carregado na memória. Sob carga, espera-se que os requisitos de disco e de memória para os dois tipos de solução aumentem, porque o Analysis Services armazena em cache, armazena, verifica e consulta os dados.  
  
 Para alguns projetos, os requisitos de dados podem ser grandes o suficiente para se tornarem um fator de escolha entre os tipos de modelo. Se os dados que você precisar carregar tiverem muitos terabytes, uma solução tabular poderá não atender seus requisitos se a memória disponível não puder acomodar os dados. Há uma opção de paginação que troca dados de memória com o disco, mas quantidades muito grandes de dados são melhor acomodadas em soluções multidimensionais. Os maiores bancos de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] em produção hoje em dia são multidimensionais. Para obter mais informações sobre opções de paginação de memória para soluções tabulares, consulte [Memory Properties](server-properties/memory-properties.md). Para obter mais informações sobre como dimensionar uma solução multidimensional, consulte [Expansão de consulta para o Analysis Services com bancos de dados somente leitura](https://go.microsoft.com/fwlink/?LinkId=251711).  
  
##  <a name="bkmk_models"></a> Recursos de modelo  
 A tabela a seguir resume a disponibilidade do recurso no nível do modelo. Se você já instalou o Analysis Services, poderá usar estas informações para entender os recursos do modo de servidor instalado. Se você já estiver familiarizado com recursos de modelo no Analysis Services e seus requisitos comerciais incluírem um ou mais destes recursos, você poderá revisar esta lista para garantir que o recurso que você deseja usar esteja disponível no tipo de modelo que planeja compilar.  
  
 Para obter mais informações sobre como os recursos são comparados por abordagem de modelagem, consulte o artigo técnico [Escolhendo uma experiência de modelagem tabular ou multidimensional no SQL Server 2012 Analysis Services](https://go.microsoft.com/fwlink/?LinkId=251588) no MSDN.  
  
> [!NOTE]  
>  A modelagem tabular tem suporte em edições específicas do SQL Server. Para obter mais informações, consulte [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
||||  
|-|-|-|  
||**Multidimensional**|**Tabular**|  
|Ações|[Sim](multidimensional-models/actions-in-multidimensional-models.md)|Não |  
|Objetos de agregação|[Sim](multidimensional-models/designing-aggregations-analysis-services-multidimensional.md)|Não |  
|Medidas calculadas|[Sim](multidimensional-models/create-calculated-members.md)|Sim|  
|Assemblies personalizados|[Sim](multidimensional-models/multidimensional-model-assemblies-management.md)|Não |  
|Rollups personalizados|Sim|Não |  
|Contagem Distinta|[Sim](multidimensional-models/use-aggregate-functions.md)|Sim (via DAX) *|  
|Detalhamento|[Sim](multidimensional-models/actions-in-multidimensional-models.md)|Sim|  
|Hierarquias|[Sim](multidimensional-models/user-defined-hierarchies-create.md)|Sim|  
|KPIs|[Sim](multidimensional-models/key-performance-indicators-kpis-in-multidimensional-models.md)|Sim|  
|Grupos de medidas vinculados|[Sim](multidimensional-models/linked-measure-groups.md)|Não|  
|Relações muitos para muitos|[Sim](multidimensional-models/define-a-many-to-many-relationship-and-many-to-many-relationship-properties.md)|Não |  
|Hierarquias pai-filho|[Sim](multidimensional-models/parent-child-dimension.md)|Sim (por DAX)|  
|Partições|[Sim](tabular-models/partitions-ssas-tabular.md)|  
|perspectivas|[Sim](multidimensional-models/perspectives-in-multidimensional-models.md)|[Sim](tabular-models/partitions-ssas-tabular.md)|  
|Medidas semiaditivas|[Sim](multidimensional-models/define-semiadditive-behavior.md)|Sim (por DAX)|  
|Translations|[Sim](multidimensional-models/translations-in-multidimensional-models-analysis-services.md)|Não |  
|Hierarquias definidas pelo usuário|[Sim](multidimensional-models/user-defined-hierarchies-create.md)|Sim|  
|Write-back|[Sim](multidimensional-models/set-partition-writeback.md)|Não |  
  
 * Se sua solução deve dar suporte a um número muito grande de contagens distintas (como muitos milhões de IDs de cliente), considere a tabela primeiro. Ela costuma ser mais funcional nesse cenário. Consulte a seção sobre contagens distintas no white paper, [estudo de caso do Analysis Services: Usando modelos de tabela em soluções comerciais de larga escala](https://msdn.microsoft.com/library/dn751533.aspx).  
  
##  <a name="bkmk_modelsize"></a> Tamanho do modelo  
 O tamanho do modelo, em termos de número total de objetos, não varia por tipo de solução. No entanto, as ferramentas de design usadas para compilar cada solução variam na maneira como elas se acomodam trabalhando com um número grande de objetos. Um modelo maior é um pouco mais fácil de compilar no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] , porque fornece mais instalações para diagramar e listar objetos por tipo no Pesquisador de Objetos e no Gerenciador de Soluções.  
  
 Os modelos muito grandes que consistem em muitas centenas de tabelas ou dimensões são geralmente compilados programaticamente no Visual Studio, e não nas ferramentas de design. Para obter mais informações sobre o número máximo de objetos em um modelo, consulte [especificações de capacidade máxima &#40;Analysis Services&#41;](multidimensional-models/olap-physical/maximum-capacity-specifications-analysis-services.md).  
  
##  <a name="bkmk_ext"></a> Programação e experiência do desenvolvedor  
 Para modelos tabulares e multidimensionais, há um modelo de objeto compartilhado para ambas as modalidades. O AMO e ADOMD.NET dão suporte a ambos os modos. Nenhuma biblioteca de cliente foi revisada para construções tabulares. Portanto, você precisará entender como construções multidimensionais e tabulares e convenções de nomenclatura relacionam-se entre si. Como uma primeira etapa, revise o exemplo de programação AMO para tabular para aprender a programação de AMO em relação a um modelo tabular. Para obter mais informações, baixe o exemplo do [site do Codeplex](https://go.microsoft.com/fwlink/?LinkID=221036).  
  
 As soluções tabulares somente dão suporte a um arquivo model.bim por solução, o que significa que todo o trabalho deve ser feito em um único arquivo. As equipes de desenvolvimento que estiverem acostumadas a trabalhar com vários projetos em uma única solução podem precisar revisar a maneira como trabalham ao criarem uma solução tabular compartilhada.  
  
##  <a name="bkmk_lang"></a> Suporte a consulta e linguagem de script  
 O Analysis Services inclui MDX, DMX, DAX, o XML/A e ASSL. O suporte para estes idiomas varia ligeiramente por tipo de modelo. Se os requisitos de consulta e linguagem de scripts forem uma consideração, analise a lista a seguir.  
  
-   Os bancos de dados modelo de tabela dão suporte a cálculos DAX, consulta DAX e consultas MDX.  
  
-   Os bancos de dados modelo multidimensional dão suporte a cálculos MDX e consultas MDX, assim como ASSL.  
  
-   Os modelos de mineração de dados dão suporte a DMX e ASSL.  
  
-   O Analysis Services PowerShell tem suporte para administração de servidor e banco de dados. O tipo de modelo (ou modo de servidor) não é um fator em uso dos cmdlets do PowerShell.  
  
 Todos os bancos de dados dão suporte a XML/A.  
  
##  <a name="bkmk_sec"></a> Suporte ao recurso de segurança  
 Todas as soluções do Analysis Services podem ser protegidas no nível do banco de dados. Mais opções de segurança granular variam por modo. Se as configurações de segurança granular forem um requisito para sua solução, analise a lista a seguir para garantir que o nível de segurança desejado tenha suporte no tipo de solução que você quer criar:  
  
-   Os bancos de dados modelo de tabela podem usar segurança em nível de linha, usando permissões baseadas em função no Analysis Services.  
  
-   Os bancos de dados modelo multidimensionais podem usar dimensão e segurança em nível de célula, usando permissões baseadas em função no Analysis Services.  
  
 Os modelos de dados do Excel podem ser restaurados para um servidor de modo de tabela. Quando o arquivo for restaurado, ele será desacoplado do SharePoint (supondo que você restaurou a partir de uma localização do SharePoint), permitindo utilizar quase todos os recursos de modelagem de tabela, incluindo segurança em nível de linha. Um recurso de modelagem tabular que você não pode usar em uma pasta de trabalho restaurada é tabela vinculada.  
  
##  <a name="bkmk_designer"></a> Ferramentas de design  
 As habilidades de modelagem de dados e a experiência técnica podem variar amplamente entre usuários que têm a tarefa de criar modelos analíticos. Se a familiaridade com a ferramenta ou a experiência do usuário for uma consideração para sua solução, compare as seguintes experiências para a criação do modelo.  
  
|**Ferramenta de modelagem**|**Como usar**|  
|-----------------------|------------------|  
|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]|Use para criar soluções Tabulares, Multidimensionais e de Mineração de dados. Este ambiente de criação usa o shell do Visual Studio para fornecer workspaces, painéis de propriedade e navegação de objeto. Os usuários técnicos que já usam o Visual Studio preferirão esta ferramenta para criar aplicativos de business intelligence. Para obter detalhes, consulte [Tools and applications used in Analysis Services](tools-and-applications-used-in-analysis-services.md) .|  
|Excel 2013 e posterior, com o PowerPivot para suplemento do Excel|O PowerPivot para Excel é uma ferramenta usada para editar e aprimorar um modelo de dados do Excel. Ele tem um workspace de aplicativo separado que abre no Excel, mas utiliza as mesmas metáforas visuais (páginas tabuladas, layout de grade e barra de fórmulas) que o Excel. Usuários proficientes em Excel costumam preferir essa ferramenta em vez do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Consulte [Power Pivot: Análise de dados avançada e modelagem de dados no Excel](https://support.office.com/en-ie/article/Power-Pivot-Powerful-data-analysis-and-data-modeling-in-Excel-d7b119ed-1b3b-4f23-b634-445ab141b59b).|  
  
##  <a name="bkmk_client"></a> Cliente e aplicativos de relatório  
 Em versões anteriores, a escolha do tipo de modelo tinha um impacto sobre quais aplicativos cliente você poderia utilizar, mas a distinção diminuiu ao longo do tempo. Os modelos de tabela e multidimensionais oferecem, principalmente, suporte equivalente com relação a aplicativos cliente que se conectam aos dados do Analysis Services. A tabela a seguir é uma lista de aplicativos cliente da Microsoft que podem ser utilizados com modelos de dados do Analysis Services.  
  
|**Aplicativo**|**Descrição**|  
|---------------------|---------------------|  
|Relatórios de tabela dinâmica do Excel|A funcionalidade do Excel é a mesmo para modelos de tabela e multidimensionais, embora tenha suporte somente para write-back (uma funcionalidade do Analysis Services que o Excel implementa) nos modelos multidimensionais.|  
|Relatórios de RDL do Reporting Services|Os relatórios RDL, criados no construtor de relatórios ou Designer de relatórios, podem utilizar qualquer modelo do Analysis Services, bem como modelos de dados do Excel hospedados no PowerPivot para SharePoint.|  
|Painéis de PerformancePoint|No SharePoint, painéis de PerformancePoint podem se conectar a todos os bancos de dados do Analysis Services, incluindo modelos de dados do Excel. Para obter mais informações consulte [Criar conexões de dados (serviços do PerformancePoint)](https://go.microsoft.com/fwlink/?linkdID=218155).|  
|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] em sites do Office 365 ou do Power BI|Somente modelos de tabelas.|  
|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] no local do SharePoint|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)], como um aplicativo ClickOnce do SharePoint, pode utilizar um cubo do Analysis Services ou o modelo de tabela.|  
  
##  <a name="bkmk_deploymentmode"></a> Modos de implantação de servidor para soluções multidimensionais e tabulares  
 Uma instância do Analysis Services está instalada em um dos três modos que definem o contexto operacional do servidor. O modo de servidor que você instala determinará o tipo de soluções que podem ser implantados nesse servidor. Armazenamento e arquitetura de memória são as principais diferenças entre os modos, mas há outras diferenças. Os três modos de servidor são descritos brevemente na tabela a seguir. Para obter mais informações, consulte [Determinar o modo de servidor de uma instância do Analysis Services](instances/determine-the-server-mode-of-an-analysis-services-instance.md).  
  
|Modo de implantação|Descrição|  
|---------------------|-----------------|  
|0 - Multidimensional e de mineração de dados|Executa soluções multidimensionais e de mineração de dados que você implanta em uma instância padrão do Analysis Services. O modo de implantação 0 é o padrão para uma instalação do Analysis Services. Para obter mais informações, consulte [Install Analysis Services in Multidimensional and Data Mining Mode](../../2014/sql-server/install/install-analysis-services-in-multidimensional-and-data-mining-mode.md).|  
|1 - PowerPivot para SharePoint|Para acessar o modelo de dados do Excel, o Analysis Services é um componente interno do SharePoint. O Analysis Services está instalado no modo de implantação 1 e aceita solicitações somente de serviços do Excel em um ambiente do SharePoint. Para obter mais informações, consulte [PowerPivot for SharePoint 2010 Installation](../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md).|  
|2 - Tabular|Executa soluções tabulares em uma instância autônoma do Analysis Services configurada para implantação do modo 2. Para obter mais informações, consulte [Install Analysis Services in Tabular Mode](instances/install-windows/install-analysis-services.md).|  
  
 Observe que os modelos de servidor não são intercambiáveis. Durante a instalação, você deverá escolher um modo de operação do servidor. É necessário instalar várias instâncias, uma para cada modo de servidor, para oferecer suporte a todas as cargas de trabalho.  
  
##  <a name="bkmk_sharePoint"></a> Plataformas de hospedagem  
 A Microsoft tem várias metodologias para hospedar aplicativos, dados, relatórios e colaborações. Nesta seção, abordaremos a interoperabilidade do Analysis Services com relação a cada plataforma de hospedagem.  
  
|**Plataforma**|**Descrição**|  
|------------------|---------------------|  
|Microsoft Azure|É possível executar qualquer versão com suporte e a edição do Analysis Services em uma Máquina Virtual do Azure. Ao contrário do Banco de Dados SQL, que é um serviço no Azure que fornece praticamente a mesma funcionalidade que um mecanismo de banco de dados relacional local, não há Analysis Services equivalente no Azure. Instalar, configurar e executar o Analysis Services em uma VM do Azure é nossa única opção com base do Azure.|  
|Office 365|O Excel online no Office 365 oferece suporte a conexões remotas com modelos de tabelas e multidimensionais que são executados no local.|  
|Sites do Power BI no Office 365|Em um site do Power BI, relatórios do Power View podem conectar-se aos modelos de dados de tabela que são executados no local.|  
|Servidores locais (instâncias do SharePoint e do SQL Server)|Um servidor de banco de dados local (ou seja, uma instância de SQL Server que tenha o Analysis Services instalado) ainda é o principal meio para disponibilizar os dados do Analysis Services para relatórios e aplicativos cliente. As soluções tabulares, multidimensionais e de mineração de dados são executadas em instâncias do Analysis Services em uma rede, sem dependência do SharePoint.<br /><br /> O SQL Server integra-se com o SharePoint adicionando suporte para acesso a dados PowerPivot e acesso a dados tabulares. O investimento no SharePoint e na integração do SQL Server cresce quando você maximiza o número de recursos usados de cada produto. Se você tiver o SharePoint, poderá instalar o SQL Server PowerPivot para SharePoint para habilitar o acesso a dados PowerPivot e obter os arquivos de conexão .bism do PowerPivot usados para acessar bancos de dados tabulares que são executados em uma instância externa do Analysis Services em um servidor de rede.<br /><br /> Se você tiver o SharePoint e o SQL Server, é possível dar suporte à seguinte combinação de serviços e aplicativos:<br /><br /> Modelos do Analysis Services (tabela ou multidimensionais)<br /><br /> Serviços do SharePoint de camada intermediária (serviços do Excel, Reporting Services no SharePoint ou Serviços PerformancePoint)<br /><br /> Clientes de navegador ou clientes avançados (Excel) para uma análise mais profunda de dados e exploração.|  
  
##  <a name="bkmk_Next"></a> Próxima etapa: Criar uma solução  
 Agora que você tem uma compreensão básica da comparação entre as soluções, experimente os tutoriais a seguir para conhecer as etapas para criar cada uma. Os links a seguir levam a tutoriais que explicam as etapas.  
  
-   Criar um modelo de tabela usando a [Modelagem de tabela &#40;Tutorial da Adventure Works&#41;](tabular-modeling-adventure-works-tutorial.md).  
  
-   Criar um modelo multidimensional usando a [Modelagem multidimensional &#40;Tutorial da Adventure Works&#41;](multidimensional-modeling-adventure-works-tutorial.md).  
  
-   Crie um modelo de mineração de dados usando o [Basic Data Mining Tutorial](../../2014/tutorials/basic-data-mining-tutorial.md).  
  
-   Crie um modelo do PowerPivot usando o [Tutorial do PowerPivot para Excel](https://go.microsoft.com/fwlink/?LinkId=251135).  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciamento de instância do Analysis Services](instances/analysis-services-instance-management.md)   
 [O que há de novo no Analysis Services e Business Intelligence](what-s-new-in-analysis-services.md)   
 [O que há de novo &#40;Reporting Services&#41;](../../2014/reporting-services/what-s-new-reporting-services.md)   
 [Quais são as novidades no PowerPivot](https://go.microsoft.com/fwlink/?LinkId=238141)   
 [Ajuda do PowerPivot do SQL Server 2012](https://go.microsoft.com/fwlink/?LinkID=220946)   
 [Conexão de modelo semântico de BI do PowerPivot &#40;. bism&#41;](power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md)   
 [Criar e gerenciar fontes de dados compartilhadas &#40;Reporting Services no modo integrado do SharePoint&#41;](../../2014/reporting-services/create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)  
  
  
