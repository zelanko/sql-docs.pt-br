---
title: Documentação do desenvolvedor do Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: ''
ms.component: reporting-services
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- developer's guide [Reporting Services]
- Reporting Services, programming
- programming [Reporting Services]
ms.assetid: d8afa405-1012-4349-a72d-e10d94f8453d
caps.latest.revision: 21
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: eb27b156224ee5689794d549ef41dbe2af2ef7cc
ms.sourcegitcommit: 31df356f89c4cd91ba90dac609a7eb50b13836de
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2018
---
# <a name="reporting-services-developer-documentation"></a>Documentação do desenvolvedor do Reporting Services
  O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] oferece várias interfaces de programação que você pode usar em seus próprios aplicativos. Você pode usar os recursos e as capacidades existentes do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para criar relatório personalizado e ferramentas de gerenciamento nos sites da Web e nos aplicativos do Windows ou você poderá estender a plataforma do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
 Estender a plataforma do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] inclui a criação de novos componentes e recursos que podem ser usados para acesso a dados, entrega de relatório e muito mais. Você pode comercializar esses componentes e recursos para empresas que estiverem usando o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] em sua organização.  
  
> [!NOTE]  
>  O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] inclui exemplos de programação e tutoriais para ajudar você começar a usá-los. Para obter mais informações, consulte [Amostras do Reporting Services](https://msdn.microsoft.com/library/ms160954\(v=sql.110\).aspx) e [Guia do desenvolvedor: Tutoriais (Reporting Services)](https://msdn.microsoft.com/library/aa337423\(v=sql.110\).aspx).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Integração do Reporting Services em aplicativos](../reporting-services/application-integration/integrating-reporting-services-into-applications.md)  
 Fornece uma visão geral de como usar o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para integrar o relatório em aplicativos personalizados. Descreve quando usar acesso de URL direto e quando usar o serviço Web para acessar o servidor de relatório.  
  
 [Serviço Web do Servidor de Relatório para aplicativos ASP.NET e tradicionais](../reporting-services/report-server-web-service/report-server-web-service.md)  
 O serviço Web do servidor de relatório fornece acesso à funcionalidade completa do servidor de relatório. O serviço Web usa o SOAP por meio de HTTP e é criado para agir como uma interface de comunicações entre programas cliente e o servidor de relatório. O serviço Web e seus métodos expõem a funcionalidade do servidor de relatório e permite que você crie ferramentas personalizadas para qualquer parte do ciclo e vida do relatório do gerenciamento até a execução.  
 
 [Desenvolver com APIs REST para aplicativos modernos](developer/rest-api.md)</br>
 As APIs REST do Reporting Services dão acesso programático aos objetos no catálogo do servidor de relatório do Reporting Services. Ao usar APIs REST, você pode navegar pela hierarquia de pastas, descobrir o conteúdo de uma pasta ou baixar uma definição de relatório. Você também pode criar, atualizar e excluir objetos.

 [Acesso à URL &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)  
 O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] dá suporte a um conjunto completo de solicitações baseadas na URL que você pode usar como um ponto de acesso rápido e fácil para navegação e exibição de relatório. Você pode usar esta tecnologia junto com o serviço Web do servidor de relatório para integrar uma solução de relatório completa em seus aplicativos comerciais personalizados. O acesso de URL será particularmente útil quando você estiver integrando relatórios como parte de um portal de Web ou exibindo relatórios de um navegador da Web.  
  
 [Extensões do Reporting Services](../reporting-services/extensions/reporting-services-extensions.md)  
 A arquitetura modular do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] foi desenhada para extensibilidade. Uma API de código gerenciado está disponível de forma que você possa desenvolver, instalar e gerenciar facilmente extensões consumidas por muitos componentes do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Você pode criar assemblies usando o [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] e adicionar uma nova funcionalidade de renderização, segurança, entrega e processamento de dados do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] de acordo com suas necessidades de negócios em evolução.  
  
 [Itens de relatório personalizados](../reporting-services/custom-report-items/custom-report-items.md)  
 Descreve como criar Itens de Relatório Personalizados para adicionar funcionalidade à RDL ou estender a funcionalidade de controles existentes.  
  
 [Usar assemblies personalizados com relatórios](../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
 Descreve como usar assemblies personalizados com Relatórios incluindo referências de código na definição de relatório.  
  
 [Acessar o provedor WMI do Reporting Services](../reporting-services/tools/access-the-reporting-services-wmi-provider.md)  
 Descreve como usar o Provedor WMI do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para gerenciar as implantações do servidor de relatório.  
  
## <a name="see-also"></a>Consulte Também  
 [Reporting Services &#40;SSRS&#41;](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [Linguagem RDL &#40;SSRS&#41;](../reporting-services/reports/report-definition-language-ssrs.md)   
 [Referência técnica &#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)   
 [Desenvolvimento seguro &#40;Reporting Services&#41;](../reporting-services/extensions/secure-development/secure-development-reporting-services.md)  
  
  
