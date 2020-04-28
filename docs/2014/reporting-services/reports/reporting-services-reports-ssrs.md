---
title: Relatórios do Reporting Services (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, report creation
ms.assetid: 52ed9e74-f2c8-488b-a2c2-6dfbc2a2c8cc
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f9697d5a53b2aac0d951445206adc4c4f30e5385
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78177067"
---
# <a name="reporting-services-reports-ssrs"></a>Relatórios do Reporting Services (SSRS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] os relatórios são definições de relatório baseadas em XML que incluem dados de relatório e elementos de layout de relatório. Em um sistema de arquivos cliente, as definições de relatório têm a extensão de arquivo .rdl. Depois que um relatório é publicado, ele se torna um item de relatório armazenada no servidor de relatório ou no site do SharePoint. Relatórios são uma parte da plataforma de relatório baseada em servidor fornecida pelo [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].

 Se o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] for novo para você, revise as informações em [Conceitos do Reporting Services &#40;SSRS&#41;](../reporting-services-concepts-ssrs.md).

## <a name="benefits-of-reporting-services-reports"></a>Benefícios de relatórios do Reporting Services
 Você pode usar as soluções de relatório do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] para:

-   Usar um conjunto de fontes de dados que fornecem uma única versão dos fatos. Baseie os relatórios nessas fontes de dados para fornecer uma exibição unificada de dados para ajudar na tomada de decisões nos negócios.

-   Visualize seus dados de diversas formas interligadas usando regiões de dados. Mostre os dados organizados em tabelas, matrizes ou guias cruzadas, expanda/recolha grupos, gráficos, medidores, indicadores ou KPIs e mapas com a capacidade de aninhar gráficos em tabelas.

-   Exiba os relatórios para seu próprio uso ou publique relatórios em um servidor de relatório ou no site do SharePoint para compartilhar com sua equipe ou organização.

-   Defina um relatório uma vez e exiba-o em uma variedade de modos. Você pode exportar o relatório para vários formatos de arquivos ou entregar o relatório aos assinantes por email ou por um arquivo compartilhado. Você pode criar vários relatórios vinculados que aplicam conjuntos de parâmetros separados à mesma definição de relatório.

-   Use partes de relatório, fontes de dados compartilhadas, consultas compartilhadas e sub-relatórios para definir visualizações de dados para reutilização.

-   Gerencie fontes de dados de relatório separadamente a partir da definição de relatório. Por exemplo, você pode mudar de uma origem de dados de teste para uma fonte de dados de produção sem alterar o relatório.

-   Elabore relatórios em um layout de forma livre. O layout de relatório não é restrito a faixas de informações. Você pode organizar a exibição dos dados na página de forma que promova a compreensão, a perspicácia e a ação.

-   Habilite ações de detalhamento, expanda/recolha alternâncias, classifique botões, dicas de ferramenta e parâmetros de relatório para permitir interações dos leitores com o relatório. Use parâmetros de relatório combinados com expressões que você grava para permitir que os leitores do relatório controlem como os dados são filtrados, agrupados e classificados.

-   Defina expressões que forneçam a capacidade de personalizar como os dados do relatório serão filtrados, agrupados e classificados.

 ![rs_GettingStartedReport](../media/rs-gettingstartedreport.gif "rs_GettingStartedReport")

##  <a name="stages-of-report-processing"></a><a name="bkmk_StagesSummary"></a> Estágios do processamento de relatório
 Ao criar um relatório, você define um arquivo de definição de relatório (.rdl) em formato XML. Esse arquivo contém todas as informações necessárias para combinar dados e layout de relatório pelo processador de relatório. Ao exibir um relatório, o relatório passa pelas seguintes fases:

-   **Compilar.** Avalie expressões na definição de relatório e armazene o formato intermediário compilado internamente no servidor de relatório.

-   **Process.** Execute as consultas de conjunto de dados e combine o formato intermediário com os dados e o layout.

