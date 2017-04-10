---
title: "Comparando solu&#231;&#245;es tabulares e multidimensionais (SSAS) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
ms.assetid: 76ee5e96-6a04-49af-a88e-cb5fe29f2e9a
caps.latest.revision: 49
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 47
---
# Comparando solu&#231;&#245;es tabulares e multidimensionais (SSAS)
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] fornece várias abordagens para criar um modelo de semântica de business intelligence: multidimensional, tabular e PowerPivot.  
  
 Ter mais de uma abordagem permite uma experiência de modelagem adaptada para diferentes negócios e requisitos de usuário. A abordagem multidimensional é uma tecnologia madura criada em padrões abertos, adotada por vários fornecedores de software de BI, mas pode ser difícil de dominar. A tabular oferece uma abordagem de modelagem relacional que muitos desenvolvedores consideram mais intuitiva. O Power Pivot é ainda mais simples, oferecendo modelagem de dados visuais no Excel, com suporte do servidor fornecido por meio do SharePoint.  
  
 Todos os modelos são implantados como bancos de dados que são executados em uma instância do Analysis Services, acessada por ferramentas de cliente usando um único conjunto de provedores de dados e visualizada em relatórios interativos e estáticos por meio de Excel, Reporting Services, Power BI e ferramentas de BI de outros fornecedores.  
  
 Devido às diferenças na arquitetura de memória e metadados, nenhum dos tipos de modelo são intercambiáveis, embora você possa atualizar facilmente de um modelo Tabular 1050-1103 para Tabular 1200 e possa importar o Power Pivot para criar um modelo totalmente novo como projeto tabular.  
  
 As soluções tabulares e multidimensionais são criadas usando o [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] e são destinadas para projetos de BI corporativo que são executados em uma instância autônoma do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Ambas as soluções rendem bancos de dados analíticos de alto desempenho que se integram facilmente com clientes de BI. Ainda assim, cada solução difere na maneira como eles são criados, usados e implantados. A maior parte deste tópico compara esses dois tipos, para que você possa identificar a abordagem certa para você.  
  
 Para novos projetos de desenvolvimento, geralmente recomendamos o tabular. Será mais rápido de criar, testar e implantar; e funcionará melhor com os aplicativos de autoatendimento de BI e de serviços de nuvem mais recentes da Microsoft.  
  
##  <a name="a-namebkmkoverviewa-overview-of-modeling-types"></a><a name="bkmk_overview"></a> Visão geral dos tipos de modelagem  
 Novo no Analysis Services? A tabela a seguir enumera os modelos diferentes, resume a abordagem e identifica o veículo de lançamento inicial.  
  
