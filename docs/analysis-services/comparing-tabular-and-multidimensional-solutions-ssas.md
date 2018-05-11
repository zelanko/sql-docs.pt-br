---
title: Comparando soluções tabulares e multidimensionais (SSAS) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f665300e4b0ffc49264d237c62c59e4a2f3343da
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="comparing-tabular-and-multidimensional-solutions"></a>Comparando soluções tabulares e multidimensionais
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  SQL Server Analysis Services fornece várias abordagens para criar um modelo semântico do business intelligence: Tabular, Multidimensional e PowerPivot para SharePoint.
  
 Ter mais de uma abordagem permite uma experiência de modelagem adaptada para diferentes negócios e requisitos de usuário. A abordagem multidimensional é uma tecnologia madura criada em padrões abertos, adotada por vários fornecedores de software de BI, mas pode ser difícil de dominar. A tabular oferece uma abordagem de modelagem relacional que muitos desenvolvedores consideram mais intuitiva. O Power Pivot é ainda mais simples, oferecendo modelagem de dados visuais no Excel, com suporte do servidor fornecido por meio do SharePoint.  
  
 Todos os modelos são implantados como bancos de dados que são executados em uma instância do Analysis Services, acessada por ferramentas de cliente usando um único conjunto de provedores de dados e visualizada em relatórios interativos e estáticos por meio de Excel, Reporting Services, Power BI e ferramentas de BI de outros fornecedores.  
  
 Soluções tabulares e multidimensionais são criadas usando o SSDT e são destinadas para projetos de BI corporativo que são executados em um programa autônomo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] instância local e para modelos de tabela, uma [Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/) servidor a nuvem. Ambas as soluções rendem bancos de dados analíticos de alto desempenho que se integram facilmente com clientes de BI. Ainda assim, cada solução difere na maneira como eles são criados, usados e implantados. A maior parte deste tópico compara esses dois tipos, para que você possa identificar a abordagem certa para você.  
  
 Para novos projetos, geralmente recomendamos modelos de tabela. Modelos de tabela são mais rápidos criar, testar e implantar; e será funcionam melhor com os mais recentes aplicativos de BI de autoatendimento e serviços da Microsoft na nuvem.  
  
##  <a name="bkmk_overview"></a> Visão geral dos tipos de modelagem  
 Novo no Analysis Services? A tabela a seguir enumera os modelos diferentes, resume a abordagem e identifica o veículo de lançamento inicial.  
 
 > [!NOTE]  
