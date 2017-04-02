---
title: "Novidades do Reporting Services (SSRS) | Microsoft Docs"
ms.date: "03/14/2017"
ms.prod: "sql-vnext"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
  - "reporting-services-sharepoint"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
helpviewer_keywords: 
  - "novidades [Reporting Services]"
  - "Reporting Services, o que há de novo"
  - "SQL Server Reporting Services, o que há de novo"
  - "SSRS, o que há de novo"
ms.assetid: bc909063-6b84-4b3a-80d2-e93fc04b4b9d
caps.latest.revision: 206
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# Novidades do SQL Server Reporting Services (SSRS)
Saiba mais sobre as novidades do SQL Server [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Isso aborda as principais áreas de recurso e é atualizado à medida que novos itens são lançados.
  
  Para obter informações sobre as novidades em outras áreas do SQL Server, veja [Novidades no SQL Server vNext](../sql-server/what-s-new-in-sql-server-vnext.md) ou [Novidades no SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md).
  
 **Download** ![download](../analysis-services/media/download.png "download")
 
- Para fazer o download da Visualização Técnica de janeiro de 2017 dos relatórios do Power BI no SQL Server Reporting Services, junto com a versão de área de trabalho do Power BI (SQL Server Reporting Services), vá para o **[Centro de downloads da Microsoft](https://go.microsoft.com/fwlink/?linkid=839351)**.
  
-   Para baixar o [!INCLUDE[ssSQL15](../includes/sssql15-md.md)], acesse o  **[Centro de Avaliação](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**.  
  
-   Tem uma conta do Azure?  Então, acesse **[aqui](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016sp1enterprisewindowsserver2016/)** para executar uma máquina virtual com o [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] já instalado.  
  
 ![observação](../analysis-services/instances/install-windows/media/ssrs-fyi-note.png "observação") Para obter as notas de versão mais recentes, veja [Visualização Técnica dos relatórios do Power BI no SSRS - Notas de versão](../reporting-services/notas-de-versão-de-reporting-services.md) ou [Notas de versão do SQL Server 2016](../sql-server/sql-server-2016-release-notes.md).  

## <a name="whats-new-in-the-january-2017-technical-preview-of-power-bi-reports-in-sql-server-reporting-services"></a>Novidades da Visualização Técnica de janeiro de 2017 dos relatórios do Power BI no SQL Server Reporting Services

### <a name="reporting-services-has-a-new-setup-experience"></a>O Reporting Services tem uma nova experiência de instalação

Agora, o Reporting Services pode ser instalado fora da instalação do SQL Server. A experiência de instalação tem menos etapas e é mais leve. A instalação instalará os arquivos do Reporting Services. Em seguida, você pode configurar o banco de dados para seu servidor de relatório. Isso requer que você tenha acesso a um servidor de SQL Server Database Engine em seu ambiente.

![ssrs-standalone-setup1](../reporting-services/media/ssrs-standalone-setup1.png)

Para mais informações, veja [Instalar a Visualização Técnica de janeiro de 2017 dos relatórios do Power BI no SQL Server Reporting Services](Install%20the%20January%202017%20Technical%20Preview%20of%20Power%20BI%20reports%20in%20SQL%20Server%20Reporting%20Services.md).

### <a name="host-power-bi-reports-within-the-web-portal"></a>Relatórios do Power BI do host no portal da Web

Agora você pode carregar os arquivos do Power BI Desktop para Reporting Services e exibir relatórios diretamente no portal da Web.

![ssrs-powerbi-report-config-render](../reporting-services/media/ssrs-powerbi-report-config-render.png)

Você precisará baixar a versão do Power BI Desktop (SQL Server Reporting Services). Atualmente, a visualização só oferece suporte a relatórios criados nesta versão do Power BI Desktop. O Power BI Desktop (SQL Server Reporting Services) pode existir lado a lado com o Power BI Desktop para o serviço do Power BI. Para baixar o Power BI Desktop (SQL Server Reporting Services), vá para o Centro de download da Microsoft. 

No momento, você está limitado à criação de um relatório de Power BI em relação a conexões em tempo real ao Analysis Services (tabela ou multidimensional). Temos planos de adicionar suporte para outras fontes de dados e usar os recursos do Power Query em uma visualização futura.

Para saber mais, confira [Relatórios do Power BI no Reporting Services](../reporting-services/power-bi-reports-in-reporting-services.md).
 
## <a name="whats-new-in-sql-server-2016"></a>Novidades no SQL Server 2016
  
### <a name="reporting-services-includessrswebportal-non-markdowntokenssrswebportal-non-markdownmdmd"></a>Reporting Services [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)]  
 Um novo [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] está disponível. Esse é um portal atualizado e moderno, que incorpora KPIs, Relatórios Móveis, Relatórios Paginados e arquivos do Excel e Power BI Desktop. O [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] substitui o Gerenciador de Relatórios de versões anteriores. Você também pode baixar o Publicador de Relatórios Móveis e o Construtor de Relatórios do [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] sem precisar da tecnologia ClickOnce.
 
 Para criar Relatórios Móveis, você precisará do [!INCLUDE[SS_MobileReptPub_Short](../includes/ss-mobilereptpub-short-md.md)].  
  
 Para saber mais sobre o [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)], veja o [Portal da Web SSRS Modo Nativo](../reporting-services/web-portal-ssrs-native-mode.md).  
  
 ![ssRSPortal](../reporting-services/media/ssrsportal.png "ssRSPortal")  
 
 #### <a name="custom-branding-for-the-includessrswebportal-non-markdowntokenssrswebportal-non-markdownmdmd"></a>Identidade visual personalizada para o [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] 
  Você pode personalizar o [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] com o logotipo e cores da sua organização usando um pacote de identidade visual.  
  
  Para obter mais informações sobre identidade visual personalizada, consulte [Identidade visual do portal da Web](http://msdn.microsoft.com/pt-br/6dac97f7-02a6-4711-81a3-e850a6b40bf1)
 
 #### <a name="key-performance-indicators-kpi-in-the-includessrswebportal-non-markdowntokenssrswebportal-non-markdownmdmd"></a>KPI (indicadores chave de desempenho) [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] 

Você pode criar KPIs contextuais para a pasta em que você está diretamente no [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)]. Ao criar KPIs, você pode escolher campos de conjunto de dados e resumir esses valores. Você também pode selecionar o conteúdo relacionado a drill-through para obter mais detalhes.
  
 ![ssrs-webportal-kpi](../reporting-services/media/ssrs-webportal-kpi.png)
 
 Para obter mais informações, consulte [Trabalhando com KPIs no portal da Web](http://msdn.microsoft.com/pt-br/a28cf500-6d47-4268-a248-04837e7a09eb)
  
 
 ### <a name="mobile-reports"></a>Relatórios móveis
 
Os relatórios móveis do Reporting Services são relatórios dedicados e otimizado para uma ampla variedade de fatores forma que proporcionam uma melhor experiência para usuários que acessam relatórios em dispositivos móveis. Relatórios móveis apresentam uma variedade de visualizações, desde gráficos de tempo, de categoria e de comparação, mapas de árvores e personalizados. Conecte seus relatórios móveis a uma variedade de fontes de dados, incluindo dados multidimensionais e tabulares do SQL Server Analysis Services local. Disponha seus relatórios móveis em uma superfície de design com colunas e linhas de grade ajustáveis e elementos de relatório móvel flexíveis que se adaptam bem a qualquer tamanho de tela. Salve esses relatórios móveis em um servidor do Reporting Service para exibir e interagir com eles em um navegador ou no aplicativo móvel do Power BI em iPads, iPhones, smartphones Android e dispositivos Windows 10.
  
#### <a name="mobile-report-publisher"></a>Publicador de Relatórios Móveis  
 O [!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long-md.md)] permite a você criar e publicar relatórios móveis do SQL Server para seu [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)].  
  
 ![SS_MRP_LayoutTabSmall](../reporting-services/media/ss-mrp-layouttabsm.png "SS_MRP_LayoutTabSmall")  
  
 Para obter mais informações, consulte [Criar relatórios móveis com o Publicador de Relatórios Móveis do SQL Server](../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md).  
  
#### <a name="sql-server-mobile-reports-hosted-in-reporting-services-available-in-power-bi-mobile-app"></a>Relatórios móveis do SQL Server hospedados no Reporting Services disponíveis no aplicativo móvel do Power BI  
 O aplicativo móvel do Power BI para iOS no iPad e iPhone agora pode exibir relatórios móveis do SQL Server hospedados no seu servidor de relatório local.  
  
 ![SS_MRP_iPad_HomeSm](../reporting-services/media/ss-mrp-ipad-homesm.png "SS_MRP_iPad_HomeSm")  
  
 Você não pode se conectar, por padrão, sem algumas alterações de configuração. Para saber mais sobre como permitir que o aplicativo móvel do Power BI se conecte ao seu servidor de relatório, veja [Enable a report server for Power BI Mobile access](../reporting-services/report-server/enable-a-report-server-for-power-bi-mobile-access.md).
  
### <a name="support-of-sharepoint-mode-and-sharepoint-2016"></a>Modo de suporte ao SharePoint e SharePoint 2016.  
 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] dá suporte à integração com o SharePoint 2013 e o SharePoint 2016.
 
