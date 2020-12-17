---
title: O que é o SQL Server Reporting Services? | Microsoft Docs
description: Saiba mais sobre as ferramentas e os serviços para relatórios móveis e paginados do Reporting Services no local.
ms.date: 05/06/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services]
- SSRS
- reports [Reporting Services], about reports
- Reporting Services
- SQL Server Reporting Services
ms.assetid: b8d18d3d-9db0-43e7-8286-7b46cc3a37ed
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b6c33eaeda2a7600039b80c49e1ba3c0fa9e36b5
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97439361"
---
# <a name="what-is-sql-server-reporting-services-ssrs"></a>O que é o SQL Server Reporting Services (SSRS)?

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../includes/ssrs-appliesto-not-pbirs.md)]

Procurando o Servidor de Relatórios do Power BI? Consulte [O que é o Servidor de Relatórios do Power BI?](https://docs.microsoft.com/power-bi/report-server/get-started).

O SSRS (SQL Server Reporting Services) fornece um conjunto de ferramentas e serviços locais para criar, implantar e gerenciar relatórios paginados e móveis.

![SQL Server Reporting Services reunido](../reporting-services/media/ss-reporting-services-all-together.png "SQL Server Reporting Services reunido")

## <a name="create-deploy-and-manage-mobile-and-paginated-reports"></a>Criar, implantar e gerenciar relatórios móveis e paginados

A solução SSRS oferece de forma flexível as informações adequadas aos usuários certos. Os usuários podem consumir os relatórios por meio de um navegador da web, em seu dispositivo móvel, ou por email.

O SQL Server Reporting Services oferece um pacote atualizado de produtos:

* **Relatórios paginados "Tradicionais"** atualizados, de forma que você possa criar relatórios de aparência moderna, com ferramentas atualizadas e novos recursos para criá-los.
* **Novos relatórios móveis** com um layout dinâmico que se adapta a diferentes dispositivos e as diferentes maneiras que você os segura.
* **Um portal da Web moderno** que você pode exibir em qualquer navegador moderno. No novo portal, organize e exiba relatórios e KPIs móveis e paginados do Reporting Services. Também armazene pastas de trabalho do Excel no portal.

Continue lendo para obter mais informações sobre cada produto.

### <a name="whats-new-in-reporting-services"></a>Novidades no Reporting Services

Essas fontes serão mantidas atualizadas com os novos recursos no SQL Server Reporting Services.

* [Novidades no Reporting Services](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)
* [Blog da equipe do SQL Server Reporting Services](https://blogs.msdn.microsoft.com/sqlrsteamblog/)
* O [canal do YouTube Guy in a Cube](https://www.youtube.com/channel/UCFp1vaKzpfvoGai0vE5VJ0w)

## <a name="paginated-reports"></a>Relatórios paginados

![Imagem de relatórios paginados em uma tela de desktop e em um tablet.](../reporting-services/media/ssrs-paginated-reports.png)

O Reporting Services está associado a relatórios paginados "tradicionais", ideais para documentos de layout fixo otimizados para impressão, como arquivos PDF e Word.

Essa carga de trabalho principal de BI ainda existe hoje, por isso, nós a modernizamos. Agora você pode criar relatórios de aparência moderna com novos recursos atualizados ao usar o Construtor de Relatórios ou o Designer de Relatórios no [SSDT (SQL Server Data Tools)](../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md).

* Atualizamos todos os estilos padrão e paletas de cores, portanto, por padrão você cria relatórios com um novo estilo moderno minimalista.
* Atualizamos o painel Parâmetro, portanto você pode organizar os parâmetros da maneira que desejar.
* Você pode exportar para novos formatos, como o PowerPoint. As visualizações do Reporting Services no PowerPoint são dinâmicas e editáveis e não apenas capturas de tela.
* Você pode criar uma experiência híbrida do Power BI/Reporting Services: em vez de recriar seus relatórios do Reporting Services localmente no Power BI, você pode fixar visuais desses relatórios nos painéis do Power BI. E então, você pode monitorar tudo em um único lugar no seu painel do Power BI.

## <a name="mobile-reports"></a>Relatórios móveis

![Imagem dos relatórios móveis em uma tela de desktop e em um tablet.](../reporting-services/media/ssrs-mobile-reports.png)

A computação em dispositivos móveis mudou os dispositivos que precisamos para trabalhar. Isso significa que as pessoas têm hoje uma necessidade de relatórios diferentes. A experiência de relatório de layout fixo não funciona bem quando se trata de tablets e celulares. Algo que foi criado para uma tela ampla de um computador não oferece a melhor experiência em uma tela pequena de um celular, que não é apenas menor, mas tem uma orientação de retrato ou paisagem.

O que você precisa para esses fatores de formas de tela muito diferentes é um layout responsivo que se adapte a esses diferentes tamanhos e orientações de tela. Para isso, adicionamos um novo tipo de relatório: relatórios móveis, baseados na tecnologia Datazen que adquirimos há cerca de um ano e integramos ao produto. Você pode migrar seus relatórios Datazen existentes para o Reporting Services com o [Assistente de Migração do SQL Server para Datazen](https://www.microsoft.com/download/details.aspx?id=53128).

Você cria esses relatórios móveis no novo aplicativo [Publicador de Relatórios Móveis](../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md) . Em seguida, nos [aplicativos nativos do Power BI para dispositivos móveis](https://powerbi.microsoft.com/documentation/powerbi-power-bi-apps-for-mobile-devices/) para Windows 10, iOS, Android e HTML5, é possível acessar os dados que você tem no Power BI, na nuvem ou no SSRS.

Conforme você cria visualizações, o Publicador de Relatórios Móveis gera automaticamente os dados de amostra. Esse recurso permite que você veja qual será a aparência da visualização com seus dados e quais tipos de dados funcionam bem em cada visualização.

## <a name="web-portal"></a>Portal da Web

![Imagem do portal da Web no laptop.](../reporting-services/media/ssrs-web-portal.png)

Para os usuários finais do Reporting Services de modo nativo, a porta da frente é um portal da Web moderno que pode ser exibido na maioria dos navegadores. Acesse todos os KPIs e relatórios móveis e paginados do Reporting Services no novo portal. Os KPIs podem expor as principais métricas de negócios em um relance no navegador, sem precisar abrir um relatório.

O novo portal da Web é uma reformulação completa do Gerenciador de Relatórios. Agora é um aplicativo de página única com base em padrões HTML5, para os quais os navegadores modernos estão otimizados: Microsoft Edge, Internet Explorer 10 e 11, Chrome, Firefox, Safari e todos os principais navegadores.

O conteúdo no portal da Web é organizado por tipo:

* relatórios paginados
* relatórios móveis 
* KPIs
* pastas de trabalho do Excel
* conjuntos de dados compartilhados
* fontes de dados compartilhadas

Armazene-os e gerencie-os com segurança no portal, na tradicional hierarquia de pastas. Marque seus relatórios favoritos para acesso rápido. Pessoas com permissões apropriadas também podem gerenciar e administrar o conteúdo do SSRS.

E você ainda pode agendar processamento de relatórios, acessar relatórios sob demanda e assinar relatórios publicados no novo portal da Web.

Mais sobre o [portal da Web](../reporting-services/web-portal-ssrs-native-mode.md).

::: moniker range="=sql-server-2016"

## <a name="reporting-services-in-sharepoint-integrated-mode"></a>Reporting Services no modo integrado do SharePoint

Você publica relatórios no Reporting Services no modo integrado do SharePoint. Você pode agendar o processamento de relatórios, acessar relatórios sob demanda, assinar relatórios publicados e exportar relatórios para outros aplicativos como o Microsoft Excel. Crie alertas de dados em relatórios publicados em um site do SharePoint e receba mensagens de email quando os dados do relatório forem alterados.  

Mais sobre o [Servidor de Relatórios do Reporting Services no modo integrado do SharePoint](../reporting-services/report-server-sharepoint/reporting-services-report-server-sharepoint-mode.md).

::: moniker-end

## <a name="ssrsnoversion-programming-features"></a>Recursos de programação do[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]

Aproveite os recursos de programação do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] que permitem estender e personalizar a funcionalidade de execução de relatórios. Use as APIs do SSRS para integrar ou estender dados e para o processamento de relatórios em aplicativos personalizados.

Mais sobre a [Documentação do Desenvolvedor do Reporting Services](../reporting-services/reporting-services-developer-documentation.md).

## <a name="next-steps"></a>Próximas etapas

* [Instalar o Reporting Services](../reporting-services/install-windows/install-reporting-services.md)
* [Baixar o SQL Server Data Tools (SSDT)](https://go.microsoft.com/fwlink/?LinkID=616714)
* [Instalar o Construtor de Relatórios](../reporting-services/install-windows/install-report-builder.md)

* Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