>  **Serviços de análise do Azure** dá suporte a modelos de tabela nos níveis de compatibilidade 1200 e superior. Entretanto, nem todas as funcionalidades de modelagem de tabela descritas neste tópico tem suporte no Azure Analysis Services. Enquanto criando e implantando modelos de tabela do Azure Analysis Services são muito semelhante a como local, é importante entender as diferenças. Para obter mais informações, consulte [o que é o Azure Analysis Services?](https://docs.microsoft.com/azure/analysis-services/analysis-services-overview)
  
||||  
|-|-|-|  
|**Tipo**|**Descrição de modelagem**|**Lançado**|  
|Tabular|Construções de modelagem relacionais (modelo, tabelas, colunas). Internamente, os metadados são herdados das construções de modelagem OLAP (cubos, dimensões, medidas). Código e script usam metadados OLAP.|SQL Server 2012 e posterior (níveis de compatibilidade 1050 – 1103) <sup>1</sup>|  
|Tabular no SQL Server 2016|Relacional de modelagem construções (modelo, tabelas, colunas), articuladas em definições de objeto de metadados de tabela em [linguagem de script de modelo Tabular (TMSL)](../analysis-services/tabular-model-scripting-language-tmsl-reference.md) e [modelo de objeto de tabela (TOM)](../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md) código.|SQL Server 2016 (nível de compatibilidade 1200)| 
|Tabular no SQL Server de 2017|Relacional de modelagem construções (modelo, tabelas, colunas), articuladas em definições de objeto de metadados de tabela em [linguagem de script de modelo Tabular (TMSL)](../analysis-services/tabular-model-scripting-language-tmsl-reference.md) e [modelo de objeto de tabela (TOM)](../analysis-services/tabular-model-programming-compatibility-level-1200/introduction-to-the-tabular-object-model-tom-in-analysis-services-amo.md) código.|SQL Server 2017 (nível de compatibilidade 1400)| 
|Multidimensional|Construções de modelagem OLAP (cubos, dimensões, medidas).|SQL Server 2000 e posterior|  
|Power Pivot|Originalmente um suplemento, mas agora está totalmente integrado no Excel. Somente modelagem visual em uma infra-estrutura tabular interna. Você pode importar um modelo do Power Pivot para SSDT para criar um novo modelo tabular que é executado em uma instância do Analysis Services.|por meio do Excel e do Power Pivot BI Desktop|  
  
 <sup>1</sup> níveis de compatibilidade são significativos na versão atual devido ao mecanismo de metadados de tabela e suporte para habilitar o cenário de recursos disponíveis apenas no nível superior. Versões posteriores oferecem suporte a níveis de compatibilidade anteriores, mas é recomendável criar novos modelos ou atualizar modelos existentes para o mais alto nível de compatibilidade com suporte a versão do servidor.
  
##  <a name="bkmk_models"></a> Recursos de modelo  
  A tabela a seguir resume a disponibilidade do recurso no nível do modelo. Examine esta lista para garantir que o recurso que você deseja usar está disponível no tipo de modelo que planeja criar.  
  
|||| 
|-|-|-|
||Multidimensional|Tabular|
|Ações|Sim|não|
|Agregações|Sim|não|
|Coluna calculada|não|Sim|  
|Medidas calculadas|Sim|Sim| 
|Tabelas calculadas|não|Sim<sup>1</sup>|  
|Assemblies personalizados|Sim|não|
|Rollups personalizados|Sim|não| 
|Membro padrão|Sim|não|  
|Pastas de exibição|Sim|Sim<sup>1</sup>|  
|Contagem Distinta|Sim|Sim (por DAX)|
|Detalhamento|Sim|Sim (depende do aplicativo cliente)|
|Hierarquias|Sim|Sim|
|KPIs|Sim|Sim| 
|Objetos vinculados|Sim|Sim (tabelas vinculadas)|
|Expressões de M|não|Sim<sup>1</sup>|
|Relações muitos para muitos|Sim|Não (mas não há [bidirecional filtros cruzados](../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md) nos níveis de compatibilidade 1200 e superior)| 
|Conjuntos nomeados|Sim|não| 
|Hierarquias desbalanceadas|Sim|Sim<sup>1</sup>|  
|Hierarquias pai-filho|Sim|Sim (por DAX)|
|Partições|Sim|Sim| 
|Perspectivas|Sim|Sim|
|Segurança em nível de linha|Sim|Sim| 
|Segurança em nível de objeto|Sim|Sim<sup>1</sup>|
|Medidas semiaditivas|Sim|Sim| 
|Traduções|[Sim](../analysis-services/multidimensional-models/translations-in-multidimensional-models-analysis-services.md)|Sim| 
|Hierarquias definidas pelo usuário|Sim|Sim|
|Write-back|Sim|não| 
  
 <sup>1</sup> consulte [modelos de nível de compatibilidade de tabela no Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md) para obter informações sobre as diferenças funcionais entre níveis de compatibilidade.  
  
##  <a name="bkmk_ds"></a> Considerações de dados  
 Modelos tabulares e multidimensionais usam dados importados de fontes externas. A quantidade e o tipo de dados que você precisa importar podem ser uma consideração primária ao decidir qual tipo de modelo melhor se adapta a seus dados.  
  
 **Compactação**  
  
 As soluções tabular e multidimensionais usam compactação de dados que reduz o tamanho do banco de dados do Analysis Services referente ao data warehouse do qual você está importando dados. Como a compactação real variará com base nas características dos dados subjacentes, não há nenhum modo de saber precisamente quanto disco e memória será exigida por uma solução depois que os dados forem processados e usados em consultas.  
  
 Uma estimativa usada por muitos desenvolvedores do Analysis Services é que o armazenamento primário de um banco de dados multidimensional será aproximadamente um terço do tamanho dos dados originais. Os bancos de dados tabulares podem muitas vezes obter quantidades maiores de compactação, cerca de um décimo do tamanho, principalmente se a maioria dos dados for importada de tabelas de fatos.  
  
 **Tamanho do modelo e desvio do recurso (na memória ou disco)**  
  
 O tamanho de um banco de dados do Analysis Services é restrito apenas pelos recursos disponíveis para executá-lo. O tipo do modelo e o modo de armazenamento também desempenham uma função no quanto o banco de dados pode crescer.  
  
 Bancos de dados tabulares executados na memória ou no modo DirectQuery que descarregam a execução da consulta para um banco de dados externo. Para análise de tabela na memória, o banco de dados é armazenado completamente na memória, o que significa que você deve ter memória suficiente para não apenas carregar todos os dados, mas também estruturas de dados adicionais criadas para oferecer suporte a consultas.  
  
 DirectQuery, renovado no SQL Server 2016, tem menos restrições do que antes e melhor desempenho. Aproveitar o banco de dados relacional de back-end para armazenamento e execução de consulta facilita a criação de um modelo tabular de grande escala mais viável do que era possível anteriormente.  
  
 Historicamente, os maiores bancos de dados em produção são multidimensionais, com cargas de trabalho de processamento e consulta executada independentemente em hardware dedicado, cada um otimizado para seu respectivo uso.  Bancos de dados tabulares estão se tornando populares rapidamente e novos avanços no DirectQuery ajudarão a preencher essa lacuna ainda mais.  
  
 Para armazenamento de dados de descarregamento multidimensional e de consulta de execução está disponível por meio de ROLAP.   Em um servidor de consulta, os conjuntos de linhas podem ser armazenados em cache e os obsoletos devem ser transferidos. O uso eficiente e equilibrado de recursos de memória e disco geralmente leva os clientes a soluções multidimensionais.  
  
 Sob carga, espera-se que os requisitos de disco e de memória para os dois tipos de solução aumentem, porque o Analysis Services armazena em cache, armazena, verifica e consulta os dados. Para saber mais sobre opções de paginação de memória, veja [Memory Properties](../analysis-services/server-properties/memory-properties.md). Para saber mais sobre escala, veja [High availability and Scalability in Analysis Services](../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md).  
  
 O Power Pivot para o Excel tem um limite artificial de tamanho de arquivo de 2 gigabytes que é imposto de modo que as pastas de trabalho criadas no Power Pivot para o Excel possam ser carregadas no SharePoint, que define limites máximos em tamanho de carregamento de arquivo. Uma das principais razões para migrar uma pasta de trabalho Power Pivot para uma solução tabular em uma instância autônoma do Analysis Services é estar próximo da limitação do tamanho do arquivo. Para obter mais informações sobre como configurar o tamanho máximo do arquivo para upload, consulte [Configurar o tamanho máximo de upload de arquivo &#40;Power Pivot para SharePoint&#41;](../analysis-services/power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint.md).  
  
 **Fontes de dados com suporte**  
  
 Os modelos de tabela podem importar dados de fontes de dados relacionais, feeds de dados e alguns formatos de documentos. Você também pode usar o OLE DB para provedores de ODBC com modelos de tabela. Modelos de tabela no nível de compatibilidade 1400 oferecem um aumento significativo na variedade de fontes de dados do qual você pode importar de. Isso é devido à introdução dos modernos obter dados de consulta de dados e importar recursos no SSDT utilizando a linguagem de fórmula de consulta M.   

  Soluções multidimensionais podem importar dados de fontes de dados relacionais usando provedores gerenciados e nativos do OLE DB.  
  
 Para exibir a lista de fontes de dados externas que você pode importar para cada modelo, consulte os seguintes tópicos:  
  
-   [Fontes de dados com suporte](../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)  

-   [Fontes de dados com suporte &#40;SSAS – Multidimensional&#41;](../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  

  
##  <a name="bkmk_lang"></a> Suporte a consulta e linguagem de script  
 O Analysis Services inclui MDX, DMX, DAX, XML/A, ASSL e TMSL. O suporte para estes idiomas pode variar por tipo de modelo. Se os requisitos de consulta e linguagem de scripts forem uma consideração, analise a lista a seguir.  

-   Os bancos de dados modelo de tabela dão suporte a cálculos DAX, consulta DAX e consultas MDX. Isso é verdadeiro em todos os níveis de compatibilidades. Linguagens de script são ASSL (em relação ao XMLA) para níveis de compatibilidade 1050-1103 e TMSL (em relação a XMLA) para o nível de compatibilidade 1200 e superior. 

-   As pasta de trabalho Power Pivot usam DAX para cálculos e DAX ou MDX para consultas.  
  
-   Bancos de dados modelo multidimensionais oferecem suporte a cálculos MDX, consultas MDX, consultas DAX e ASSL. 
  
-   Os modelos de mineração de dados dão suporte a DMX e ASSL.  
  
-   O Analysis Services PowerShell tem suporte para modelos e banco de dados tabulares e multidimensionais.  
  
 Todos os bancos de dados dão suporte a XML/A. Consulte [Referência à linguagem de consulta e expressão &#40;Analysis Services&#41;](http://msdn.microsoft.com/library/9597533d-35f4-4742-9d8c-7af392163527) e [Documentação do desenvolvedor do Analysis Services](../analysis-services/analysis-services-developer-documentation.md) para obter mais informações.  
  
##  <a name="bkmk_sec"></a> Recursos de segurança  
 Todas as soluções do Analysis Services podem ser protegidas no nível do banco de dados. Mais opções de segurança granular variam por modo. Se as configurações de segurança granular forem um requisito para sua solução, analise a lista a seguir para garantir que o nível de segurança desejado tenha suporte no tipo de solução que você quer criar:  

  
-   Bancos de dados de modelo de tabela podem usar segurança em nível de linha, usando permissões baseadas em função.  
  
-   Bancos de dados modelo multidimensionais podem usar dimensão e segurança em nível de célula, usando permissões baseadas em função.  

-   As pastas de trabalho[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] são protegidas no nível de arquivo, usando permissões do SharePoint.  
  
 As pastas de trabalho[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] podem ser restauradas para um servidor de modo tabular. Quando o arquivo for restaurado, ele será desacoplado do SharePoint, permitindo que você use todos os recursos de modelagem de tabela, incluindo segurança em nível de linha.  
  
##  <a name="bkmk_designer"></a> Ferramentas de design  
 As habilidades de modelagem de dados e a experiência técnica podem variar amplamente entre usuários que têm a tarefa de criar modelos analíticos. Se a familiaridade com a ferramenta ou a experiência do usuário for uma consideração para sua solução, compare as seguintes experiências para a criação do modelo.  
  
|Ferramenta de modelagem|Como usar|  
|-------------------|--------------|  
|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]|Use para criar tabulares, multidimensionais e soluções de mineração de dados. Este ambiente de criação usa o shell do Visual Studio para fornecer espaços de trabalho, painéis de propriedade e navegação de objeto. Os usuários técnicos que já usam o Visual Studio preferirão esta ferramenta para criar aplicativos de business intelligence.|  
|[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para Excel|Use para criar uma pasta de trabalho [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] que você implanta posteriormente em um farm do SharePoint que tiver uma instalação do [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para SharePoint. [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para Excel tem um espaço de trabalho de aplicativo separado que abre sobre o Excel. Ele usa as mesmas metáforas visuais (páginas tabuladas, layout de grade e barra de fórmula) que o Excel. Usuários que são proficientes no Excel preferirão esta ferramenta sobre o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].|  
  
##  <a name="bkmk_client"></a> Suporte a aplicativo cliente  
 Soluções em geral, tabulares e multidimensionais dão suporte a aplicativos cliente que usam uma ou mais das bibliotecas de cliente do Analysis Services (MSOLAP, AMOMD, ADOMD). Por exemplo, Excel, Power BI Desktop e aplicativos personalizados.   
 
 Se você estiver usando o Reporting Services, a disponibilidade do recurso de relatório varia de acordo com as edições e os modos de servidor. Por isto, o tipo de relatório que você deseja compilar pode influenciar a escolha do modo de servidor a ser instalado.  
  
 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)], uma nova ferramenta de criação do Reporting Services que é executado no SharePoint, está disponível em um servidor de relatório que é implantado em um farm do SharePoint 2010. O único tipo de fonte de dados que pode ser usado com este relatório é um banco de dados modelo de tabela do Analysis Services ou uma pasta de trabalho [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] . Isto significa que você deve ter um servidor de modo de tabela ou um servidor do [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para SharePoint para hospedar a fonte de dados usada por este tipo de relatório. Você não pode usar um modelo multidimensional como uma fonte de dados para um relatório do [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] . Você deve criar uma conexão de modelo semântico BI do [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] ou uma fonte de dados compartilhados do Reporting Services para usar como a fonte de dados para o relatório do [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] .  
  
 O Construtor de Relatórios e o Designer de Relatórios podem usar qualquer banco de dados do Analysis Services, inclusive pastas de trabalho [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] que são hospedadas no [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para SharePoint.  
  
 Os relatórios de Tabela Dinâmica do Excel têm suporte em todos os bancos de dados do Analysis Services. A funcionalidade do Excel é o mesmo, se você usar um banco de dados de tabela, banco de dados multidimensional ou pasta de trabalho [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] , embora Writeback só tenha suporte para bancos de dados multidimensionais.  
 
  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciamento de instância do Analysis Services](../analysis-services/instances/analysis-services-instance-management.md)   
 [Novidades do Analysis Services](../analysis-services/what-s-new-in-analysis-services.md)     

  
  