-   **Aplicar.** Envie o relatório processado para uma extensão de renderização para determinar quantas informações cabem em cada página e crie o relatório paginado.

-   **Exportar (opcional).** Exporte o relatório para um formato de arquivo diferente.

 Para obter mais informações, consulte [Estágios de desenvolvimento de relatórios](../reporting-services-concepts-ssrs.md#bkmk_StagesofReports) em [Conceitos do Reporting Services e &#40;SSRS&#41;](../reporting-services-concepts-ssrs.md).

## <a name="create-reports"></a>Criar relatórios
 Para criar um relatório:

-   **Determine o objetivo do relatório.** Identifique o propósito do relatório para o público que o usará. Um relatório bem-elaborado fornece informações aos leitores que proporcionam perspicácia e ação. As decisões tomadas durante a etapa de elaboração influenciam na escolha dos parâmetros do seu relatório, no layout e na experiência de exibição de relatório. Para obter mais informações, consulte [Planejando um relatório &#40;Construtor de Relatórios&#41;](../report-design/planning-a-report-report-builder.md) e [Dicas de design de relatórios &#40;Construtor de Relatórios e SSRS&#41;](../report-design/report-design-tips-report-builder-and-ssrs.md) na [documentação do Construtor de Relatórios](https://go.microsoft.com/fwlink/?LinkId=154494) em msdn.microsoft.com.

-   **Escolha o tipo de consulta.** Determine se usará uma consulta de conjuntos de dados generalizada e compartilhada ou uma consulta de dados específica do seu conjunto de relatórios. Um conjunto de dados compartilhado com uma consulta generalizada é fácil de manter para uso por vários relatórios, mas cada designer de relatório deve filtrar os dados conforme necessário para seu conjunto específico de relatórios. Para obter mais informações, consulte [Dados de relatório &#40;SSRS&#41;](../report-data/report-data-ssrs.md).

-   **Planeje exibições de dados relacionados.** Planeje a experiência de exibição dos leitores dos seus relatórios. Relatórios resumidos com capacidade para busca detalhada de dados são uma abordagem útil para tratar grandes quantidades de dados. Para obter mais informações, consulte [Detalhamento, busca detalhada, sub-relatórios e regiões de dados aninhadas &#40;Construtor de Relatórios e SSRS&#41;](../report-design/drillthrough-drilldown-subreports-and-nested-data-regions.md).

-   **Configure permissões.** Planeje a estratégia para conceder o nível certo de permissões. Uma estratégia comum é criar uma estrutura de pastas no servidor de relatório e conceder acesso aos relatórios e itens relacionados aos relatórios com base em funções e segurança de pasta. Para obter mais informações, consulte [Relatórios seguros](#bkmk_SecureReportsSummary).

-   **Escolha um ambiente de criação.** As ferramentas de criação variam o suporte para recursos. Para obter mais informações, consulte [Ferramentas do Reporting Services](../tools/reporting-services-tools.md).

-   Para cada relatório:

    -   **Identifique fontes de dados.** Defina fontes de dados de relatório, uma para cada fonte de dados. Para obter mais informações, consulte [Conexões de dados, fontes de dados e cadeias de conexão no Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md).

    -   **Escolha os dados que serão usados em cada origem.** Para cada fonte de dados, defina conjuntos de dados de relatório. Cada conjunto de dados inclui uma consulta para especificar os dados que serão usados. Se você tiver parâmetros de relatório, defina um conjunto de dados para preencher a lista de valores disponíveis para cada parâmetro. Para obter mais informações, consulte [Adicionar dados a um relatório &#40;Construtor de Relatórios e SSRS&#41;](../report-data/report-datasets-ssrs.md) e [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de relatórios&#41;](../report-design/report-parameters-report-builder-and-report-designer.md).

    -   **Escolha uma visualização de dados.** Para cada conjunto de dados, escolha a região de dados que será usada para exibir os dados. Escolha entre lista de tabelas, gráficos, medidores e mapas. Para obter mais informações, consulte estes tópicos:

        -   [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)

        -   [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](../report-design/charts-report-builder-and-ssrs.md)

        -   [Minigráficos e barras de dados &#40;Construtor de Relatórios e SSRS&#41;](../report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)

        -   [Indicadores &#40;Construtor de Relatórios e SSRS&#41;](../report-design/indicators-report-builder-and-ssrs.md)

        -   [Mapas &#40;Construtor de Relatórios e SSRS&#41;](../report-design/maps-report-builder-and-ssrs.md)

        -   [Medidores &#40;Construtor de Relatórios e SSRS&#41;](../report-design/gauges-report-builder-and-ssrs.md)

    -   **Personalize o layout e os dados.** Elabore o layout do relatório. Uma definição de relatório tem um corpo de relatório, fontes de dados, conjuntos de dados, regiões de dados, caixas de texto, linhas e imagens. Retângulos são usados como contêineres para layout e elementos visuais. Personalize cada região de dados gravando expressões para controlar filtro, grupo, classificação, formato e exibição dos dados. Adicione nomes de relatório, locais e outras informações de identificação que ajudam a gerenciar dúzias ou centenas de relatórios. Adicione elementos visuais e contêineres para organizar os elementos de layout na página. Para obter mais informações, consulte estes tópicos:

        -   [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)

        -   [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)

        -   [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)

        -   [Formatando itens de relatório &#40;Construtor de Relatórios e SSRS&#41;](../report-design/formatting-report-items-report-builder-and-ssrs.md)

        -   [Imagens, caixas de texto, retângulos e linhas &#40;Construtor de Relatórios e SSRS&#41;](../report-design/rectangles-and-lines-report-builder-and-ssrs.md)

        -   [Layout da página e renderização &#40;Construtor de Relatórios e SSRS&#41;](../report-design/page-layout-and-rendering-report-builder-and-ssrs.md)

    -   **Configure recursos de interatividade.** Adicione recursos de interatividade para os leitores dos seus relatórios. Por exemplo, adicione botões de classificação ou itens de alternância de exibição das consultas. Para obter mais informações, consulte [Classificação interativa, mapas de documentos e links &#40;Construtor de Relatórios e SSRS&#41;](../report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md).

    -   **Examine e itere o design.** Visualize o relatório. Publique uma versão preliminar para obter comentários dos leitores de seus relatórios. Itere o design.

-   **Examine a solução de relatório.** Verifique se o conjunto de relatórios interage corretamente.

-   **Considere os componentes que podem reutilizados.**  Determine se alguma das fontes de dados ou consultas de conjunto de dados pode ser compartilhada para reutilização. Se puder, no servidor de relatório ou no site do SharePoint, crie fontes de dados ou conjuntos de dados compartilhados. Determine se as regiões de dados são adequadas para reutilização como partes de relatório. Para obter mais informações, consulte [Partes de relatório no Designer de Relatórios &#40;SSRS&#41;](../report-design/report-parts-in-report-designer-ssrs.md).

## <a name="preview-reports"></a>Visualizar relatórios
 Cada ferramenta de criação de relatório oferece suporte à visualização de relatórios. Para obter mais informações, consulte [Visualização](../tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md#bkmk_Preview), [Construtor de Relatórios &#40;SSRS&#41;](../tools/report-builder-authoring-environment-ssrs.md) e [Visualizando relatórios no Construtor de Relatórios](../report-builder/previewing-reports-in-report-builder.md) na [documentação do Construtor de Relatórios](https://go.microsoft.com/fwlink/?LinkId=154494) em msdn.microsoft.com.

## <a name="save-or-publish-reports"></a>Salvar ou publicar relatórios
 Cada ferramenta de criação oferece suporte para salvar relatórios localmente ou publicá-los em um servidor de relatório ou no site do SharePoint. Para obter mais informações, consulte [Salvar e implantar](../tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md#bkmk_SaveandDeploy), [Construtor de Relatórios &#40;SSRS&#41;](../tools/report-builder-authoring-environment-ssrs.md) e [Salvando relatórios &#40;Construtor de Relatórios&#41;](../report-builder/saving-reports-report-builder.md) na [documentação do Construtor de Relatórios](https://go.microsoft.com/fwlink/?LinkId=154494) em msdn.microsoft.com.

## <a name="view-reports"></a>Exibir relatórios
 Além de visualizar um relatório salvo localmente ou publicado em um servidor de relatório, você pode fornecer uma variedade de experiências de exibição para os leitores de seus relatórios. Para exibir um relatório:

-   **Navegador.**  Use o Serviço Web Servidor de Relatórios ou o site do SharePoint para exibir relatórios publicados. Em um site do SharePoint, você também pode configurar uma Web Part para exibir relatórios publicados. Para obter mais informações, consulte [Planejando o suporte a navegador do Reporting Services e Power View &#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md), [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../report-manager-ssrs-native-mode.md) e [Acesso à URL &#40;SSRS&#41;](../url-access-ssrs.md).

-   **Entrega.**  Configure uma assinatura para entregar relatórios aos leitores por email ou por uma pasta de arquivos compartilhada.  Para obter mais informações, consulte [Assinaturas e entrega &#40;Reporting Services&#41;](../subscriptions/subscriptions-and-delivery-reporting-services.md).

-   **Export.**  Na barra de ferramentas do visualizador de relatórios, o leitor do relatório pode exportá-lo para um formato de arquivo diferente. Os formatos de arquivos de exportação podem ser configurados pelo administrador do servidor de relatório. Para obter mais informações, consulte [Exportando relatórios &#40;Construtor de Relatórios e SSRS&#41;](../report-builder/export-reports-report-builder-and-ssrs.md)

-   **Imprimir.**  O leitor do relatório pode imprimir um relatório ou páginas do documento dependendo do modo no qual é exibido. Para obter mais informações, consulte [Imprimir Relatórios &#40;Construtor de Relatórios e SSRS&#41;](../report-builder/print-reports-report-builder-and-ssrs.md).

-   **Web ou aplicativo Windows Form.**  Use o Visual Studio para desenvolver um aplicativo ASP.NET AJAX ou Windows Form que hospede o controle do Visualizador de Relatórios. O controle pode apontar para relatórios publicados em um servidor de relatório. Para obter mais informações, consulte [Relatórios da Microsoft](https://go.microsoft.com/fwlink/?LinkID=205399).

## <a name="manage-reports"></a>Gerenciar relatórios
 Para gerenciar um relatório publicado:

-   **Fontes de dados.** As fontes de dados inseridas e compartilhadas são gerenciadas de forma independente da definição do relatório.

-   **Conjuntos.**  Os conjuntos de dados compartilhados são gerenciados de forma independente da definição do relatório.

-   **Parâmetro.**  Os parâmetros são gerenciados independentemente da definição de relatório. Depois que os parâmetros são alterados no servidor de relatório, os clientes de criação de relatório não podem publicar sobre as alterações feitas no servidor.

-   **Os.**  Imagens e dados espaciais em shapefiles ESRI são recursos que podem ser publicados e gerenciados de forma independente da definição de relatório.

-   **Cache de relatório.**  Agendando a execução de grandes relatórios durante horas fora do pico de atividade, você pode reduzir o impacto do processamento no servidor de relatório durante o horário comercial.

-   **Instantâneos.**  Use instantâneos de relatório quando desejar fornecer resultados consistentes para vários usuários que devem trabalhar com conjuntos de dados idênticos. Com dados voláteis, um relatório sob demanda pode produzir resultados diferentes de um minuto para o outro. Por outro lado, um instantâneo de relatório permite fazer comparações válidas com outros relatórios ou ferramentas analíticas que contêm dados do mesmo momento.

-   **Histórico de relatórios.** Com a criação de uma série de instantâneos de relatórios, você pode criar um histórico de um relatório que mostra como os dados mudam com o passar do tempo.

 Para obter mais informações sobre o desempenho, consulte [Desempenho, instantâneos, caching &#40;Reporting Services&#41;](../report-server/performance-snapshots-caching-reporting-services.md).

##  <a name="secure-reports"></a><a name="bkmk_SecureReportsSummary"></a> Relatórios seguros
 Para proteger um relatório:

-   No administrador do servidor de relatório, identifique a autorização e o sistema de autenticação que são usados em sua instalação do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] . Por padrão, o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] usa a autenticação do Windows, segurança integrada e atribuição de função para ajudar a controlar o acesso aos relatórios publicados. Para obter mais informações, consulte [Funções e permissões &#40;Reporting Services&#41;](../security/roles-and-permissions-reporting-services.md) e [Segurança e proteção do Reporting Services](../security/reporting-services-security-and-protection.md).

## <a name="create-notifications-based-on-report-data"></a>Criar notificações com base em dados de relatório
 Você pode criar alertas de dados para relatórios publicados em um site do SharePoint. Os alertas de dados são baseados em feeds de dados de regiões de dados no relatório. Por padrão, as regiões de dados são nomeadas automaticamente. Os autores de relatório podem facilitar a criação de alertas de dados em seus relatórios nomeando regiões de dados com base no propósito de negócios. Ao criar um alerta de dados, você é notificado por email quando os dados atendem às condições especificadas. Para obter mais informações, consulte [Gerando feeds de dados com base em relatórios &#40;Construtor de Relatórios e SSRS&#41;](../report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md), [Criar um alerta de dados no Designer de Alertas de Dados](../create-a-data-alert-in-data-alert-designer.md) e [Alertas de dados do Reporting Services](../reporting-services-data-alerts.md).

## <a name="upgrade-reports"></a>Upgrade Reports
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] oferece suporte a várias versões de definições de relatório, servidores de relatório e sites do SharePoint. Para atualizar um relatório:

-   Atualize uma instalação de servidor de relatório. Os relatórios compilados armazenados no servidor de relatório são atualizados automaticamente no primeiro uso. A definição de relatório (.rdl) não é alterada. Para obter mais informações, consulte [atualizar e migrar Reporting Services](../install-windows/upgrade-and-migrate-reporting-services.md).

-   Abra um relatório em um ambiente de criação de relatórios. A definição de relatório é atualizada na maioria das circunstâncias. Para obter mais informações, consulte [Atualizar Relatórios](../install-windows/upgrade-reports.md) e [Implantação e suporte de versão no SQL Server Data Tools &#40;SSRS&#41;](../tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md).

## <a name="troubleshoot-reports"></a>Solucionar problemas de relatórios
 Para solucionar problemas de um relatório:

-   **Determine onde o problema está ocorrendo.** Revise as informações em [Fases de um relatório](#bkmk_StagesSummary).

-   **Determine onde você pode encontrar mais informações.** Por exemplo, para design de relatório que inclui expressões, a ferramenta Designer de Relatórios fornece mais informações sobre problemas de avaliação de expressões do que a ferramenta Construtor de Relatórios. Para erros de processamento de relatório, os arquivos de log contêm informações detalhadas.

## <a name="tasks"></a>Tarefas
 Para links para tópicos passo a passo, consulte a seção Tarefa em artigos sobre o recurso mencionados nas seções anteriores deste tópico.

## <a name="see-also"></a>Consulte Também
 Extensões de [ferramentas de Reporting Services](../tools/reporting-services-tools.md) [&#40;SSRS&#41;](../extensions-ssrs.md) [Reporting Services servidor de relatório](../reporting-services-report-server.md)


