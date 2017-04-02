---
title: "Portal da Web (Modo Nativo do SSRS) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "02/24/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
ms.assetid: 7349e626-6ed5-4d21-b05f-cf042ad9ad70
caps.latest.revision: 15
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 13
---
# Portal da Web (Modo Nativo do SSRS)
O [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] do Reporting Services é uma experiência baseada na Web que permite exibir relatórios, relatórios móveis e KPIs, bem como navegar por meio de elementos que estão em sua instância do servidor de relatório. Você também pode usar o [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] para administrar uma única instância do servidor de relatório.  
  
![ssRSPortal](../reporting-services/media/ssrsportal.png)  
  
Neste tópico:  
  
-   [O que é o portal da Web?](#whatisportal)  
  
-   [Iniciar e usar o portal da Web](#startanduse)  
  
-   [Agrupando por categorias](#categories)  
  
-   [Pesquisar itens](#search)  
  
-   [Tarefas do portal da Web](#tasks)  
  
<a name="whatisportal"/>  
## O que é o [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]?  
  
Você pode utilizar o [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] para executar as seguintes tarefas:  
  
-   Exibir, pesquisar, imprimir e assinar relatórios.  
  
-   Criar, proteger e manter a hierarquia de pastas para organizar itens no servidor.  
  
-   Configure a segurança baseada em função que determina o acesso a itens e operações.  
  
-   Configurar propriedades de execução de relatório, histórico de relatórios e parâmetros de relatório.  
  
-   Criar agendas compartilhadas e fontes de dados compartilhadas para tornar as agendas e as conexões de fonte de dados mais gerenciáveis.  
  
-   Criar assinaturas controladas por dados que distribuem relatórios para uma grande lista de destinatários.  
  
-   Criar relatórios vinculados para reutilizar e realocar um relatório existente de diferentes maneiras.  
  
-   Baixar ferramentas comuns, como o Construtor de Relatórios e o Publicador de Relatórios Móveis.  
  
-   [Criar KPIs](../reporting-services/working-with-kpis-in-reporting-services.md).  
  
-   Enviar comentários ou fazer solicitações de recursos.  
  
Você pode usar o [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] para navegar pelas pastas do servidor de relatório ou procurar relatórios específicos. É possível exibir um relatório, suas propriedades gerais e cópias antigas do relatório que são capturadas no histórico de relatórios. Dependendo de suas permissões, você também pode assinar relatórios para serem entregues em uma caixa de entrada de email ou pasta compartilhada no sistema de arquivos.  
  
> [!NOTE] Para saber mais sobre navegadores e versões compatíveis, confira [Planning for Reporting Services Browser Support](../reporting-services/browser-support-for-reporting-services-and-power-view.md) (Planejar o suporte ao navegador do Reporting Services).  
  
O [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] é usado apenas para um servidor de relatório executado no modo nativo. Ele não possui suporte para um servidor de relatório configurado no modo integrado do SharePoint.  
  
Alguns recursos do [!INCLUDE[ssNoVersion](../includes/ssnoversion.md)] só estão disponíveis em edições específicas do [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]. Para saber mais, confira [Features supported by the Editions of SQL Server 2016](Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.xml) (Recursos compatíveis com as edições do SQL Server 2016).  
  
Em uma nova instalação, somente os administradores locais têm permissões suficientes para trabalhar com o conteúdo e as configurações. Para conceder permissões a outros usuários, o administrador local deve criar atribuições de função que fornecem acesso ao servidor de relatório. As páginas de aplicativo e as tarefas que um usuário pode acessar posteriormente dependem das atribuições de função do usuário em questão. Para saber mais, confira como adicionar um usuário ao Servidor de Relatório.  
  
> [!NOTE] Se você estiver navegando para o portal da Web no computador local em que o servidor está em execução, será exibida uma mensagem indicando que você não tem permissão para exibir essa pasta. Isso se deve ao UAC (Controle de Acesso Universal) e ao fato de que você não está executando o navegador como um administrador. Não é possível executar o Edge como um administrador. Você precisará usar o Internet Explorer. É possível navegar até o servidor remotamente ou iniciar o Internet Explorer como administrador e navegar até o portal da Web. Se quiser usar o portal da Web remotamente, você precisará conceder direitos de pasta ao gerenciador de conteúdo da sua conta.  
  
<a name="startanduse"/>  
## Iniciar e usar o [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]  
  
O [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] é um aplicativo Web que você abre digitando a URL do [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] na barra de endereços em uma janela do navegador. Ao iniciar o [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)], as páginas, os links e as opções exibidas variam com base nas permissões que você tem no servidor de relatório. Para executar uma tarefa, você deve estar atribuído a uma função que inclua a tarefa.  Um usuário que é atribuído a uma função que possui permissões totais tem acesso ao conjunto completo de menus e páginas de aplicativo disponíveis para gerenciar um servidor de relatório. Um usuário atribuído a uma função que possui permissões totais para exibir e executar relatórios vê apenas os menus e páginas que oferecem suporte a essas atividades. Cada usuário pode ter diferentes atribuições de função para diferentes servidores de relatório ou mesmo para diversos relatórios e pastas armazenados em um único servidor de relatório.  
  
Para saber mais sobre funções, confira [Concedendo permissões em um servidor de relatório no modo nativo](../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md).  
  
### Iniciar o [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]  
Para iniciar o [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] em um navegador, siga estas etapas:  
  
1.  Abra o navegador da Web. Para obter uma lista de navegadores da Web compatíveis, confira [Planning for Reporting Services Browser Support](../reporting-services/browser-support-for-reporting-services-and-power-view.md) (Planejando o suporte ao navegador do Reporting Services).  
  
2.  Na barra de endereço do navegador da Web, digite a URL do [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)].  
  
    Por padrão, a URL é *http://[NomeDoComputador]/relatórios*.  
  
    O servidor de relatório pode estar configurado para usar uma porta específica. Por exemplo *http://[NomeDoComputador]:80/relatórios* ou *http://[NomeDoComputador]:8080/relatórios*  
  
<a name="categories">  
## Agrupando por categorias  
  
O [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] agrupará itens em diferentes categorias. As categorias disponíveis incluem:  
  
-   KPIs  
-   Relatórios móveis  
-   Relatórios paginados  
-   Relatórios do Power BI Desktop  
-   Pastas de trabalho do Excel  
-   Conjuntos de dados  
-   Fontes de Dados  
-   Recursos  
  
Você pode controlar o que é exibido selecionando **Exibir** no canto superior direito. Os itens marcados serão exibidos se houver itens disponíveis na pasta especificada. Para ocultar itens, você pode desmarcá-los.  
  
![ssRSWebPortal-view](../reporting-services/media/ssrswebportal-view.png)  
   
Se você selecionar Mostrar Ocultos, esses itens serão exibidos em uma cor mais clara.  
  
![ssRSWebPortal-hidden](../reporting-services/media/ssrswebportal-hidden.png)  
   
### Relatórios do Power BI Desktop e pastas de trabalho do Excel  
  
É possível carregar, organizar e gerenciar permissões para relatórios do Power BI Desktop e pastas de trabalho do Excel. Eles serão agrupados juntas no portal da Web.  
  
![ssRSWebPortal-view-pbi-and-excel](../reporting-services/media/ssrswebportal-view-pbi-and-excel.png)  
   
Os arquivos são armazenados no Reporting Services, semelhante a outros arquivos de recurso. Selecionar um desses itens os baixará localmente no desktop. Você pode salvar as alterações feitas ao carregá-las no servidor de relatório.  
  
<a name="search">  
## Pesquisar itens  
  
Você pode inserir uma equipe de pesquisa e verá tudo que pode ser acessado. Os resultados são categorizados em KPIs, relatórios, conjuntos de dados e outros itens. Desse modo, você pode interagir com os resultados e adicioná-los aos seus favoritos.  
  
![ssRSWebPortal-Search](../reporting-services/media/ssrswebportal-search.png)  
  
<a name="tasks">  
## Tarefas do portal da Web  
  
[Identidade visual do portal da Web](../reporting-services/branding-the-web-portal.md)  

[Como trabalhar com KPIs](../reporting-services/working-with-kpis-in-reporting-services.md)
  
[Working with shared datasets (Trabalhando com conjuntos de dados compartilhados)](../reporting-services/working-with-shared-datasets-web-portal.md)  
  
## Consulte também

[Criar relatórios móveis com o Publicador de Relatórios Móveis do SQL Server](../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)
  
[Configurar um URL (Gerenciador de configurações SSRS)](../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
  
[Ferramentas do Reporting Services](../reporting-services/tools/reporting-services-tools.md)  
  
[Planejamento para suporte ao navegador do Reporting Services](../reporting-services/browser-support-for-reporting-services-and-power-view.md)  
  
[Recursos compatíveis com as edições do SQL Server 2016](Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.xml)  
  
  