Para obter mais informações, consulte:  
  
-   [Combinações do SharePoint e do servidor e suplemento Reporting Services com suporte &#40;SQL Server 2016&#41;](../reporting-services/install-windows/supported combinations of sharepoint and reporting services server.md)  
  
-   [Onde encontrar o suplemento Reporting Services para produtos do SharePoint](../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)  
  
-   [Instalar o Reporting Services no modo do SharePoint](../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)  

### <a name="microsoft-net-framework-4-support"></a>Suporte ao Microsoft .NET Framework 4  
 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] dá suporte à versão atual do Microsoft .NET Framework 4. Isso inclui a versão 4.0 e 4.5.1. Se nenhuma versão do .Net Framework 4.x estiver instalada, a configuração do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instalará o .NET 4.0 durante a etapa de instalação do recurso.  

### <a name="report-improvements"></a>Aprimoramentos de relatórios

**Mecanismo de Renderização HTML 5:** Um novo mecanismo de renderização HTML5 que se destina ao modo de padrões "completo" da Web moderna e navegadores modernos.  O novo mecanismo de renderização não depende do modo quirks usado por alguns navegadores mais antigos.
  
 Para obter mais informações sobre o suporte ao navegador, veja [Suporte ao navegador para Reporting Services e Power View](../reporting-services/browser-support-for-reporting-services-and-power-view.md).  

