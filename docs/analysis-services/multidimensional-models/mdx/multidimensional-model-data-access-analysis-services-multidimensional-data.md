---
title: Acesso a dados modelo multidimensional (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5bbf66795c7ac21b0c638aadffaa7bd2ab0a5974
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="multidimensional-model-data-access-analysis-services---multidimensional-data"></a>Acesso a dados de modelo multidimensional (Analysis Services – Dados Multidimensionais)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Use as informações neste tópico para saber como acessar os dados multidimensionais do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] usando métodos programáticos, script ou aplicativos cliente que incluem suporte interno para conexão a um servidor do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] em sua rede.  
  
 Este tópico contém as seguintes seções:  
  
 [Aplicativos cliente](#bkmk_clientapps)  
  
 [Linguagens de consulta](#bkmk_querylang)  
  
 [Interfaces programáticas](#bkmk_api)  
  
##  <a name="bkmk_clientapps"></a> Aplicativos cliente  
 Embora o Analysis Services forneça interfaces que permitem criar ou integrar bancos de dados multidimensionais programaticamente, uma abordagem mais comum é usar aplicativos cliente existentes da Microsoft e de outros fornecedores de software que têm acesso a dados interno aos dados do Analysis Services.  
  
 Os aplicativos da Microsoft a seguir oferecem suporte a conexões nativas a dados multidimensionais.  
  
### <a name="excel"></a>Excel  
 Os dados multidimensionais do Analysis Services geralmente são apresentados usando tabelas dinâmicas e controles de gráfico dinâmico em uma pasta de trabalho do Excel. As Tabelas Dinâmicas são destinadas a dados multidimensionais porque as hierarquias, as agregações e as construções de navegação no modelo ajustam-se aos recursos de resumo de uma Tabela Dinâmica. Um provedor de dados OLE DB do Analysis Services está incluído em uma instalação do Excel para facilitar a configuração de conexões de dados. Para obter mais informações, consulte [Conectar ou importar dados do SQL Server Analysis Services](http://go.microsoft.com/fwlink/?linkID=215150).  
  
### <a name="reporting-services-reports"></a>Relatórios do Reporting Services  
 Você pode usar o Construtor de Relatórios ou Designer de Relatórios para criar relatórios que consomem bancos de dados do Analysis Services que contêm dados analíticos. O Construtor de Relatórios e o Designer de Relatórios incluem um designer de consulta MDX que você pode usar para digitar ou criar instruções MDX que recuperam dados de uma fonte de dados disponível. Para obter mais informações, consulte [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md) e [Tipo de conexão do Analysis Services para MDX &#40;SSRS&#41;](../../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md).  
  
### <a name="performancepoint-dashboards"></a>Painéis de PerformancePoint  
 Os Painéis de PerformancePoint são usados para criar cartões de marcação no SharePoint que comunicam desempenho comercial em medidas predefinidas. O PerformancePoint inclui suporte a conexões de dados para dados multidimensionais do Analysis Services. Para obter mais informações consulte [Criar uma conexão de dados do Analysis Services (serviços do PerformancePoint)](http://go.microsoft.com/fwlink/?linkid=232471).  
  
### <a name="sql-server-data-tools"></a>SQL Server Data Tools  
 Os designers de modelo e relatório usam as Ferramentas de Dados do SQL Server para criar soluções que incluem modelos multidimensionais. Implantar a solução em uma instância do Analysis Services é o que cria o banco de dados ao qual você se conecta subsequentemente do Excel, Reporting Services e outros aplicativos cliente de business intelligence.  
  
 O SQL Server Data Tools é criado em um shell do Visual Studio e usa projetos para organizar e conter o modelo. Para obter mais informações, consulte [Criando modelos multidimensionais usando o SSDT &#40;SQL Server Data Tools&#41;](../../../analysis-services/multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt.md).  
  
### <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 Para administradores de banco de dados, o SQL Server Management Studio é um ambiente integrado para gerenciar suas instâncias do SQL Server, incluindo instâncias do Analysis Services e bancos de dados multidimensionais. Para obter mais informações, consulte [SQL Server Management Studio](http://msdn.microsoft.com/library/66a6b7b1-de6a-4161-82bd-98ded486947b) e [Conectar-se ao Analysis Services](../../../analysis-services/instances/connect-to-analysis-services.md).  
  
##  <a name="bkmk_querylang"></a> Linguagens de consulta  
 O MDX é uma linguagem de cálculo e consulta padrão da indústria usada para recuperar dados de bancos de dados OLAP. No Analysis Services, o MDX é a linguagem de consulta usada para recuperar dados, mas também dá suporte à definição de dados e manipulação de dados. Os editores de MDX estão incorporados no SQL Server Management Studio, no Reporting Services e nas Ferramentas de Dados do SQL Server. Você poderá usar os editores de MDX para criar consultas ad hoc ou script reutilizável se a operação de dados for repetível.  
  
 Algumas ferramentas e aplicativos, como o Excel, usam construções MDX internamente para consultar uma fonte de dados do Analysis Services. Você também pode usar o MDX programaticamente, inserindo uma instrução MDX em uma solicitação XMLA Execute.  
  
 Os seguintes links fornecem mais informações sobre o MDX:  
  
 [Consultando dados multidimensionais com MDX](../../../analysis-services/multidimensional-models/mdx/querying-multidimensional-data-with-mdx.md)  
  
 [Principais conceitos em MDX & #40; Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)  
  
 [Conceitos básicos de consulta MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
 [Conceitos básicos de script MDX & #40; Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)  
  
##  <a name="bkmk_api"></a> Interfaces programáticas  
 Se você estiver criando um aplicativo personalizado que usa dados multidimensionais, sua abordagem para acessar os dados provavelmente cairá em uma das categorias a seguir:  
  
-   **XMLA**. Use XMLA quando você exigir compatibilidade com um ampla variedade de sistemas operacionais e protocolos. O XMLA oferece a maior flexibilidade, mas geralmente a um custo de desempenho aprimorado e facilidade de programação.  
  
-   **Bibliotecas de cliente**. Use as bibliotecas de cliente do Analysis Services, como ADOMD.NET, AMO e OLE DB quando você quiser acessar dados programaticamente de aplicativos cliente que são executados em um sistema operacional Microsoft Windows. As bibliotecas de cliente encapsulam o XMLA com um modelo de objeto e otimizações que fornecem um desempenho melhor.  
  
     As bibliotecas de cliente ADOMD.NET e AMO são para aplicativos escritos em código gerenciado. Use o OLE DB para Analysis Services se seu aplicativo for escrito em código nativo.  
  
 A tabela a seguir fornece detalhes adicionais e links sobre as bibliotecas de cliente usadas para conectar o Analysis Services a um aplicativo personalizado.  
  
|Interface|Description|  
|---------------|-----------------|  
|Objetos de Gerenciamento do Analysis Services (AMO)|AMO é o modelo de objeto primário para administrar instâncias do Analysis Services e bancos de dados multidimensionais em código. Por exemplo, o SQL Server Management Studio usa o AMO para dar suporte à administração de servidor e banco de dados. Para obter mais informações, consulte [Desenvolvendo com AMO &#40;Objetos de Gerenciamento de Análise&#41;](../../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md).|  
|ADOMD.NET|O ADOMD.NET é o modelo de objeto primário que cria e acessa dados multidimensionais em aplicativos personalizados. Você pode usar ADOMD.NET em um aplicativo cliente gerenciado para recuperar informações do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] através de interfaces comuns de acesso a dados do Microsoft .NET Framework. Para obter mais informações, consulte [Desenvolvendo com o ADOMD.NET](../../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md) e [Programação de cliente do ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md).|  
|Provedor OLE DB do Analysis Services (MSOLAP.dll)|Você pode usar o provedor OLE DB nativo para acessar o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] programaticamente de uma API não gerenciada. Para obter mais informações, consulte [Provedor OLE DB do Analysis Services &#40;Analysis Services – Dados Multidimensionais&#41;](http://msdn.microsoft.com/library/cdeecd50-1d91-4162-a4a2-01c7799b02a8).|  
|Conjuntos de linhas de esquema|As tabelas de conjunto de linhas de esquema são estruturas de dados que contêm informações descritivas sobre um modelo multidimensional que é implantado no servidor, assim como informações sobre a atividade atual no servidor. Como programador, você pode consultar tabelas de conjunto de linhas de esquema em aplicativos cliente para examinar metadados armazenados, além de recuperar o suporte e informações de monitoramento a partir de uma instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] . Você pode usar conjuntos de linhas de esquema com estas interfaces programáticas: OLE DB, OLE DB para Analysis Services, OLE DB para Mineração de Dados ou XMLA. Para obter mais informações, consulte [Conjuntos de linhas de esquema do Analysis Services](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md).<br /><br /> A lista a seguir explica várias abordagens para usar conjuntos de linhas de esquema:<br /><br /> - Execute consultas de DMV no SQL Server Management Studio ou em relatórios personalizados para acessar conjuntos de linhas de esquema usando sintaxe de SQL. Para obter mais informações, consulte [Usar DMVs &#40;Exibições de Gerenciamento Dinâmico&#41; para monitorar o Analysis Services](../../../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md).<br /><br /> - Grave o código ADOMD.NET que chama um conjunto de linhas de esquema.<br /><br /> – Execute o método **Discover** de XMLA diretamente em uma instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] para recuperar informações sobre o conjunto de linhas de esquema. Para obter mais informações, consulte [Método Discover &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-methods-discover.md).|  
|XMLA|O XMLA é a API de nível baixo disponível para um programador do Analysis Services e é o denominador comum que está por baixo de todas as metodologias de acesso a dados do Analysis Services. O XMLA é um padrão da indústria, um protocolo XML baseado em SOAP que dá suporte a acesso a dados universal em qualquer fonte de dados multidimensional padrão disponível em uma conexão HTTP. Ele usa o SOAP para formular solicitações e respostas para dados multidimensionais. Se seu aplicativo for executado em uma plataforma não Windows, você poderá usar XMLA para acessar um banco de dados multidimensional que está sendo executado em um servidor de Windows em sua rede. Para obter mais informações, consulte [Desenvolvendo com XMLA no Analysis Services](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md).|  
|ASSL (linguagem de script do Analysis Services)|ASSL é um termo descritivo que se aplica a extensões de Analysis Services do protocolo XMLA. Embora os métodos Execute e Discover são descritos pelo protocolo XMLA, o ASSL adiciona o recurso a seguir:<br /><br /> - Script XMLA<br /><br /> - Definições do objeto XMLA<br /><br /> - Comandos XMLA<br /><br /> As extensões de ASSL permitem que o Analysis Services use as construções do XMLA além das providências básicas do protocolo, adicionando definição de dados, manipulação de dados e suporte a controle de dados. Para obter mais informações, consulte [Desenvolvendo com ASSL &#40;linguagem de script do Analysis Services&#41;](../../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).|  
  
## <a name="see-also"></a>Consulte também  
 [Conectar-se ao Analysis Services](../../../analysis-services/instances/connect-to-analysis-services.md)   
 [Desenvolvimento com o Analysis Services Scripting Language &#40;ASSL&#41;](../../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Desenvolvendo com XMLA no Analysis Services](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)   
 [Acesso de dados de modelo de tabela](../../../analysis-services/tabular-models/tabular-model-data-access.md)  
  
  
