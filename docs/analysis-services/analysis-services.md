---
title: "Analysis Services | Microsoft Docs"
ms.date: "03/28/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
helpviewer_keywords: 
  - "Analysis Services, sobre o Analysis Services - Dados Multidimensionais"
  - "SSAS"
  - "Analysis Services"
  - "SQL Server Analysis Services, sobre o Analysis Services - Dados Multidimensionais"
  - "SQL Server Analysis Services"
  - "dados multidimensionais [Analysis Services]"
  - "SSAS, sobre o Analysis Services - Dados Multidimensionais"
ms.assetid: 49d186f4-4b4d-4a5a-bb1a-e2699c64a731
caps.latest.revision: 60
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 60
---
# Analysis Services
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] é um mecanismo de dados analíticos online usado em soluções de apoio à decisão e análise de negócios, que fornece os dados analíticos para relatórios de negócios e aplicativos cliente, tais como Excel, relatórios do Reporting Services e outras ferramentas de visualização de dados de terceiros.  
  
 Um fluxo de trabalho típico do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] inclui criar um modelo de dados multidimensional ou de tabela, implantar o modelo como um banco de dados em uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , processar o banco de dados para carregá-lo com dados ou metadados, configurar a atualização dos dados e, em seguida, atribuir permissões para permitir o acesso a dados pelos usuários finais. Quando ele estiver pronto, esse modelo de dados semânticos om vários fins poderá ser acessado por qualquer aplicativo cliente que dê suporte ao [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] como uma fonte de dados.  
  
 Os modelos são preenchidos com dados de sistemas de dados externos, geralmente data warehouses hospedados em um SQL Server ou um mecanismo de banco de dados relacional Oracle (os modelos de tabela oferecem suporte a tipos de fontes de dados). Modelos especificam objetos de consulta, como cubos, mas também especificam as dimensões que podem ser utilizadas em vários cubos, cálculos e KPIs que encapsulam a lógica de negócios e as interações, como comportamentos de detalhamento e navegação.  
 
## <a name="analysis-services-on-premises-and-in-the-cloud"></a>Analysis Services local e na nuvem
Analysis Services agora está disponível na nuvem como um serviço do Azure. Atualmente na visualização, os serviços de análise do Azure oferece suporte a modelos de tabela no nível de compatibilidade 1200. DirectQuery, partições, segurança de nível de linha, relações bidirecionais e traduções todas têm suporte. Para saber mais e experimentar gratuitamente, consulte [Azure Analysis Services](https://azure.microsoft.com/en-us/services/analysis-services/). 
  
## <a name="server-mode"></a>Modo do Servidor  
 Ao instalar o Analysis Services usando a Instalação do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] , durante a configuração, especifique um modo de servidor para a instância.  Cada modo inclui diferentes recursos exclusivos para uma solução específica do Analysis Services.  
  
-   **Modo de mineração de dados e multidimensional** – Implemente construções de modelagem OLAP (cubos, dimensões, medidas).  
  
-   **Modo de Tabela** – Implemente construções de modelagem de dados relacionais na memória (modelo, tabelas, colunas).  
  
     Os modelos de tabela podem ser criados no nível de compatibilidade padrão 1200, usando a funcionalidade mais recente, ou no nível de compatibilidade 1103 mais antigo. Há diferenças significativas entre os níveis de compatibilidade. Consulte [Nível de compatibilidade para modelos de Tabela no Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md) para obter informações sobre como os níveis se comparam.  
  
-   **Modo do Power Pivot** – Implemente modelos de dados do [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] e do Excel no SharePoint (o[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para SharePoint é um mecanismo de dados de camada intermediária que carrega, consulta e atualiza modelos de dados hospedados no SharePoint).  
  
 Uma única instância pode ser configurada com apenas um modo, e não pode ser alterada posteriormente.  Você pode instalar várias instâncias com modos diferentes no mesmo servidor, mas precisará executar a Instalação e especificar as definições de configuração para cada instância.  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] recursos variam de acordo com a edição. Para obter mais informações, consulte [Edições e Recursos com suporte do SQL Server 2016](../sql-server/edições-e-recursos-com-suporte-para-sql-server-2016.md) 
  
## <a name="authoring-solutions"></a>Criação de soluções  
 Para criar um modelo, use o SQL Server Data Tools (consulte [Ferramentas e aplicativos usados no Analysis Services](../analysis-services/tools-and-applications-used-in-analysis-services.md)), escolha um modelo de projeto de Tabela ou Multidimensional e Mineração de Dados. O modelo de projeto contém pastas de todos os objetos necessários em um modelo. Assistentes ajudam a criar muitos dos elementos básicos, como fontes de dados, modos de exibição de fonte de dados, dimensões, cubos e funções.  
  
## <a name="documentation-by-area"></a>Documentação por área  
A documentação do Analysis Services é organizada em seções que correspondem ao tipo de projeto que você está criando. Escolha entre os links a seguir para saber mais sobre cada modo ou área de recurso.  
   
 ![Ícone de pasta de arquivos pequeno](../analysis-services/media/filefolder-small.png "Ícone de pasta de arquivos pequeno") [Novidades](../analysis-services/what-s-new-in-analysis-services.md)  
  
 ![Ícone de pasta de arquivos pequeno](../analysis-services/media/filefolder-small.png "Ícone de pasta de arquivos pequeno") [Comparando soluções tabulares e multidimensionais](../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)  
  
 ![Ícone de pasta de arquivos pequeno](../analysis-services/media/filefolder-small.png "Ícone de pasta de arquivos pequeno") [Modelos de tabela](../analysis-services/tabular-models/tabular-models-ssas.md)  
  
 ![Ícone de pasta de arquivos pequeno](../analysis-services/media/filefolder-small.png "Ícone de pasta de arquivos pequeno") [Modelos multidimensionais](../analysis-services/multidimensional-models/multidimensional-models-ssas.md)  
  
 ![Ícone de pasta de arquivos pequeno](../analysis-services/media/filefolder-small.png "Ícone de pasta de arquivos pequeno") [Mineração de dados](../analysis-services/data-mining/data-mining-ssas.md)  
  
 ![Ícone de pasta de arquivos pequeno](../analysis-services/media/filefolder-small.png "Ícone de pasta de arquivos pequeno") [Power Pivot para SharePoint](../analysis-services/power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)  
  
 ![Ícone de pasta de arquivos pequeno](../analysis-services/media/filefolder-small.png "Ícone de pasta de arquivos pequeno") [Gerenciamento de instância do Analysis Services](../analysis-services/instances/analysis-services-instance-management.md)  
   
 ![Ícone de pasta de arquivos pequeno](../analysis-services/media/filefolder-small.png "Ícone de pasta de arquivos pequeno") [Tutoriais do Analysis Services](../analysis-services/analysis-services-tutorials-ssas.md)  
  
![Ícone de pasta de arquivos pequeno](../analysis-services/media/filefolder-small.png "Ícone de pasta de arquivos pequeno") [Documentação do desenvolvedor do Analysis Services](https://msdn.microsoft.com/library/bb500153(SQL.130).aspx)  
 
![Ícone de pasta de arquivos pequeno](../analysis-services/media/filefolder-small.png "Ícone de pasta de arquivos pequeno") [Referência técnica (SSAS)](../analysis-services/powershell/technical-reference-ssas.md)