**Relatórios paginados modernos:** desenvolva relatórios paginados modernos perfeitos com estilos novos e modernos para gráficos, medidores, mapas e outras visualizações de dados.
  
**Gráficos de Mapa de Árvore e Explosão Solar:** Aprimore seus relatórios com os gráficos de Mapa de Árvore ![ssrs_treemap_icon](../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon") e Explosão Solar ![ssrs_sunburst_icon](../reporting-services/media/ssrs-sunburst-icon.png "ssrs_sunburst_icon"), excelentes maneiras de exibir dados hierárquicos. Para saber mais, confira [Tree Map and Sunburst Charts in Reporting Services](../reporting-services/report-design/tree-map-and-sunburst-charts-in-reporting-services.md).  

**Inserção de relatório:** agora você pode incorporar relatórios móveis e paginados a outras páginas da Web e aplicativos usando um iframe juntamente com os parâmetros da URL.  

**Fixar itens de relatórios a um Painel do Power BI:** Ao exibir um relatório no [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)], você pode selecionar itens de relatório e fixá-los a um painel do [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)].   Os itens que você pode fixar são gráficos, painéis de medidores, mapas e imagens. Você pode selecionar **(1)** o grupo que contém o painel que você quer fixar, **(2)** selecionar o painel no qual você quer fixar o item e **(3)** selecionar a frequência com que você quer que o bloco seja atualizado no painel.   ![observação](../analysis-services/instances/install-windows/media/ssrs-fyi-note.png "observação") A atualização é gerenciada pelas assinaturas do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e, depois que o item é fixado, você poderá editar a assinatura e configurar outro agendamento de atualização.  
  
 ![ssRS_Pin_to_PowerBI](../reporting-services/media/ssrs-pin-to-powerbi.png) 
  
 Para obter mais informações, consulte [Integração do Servidor de Relatório do Power BI &#40;Configuration Manager&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md) e [Fixar itens do Reporting Services nos painéis do Power BI](../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md).  
 
 **Renderização e exportação do PowerPoint:** o formato Microsoft PowerPoint (PPTX) é uma nova extensão de renderização do [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]. Você pode exportar relatórios no formato PPTX de aplicativos comuns; Construtor de Relatórios, Designer de Relatórios (no SSDT) e o [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]. Por exemplo, a imagem a seguir mostra o menu de exportação do [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]. 
  
 ![ssrs-export-powerpoint](../reporting-services/media/ssrs-export-powerpoint.png) 
  
 Você também pode selecionar o formato PPTX para saída de assinatura e usar o acesso à URL do Servidor de Relatório para renderizar e exportar um relatório. Por exemplo, o seguinte comando de URL no seu navegador exporta um relatório de uma instância nomeada do servidor de relatório.  
  
```  
http://servername/ReportServer_THESQLINSTANCE/Pages/ReportViewer.aspx?%2freportfolder%2freport+name+with+spaces&rs:Format=pptx  
```  
  
 Para saber mais, confira [Export a Report Using URL Access](../reporting-services/export-a-report-using-url-access.md).  
 
 **PDF substitui o ActiveX para Impressão Remota:** A experiência de impressão do ActiveX da barra de ferramentas do visualizador de relatórios foi substituída por uma experiência moderna baseada em PDF que funciona na matriz dos navegadores com suporte, incluindo o Microsoft Edge. Não é mais necessário baixar os controles do ActiveX! Dependendo do navegador que você usa e dos aplicativos e serviços de visualização de PDF que você tenha instalados, o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] abrirá um diálogo de impressão para imprimir o seu relatório ou solicitará que você baixe um arquivo .PDF do seu relatório.  Como administrador, você ainda pode desabilitar impressão do lado do cliente do [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]. Para obter mais informações, consulte [Habilitar e desabilitar a impressão do lado do cliente para Reporting Services](../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md).

