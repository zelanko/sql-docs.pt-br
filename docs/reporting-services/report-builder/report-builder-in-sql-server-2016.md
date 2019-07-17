---
title: Construtor de Relatórios no SQL Server | Microsoft Docs
ms.date: 05/10/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
f1_keywords:
- "10428"
helpviewer_keywords:
- overview of Report Builder
- getting started
ms.assetid: 55bf4f9c-d037-412f-ae57-3fc39ce32fa5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c10e37d7c1231a3ed4db2d7412ea223cccc6922d
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67688513"
---
# <a name="report-builder-in-sql-server"></a>Construtor de Relatórios no SQL Server

 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] é uma ferramenta para criação de relatórios paginados para usuários comerciais que preferem trabalhar em um ambiente autônomo em vez de usar o Designer de Relatórios no Visual Studio/SSDT.  Quando você cria um relatório paginado, está criando uma definição de relatório que especifica quais dados recuperar, onde obtê-los e como exibi-los. Ao executar o relatório, o processador de relatório obtém todas as informações especificadas, recupera os dados e combina-os ao layout de relatório para gerar este relatório. Você pode visualizar o relatório no [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]. Em seguida, publicar seu relatório em um servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo nativo ou no modo integrado do SharePoint (2016 e anterior). 

Você também pode publicar um relatório paginado no serviço do Power BI. Leia mais sobre [relatórios paginados no Power BI Premium](https://docs.microsoft.com/power-bi/paginated-reports-report-builder-power-bi) (Versão prévia).
  
 ![rs_GettingStartedReport](../../reporting-services/report-builder/media/rs-gettingstartedreport.png "rs_GettingStartedReport")  
  
 Esse relatório paginado caracteriza uma matriz com grupos de linhas e colunas, minigráficos, indicadores e um gráfico de pizza resumido na célula de canto, acompanhada de um mapa com dois conjuntos de dados geográficos representados pela cor e pelo tamanho do círculo.  
  
##  <a name="JumpStartReptCreation"></a> Iniciar a criação de relatório  
  
-   **Iniciar com um conjunto de dados compartilhado**. Os conjuntos de dados compartilhados são consultas baseadas em uma fonte de dados compartilhados e salvos em um servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em modo nativo ou modo integrado do SharePoint.  
  
-   **Inicie com o assistente de Tabela, Matriz ou Gráfico**. Escolha uma conexão de fonte de dados, arraste e solte campos para criar uma consulta de conjunto de dados, selecione um layout e um estilo e personalize seu relatório.  
  
-   **Inicie com o assistente de Mapa** para criar relatórios que exibam dados agregados em um plano de fundo geográfico ou geométrico. Os dados de mapa podem ser dados espaciais de uma consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] ou um arquivo de forma ESRI (Environmental Systems Research Institute, Inc.). Também é possível adicionar um plano de fundo de peça de mapa do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Bing.  
  
-   **Iniciar o relatório com partes de relatório**. As partes de relatório são itens de relatório que foram publicados separadamente em um servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em modo nativo ou em modo integrado do SharePoint. Partes de relatório podem ser reutilizadas em outros relatórios. Itens de relatório como tabelas, matrizes, gráficos e imagens podem ser publicados como partes de relatório.  
  
##  <a name="DesignRept"></a> Criar seu relatório  
  
-   **Crie relatórios paginados com tabela, matriz, gráfico e layouts de relatório de forma livre.** Crie relatórios de tabelas para dados baseados em colunas, relatórios de matriz (como relatórios de tabela de referência cruzada ou de Tabela Dinâmica) para dados resumidos, relatórios de gráficos para dados geográficos e relatórios de formato livre para qualquer outra finalidade. Os relatórios podem ser inseridos em outros relatórios e gráficos, junto com listas, gráficos e controles para aplicativos dinâmicos baseados na Web.  
  
-   **Use várias fontes de dados para gerar relatórios.** Crie relatórios usando dados de qualquer tipo de fonte de dados que tenham um provedor de dados gerenciado por [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], um provedor OLE DB ou uma fonte de dados ODBC. Você pode criar relatórios que usam dados relacionais e multidimensionais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], Oracle, Hyperion e outros bancos de dados. Você pode usar uma extensão de processamento de dados XML para recuperar dados de qualquer fonte de dados XML. Também é possível usar funções com valor de tabela para projetar fontes de dados personalizadas.  
  
