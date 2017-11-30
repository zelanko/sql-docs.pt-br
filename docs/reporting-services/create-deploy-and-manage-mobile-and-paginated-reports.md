---
title: Reporting Services (SSRS) | Microsoft Docs
description: "Saiba mais sobre as ferramentas e os serviços para relatórios móveis e paginados do Reporting Services e relatórios do Power BI localmente."
ms.custom: 
ms.date: 07/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- reports [Reporting Services]
- SSRS
- reports [Reporting Services], about reports
- Reporting Services
- SQL Server Reporting Services
ms.assetid: b8d18d3d-9db0-43e7-8286-7b46cc3a37ed
caps.latest.revision: "70"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Active
ms.openlocfilehash: 94d3e2266c6539cc75b0ac5a51c47f6b6c20b0b3
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="what-is-sql-server-reporting-services-ssrs"></a>O que é o SQL Server Reporting Services (SSRS)?

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../includes/ssrs-previous-versions.md)]

Criar, implantar e gerenciar relatórios móveis e paginados do Reporting Services e relatórios do Power BI localmente com a variedade de ferramentas e serviços prontos para uso fornecidos pelo SSRS (SQL Server Reporting Services) e Power BI.

![SQL Server Reporting Services reunidos](../reporting-services/media/ss-reporting-services-all-together.png "SQL Server Reporting Services reunidos")

## <a name="create-deploy-and-manage-mobile-and-paginated-reports"></a>Criar, implantar e gerenciar relatórios móveis e paginados

O SQL Server Reporting Services é uma solução que os clientes implantam em seus locais para criar, publicar e gerenciar relatórios e entregá-los aos usuários corretos de diferentes maneiras: exibindo-os em um navegador da Web, em seus dispositivos móveis ou como um email em suas caixas de entrada.

Para o SQL Server 2016, o Reporting Services oferece um pacote atualizado de produtos:

* **Relatórios paginados "Tradicionais"** atualizados, de forma que você possa criar relatórios de aparência moderna, com ferramentas atualizadas e novos recursos para criá-los.
* **Novos relatórios móveis** com um layout dinâmico que se adapta a diferentes dispositivos e as diferentes maneiras que você os segura.
* **Um portal da Web moderno** que você pode exibir em qualquer navegador moderno. No novo portal, organize e exiba KPIs e relatórios móveis e paginados do Reporting Services, além de relatórios do Power BI Desktop. Também armazene pastas de trabalho do Excel no portal.

Continue lendo para obter mais informações sobre cada produto.