![ssrs-pdf-printing](../reporting-services/media/ssrs-pdf-printing.png)

### <a name="subscription-improvements"></a>Aprimoramentos de Assinatura  
 
|Recurso|Modo de servidor com suporte|  
|-------------|---------------------------|  
|**Habilitar e desabilitar assinaturas**. Novas opções de interface de usuário para desabilitar e habilitar rapidamente as assinaturas. As assinaturas desabilitadas mantêm suas outras propriedades de configuração, como o cronograma, e podem ser facilmente habilitadas.<br /><br /> ![ssrs-enable-disable-subscriptions](../reporting-services/media/ssrs-enable-disable-subscriptions.png)<br /><br /> Para saber mais, confira [Disable or Pause Report and Subscription Processing](../reporting-services/subscriptions/disable-or-pause-report-and-subscription-processing.md).|Modo nativo|  
|**Descrição da assinatura**. Quando você cria uma nova assinatura, você pode incluir uma descrição do relatório como parte das propriedades de assinatura. A descrição será incluída na página de resumo da assinatura.|Modo do SharePoint e Nativo|  
|**Alterar o proprietário da assinatura**. Interface de usuário aprimorada para alterar rapidamente o proprietário de uma assinatura. As versões anteriores do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] permitem que os administradores alterem os proprietários de assinatura usando o script. A partir da versão [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] , você pode alterar os proprietários da assinatura usando a interface do usuário ou o script. Alterar o proprietário da assinatura é uma tarefa administrativa comum quando os usuários deixam ou alteraram funções em sua organização.|Modo do SharePoint e Nativo|  
|**Credenciais compartilhadas para assinaturas de compartilhamento de arquivos**. Agora existem dois fluxos de trabalho com as assinaturas de compartimento de arquivos do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] :<br /><br /> Novidades desta versão, o administrador do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] pode configurar uma conta única de compartilhamento de arquivo, que é usada para várias assinaturas. A conta de compartilhamento de arquivo é configurada no gerenciador de configuração do modo nativo do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] **Especificar uma conta de compartilhamento de arquivo**e, em seguida, na página de configuração da assinatura, os usuários selecionam **Usar uma conta de compartilhamento de arquivo**.<br /><br /> Configure assinaturas individuais com credenciais específicas para o compartilhamento de arquivos de destino.<br /><br /> Você também pode combinar as duas abordagens e fazer com que algumas assinaturas de compartilhamento de arquivos usem a conta de compartilhamento de arquivos central, enquanto outras assinaturas usam credenciais específicas.|Modo nativo|  

