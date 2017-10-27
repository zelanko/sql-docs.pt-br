---
title: "Servidor do Reporting Services relatórios (modo SharePoint) | Microsoft Docs"
ms.custom: 
ms.date: 09/26/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: a8cd1bd00ec92535fff73c5eaa4ff9bbe9274ef2
ms.contentlocale: pt-br
ms.lasthandoff: 10/06/2017

---

# <a name="reporting-services-report-server-sharepoint-mode"></a>Servidor de relatório do Reporting Services (modo do SharePoint)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  Um servidor de relatório do Reporting Services configurado para **modo do SharePoint** pode ser executado em uma implantação de um produto do SharePoint. Um servidor de relatório no modo do SharePoint pode usar os recursos de colaboração e gerenciamento do SharePoint para relatórios e outros tipos de conteúdo do [!INCLUDE[ssRSnfoversion_md](../../includes/ssrsnoversion-md.md)] . Modo do SharePoint requer instalando a versão apropriada do suplemento Reporting Services para produtos do SharePoint em seu SharePoint Front-Ends da Web.  
  
> [!NOTE]
> Integração do Reporting Services com o SharePoint não está mais disponível após o SQL Server 2016.

 Para obter mais informações sobre como instalar e configurar, consulte o seguinte:  
  
-   [Instalar o modo do SharePoint do Reporting Services para SharePoint 2010](http://msdn.microsoft.com/47efa72e-1735-4387-8485-f8994fb08c8c).  
  
-   [Adicionar um servidor de relatório a um farm](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md).  
  
## <a name="feature-summary"></a>Resumo de recursos

 Configurar um servidor de relatório para ser executado no modo integrado do SharePoint fornece as seguintes funcionalidades adicionais disponíveis somente ao implantar um servidor de relatório nesse modo:  
  
-   Use os recursos de gerenciamento de documentos e colaboração do SharePoint, incluindo alertas. Um site de SharePoint fornece um portal unificado para acessar e gerenciar todos os itens de relatório em um único lugar.  
  
-   Use as permissões e os provedores de autenticação do SharePoint para controlar o acesso a relatórios, modelos e outros itens.  
  
-   Use as topologias de implantação do SharePoint para distribuir relatórios em uma conexão com a Internet fora do firewall. Um servidor de relatório fornece serviços de processamento de relatório e dados no contexto de uma implantação maior do SharePoint configurada para acesso à Internet.  
  
-   Gerencie relatórios, modelos, fontes de dados, agendas e histórico de relatório em páginas de aplicativo personalizadas de um site do SharePoint. Você pode definir propriedades, definir agendas e assinaturas, e criar e gerenciar o histórico de relatório em um site do SharePoint da mesma maneira que os cria e gerencia com outras ferramentas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Publique ou atualize relatórios, modelos de relatórios, recursos e arquivos de fonte de dados compartilhados em uma biblioteca do SharePoint, incluindo a Central de Relatórios no Office SharePoint Server.  
  
     Use o Designer de Relatórios, o Designer de Modelos e o Construtor de Relatórios para criar relatórios e fontes de dados a serem publicados diretamente em uma biblioteca do SharePoint. Você também pode usar a ação Carregar em um site do SharePoint para adicionar qualquer definição e modelos de relatório a uma biblioteca do SharePoint.  
  
     Como o servidor de relatório processa as definições de relatório da mesma maneira, independentemente do modo do servidor usado, os dados e o layout de relatório não são afetados pelo modo do servidor. Qualquer relatório executado em um servidor de relatório no modo nativo poderá ser executado em um servidor de relatório configurado para o modo integrado do SharePoint.  
  
-   Assine e entregue relatórios em uma biblioteca do SharePoint usando uma nova extensão de entrega do SharePoint. Também é possível entregar relatórios por email ou para uma pasta compartilhada. As extensões de entrega de servidor de relatório são usadas para entregar relatórios. Você pode criar assinaturas controladas por dados para uma distribuição de relatório em larga escala usando dados de assinante consultados em tempo de execução.  
  
-   Uma web part do Visualizador de relatórios que você pode adicionar a páginas do SharePoint para exibir um relatório dentro seu aplicativo da web do SharePoint. A web part inclui navegação de página, pesquisar, imprimir e exportar recursos.  
  
-   Programe em um novo ponto de extremidade SOAP para criar aplicativos personalizados que se integrem a um site do SharePoint. Também é possível usar o provedor WMI (Instrumentação de Gerenciamento do Windows) para configurar programaticamente uma instância do servidor de relatório que seja executada no modo integrado do SharePoint.  
  
-   Serviços do Microsoft Access reportados no modo conectado.  
  
-   As zonas AAM, as implantações voltadas para Internet e os tokens de usuário do SharePoint para listas do SharePoint.  
  
## <a name="connected-mode-and-local-mode"></a>Modo conectado e modo local

 A versão do SQL Server 2008 R2 introduziu um novo *modo local* para exibição de relatórios de um servidor do SharePoint 2010 com o Suplemento Reporting Services do Microsoft SQL Server 2008 R2 ou posterior para os produtos SharePoint 2010 instalados.  
  
-   *Modo local*: modo Local permite que os relatórios sejam renderizados localmente a partir da biblioteca de documentos do SharePoint, sem integração com um servidor de relatório do Reporting Services. O suplemento Reporting Services para produtos do SharePoint é necessário, mas não é de um servidor de relatório do Reporting Services. O suplemento pode ser instalado de várias maneiras diferentes, incluindo a ferramenta de preparação de produtos do SharePoint 2010. Para obter mais informações sobre o modo local, consulte [modo Local VS modo conectado relatórios no Visualizador de relatórios](../../reporting-services/report-server-sharepoint/local-mode-vs-connected-mode-reports-in-the-report-viewer.md) e [onde encontrar o suplemento Reporting Services para produtos do SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).  
  
-   *Modo conectado*: há suporte para o modo conectado integrando um servidor de relatório do Reporting Services no farm do SharePoint usando a Administração Central do SharePoint. A integração com um servidor de relatório permite relatórios completos de ponta a ponta, fornecendo os recursos de colaboração do SharePoint 2010 e os recursos baseados no servidor de um servidor de relatório, inclusive: Assinaturas, Instantâneos e processamento baseado no servidor.  
  
## <a name="unsupported-sharepoint-features"></a>Recursos do sharePoint sem suporte

 Nem todos os recursos do SharePoint estão disponíveis para operações integradas. A seguir está uma lista dos recursos do SharePoint com que do Reporting Services não integra diretamente:  
  
-   Serviço de Repositório Seguro.  
  
-   Não é possível usar a integração de Calendário do SharePoint Outlook ou o agendamento do SharePoint para arquivos do Reporting Services em uma biblioteca de documentos.  
  
-   Catálogo de dados comerciais do SharePoint.  
  
-   Personalização do SharePoint também não é compatível nas páginas do Reporting Services. Não há suporte para integração do Servidor de Relatório quando o aplicativo Web do SharePoint é habilitado para acesso Anônimo.  
  
-   SQL Server Reporting Services **não** dão suporte a controle de versão de biblioteca de documentos do SharePoint. Se você salvar itens de relatório em uma biblioteca de documentos que está configurada com “Histórico de Versão de Documento” habilitado, os recursos do Reporting Services não funcionarão corretamente e gerarão erros no log do ULS. Este é um exemplo de um erro no log do ULS:  
  
    -   “…uma fonte de dados associada ao relatório foi desabilitada”.  
  
     O histórico de versão da biblioteca de documento está configurada na página ”Configurações de versão” de “Configurações da biblioteca”.  
  
## <a name="supported-combinations-of-the-sharepoint-add-in-and-report-server"></a>Combinações com suporte do servidor do SharePoint suplemento e relatório

 Nem todos os recursos são compatíveis em todas as combinações de servidor de relatório, suplemento Reporting Services para SharePoint e produtos do SharePoint. Para obter mais informações, consulte [combinações do SharePoint e servidor do Reporting Services e do suplemento com suporte](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
> [!NOTE]  
>  A versão correta do suplemento do Reporting Services deve ser usada com a versão correspondente dos produtos SharePoint.  
  
## <a name="components-that-provide-integration"></a>Componentes que fornecem integração

 Para combinar os servidores em uma única implantação, integre uma instalação de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Reporting Services com uma instância dos produtos do SharePoint  
  
 Integração é fornecida pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o suplemento do Reporting Services para produtos do SharePoint. O suplemento Reporting Services é um componente de distribuição livre que você pode baixar e instalar em um servidor que está executando a versão apropriada do SharePoint.  
  
> [!TIP]  
>  Nem todos os recursos são compatíveis em todas as combinações de servidor de relatório, suplemento Reporting Services para SharePoint e produtos do SharePoint. Para obter mais informações, consulte [suporte para combinações do SharePoint e servidor do Reporting Services e suplemento](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md).  
  
-   No SharePoint, o suplemento Reporting Services fornece o ponto de extremidade de proxy do ReportServer, uma web part do Visualizador de relatórios e páginas de aplicativo para que você pode exibir, armazenar e gerenciar o conteúdo do servidor de relatório em um site do SharePoint ou farm.  
  
-   No Reporting Services fornece arquivos de programa atualizados, um ponto de extremidade SOAP e extensões de entrega e de segurança personalizadas. O servidor de relatório deve estar configurado para ser executado no modo integrado do SharePoint, dedicado exclusivamente a dar suporte ao acesso e à entrega de relatórios pelo seu site do SharePoint.  
  
 Depois de instalar o suplemento Reporting Services no SharePoint e configurar os dois servidores para integração, você pode carregar ou publicar tipos de conteúdo de servidor de relatório em uma biblioteca do SharePoint e, em seguida, exibir e gerenciar esses documentos em um site do SharePoint. Carregar ou publicar o conteúdo do servidor de relatório é uma primeira etapa importante; a web part e as páginas ficam disponíveis quando você seleciona definições de relatório (. RDL), modelos (. SMDL) de relatório e fontes de dados (. rsds) em um site do SharePoint.  
  
##  <a name="language-considerations"></a>Considerações sobre idioma

 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] e [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] estão disponíveis em muito mais idiomas do que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 Ao configurar um servidor de relatório para ser executado em uma implantação de produto do SharePoint, é possível encontrar uma combinação de idiomas. A interface do usuário, a documentação e as mensagens aparecerão nos seguintes idiomas:  
  
-   Todas as páginas de aplicativos, ferramentas, erros, avisos e mensagens originadas do Reporting Services serão exibido no idioma usado pela instância do Reporting Services em um do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] idiomas.  
  
