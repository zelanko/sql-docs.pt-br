---
title: Desenvolvedor&#39;guia (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- developer's guide [Reporting Services]
- Reporting Services, programming
- programming [Reporting Services]
ms.assetid: d8afa405-1012-4349-a72d-e10d94f8453d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e8c555d853fd791bed29a06f561021b138526ea1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63255097"
---
# <a name="developer39s-guide-reporting-services"></a>Desenvolvedor&#39;guia (Reporting Services)
  O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] oferece várias interfaces de programação que você pode usar em seus próprios aplicativos. Você pode usar os recursos e as capacidades existentes do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para criar relatório personalizado e ferramentas de gerenciamento nos sites da Web e nos aplicativos do Windows ou você poderá estender a plataforma do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
 Estender a plataforma do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] inclui a criação de novos componentes e recursos que podem ser usados para acesso a dados, entrega de relatório e muito mais. Você pode comercializar esses componentes e recursos para empresas que estiverem usando o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] em sua organização.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Integração do Reporting Services em aplicativos](application-integration/integrating-reporting-services-into-applications.md)  
 Fornece uma visão geral de como usar o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para integrar o relatório em aplicativos personalizados. Descreve quando usar acesso de URL direto e quando usar o serviço Web para acessar o servidor de relatório.  
  
 [Serviço Web do Servidor de Relatório](report-server-web-service/report-server-web-service.md)  
 O serviço Web do servidor de relatório fornece acesso à funcionalidade completa do servidor de relatório. O serviço Web usa o SOAP por meio de HTTP e é criado para agir como uma interface de comunicações entre programas cliente e o servidor de relatório. O serviço Web e seus métodos expõem a funcionalidade do servidor de relatório e permite que você crie ferramentas personalizadas para qualquer parte do ciclo e vida do relatório do gerenciamento até a execução.  
  
 [Acesso à URL &#40;SSRS&#41;](url-access-ssrs.md)  
 O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] dá suporte a um conjunto completo de solicitações baseadas na URL que você pode usar como um ponto de acesso rápido e fácil para navegação e exibição de relatório. Você pode usar esta tecnologia junto com o serviço Web do servidor de relatório para integrar uma solução de relatório completa em seus aplicativos comerciais personalizados. O acesso de URL será particularmente útil quando você estiver integrando relatórios como parte de um portal de Web ou exibindo relatórios de um navegador da Web.  
  
 [Extensões do Reporting Services](extensions/reporting-services-extensions.md)  
 A arquitetura modular do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] foi desenhada para extensibilidade. Uma API de código gerenciado está disponível de forma que você possa desenvolver, instalar e gerenciar facilmente extensões consumidas por muitos componentes do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Você pode criar assemblies usando o [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] e adicionar uma nova funcionalidade de renderização, segurança, entrega e processamento de dados do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] de acordo com suas necessidades de negócios em evolução.  
  
 [Itens de relatório personalizados](custom-report-items/custom-report-items.md)  
 Descreve como criar Itens de Relatório Personalizados para adicionar funcionalidade à RDL ou estender a funcionalidade de controles existentes.  
  
 [Usar assemblies personalizados com relatórios](custom-assemblies/using-custom-assemblies-with-reports.md)  
 Descreve como usar assemblies personalizados com Relatórios incluindo referências de código na definição de relatório.  
  
 [Acessar o provedor WMI do Reporting Services](tools/access-the-reporting-services-wmi-provider.md)  
 Descreve como usar o Provedor WMI do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para gerenciar as implantações do servidor de relatório.  
  
## <a name="see-also"></a>Consulte também  
 [Reporting Services &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [Linguagem RDL &#40;SSRS&#41;](reports/report-definition-language-ssrs.md)   
 [Referência técnica &#40;SSRS&#41;](technical-reference-ssrs.md)   
 [Desenvolvimento seguro &#40;Reporting Services&#41;](extensions/secure-development/secure-development-reporting-services.md)  
  
  
