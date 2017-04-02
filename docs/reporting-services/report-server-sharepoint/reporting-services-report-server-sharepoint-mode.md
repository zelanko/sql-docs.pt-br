---
title: "Reporting Services Report Server (SharePoint Mode) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 10778ec9-5fe4-4b4e-89b0-ade1f06b781d
caps.latest.revision: 17
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 17
---
# Reporting Services Report Server (SharePoint Mode)
  Um servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] configurado para o **Modo do SharePoint** pode ser executado em uma implantação de um produto do SharePoint. Um servidor de relatório no modo do SharePoint pode usar os recursos de colaboração e gerenciamento do SharePoint para relatórios e outros tipos de conteúdo do [!INCLUDE[ssRSnfoversion_md](../../includes/ssrsnoversion-md.md)] . O modo do SharePoint requer a instalação da versão apropriada do suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para produtos do SharePoint nos seus Front Ends Web do SharePoint.  
  
 Para obter mais informações sobre como instalar e configurar, consulte o seguinte:  
  
-   [Instalar o Reporting Services no Modo do SharePoint para SharePoint 2010](http://msdn.microsoft.com/pt-br/47efa72e-1735-4387-8485-f8994fb08c8c).  
  
-   [Adicionar um servidor de relatório a um farm &#40;Expansão do SSRS&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md).  
  
 Para obter informações sobre as novidades nesta versão, consulte a seção “SharePoint” em [Novidades no Reporting Services &#40;SSRS&#41;](../Topic/What's%20New%20in%20Reporting%20Services%20\(SSRS\).md).  
  
 Neste tópico:  
  
-   [Resumo de recursos](#bkmk_featuresum)  
  
-   [Modo conectado e modo local](#bkmk_connectedandlocal)  
  
-   [Recursos do SharePoint sem suporte](#bkmk_unsupportedsharepoint)  
  
-   [Combinações compatíveis do suplemento do SharePoint e servidor de relatório](#bkmk_supportedcombinations)  
  
-   [Componentes que fornecem integração](#bkmk_components)  
  
-   [Considerações sobre idioma](#bkmk_language)  
  
-   [Tarefas relacionadas](#bkmk_relatedtasks)  
  
##  <a name="bkmk_featuresum"></a> Resumo de recursos  
 Configurar um servidor de relatório para ser executado no modo integrado do SharePoint fornece as seguintes funcionalidades adicionais disponíveis somente ao implantar um servidor de relatório nesse modo:  
  
-   Use os recursos de gerenciamento de documentos e colaboração do SharePoint, incluindo alertas. Um site de SharePoint fornece um portal unificado para acessar e gerenciar todos os itens de relatório em um único lugar.  
  
-   Use as permissões e os provedores de autenticação do SharePoint para controlar o acesso a relatórios, modelos e outros itens.  
  
-   Use as topologias de implantação do SharePoint para distribuir relatórios em uma conexão com a Internet fora do firewall. Um servidor de relatório fornece serviços de processamento de relatório e dados no contexto de uma implantação maior do SharePoint configurada para acesso à Internet.  
  
-   Gerencie relatórios, modelos, fontes de dados, agendas e histórico de relatório em páginas de aplicativo personalizadas de um site do SharePoint. Você pode definir propriedades, definir agendas e assinaturas, e criar e gerenciar o histórico de relatório em um site do SharePoint da mesma maneira que os cria e gerencia com outras ferramentas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Publique ou atualize relatórios, modelos de relatórios, recursos e arquivos de fonte de dados compartilhados em uma biblioteca do SharePoint, incluindo a Central de Relatórios no Office SharePoint Server.  
  
     Use o Designer de Relatórios, o Designer de Modelos e o Construtor de Relatórios para criar relatórios e fontes de dados a serem publicados diretamente em uma biblioteca do SharePoint. Você também pode usar a ação Carregar em um site do SharePoint para adicionar qualquer definição e modelos de relatório a uma biblioteca do SharePoint.  
  
     Como o servidor de relatório processa as definições de relatório da mesma maneira, independentemente do modo do servidor usado, os dados e o layout de relatório não são afetados pelo modo do servidor. Qualquer relatório executado em um servidor de relatório no modo nativo poderá ser executado em um servidor de relatório configurado para o modo integrado do SharePoint.  
  
-   Assine e entregue relatórios em uma biblioteca do SharePoint usando uma nova extensão de entrega do SharePoint. Também é possível entregar relatórios por email ou para uma pasta compartilhada. As extensões de entrega de servidor de relatório são usadas para entregar relatórios. Você pode criar assinaturas controladas por dados para uma distribuição de relatório em larga escala usando dados de assinante consultados em tempo de execução.  
  
-   Uma Web Part Visualizador de Relatórios que você pode adicionar a páginas do SharePoint para exibir um relatório dentro seu aplicativo Web do SharePoint. A Web Part inclui navegação de página, pesquisa, impressão e recursos de exportação.  
  
-   Programe em um novo ponto de extremidade SOAP para criar aplicativos personalizados que se integrem a um site do SharePoint. Também é possível usar o provedor WMI (Instrumentação de Gerenciamento do Windows) para configurar programaticamente uma instância do servidor de relatório que seja executada no modo integrado do SharePoint.  
  
-   Serviços do Microsoft Access reportados no modo conectado.  
  
-   As zonas AAM, as implantações voltadas para Internet e os tokens de usuário do SharePoint para listas do SharePoint.  
  
##  <a name="bkmk_connectedandlocal"></a> Modo conectado e modo local  
 A versão do SQL Server 2008 R2 introduziu um novo *modo local* para exibição de relatórios de um servidor do SharePoint 2010 com o Suplemento Reporting Services do Microsoft SQL Server 2008 R2 ou posterior para os produtos SharePoint 2010 instalados.  
  
-   *Modo local*: este modo permite que os relatórios sejam renderizados localmente a partir da biblioteca de documentos do SharePoint, sem integração com um servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . O suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para produtos do SharePoint é necessário, mas um servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não é. O suplemento pode ser instalado de várias maneiras diferentes, incluindo a ferramenta de preparação de produtos do SharePoint 2010. Para obter mais informações sobre o modo local, consulte [Relatórios em modo Local versus em modo Conectado no Visualizador de Relatórios &#40;Reporting Services no Modo do SharePoint&#41;](../../reporting-services/report-server-sharepoint/local mode vs. connected mode reports in the report viewer.md) e [Onde encontrar o suplemento Reporting Services para produtos SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).  
  
-   *Modo conectado*: este modo tem suporte com a integração de um servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no farm do SharePoint usando a Administração Central do SharePoint. A integração com um servidor de relatório permite relatórios completos de ponta a ponta, fornecendo os recursos de colaboração do SharePoint 2010 e os recursos baseados no servidor de um servidor de relatório, inclusive: Assinaturas, Instantâneos e processamento baseado no servidor.  
  
##  <a name="bkmk_unsupportedsharepoint"></a> Recursos do SharePoint sem suporte  
 Nem todos os recursos do SharePoint estão disponíveis para operações integradas. A lista a seguir apresenta os recursos do SharePoint com os quais o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não integra diretamente:  
  
-   Serviço de Repositório Seguro.  
  
-   Não é possível usar a integração de Calendário do SharePoint Outlook ou o agendamento do SharePoint para arquivos do Reporting Services em uma biblioteca de documentos.  
  
-   Catálogo de dados comerciais do SharePoint.  
  
-   A personalização do SharePoint também não é compatível nas páginas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Não há suporte para integração do Servidor de Relatório quando o aplicativo Web do SharePoint é habilitado para acesso Anônimo.  
  
-   SQL Server Reporting Services **não** dão suporte a controle de versão de biblioteca de documentos do SharePoint. Se você salvar itens de relatório em uma biblioteca de documentos que está configurada com “Histórico de Versão de Documento” habilitado, os recursos do Reporting Services não funcionarão corretamente e gerarão erros no log do ULS. Este é um exemplo de um erro no log do ULS:  
  
    -   “…uma fonte de dados associada ao relatório foi desabilitada”.  
  
     O histórico de versão da biblioteca de documento está configurada na página ”Configurações de versão” de “Configurações da biblioteca”.  
  
##  <a name="bkmk_supportedcombinations"></a> Combinações compatíveis do suplemento do SharePoint e servidor de relatório  
 Nem todos os recursos são compatíveis em todas as combinações de servidor de relatório, suplemento Reporting Services para SharePoint e produtos do SharePoint. Para obter mais informações, consulte [Combinações do SharePoint e do servidor e suplemento Reporting Services com suporte &#40;SQL Server 2016&#41;](../../reporting-services/install-windows/supported combinations of sharepoint and reporting services server.md)  
  
> [!NOTE]  
>  A versão correta do suplemento do Reporting Services deve ser usada com a versão correspondente dos produtos SharePoint.  
  
##  <a name="bkmk_components"></a> Componentes que fornecem integração  
 Para combinar os servidores em uma única implantação, você integra uma instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a uma instância dos produtos SharePoint  
  
 A integração é fornecida pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e pelo Suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para produtos SharePoint. O Suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é um componente de distribuição livre que é possível baixar e, em seguida, instalar em um servidor no qual a versão apropriada do SharePoint está em execução.  
  
> [!TIP]  
>  Nem todos os recursos são compatíveis em todas as combinações de servidor de relatório, suplemento Reporting Services para SharePoint e produtos do SharePoint. Para obter mais informações, consulte [Combinações do SharePoint e do servidor e suplemento Reporting Services com suporte &#40;SQL Server 2016&#41;](../../reporting-services/install-windows/supported combinations of sharepoint and reporting services server.md).  
  
-   No SharePoint, o Suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece o ponto de extremidade de proxy do ReportServer, uma Web part do Visualizador de Relatórios e páginas de aplicativos para que seja possível exibir, armazenar e gerenciar o conteúdo do servidor de relatório em um site ou farm do SharePoint.  
  
-   O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece arquivos de programa atualizados, um ponto de extremidade SOAP e extensões de entrega e segurança personalizadas. O servidor de relatório deve estar configurado para ser executado no modo integrado do SharePoint, dedicado exclusivamente a dar suporte ao acesso e à entrega de relatórios pelo seu site do SharePoint.  
  
 Depois de instalar o Suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no SharePoint e configurar os dois servidores para integração, você pode carregar ou publicar tipos de conteúdo de servidor de relatório em uma biblioteca do SharePoint e exibir e gerenciar esses documentos a partir de um site do SharePoint. O carregamento ou a publicação do conteúdo de servidor de relatório é uma primeira etapa importante; a Web part e as páginas são disponibilizadas quando você seleciona definições de relatório (.rdl), modelos de relatório (.smdl) e fontes de dados compartilhadas (.rsds) em um site do SharePoint.  
  
##  <a name="bkmk_language"></a> Considerações sobre idioma  
 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] e [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] estão disponíveis em muito mais idiomas do que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 Ao configurar um servidor de relatório para ser executado em uma implantação de produto do SharePoint, é possível encontrar uma combinação de idiomas. A interface do usuário, a documentação e as mensagens aparecerão nos seguintes idiomas:  
  
-   Todas as páginas de aplicativo, ferramentas, erros, avisos e mensagens originadas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aparecerão no idioma usado pela instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em um dos idiomas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   As páginas de aplicativo que você abrir em um site do SharePoint, a Web Part do Visualizador de Relatórios e do Construtor de Relatórios aparecerão em um dos idiomas com suporte no Suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para exibir a lista de idiomas com suporte, acesse [Downloads do SQL Server](http://msdn.microsoft.com/sql/downloads/) e localize a página de download do Suplemento do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
-   Sites do SharePoint, Administração Central do SharePoint, ajuda online e mensagens estão disponíveis nos idiomas que possuem suporte nos produtos do Office Server.  
  
 Se o idioma do seu produto ou tecnologia do SharePoint for diferente do idioma do servidor de relatório, o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] tentará usar um idioma da mesma família de idiomas que forneça a correspondência mais aproximada. Se não houver um substituto aproximado, o servidor de relatório usará o inglês.  
  
##  <a name="bkmk_relatedtasks"></a> Tarefas relacionadas  
 A tabela a seguir resume as tarefas relacionadas a um servidor de relatório no modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :  
  
|**Tarefa**|**Link**|  
|--------------|--------------|  
|Etapas detalhadas para instalar e configurar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint.|[Instalar o Reporting Services no modo do SharePoint para SharePoint 2010](http://msdn.microsoft.com/pt-br/47efa72e-1735-4387-8485-f8994fb08c8c) e [Adicionar outro servidor de relatório a um farm &#40;Expansão do SSRS&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md).|  
|Expanda a implantação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint adicionando outros servidores de relatório.|[Adicionar outro servidor de relatório a um farm &#40;Expansão do SSRS&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md) e [Topologias de implantação para recursos de BI do SQL Server no SharePoint](../Topic/Deployment%20Topologies%20for%20SQL%20Server%20BI%20Features%20in%20SharePoint.md).|  
|Adicione outros front-ends da Web do SharePoint que têm os componentes do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalados para exibir e relatar itens.|[Adicionar um front-end da Web do Reporting Services a um farm](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)|  
|Configure o email para recursos de alerta de dados e assinatura do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|[Configurar o email para um serviço de aplicativo do Reporting Services &#40;SharePoint 2010 e SharePoint 2013&#41;](https://msdn.microsoft.com/library/hh231673.aspx)|  
|Informações recentes para esta versão, encontradas no TechNet Wiki.|[Dicas, truques e soluções de problemas do SQL Server 2012 Reporting Services](http://go.microsoft.com/fwlink/?LinkId=221297).|  
  
## Consulte também  
 [Instalar ou desinstalar o suplemento Reporting Services para SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
 [Web Part do Visualizador de Relatórios em um site do SharePoint](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [Teste: Configurando o SSRS 2012 para integração com o SharePoint](http://go.microsoft.com/fwlink/?LinkId=306443)  
  
  