> [!NOTE]
> Procurando o Servidor de Relatórios do Power BI? Consulte [Introdução ao Servidor de Relatórios do Power BI](https://powerbi.microsoft.com/documentation/reportserver-get-started/).

### <a name="whats-new-in-reporting-services"></a>Novidades no Reporting Services

Essas fontes serão mantidas atualizadas com os novos recursos no SQL Server 2016 Reporting Services.

* [Novidades no Reporting Services](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)
* [Blog da equipe do SQL Server Reporting Services](https://blogs.msdn.microsoft.com/sqlrsteamblog/)
* O [canal do YouTube Guy in a Cube](https://www.youtube.com/channel/UCFp1vaKzpfvoGai0vE5VJ0w)

## <a name="paginated-reports"></a>Relatórios paginados

![ssrs-paginated-reports](../reporting-services/media/ssrs-paginated-reports.png)

O Reporting Services está associado com os "tradicionais" relatórios paginados com estilo de documento, nos quais quanto mais dados você tiver, mais linhas haverá nas tabelas e mais páginas haveria no relatório. Isso é ótimo para geração de documentos de layout fixo, de resolução perfeita, otimizado para impressão, como os arquivos PDF e Word.

Essa carga de trabalho principal de BI ainda existe hoje, por isso nós a modernizamos. Agora você pode criar relatórios de aparência moderna com novos recursos atualizados, usando o [Construtor de Relatórios](../reporting-services/report-builder/report-builder-in-sql-server-2016.md) ou o Designer de Relatórios no [SSDT (SQL Server Data Tools)](../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md).

* Atualizamos todos os estilos padrão e paletas de cores, portanto, por padrão você cria relatórios com um novo estilo moderno minimalista.
* Atualizamos o painel Parâmetro, portanto você pode organizar os parâmetros da maneira que desejar.
* Você pode exportar para novos formatos, como o PowerPoint. As visualizações do Reporting Services no PowerPoint são dinâmicas e editáveis e não apenas capturas de tela.
* Você pode criar uma experiência híbrida do Power BI/Reporting Services: em vez de recriar seus relatórios do Reporting Services localmente no Power BI, você pode fixar visuais desses relatórios nos painéis do Power BI. E então, você pode monitorar tudo em um único lugar no seu painel do Power BI.

## <a name="mobile-reports"></a>Relatórios móveis

![ssrs-mobile-reports](../reporting-services/media/ssrs-mobile-reports.png)

A computação em dispositivos móveis mudou os dispositivos que precisamos para trabalhar. Isso significa que as pessoas têm hoje uma necessidade de relatórios diferentes. A experiência de relatório de layout fixo não funciona bem quando você introduz tablets e telefones. Algo que foi criado para uma tela ampla de um computador não é a melhor experiência em uma tela pequena de um telefone, que não é apenas menor, mas tem uma orientação de retrato ou paisagem.

O que você precisa para esses fatores de formas de tela muito diferentes não é um layout fixo, mas um layout dinâmico que se adapta a esses dispositivos diferentes e as diferentes maneiras de que você pode segurá-los. Para isso, adicionamos um novo tipo de relatório: relatórios móveis, baseados na tecnologia Datazen que adquirimos há cerca de um ano e integramos ao produto. Você pode migrar seus relatórios Datazen existentes para o Reporting Services com o [Assistente de Migração do SQL Server para Datazen](https://www.microsoft.com/download/details.aspx?id=53128). 

Você cria esses relatórios móveis no novo aplicativo [Publicador de Relatórios Móveis](../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md) . Em seguida nos [aplicativos nativos do Power BI para dispositivos móveis](https://powerbi.microsoft.com/documentation/powerbi-power-bi-apps-for-mobile-devices/) para Windows 10, iOS, Android e HTML5, você pode acessar os dados que tem no Power BI na nuvem, bem como seus dados do SQL Server 2016 Reporting Services local. Conforme cria visualizações, o Publicador de Relatórios Móveis gera automaticamente dados de exemplo para cada uma delas, assim você vê qual será a aparência da visualização com os seus dados e que tipo de dados funciona bem em cada visualização.

## <a name="web-portal"></a>Portal da Web

![ssrs-web-portal](../reporting-services/media/ssrs-web-portal.png)

Para os usuários finais do Reporting Services de modo nativo, a porta da frente é um portal da Web moderno que você pode exibir em qualquer navegador moderno. Acesse todos os KPIs e relatórios móveis e paginados do Reporting Services no novo portal, além dos relatórios do Power BI Desktop. Leia mais sobre os [relatórios do Power BI no Reporting Services](../reporting-services/power-bi-reports-in-reporting-services.md).  

Você pode aplicar sua própria marca personalizada ao portal da web. E você pode criar KPIs direitamente no portal da Web. Os KPIs podem expor as principais métricas de negócios em um relance no navegador, sem precisar abrir um relatório. 

O novo portal da Web é uma reformulação completa do Gerenciador de Relatórios. Agora é um aplicativo de página única, com base em padrões HTML5, para os quais os navegadores modernos são otimizados: Edge, Internet Explorer 10 e 11, Chrome, Firefox, Safari e todos os principais navegadores.

O conteúdo do portal da Web é organizado por tipo: KPIs, relatórios móveis e paginados do Reporting Services, além de relatórios do Power BI Desktop, pastas de trabalho do Excel, conjuntos de dados compartilhados e fontes de dados compartilhadas para usar como blocos de construção em seus relatórios. Armazene-os e gerencie-os com segurança no portal, na tradicional hierarquia de pastas. Você pode rotular os seus favoritos e pode gerenciar o conteúdo, se você tiver essa função.

E você ainda pode agendar processamento de relatórios, acessar relatórios sob demanda e assinar relatórios publicados no novo portal da Web.

Saiba mais sobre o [portal da Web (modo nativo do SSRS)](../reporting-services/web-portal-ssrs-native-mode.md).

## <a name="reporting-services-in-sharepoint-integrated-mode"></a>Reporting Services no modo integrado do SharePoint

Você publica relatórios no Reporting Services no modo integrado do SharePoint. Você pode agendar o processamento de relatórios, acessar relatórios sob demanda, assinar relatórios publicados e exportar relatórios para outros aplicativos como o Microsoft Excel. Crie alertas de dados em relatórios publicados em um site do SharePoint e receba mensagens de email quando os dados do relatório forem alterados.  

Mais sobre o [Servidor de Relatórios do Reporting Services no modo integrado do SharePoint](../reporting-services/report-server-sharepoint/reporting-services-report-server-sharepoint-mode.md).

## <a name="includessrsnoversionincludesssrsnoversion-mdmd-programming-features"></a>Recursos de programação do[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 

Aproveite os recursos de programação do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para ampliar e personalizar sua funcionalidade de geração de relatórios, com APIs para integrar ou ampliar dados e processar relatórios em aplicativos personalizados.

Mais sobre a [Documentação do Desenvolvedor do Reporting Services](../reporting-services/reporting-services-developer-documentation.md). 

## <a name="next-steps"></a>Próximas etapas

* [Instalar o Reporting Services](../reporting-services/install-windows/install-reporting-services.md)  
* [Instalar o Construtor de Relatórios](../reporting-services/install-windows/install-report-builder.md)   
* [Baixar o SQL Server Data Tools (SSDT)](http://go.microsoft.com/fwlink/?LinkID=616714)  
* [Relatórios do Power BI no Reporting Services](../reporting-services/power-bi-reports-in-reporting-services.md)

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
