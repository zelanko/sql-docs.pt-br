---
title: Reporting Services Report Server | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- security [Reporting Services], extensions
- report servers [Reporting Services], about report server
- rendering extensions [Reporting Services], about extensions
- extensions [Reporting Services], about extensions
- storing data [Reporting Services]
- report servers [Reporting Services]
- data processing extensions [Reporting Services], about extensions
- delivery extensions [Reporting Services], about extensions
- data storage [Reporting Services]
- components [Reporting Services], report server
- report processing [Reporting Services], extensions
- Web service [Reporting Services], report server
- storage [Reporting Services]
ms.assetid: 88ed5b97-1d28-4980-80e4-b36761f3c03a
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e91d3e4ec882793ded89c934a598cafd1b4ca6e6
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53352350"
---
# <a name="reporting-services-report-server"></a>Servidor de Relatório do Reporting Services
  Este tópico é uma visão geral do servidor de relatório [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , o componente central da instalação de um [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Ele consiste em um par de mecanismos de processamento mais uma coleção de extensões de propósitos especiais que manipulam autenticação, processamento de dados, renderização e operações de entrega. Um servidor de relatório do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] é executado em um destes dois modos de implantação: modo nativo ou modo do SharePoint. Consulte a seção [Comparação de recursos do SharePoint e do modo nativo](#bkmk_featuresupport) para obter uma comparação entre os recursos.  
  
 **Instalação:** Para obter informações sobre a instalação do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], consulte o seguinte:  
  
-   [Instalar o servidor de relatórios de modo nativo do Reporting Services](install-windows/install-reporting-services-native-mode-report-server.md)  
  
-   [Instalar recursos de BI do SQL Server com o SharePoint &#40;PowerPivot e Reporting Services&#41;](../../2014/sql-server/install/install-sql-server-bi-features-sharepoint-powerpivot-reporting-services.md)  
  
 **Windows Azure**: Para obter informações sobre como usar o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] com Máquinas Virtuais do Microsoft Azure, consulte o seguinte:  
  
-   [SQL Server Business Intelligence em máquinas virtuais do Windows Azure](https://msdn.microsoft.com//library/windowsazure/jj992719.aspx).  
  
-   [Use o PowerShell para criar uma VM do Windows Azure com um servidor de relatório no modo nativo](https://msdn.microsoft.com/library/windowsazure/dn449661.aspx).  
  
##  <a name="bkmk_top"></a> Neste tópico  
  
-   [Visão geral dos modos de servidor de relatório](#bkmk_overview)  
  
-   [Comparação de recursos do SharePoint e modo nativo](#bkmk_featuresupport)  
  
-   [Native Mode](#bkmk_nativemode)  
  
-   [Modo nativo com Web Parts do SharePoint](#bkmk_nativewithwebparts)  
  
-   [Modo do SharePoint](#bkmk_sharepointmode)  
  
-   [Processo de relatório e o agendamento e o processo de entrega](#bkmk_reportprocessor)  
  
-   [Banco de dados do Servidor de Relatório](#bkmk_reportdatabase)  
  
-   [Autenticação, renderização, dados e extensões de entrega](#bkmk_authentication)  
  
-   [Tarefas relacionadas](#bkmk_relatedtasks)  
  
##  <a name="bkmk_overview"></a> Visão geral dos modos de servidor de relatório  
 Mecanismos de processamento (processadores) são o núcleo do servidor de relatório. Os processadores oferecem suporte à integridade do sistema de geração de relatórios e não podem ser modificados ou estendidos. Extensões também são processadores, mas elas executam funções muito específicas. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] inclui uma ou mais extensões padrão para todo tipo de extensão com suporte. É possível adicionar extensões personalizadas a um servidor de relatório. Isso permite estender um servidor de relatório para que ofereça suporte a recursos que não vêm com suporte de fábrica; exemplos da funcionalidade personalizada podem incluir suporte a tecnologias de logon único, saída de relatório em formatos de aplicativo que não estão prontos para serem manipulados pelas extensões de renderização padrão e entrega de relatório para uma impressora ou aplicativo.  
  
 Uma única instância de servidor de relatório é definida pela coleção inteira de processadores e extensões que fornecem processamento de ponta a ponta, desde a manipulação da solicitação inicial até a apresentação de um relatório concluído. Através de seus subcomponentes, o servidor de relatório processa as solicitações de relatório e torna os relatórios disponíveis para acesso sob demanda ou distribuição agendada.  
  
 Funcionalmente, um servidor de relatório permite experiências de criação de relatório, renderização de relatório e entrega de relatório para várias fontes de dados, bem como autenticação extensível e esquemas de autorização. Além disso, um servidor de relatório contém bancos de dados de servidor de relatório que armazenam relatórios publicados, fontes de dados compartilhadas, conjuntos de dados compartilhados, partes de relatório, agendas compartilhadas e assinaturas, arquivos de origem de definição de relatórios, definições de modelos, relatórios compilados, instantâneos, parâmetros e outros recursos. Um servidor de relatório também permite que um administrador configure o servidor de relatório para processar solicitações de relatório, mantenha históricos de instantâneos e gerencie permissões para relatórios, fontes de dados, conjuntos de dados e assinaturas.  
  
 Um servidor de relatório do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] oferece suporte a dois modos de implantação para instâncias do servidor de relatório:  
  
-   O modo**nativo**, incluindo o modo nativo com Web Parts do SharePoint, no qual um servidor de relatório é executado como um servidor de aplicativo que fornece todos os recursos de processamento e gerenciamento exclusivamente através de componentes do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Você configura um servidor de relatório de modo nativo com o gerenciador de configurações do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e o SQL Server Management Studio.  
  
-   O modo do**SharePoint**, no qual um servidor de relatório é instalado como parte de um farm de servidores do SharePoint.  Implante e configure o modo do SharePoint usando comandos do PowerShell ou páginas de gerenciamento de conteúdo do SharePoint.  
  
 No [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] , você não pode alternar o servidor de relatório de um modo para outro. Se você quiser alterar o tipo de servidor de relatório que seu ambiente usa, deve instalar o modo do servidor de relatório desejado e, em seguida, copiar ou mover os itens de relatório ou o banco de dados do servidor de relatório antigo para o novo. Esse processo geralmente é denominado 'migração'. As etapas necessárias para migrar dependem do modo que você está migrando e a versão da qual você está migrando. Para obter mais informações, consulte [Upgrade and Migrate Reporting Services](install-windows/upgrade-and-migrate-reporting-services.md).  
  
##  <a name="bkmk_featuresupport"></a> Comparação de recursos do SharePoint e modo nativo  
  
|Recurso ou componente|Modo nativo|SharePoint Mode|  
|--------------------------|-----------------|---------------------|  
|**Endereçamento de URL**|Sim|O endereçamento de URL é diferente no modo integrado do SharePoint. As URLs do SharePoint são usadas para relatórios de referência, modelos de relatório, fontes de dados compartilhadas e recursos. A hierarquia de pastas do servidor de relatório não é usada. Se você tiver aplicativos personalizados que dependem do acesso à URL com suporte em um servidor de relatório no modo nativo, essa funcionalidade deixará de funcionar quando o servidor de relatório for configurado para integração com o SharePoint.<br /><br /> Para obter mais informações sobre acesso à URL, consulte [Referência de parâmetro de acesso à URL](url-access-parameter-reference.md)|  
|**Extensões de segurança personalizadas**|Sim|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] não podem ser implantadas nem usadas no servidor de relatório. O servidor de relatório inclui uma extensão de segurança para fins especiais que é usada sempre que você configura um servidor de relatório para ser executado no modo integrado do SharePoint. Essa extensão de segurança é um componente interno e é necessário para operações integradas.|  
|**Configuration Manager**|Sim|**\*\* Importante \*\*** O Configuration Manager não pode ser usado para gerenciar servidor de relatório do modo do SharePoint. Em vez disso, use a administração central do SharePoint.|  
|**Gerenciador de Relatórios**|Sim|O Gerenciador de Relatórios não pode ser usado para gerenciar o modo do SharePoint. Use as páginas do aplicativo do SharePoint. Para obter mais informações, consulte [Serviço SharePoint do Reporting Services e aplicativos de serviço](../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md).|  
|**Relatórios vinculados**|Sim|Nenhum.|  
|**Meus Relatórios**|Sim|Não|  
|**Minhas Assinaturas** e métodos de envio em lote.|Sim|Não|  
|**Alertas de dados**|Não|Sim|  
|**Power View**|Não|Sim<br /><br /> Exige o Silverlight no navegador do cliente. Para obter mais informações sobre requisitos de navegador, consulte [Planning for Reporting Services e o suporte a navegador Power View &#40;Reporting Services 2014&#41;](../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md)|  
|**Relatórios .RDL**|Sim|Sim<br /><br /> Relatórios .RDL podem ser executados em servidores de relatório do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no modo nativo ou no modo do SharePoint.|  
|**Relatórios .RDLX**|Não|Sim<br /><br /> Relatórios .RDLX do Power View só podem ser executados em servidores de relatório do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no modo do SharePoint.|  
|**Credenciais do token do usuário do SharePoint para a extensão de lista do SharePoint**|Não|Sim|  
|**As zonas do AAM para implantações voltadas para a Internet**|Não|Sim|  
|**Backup e recuperação do SharePoint**|Não|Sim|  
|**Suporte de log ULS**|Não|Sim|  
  
##  <a name="bkmk_nativemode"></a> Modo nativo  
 No modo nativo, um servidor de relatório é um servidor de aplicativo autônomo que fornece todas as exibições, gerenciamento, processamento e entrega de relatórios e modelos de relatório. Este é o modo padrão para instâncias do servidor de relatório. Você pode instalar um servidor de relatório no modo nativo que seja configurado durante a instalação ou pode configurá-lo para operações do modo nativo quando a instalação for concluída.  
  
 O diagrama seguinte mostra a arquitetura de três camadas de uma implantação de modo Nativo do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Ele mostra o banco de dados do servidor de relatório e as fontes de dados na camada de dados, os componentes do servidor do relatório na camada intermediária, os aplicativos cliente e as ferramentas internas ou personalizadas na camada de apresentação. Apresenta o fluxo de solicitações, os dados entre os componentes do servidor e quais componentes enviam e recuperam conteúdo a partir de um repositório de dados.  
  
 ![Arquitetura do Reporting Services](media/reporting-serv-arch.gif "Arquitetura do Reporting Services")  
  
 O servidor de relatório é implementado como um serviço do [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows, chamado "serviço Servidor de Relatório", que hospeda um serviço Web, processamento em segundo plano e outras operações. No aplicativo do console Serviços, o serviço é listado como MSSQLSERVER (SQL Server Reporting Services).  
  
 Desenvolvedores de terceiros podem criar extensões adicionais para substituir ou estender a capacidade de processamento do servidor de relatório. Para obter mais informações sobre as interfaces programáticas disponíveis para desenvolvedores de aplicativos, consulte a [Referência Técnica](../../2014/reporting-services/technical-reference-ssrs.md).  
  
###  <a name="bkmk_nativewithwebparts"></a> Modo nativo com Web Parts do SharePoint  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] fornece duas Web Parts que você pode instalar e registrar em uma instância de [!INCLUDE[winSPServ](../includes/winspserv-md.md)] 2.0 ou posterior, ou o SharePoint Portal Server 2003 ou posterior. A partir de um site do SharePoint, você pode usar as Web Parts para localizar e exibir relatórios armazenados e processados em um servidor de relatório executado no modo nativo. Essas Web Parts foram introduzidas em versões anteriores do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
##  <a name="bkmk_sharepointmode"></a> Modo do SharePoint  
 No modo do SharePoint, um servidor de relatório deve ser executado em um farm de servidores do SharePoint. Os recursos de processamento, renderização e gerenciamento do servidor de relatório são representados por um servidor de aplicativos do SharePoint que executa o serviço compartilhado SharePoint para [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e um ou mais aplicativos de serviço do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Um site do SharePoint fornece o acesso front-end ao conteúdo e às operações do servidor de relatório.  
  
 O modo do SharePoint requer:  
  
-   [!INCLUDE[SPF2010](../includes/spf2010-md.md)] ou [!INCLUDE[SPS2010](../includes/sps2010-md.md)].  
  
-   Uma versão apropriada do Suplemento do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para Produtos do SharePoint 2010.  
  
-   Um servidor de aplicativos do SharePoint com o serviço compartilhado do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] instalado e pelo menos um aplicativo de serviço do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
 A ilustração a seguir mostra um ambiente do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no modo do SharePoint:  
  
 ![Arquitetura funcional do SharePoint do SSRS](media/rs-sharepoint-architecture.gif "Arquitetura funcional do SharePoint do SSRS")  
  
||Descrição|  
|-|-----------------|  
|**(1)**|Servidores Web ou WFE (front-ends da Web). O suplemento do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] deve ser instalado em cada servidor Web do qual você deseja utilizar os recursos de aplicativo Web, como exibição de relatórios ou páginas de gerenciamento do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para tarefas como gerenciar fontes de dados ou assinaturas.|  
|**(2)**|O suplemento instala a URL e pontos de extremidade SOAP para clientes se comunicarem com os servidores de aplicativos, pelo proxy de serviço do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .|  
|**(3)**|Os servidores de aplicativos que executam o serviço compartilhado do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . A expansão do processamento de relatório é gerenciado como parte do farm do SharePoint e adicionando o serviço do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para servidores de aplicativos adicionais.|  
|**(4)**|Você pode criar mais de um aplicativo de serviço do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , com configurações diferentes inclusive permissões, email, proxy e assinaturas.|  
|**(5)**|Relatórios, fontes de dados e outros itens são armazenados nos bancos de dados de conteúdo do SharePoint.|  
|**(6)**|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] criam três bancos de dados para servidor de relatório, temporário e recursos de alertas de dados. Os parâmetros de configuração que se aplicam a todos os aplicativos de serviço do SSRS são armazenadas no arquivo **RSReportserver.config** .|  
  
##  <a name="bkmk_reportprocessor"></a> Processo de relatório e o agendamento e o processo de entrega  
 O servidor de relatório inclui dois mecanismos de processamento que executam processamento de relatório preliminar e intermediário, além de operações agendadas e de entrega. O Processador de Relatório recupera a definição ou modelo de relatório, combina informações de layout com dados a partir da extensão de processamento de dados e as renderiza no formato solicitado. O Processo de Agendamento e Entrega processa relatórios disparados a partir de um agendamento e entrega os relatórios aos destinos pretendidos.  
  
##  <a name="bkmk_reportdatabase"></a> Banco de dados de servidor de relatório  
 O servidor de relatório é um servidor sem monitoração de estado que armazena todas as propriedades, objetos e metadados em um banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Os dados armazenados incluem relatórios publicados, relatórios compilados, modelos de relatório e a hierarquia de pastas que fornece o endereço para todos os itens gerenciados pelo servidor de relatório. Um banco de dados do servidor de relatório pode fornecer armazenamento interno para uma única instalação do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ou para vários servidores de relatório que façam parte de uma implantação de expansão. Se você configurar um servidor de relatório para ser executado em uma implantação maior do produto ou tecnologia do SharePoint, o servidor de relatório usará os bancos de dados do SharePoint além do banco de dados do servidor de relatório. Para obter mais informações sobre os repositórios de dados usados na instalação do Reporting Services, consulte [Banco de dados do servidor de relatório &#40;modo nativo do SSRS&#41;](report-server/report-server-database-ssrs-native-mode.md).  
  
##  <a name="bkmk_authentication"></a> Autenticação, renderização, dados e extensões de entrega  
 O servidor de relatório oferece suporte aos seguintes tipos de extensões: autenticação, processamento de dados, processamento de relatórios, renderização e entrega. Um servidor de relatório requer pelo menos uma extensão de autenticação, de processamento de dados e de renderização. As extensões de processamento de relatório personalizado e de entrega são opcionais, mas necessárias se você quiser oferecer suporte aos controles de distribuição e personalização.  
  
 O Reporting Services fornece extensões padrão para que você possa usar todos os recursos de servidor sem ter de desenvolver componentes personalizados. A tabela a seguir descreve as extensões padrão que contribuem para uma instância de servidor de relatório completa que fornece funcionalidades prontas para uso:  
  
|Tipo|Padrão|  
|----------|-------------|  
|Autenticação|Uma instância de servidor de relatório padrão oferece suporte à Autenticação do Windows, incluindo recursos de representação e delegação, caso estejam habilitados no seu domínio.|  
|Processamento de dados|Uma instância do servidor de relatório padrão inclui extensões de processamento de dados para fontes de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], Oracle, Hyperion Essbase, SAPBW, OLE DB, Parallel Data Warehouse e ODBC.|  
|Renderização|Uma instância de servidor de relatório padrão inclui extensões de renderização para HTML, Excel, CSV, XML, Imagem, Word, lista do SharePoint e PDF.|  
|Entrega|Uma instância de servidor de relatório padrão inclui uma extensão de entrega de email e uma extensão de entrega de compartilhamento de arquivos. Se o servidor de relatório for configurado para integração com o SharePoint, você poderá usar uma extensão de entrega que salva relatórios em uma biblioteca do SharePoint.|  
  
> [!NOTE]  
>  O Reporting Services inclui um conjunto completo de ferramentas e aplicativos que você pode usar para administrar o servidor, criar conteúdo e torná-lo disponível aos usuários de sua organização.  
  
##  <a name="bkmk_relatedtasks"></a> Tarefas relacionadas  
 Os tópicos a seguir fornecem mais informações sobre como instalar, usar e manter um servidor de relatório:  
  
|Tarefa|Link|  
|----------|----------|  
|Revisar os requisitos de hardware e software.|[Hardware and Software Requirements for Reporting Services in SharePoint Mode](../../2014/sql-server/install/hardware-and-software-requirements-for-reporting-services-in-sharepoint-mode.md).|  
|Instalar o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no modo do SharePoint.|[Instalar o Reporting Services no modo do SharePoint para SharePoint 2010](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)|  
|Se você for um desenvolvedor Web ou possuir conhecimento especializado na criação de folhas de estilo em cascata, poderá modificar os tamanhos padrão por seu próprio risco para alterar cores, fontes e layout da barra de ferramentas do Gerenciador de Relatórios. Nem as folhas de estilo padrão nem as instruções para modificar as folhas de estilo são documentadas nesta versão.|[Personalizar folhas de estilo para o Visualizador de HTML e o Gerenciador de Relatórios](../../2014/reporting-services/customize-style-sheets-for-html-viewer-and-report-manager.md)|  
|Desenvolvedores Web familiares com estilos de HTML e CSS (Folhas de Estilo em Cascata) podem usar as informações neste tópico para determinar quais arquivos podem ser modificados para personalizar a aparência do Gerenciador de Relatórios.|[Configurar o Gerenciador de Relatórios para passar cookies de autenticação personalizados](security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)|  
|Explica como ajustar as configurações de memória para o serviço Web Servidor de Relatórios e serviço Windows.|[Configurar memória disponível para aplicativos do Servidor de Relatórios](report-server/configure-available-memory-for-report-server-applications.md)|  
|Explica as etapas recomendadas para configurar o servidor de relatório para administração remota.|[Configurar um servidor de relatório para administração remota](report-server/configure-a-report-server-for-remote-administration.md)|  
|Fornece instruções sobre como configurar a disponibilidade de **Meus Relatórios** em uma instância nativa de servidor de relatório.|[Habilitar e desabilitar Meus Relatórios](report-server/enable-and-disable-my-reports.md)|  
|Fornece instruções para configurar o controle RSClientPrint que fornece a funcionalidade de impressão nos navegadores com suporte. Para obter mais informações sobre requisitos de navegador, consulte [Planning for Reporting Services e o suporte a navegador Power View &#40;Reporting Services 2014&#41;](../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md).|[Habilitar e desabilitar a impressão do lado do cliente para Reporting Services](report-server/enable-and-disable-client-side-printing-for-reporting-services.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Extensões do Reporting Services](extensions/reporting-services-extensions.md)   
 [Ferramentas do Reporting Services](tools/reporting-services-tools.md)   
 [Assinaturas e entrega &#40;Reporting Services&#41;](subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Banco de dados do servidor de relatório &#40;modo nativo do SSRS&#41;](report-server/report-server-database-ssrs-native-mode.md)   
 [Implementando uma extensão de segurança](extensions/security-extension/implementing-a-security-extension.md)   
 [Implementando uma extensão de processamento de dados](extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [Como administrar SSRS usando PowerShell (resposta da curadoria)](https://go.microsoft.com/fwlink/?LinkId=321992)  
  
  