||||  
|-|-|-|  
|**Tipo**|**Descrição de modelagem**|**Lançado**|  
|Multidimensional|Construções de modelagem OLAP (cubos, dimensões, medidas).|SQL Server 2000 e posterior|  
|Tabular|Construções de modelagem relacionais (modelo, tabelas, colunas).<br /><br /> Internamente, os metadados são herdados das construções de modelagem OLAP (cubos, dimensões, medidas). Código e script usam metadados OLAP.|SQL Server 2012 e posterior (níveis de compatibilidade 1050 – 1103) <sup>1</sup>|  
|Tabular no SQL Server 2016|Construções de modelagem relacional (modelo, tabelas, colunas), articuladas em definições de objeto de metadados tabulares em código e script.|SQL Server 2016 (nível de compatibilidade 1200)|  
|Power Pivot|Originalmente um suplemento, mas agora está totalmente integrado no Excel. Somente modelagem visual em uma infra-estrutura tabular interna. Você pode importar um modelo do Power Pivot para SSDT para criar um novo modelo tabular que é executado em uma instância do Analysis Services.|por meio do Excel e do Power Pivot BI Desktop|  
  
 <sup>1</sup> Os níveis de compatibilidade, introduzidos no SQL Server 2012, são significativos na versão atual devido ao novo mecanismo de metadados tabulares e ao suporte para recursos de habilitação de cenário disponíveis apenas no nível superior. Os avanços perceptíveis incluem DirectQuery, script e programação. Para obter detalhes, consulte [What's New in Analysis Services](../analysis-services/what-s-new-in-analysis-services.md) .  
  
##  <a name="a-namebkmkmodelsa-model-features"></a><a name="bkmk_models"></a> Recursos de modelo  
  A tabela a seguir resume a disponibilidade do recurso no nível do modelo. Examine esta lista para garantir que o recurso que você deseja usar está disponível no tipo de modelo que planeja criar.  
  
|||||  
|-|-|-|-|  
||Multidimensional|Tabular|Power Pivot|  
|Ações|Sim|Não|Não|  
|Agregações|Sim|Não|Não|  
|Coluna calculada|Não|Sim|Sim|  
|Medidas calculadas|Sim|Sim|Sim|  
|Tabelas calculadas|Não|Sim <sup>1</sup>|Não|  
|Assemblies personalizados|Sim|Não|Não|  
|Rollups personalizados|Sim|Não|Não|  
|Membro padrão|Sim|Não|Não|  
|Pastas de exibição|Sim|Sim <sup>1</sup>|Não|  
|Contagem Distinta|Sim|Sim (por DAX)|Sim (por DAX)|  
|Detalhamento|Sim|Sim (o detalhe abre em planilha separada)|Sim|  
|Hierarquias|Sim|Sim|Sim|  
|KPIs|Sim|Sim|Sim|  
|Objetos vinculados|Sim|Sim (tabelas vinculadas)|Não|  
|Relações muitos para muitos|Sim|Não (mas há [filtros cruzados bidirecionais](../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md) no nível de compatibilidade 1200)|Não|  
|Conjuntos nomeados|Sim|Não|Não|  
|Hierarquias pai-filho|Sim|Sim (por DAX)|Sim (por DAX)|  
|Partições|Sim|Sim|Sim|  
|Perspectivas|Sim|Sim|Sim|  
|Medidas semiaditivas|Sim|Sim|Sim|  
|Translations|[Sim](../analysis-services/multidimensional-models/translations-in-multidimensional-models-analysis-services.md)|Sim|[Sim](../analysis-services/tabular-models/translations-in-tabular-models-analysis-services.md)|  
|Hierarquias definidas pelo usuário|Sim|Sim|Sim|  
|Write-back|Sim|Não|Não|  
  
 <sup>1</sup> Consulte [Nível de compatibilidade para modelos tabulares no Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md) para obter informações sobre as diferenças funcionais dentro da faixa tabular.  
  
##  <a name="a-namebkmkdsa-data-considerations"></a><a name="bkmk_ds"></a> Considerações de dados  
 Modelos multidimensionais e de tabela usam dados importados de fontes externas. A quantidade e o tipo de dados que você precisa importar podem ser uma consideração primária ao decidir qual tipo de modelo melhor se adapta a seus dados.  
  
 **Compactação**  
  
 As soluções tabular e multidimensionais usam compactação de dados que reduz o tamanho do banco de dados do Analysis Services referente ao data warehouse do qual você está importando dados. Como a compactação real variará com base nas características dos dados subjacentes, não há nenhum modo de saber precisamente quanto disco e memória será exigida por uma solução depois que os dados forem processados e usados em consultas.  
  
 Uma estimativa usada por muitos desenvolvedores do Analysis Services é que o armazenamento primário de um banco de dados multidimensional será aproximadamente um terço do tamanho dos dados originais. Os bancos de dados tabulares podem muitas vezes obter quantidades maiores de compactação, cerca de um décimo do tamanho, principalmente se a maioria dos dados for importada de tabelas de fatos.  
  
 **Tamanho do modelo e desvio do recurso (na memória ou disco)**  
  
 O tamanho de um banco de dados do Analysis Services é restrito apenas pelos recursos disponíveis para executá-lo. O tipo do modelo e o modo de armazenamento também desempenham uma função no quanto o banco de dados pode crescer.  
  
 Bancos de dados tabulares executados na memória ou no modo DirectQuery que descarregam a execução da consulta para um banco de dados externo. Para análise de tabela na memória, o banco de dados é armazenado completamente na memória, o que significa que você deve ter memória suficiente para não apenas carregar todos os dados, mas também estruturas de dados adicionais criadas para dar suporte a consultas.  
  
 DirectQuery, renovado nesta versão, tem menos restrições do que antes e melhor desempenho. Aproveitar o banco de dados relacional de back-end para armazenamento e execução de consulta facilita a criação de um modelo tabular de grande escala mais viável do que era possível anteriormente.  
  
 Historicamente, os maiores bancos de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] em produção são multidimensionais, com processamento e cargas de trabalho de consulta em execução de modo independente em hardware dedicado, cada um otimizado para seu respectivo uso.  Bancos de dados tabulares estão se tornando populares rapidamente e novos avanços no DirectQuery ajudarão a preencher essa lacuna ainda mais.  
  
 Para descarga multidimensional, o armazenamento de dados e a execução de consulta estão disponíveis por meio de ROLAP.   Em um servidor de consulta, os conjuntos de linhas podem ser armazenados em cache e os obsoletos devem ser transferidos. O uso eficiente e equilibrado de recursos de memória e disco geralmente leva os clientes a soluções multidimensionais.  
  
 Sob carga, espera-se que os requisitos de disco e de memória para os dois tipos de solução aumentem, porque o Analysis Services armazena em cache, armazena, verifica e consulta os dados. Para saber mais sobre opções de paginação de memória, veja [Memory Properties](../analysis-services/server-properties/memory-properties.md). Para saber mais sobre escala, veja [High availability and Scalability in Analysis Services](../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md).  
  
 O Power Pivot para o Excel tem um limite artificial de tamanho de arquivo de 2 gigabytes que é imposto de modo que as pastas de trabalho criadas no Power Pivot para o Excel possam ser carregadas no SharePoint, que define limites máximos em tamanho de carregamento de arquivo. Uma das principais razões para migrar uma pasta de trabalho Power Pivot para uma solução tabular em uma instância autônoma do Analysis Services é estar próximo da limitação do tamanho do arquivo. Para obter mais informações sobre como configurar o tamanho máximo do arquivo para upload, consulte [Configurar o tamanho máximo de upload de arquivo &#40;Power Pivot para SharePoint&#41;](../analysis-services/power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint.md).  
  
 **Fontes de dados com suporte**  
  
 Soluções multidimensionais podem importar dados de fontes de dados relacionais usando provedores gerenciados e nativos do OLE DB.  
  
 Os modelos de tabela podem importar dados de fontes de dados relacionais, feeds de dados e alguns formatos de documentos. Você também pode usar OLE DB para provedores de ODBC com modelos tabulares.  
  
 Para exibir a lista de fontes de dados externas que você pode importar para cada modelo, consulte os seguintes tópicos:  
  
-   [Fontes de dados com suporte &#40;SSAS – Multidimensional&#41;](../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  
-   [Fontes de dados com suporte &#40;SSAS Tabular&#41;](../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)  
  
##  <a name="a-namebkmklanga-query-and-scripting-language-support"></a><a name="bkmk_lang"></a> Suporte a consulta e linguagem de script  
 O Analysis Services inclui MDX, DMX, DAX, XML/A, ASSL e TMSL. O suporte para estes idiomas pode variar por tipo de modelo. Se os requisitos de consulta e linguagem de scripts forem uma consideração, analise a lista a seguir.  
  
-   As pasta de trabalho Power Pivot usam DAX para cálculos e DAX ou MDX para consultas.  
  
-   Os bancos de dados modelo de tabela dão suporte a cálculos DAX, consulta DAX e consultas MDX. Isso é verdadeiro em todos os níveis de compatibilidades. As linguagens de script são ASSL (em relação a XMLA) para níveis de compatibilidade 1050-1103 e TMSL (em relação a XMLA) para o nível de compatibilidade 1200.  
  
-   Os bancos de dados modelo multidimensional dão suporte a cálculos MDX e consultas MDX, assim como ASSL.  
  
-   Os modelos de mineração de dados dão suporte a DMX e ASSL.  
  
-   O Analysis Services PowerShell tem suporte para modelos e banco de dados tabulares e multidimensionais.  
  
 Todos os bancos de dados dão suporte a XML/A. Consulte [Referência à linguagem de consulta e expressão &#40;Analysis Services&#41;](../Topic/Query%20and%20Expression%20Language%20Reference%20\(Analysis%20Services\).md) e [Documentação do desenvolvedor do Analysis Services](../analysis-services/analysis-services-developer-documentation.md) para obter mais informações.  
  
##  <a name="a-namebkmkseca-security-features"></a><a name="bkmk_sec"></a> Recursos de segurança  
 Todas as soluções do Analysis Services podem ser protegidas no nível do banco de dados. Mais opções de segurança granular variam por modo. Se as configurações de segurança granular forem um requisito para sua solução, analise a lista a seguir para garantir que o nível de segurança desejado tenha suporte no tipo de solução que você quer criar:  
  
-   As pastas de trabalho [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] são protegidas no nível de arquivo, usando permissões do SharePoint.  
  
-   Os bancos de dados modelo de tabela podem usar segurança em nível de linha, usando permissões baseadas em função no Analysis Services.  
  
-   Os bancos de dados modelo multidimensionais podem usar dimensão e segurança em nível de célula, usando permissões baseadas em função no Analysis Services.  
  
 As pastas de trabalho [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] podem ser restauradas para um servidor de modo tabular. Quando o arquivo for restaurado, ele será desacoplado do SharePoint, permitindo usar todos os recursos de modelagem Tabular, incluindo segurança em nível de linha.  
  
##  <a name="a-namebkmkdesignera-design-tools"></a><a name="bkmk_designer"></a> Ferramentas de design  
 As habilidades de modelagem de dados e a experiência técnica podem variar amplamente entre usuários que têm a tarefa de criar modelos analíticos. Se a familiaridade com a ferramenta ou a experiência do usuário for uma consideração para sua solução, compare as seguintes experiências para a criação do modelo.  
  
|Ferramenta de modelagem|Como usar|  
|-------------------|--------------|  
|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]|Use para criar soluções Tabulares, Multidimensionais e de Mineração de dados. Este ambiente de criação usa o shell do Visual Studio para fornecer espaços de trabalho, painéis de propriedade e navegação de objeto. Os usuários técnicos que já usam o Visual Studio preferirão esta ferramenta para criar aplicativos de business intelligence.|  
|[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para Excel|Use para criar uma pasta de trabalho [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] que você implanta posteriormente em um farm do SharePoint que tiver uma instalação do [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para SharePoint. [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para Excel tem um espaço de trabalho de aplicativo separado que abre sobre o Excel. Ele usa as mesmas metáforas visuais (páginas tabuladas, layout de grade e barra de fórmula) que o Excel. Usuários que são proficientes no Excel preferirão esta ferramenta sobre o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].|  
  
##  <a name="a-namebkmkclienta-client-application-support"></a><a name="bkmk_client"></a> Suporte a aplicativo cliente  
 Se você estiver usando o Reporting Services, a disponibilidade do recurso de relatório varia de acordo com as edições e os modos de servidor. Por isto, o tipo de relatório que você deseja compilar pode influenciar a escolha do modo de servidor a ser instalado.  
  
 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)], uma nova ferramenta de criação do Reporting Services que é executado no SharePoint, está disponível em um servidor de relatório que é implantado em um farm do SharePoint 2010. O único tipo de fonte de dados que pode ser usado com este relatório é um banco de dados modelo de tabela do Analysis Services ou uma pasta de trabalho [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] . Isto significa que você deve ter um servidor de modo de tabela ou um servidor do [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para SharePoint para hospedar a fonte de dados usada por este tipo de relatório. Você não pode usar um modelo multidimensional como uma fonte de dados para um relatório do [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] . Você deve criar uma conexão de modelo semântico BI do [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] ou uma fonte de dados compartilhados do Reporting Services para usar como a fonte de dados para o relatório do [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] .  
  
 O Construtor de Relatórios e o Designer de Relatórios podem usar qualquer banco de dados do Analysis Services, inclusive pastas de trabalho [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] que são hospedadas no [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para SharePoint.  
  
 Os relatórios de Tabela Dinâmica do Excel têm suporte em todos os bancos de dados do Analysis Services. A funcionalidade do Excel é o mesmo, se você usar um banco de dados de tabela, banco de dados multidimensional ou pasta de trabalho [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] , embora Writeback só tenha suporte para bancos de dados multidimensionais.  
  
 Os painéis de PerformancePoint podem se conectar a todos os bancos de dados do Analysis Services, inclusive pastas de trabalho [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] . Para obter mais informações consulte [Criar conexões de dados (serviços do PerformancePoint)](http://go.microsoft.com/fwlink/?linkdID=218155).  
  
##  <a name="a-namebkmkdeploymentmodea-server-deployment-modes-for-multidimensional-and-tabular-solutions"></a><a name="bkmk_deploymentmode"></a> Modos de implantação de servidor para soluções multidimensionais e tabulares  
 Uma instância do Analysis Services está instalada em um dos três modos que definem o contexto operacional do servidor. O modo de servidor que você instala determinará o tipo de soluções que podem ser implantados nesse servidor. Armazenamento e arquitetura de memória são as principais diferenças entre os modos, mas há outras diferenças. Os três modos de servidor são descritos brevemente na tabela a seguir. Para obter mais informações, consulte [Determinar o modo de servidor de uma instância do Analysis Services](../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md).  
  
|Modo de implantação|Descrição|  
|---------------------|-----------------|  
|0 - Multidimensional e de mineração de dados|Executa soluções multidimensionais e de mineração de dados que você implanta em uma instância padrão do Analysis Services. O modo de implantação 0 é o padrão para uma instalação do Analysis Services.|  
|1 – [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para SharePoint|Para obter acesso a dados [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] , o Analysis Services é um componente interno de uma instalação do [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para SharePoint. O Analysis Services é instalado no modo de implantação 1 e usado exclusivamente pelos serviços [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] em um ambiente do SharePoint.|  
|2 - Tabular|Executa soluções tabulares em uma instância autônoma do Analysis Services configurada para implantação do modo 2.|  
  
 Consulte [Instalar o Analysis Services](../analysis-services/instances/install-windows/install-analysis-services.md) para obter mais informações.  
  
##  <a name="a-namebkmksharepointa-sharepoint-requirements"></a><a name="bkmk_sharePoint"></a> Requisitos do SharePoint  
 O SQL Server integra-se com o SharePoint adicionando suporte para acesso a dados [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] e acesso a dados tabulares. O investimento no SharePoint e na integração do SQL Server cresce quando você maximiza o número de recursos usados de cada produto. Se você tiver o SharePoint, poderá instalar o SQL Server [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para SharePoint para habilitar o acesso a dados [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] e obter os arquivos de conexão .bism do [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] usados para acessar bancos de dados tabulares que são executados em uma instância externa do Analysis Services em um servidor de rede.  
  
 O relatório do Power View, que usa [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] e bancos de dados tabulares como uma fonte de dados, é um recurso do SharePoint fornecido pelo SQL Server e um recurso interno do Excel. Embora os bancos de dados tabulares sejam executados em uma instância do Analysis Services fora do SharePoint, esses dados são consumidos por relatórios do Power View que são executados no SharePoint.  
  
 Se você não usar o SharePoint, ainda poderá usar o [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para Excel para criar pastas de trabalho [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] , mas não terá uma experiência de visualização de dados coesa. Cada pessoa que usa a pasta de trabalho deverá baixar e exibir cada pasta de trabalho no Excel usando o suplemento [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para Excel para obter interação de dados e exploração usando segmentações de dados, filtros e dinamizações. Caso contrário, a visualização da pasta de trabalho será limitada a dados estáticos conforme aparecem quando você abre a pasta de trabalho.  
  
 As soluções tabulares, multidimensionais e de mineração de dados são executadas em instâncias do Analysis Services em uma rede, sem dependência do SharePoint.  
  
##  <a name="a-namebkmkexta-programmability-and-extensibility-support"></a><a name="bkmk_ext"></a> Suporte a programação e extensibilidade  
 Embora haja suporte ao desenvolvedor para o Power BI, não há nenhum suporte para pastas de trabalho do [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] . Se você estiver usando pastas de trabalho [!INCLUDE[ssGemini](../includes/ssgemini-md.md)], deverá usar o cliente interno e aplicativos de servidor como parte de sua solução. A programação no Excel e a programação no SharePoint são as únicas opções.  
  
 Para o Power BI, veja [Power BI inserido](https://azure.microsoft.com/services/power-bi-embedded/).  
  
 As soluções tabulares somente dão suporte a um arquivo model.bim por solução, o que significa que todo o trabalho deve ser feito em um único arquivo. As equipes de desenvolvimento que estiverem acostumadas a trabalhar com vários projetos em uma única solução podem precisar revisar a maneira como trabalham ao criarem uma solução tabular compartilhada.  
  
 As soluções tabulares no nível de compatibilidade 1200 mapeiam para um novo modelo de objeto que usa os metadados tabulares. Os modelos tabulares mais antigos e todos os multidimensionais usam metadados multidimensionais como descritores. É recomendável atualizar os modelos tabulares mais antigos para o nível de compatibilidade 1200 para que você possa usar os namespaces tabulares no AMO para script e código personalizado.  
  
 Consulte a [Documentação do desenvolvedor do Analysis Services](https://msdn.microsoft.com/library/bb500153.aspx) para saber mais.  
  
##  <a name="a-namebkmknexta-next-step-build-a-solution"></a><a name="bkmk_Next"></a> Próxima etapa: criar uma solução  
 Agora que você tem uma compreensão básica da comparação entre as soluções, experimente os tutoriais a seguir para conhecer as etapas para criar cada uma. Os links a seguir levam a tutoriais que explicam as etapas.  
  
-   Crie um modelo do [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]. Consulte [Introdução ao Power Pivot no Microsoft Excel](https://support.office.com/article/Get-started-with-Power-Pivot-in-Microsoft-Excel-fdfcf944-7876-424a-8437-1a6c1043a80b).  
  
-   Crie um modelo de tabela. Consulte [Modelagem de tabela &#40;Tutorial do Adventure Works&#41;](../analysis-services/tabular-modeling-adventure-works-tutorial.md).  
  
-   Crie um modelo multidimensional. Consulte [Modelagem multidimensional &#40;Tutorial do Adventure Works&#41;](../analysis-services/multidimensional-modeling-adventure-works-tutorial.md).  
  
-   Crie um modelo de mineração de dados. Consulte [Tutorial básico de mineração de dados](../Topic/Basic%20Data%20Mining%20Tutorial.md).  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciamento de instância do Analysis Services](../analysis-services/instances/analysis-services-instance-management.md)   
 [Novidades no Analysis Services](../analysis-services/what-s-new-in-analysis-services.md)     
 [Novidades no Power Pivot](http://go.microsoft.com/fwlink/?LinkId=238141)   
 [Conexão de modelo semântico do BI &#40;.bism&#41; do Power Pivot ](../analysis-services/power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md)   
 [Criar e gerenciar fontes de dados compartilhadas &#40;Reporting Services no modo integrado do SharePoint&#41;](../Topic/Create%20and%20Manage%20Shared%20Data%20Sources%20\(Reporting%20Services%20in%20SharePoint%20Integrated%20Mode\).md)  
  
  