-   Páginas de aplicativo que você abrir em um site do SharePoint, a web part do Visualizador de relatórios e construtor de relatórios aparecerão em um dos idiomas com suporte para o suplemento do Reporting Services. Para exibir a lista de idiomas com suporte, vá para [downloads do SQL Server](http://msdn.microsoft.com/sql/downloads/) e localize a página de download para o SQL Server 2016 Reporting Services suplemento.  
  
-   Sites do SharePoint, Administração Central do SharePoint, ajuda online e mensagens estão disponíveis nos idiomas que possuem suporte nos produtos do Office Server.  
  
 Se o idioma do seu produto ou tecnologia SharePoint for diferente do idioma do servidor de relatório, o Reporting Services tentará usar um idioma da mesma família de idiomas que forneça a correspondência mais próxima. Se não houver um substituto aproximado, o servidor de relatório usará o inglês.  
  
## <a name="related-tasks"></a>Tarefas relacionadas

 A tabela a seguir resume as tarefas relacionadas a um servidor de relatório do modo SharePoint do Reporting Services:  
  
|**Tarefa**|**Link**|  
|--------------|--------------|  
|Etapas detalhadas para instalar e configurar o Reporting Services no modo do SharePoint.|[Instalar o modo do SharePoint do Reporting Services para SharePoint 2010](http://msdn.microsoft.com/47efa72e-1735-4387-8485-f8994fb08c8c) e [adicionar um servidor de relatório a um farm](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md).|  
|Expansão sua implantação do SharePoint do Reporting Services, adicionando mais servidores de relatório.|[Adicionar um servidor de relatório a um Farm](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md) e [topologias de implantação para recursos de BI do SQL Server no SharePoint](http://msdn.microsoft.com/library/39f76bc7-94e6-4dbc-bfa5-d56f4430bb26).|  
|Adicione adicionais do SharePoint front-ends da web que têm os componentes do Reporting Services instalados para exibir itens de relatório.|[Adicionar um front-end de web do Reporting Services adicional a um farm](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)|  
|Configure o email do servidor de relatório no SharePoint.|[Configurar o email para um aplicativo de serviço do Reporting Services](../install-windows/configure-e-mail-for-a-reporting-services-service-application.md)|
|Informações recentes para esta versão, encontradas no TechNet Wiki.|[Dicas do SQL Server 2012 Reporting Services, truques e solução de problemas](http://go.microsoft.com/fwlink/?LinkId=221297).|  

## <a name="next-steps"></a>Próximas etapas

[Instalar ou desinstalar o Reporting Services em sdd para SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
[Relatório de web part do visualizador em um site do SharePoint](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
[Teste: Configurando SSRS 2012 para integração do SharePoint](http://go.microsoft.com/fwlink/?LinkId=306443)  

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)