-   **Modifique relatórios existentes.** Com o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)], você pode personalizar e atualizar relatórios criados no Designer de Relatórios do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
-   **Modifique seus dados** filtrando, agrupando e classificando dados ou adicionando fórmulas ou expressões.  
-   **Adicione gráficos, medidores, minigráficos e indicadores** para resumir dados em um formato visual e apresentar grandes volumes de informações agregadas de forma concisa.  
  
-   **Adicione recursos interativos** , como mapas de documento, botões para mostrar/ocultar e links de detalhamento, a sub-relatórios e relatórios de detalhamento. Use parâmetros e filtros para filtrar dados para exibições personalizadas.  
  
-   **Insira ou referencie imagens** e outros recursos, incluindo conteúdo externo.  
  
##  <a name="ManageRpt"></a> Gerenciar seu Relatório  
  
-   **Salve a definição do relatório** no computador ou no servidor de relatório, onde é possível gerenciá-lo e compartilhá-lo com outros.  
  
-   **Escolha um formato de apresentação** ao abrir o relatório ou depois de abri-lo. Você pode selecionar formatos voltados para a Web, para a página e de aplicativos de desktop. Os formatos incluem HTML, MHTML, PDF, XML, CSV, TIFF, Word e Excel.  
  
-   **Configure assinaturas.** Depois de publicar o relatório no servidor de relatório ou em um servidor de relatório no modo integrado do SharePoint, você poderá configurá-lo para ser executado em um determinado horário, criar um histórico do relatório e configurar assinaturas de email.  
  
-   **Gere feeds de dados** de seu relatório usando a extensão de renderização Atom do Reporting Services.  
  
> [!NOTE]  
>  Os relatórios publicados são gerenciados em um servidor de relatório ou um servidor de relatório no modo integrado do SharePoint por um administrador do servidor de relatório. Os administradores de servidor de relatório podem definir a segurança, estabelecer as propriedades e agendar operações, como histórico de relatório e entrega de relatório de email. Também podem criar agendas e fontes de dados compartilhadas e disponibilizá-las para uso geral. Os administradores também gerenciam todas as pastas de servidor de relatório. A possibilidade de executar tarefas de gerenciamento depende das permissões de usuário.  
  
## <a name="see-also"></a>Consulte Também  
  [Iniciar o Construtor de Relatórios](../../reporting-services/report-builder/start-report-builder.md)  
  
  [Instalar o Construtor de Relatórios](../../reporting-services/install-windows/install-report-builder.md)

  [Novidades no SQL Server Reporting Services e no Construtor de Relatórios](~/reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)  
  Descreve os novos recursos nesta versão do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] e [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)].   
  [Tutorial: Criando um relatório de gráfico rápido offline](../../reporting-services/report-builder/tutorial-create-a-quick-chart-report-offline-report-builder.md)  
 Apresenta o [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] e os assistentes disponíveis para ajudá-lo a criar relatórios. O tutorial fornece um conjunto de dados com o qual trabalhar, de modo que você não precise se conectar a uma fonte de dados para começar.  
  
 [Planejando um relatório &#40;Construtor de Relatórios&#41;](../../reporting-services/report-design/planning-a-report-report-builder.md)  
 Fornece informações sobre o que você deve considerar antes de começar a criar seu relatório.  
  
 [Conceitos do Reporting Services (SSRS)](../reporting-services-concepts-ssrs.md)  
 Define os conceitos-chave usados em toda a documentação do [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] .  
  
 [Modo de exibição de Design de relatório &#40;Construtor de Relatórios&#41;](../../reporting-services/report-builder/report-design-view-report-builder.md)  
 Explica os diferentes painéis e regiões da exibição de design de relatório.  
  
 [Modo de exibição de Design de conjunto de dados compartilhados &#40;Construtor de Relatórios&#41;](../../reporting-services/report-builder/shared-dataset-design-view-report-builder.md)  
 Explica os diferentes painéis e regiões da exibição de design do conjunto de dados compartilhados.  
  
 [Atalhos de teclado &#40;Construtor de Relatórios&#41;](../../reporting-services/report-builder/keyboard-shortcuts-report-builder.md)  
 Descreve as teclas de atalho disponíveis para navegar e criar relatórios no [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)].  
  