### <a name="sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT)  
 A nova versão do SSDT inclui os modelos de projeto para o [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]: Assistente de Projeto do Servidor de Relatório e Projeto do Servidor de Relatório. Para saber mais sobre como baixar o SSDT, veja [Ferramentas de Dados do SQL Server para Visual Studio 2015](http://go.microsoft.com/fwlink/?LinkId=827542).  

### <a name="report-builder-improvements"></a>Aprimoramentos do Construtor de Relatórios

**Nova interface de usuário do Construtor de Relatórios:** a principal interface de usuário do [!INCLUDE[ssRBnoversion](../includes/ssrbnoversion-md.md)] agora tem uma aparência moderna com elementos de interface do usuário simplificados.  
  
|||  
|-|-|  
|Nova|Previous|  
|![ssrs_rbfacelift_new](../reporting-services/media/ssrs-rbfacelift-new.png "ssrs_rbfacelift_new")|![ssrs_rbfacelift_old](../reporting-services/media/ssrs-rbfacelift-old.png "ssrs_rbfacelift_old")|  

**Painel de parâmetros personalizado:** agora você pode personalizar o painel de parâmetros. Usando a superfície de design no Construtor de Relatórios, você pode arrastar um parâmetro para uma coluna e linha específica no painel de parâmetros. Você pode adicionar e remover colunas para alterar o layout do painel.   Para obter mais informações, consulte [Personalizar o painel de parâmetros em um relatório &#40;Construtor de Relatórios&#41;](../reporting-services/report-design/customize-the-parameters-pane-in-a-report-report-builder.md).  
  
 ![Parameter list in Report Data pane and in parameters pane](../reporting-services/media/ssrs-customizeparameter-parameterlist-reportdatapane.png "Parameter list in Report Data pane and in parameters pane")  

  
**Suporte a alto DPI:** o [!INCLUDE[ssRBnoversion](../includes/ssrbnoversion-md.md)] para [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] dá suporte a dispositivos e dimensionamento de Alto DPI (Pontos por Polegada).  Para saber mais sobre Alto DPI, veja o seguinte:  
  
-   [Aprimoramentos de dimensionamento de DPI do Windows 8.1](https://blogs.windows.com/windowsexperience/2013/07/15/windows-8-1-dpi-scaling-enhancements/)  
  
-   [Alto DPI e Windows 8.1](http://technet.microsoft.com/library/dn528848.aspx)  
  
## <a name="see-also"></a>Consulte também  
 [Novidades do Analysis Services](http://msdn.microsoft.com/pt-br/aa69c299-b8f4-4969-86d8-b3292fe13f08)  
 [Visualização Técnica dos relatórios do Power BI no SSRS - Notas de versão](../reporting-services/notas-de-versão-de-reporting-services.md)  
 [Notas de Versão do SQL Server 2016.](../sql-server/sql-server-2016-release-notes.md)   
 [Compatibilidade com versões anteriores](http://msdn.microsoft.com/pt-br/675b0e0e-cfee-4790-9675-80fc3ea6d30f)   
 [Recursos do Reporting Services com suporte nas edições do SQL Server 2016](http://msdn.microsoft.com/pt-br/39f03d2d-6e48-4b34-a9d3-07f86313b937)   
 [Atualizar e migrar o Reporting Services](../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
 [Reporting Services &#40;SSRS&#41;](../reporting-services/reporting-services-ssrs.md)  
  
  