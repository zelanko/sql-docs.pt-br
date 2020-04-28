---
title: Problemas de atualização de Reporting Services (Supervisor de atualização) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Report Manager [Reporting Services], upgrade issues
- Reporting Services, upgrades
- upgrading Reporting Services
- report servers [Reporting Services], upgrade issues
ms.assetid: d9663f25-98d7-4508-ae3c-55a7277211bd
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 75c3bda5d15e3930fcdeba9ca73d70128fd90336
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "71952066"
---
# <a name="reporting-services-upgrade-issues-upgrade-advisor"></a>Problemas de atualização do Reporting Services (supervisor de atualização)
  Os tópicos a seguir descrevem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] os problemas que podem afetar a atualização [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]para o. Eles descrevem ações que podem ser tomadas para diminuir o efeito dessas alterações em seu ambiente.  
  
 O Supervisor de Atualização analisa uma instalação do servidor de relatório. Se apenas componentes cliente estiverem instalados (por exemplo, se o Designer de Relatórios for o único componente do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalado no computador), nenhum problema será reportado.  
  
 Dependendo de como sua instalação foi configurada, você poderá encontrar outros problemas que não foram reportados pelo Supervisor de Atualização. Esses problemas não impedem que a atualização do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] tenha êxito, mas podem afetar a maneira como os relatórios e os aplicativos são executados depois que a atualização é concluída. Para obter mais informações sobre esses problemas, consulte "Compatibilidade com versões anteriores do Reporting Services" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Se não for possível usar a Instalação para atualizar uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], você poderá instalar uma nova instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e migrar a instalação existente para essa nova instância. Para obter mais informações, consulte "atualizar e migrar Reporting Services [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] " nos manuais online, [atualizar e migrar Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).  
  
 Os tópicos a seguir descrevem problemas conhecidos reportados pelo Supervisor de Atualização e explicam como modificar a instalação existente para permitir que a atualização ocorra.  
  
> [!IMPORTANT]  
>  O Supervisor de Atualização deve estar instalado no servidor de relatório para analisar a instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não dá suporte à análise remota.  
>   
>  Para obter mais informações, consulte [instalando o supervisor de atualização](../../../2014/sql-server/install/installing-upgrade-advisor.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Certificados de cliente no site do servidor de relatório &#40;supervisor de atualização&#41;](../../../2014/sql-server/install/client-certificates-on-the-report-server-web-site-upgrade-advisor.md)  
  
-   [Extensões personalizadas foram detectadas no servidor de relatório &#40;supervisor de atualização&#41;](../../../2014/sql-server/install/custom-extensions-were-detected-on-the-report-server-upgrade-advisor.md)  
  
-   [Foram detectados itens de relatório personalizados no servidor de relatório &#40;supervisor de atualização&#41;](../../../2014/sql-server/install/custom-report-items-were-detected-on-the-report-server-upgrade-advisor.md)  
  
-   [Os componentes de compatibilidade com versões anteriores do IIS não foram detectados &#40;supervisor de atualização&#41;](../../../2014/sql-server/install/iis-backward-compatibility-components-were-not-detected-upgrade-advisor.md)  
  
-   [Restrição de endereço IP detectada &#40;supervisor de atualização&#41;](../../../2014/sql-server/install/ip-address-restriction-detected-upgrade-advisor.md)  
  
-   [Filtros ISAPI detectados no site do servidor de relatório &#40;supervisor de atualização&#41;](../../../2014/sql-server/install/isapi-filters-detected-on-the-report-server-site-upgrade-advisor.md)  
  
-   [Foram detectadas extensões obsoletas no computador do servidor de relatório &#40;o supervisor de atualização&#41;](../../../2014/sql-server/install/obsolete-extensions-were-detected-on-the-report-server-computer-upgrade-advisor.md)  
  
-   [O banco de dados do servidor de relatório não está configurado &#40;supervisor de atualização&#41;](../../../2014/sql-server/install/report-server-database-is-not-configured-upgrade-advisor.md)  
  
-   [SQL Server grupo de serviço Web do servidor de relatório 2005 detectado &#40;supervisor de atualização&#41;](../../../2014/sql-server/install/sql-server-2005-report-server-web-service-group-detected-upgrade-advisor.md)  
  
-   [Os diretórios virtuais não são especificados &#40;supervisor de atualização&#41;](../../../2014/sql-server/install/virtual-directories-are-unspecified-upgrade-advisor.md)  
  
-   [O diretório virtual tem um método de autenticação sem suporte &#40;supervisor de atualização&#41;](../../../2014/sql-server/install/virtual-directory-has-unsupported-authentication-method-upgrade-advisor.md)  
  
-   [Alterações nos limites de CPU e memória para SQL Server Standard e Enterprise &#40;Upgrade Advisor&#41;](../../../2014/sql-server/install/cpu-memory-limits-changes-sql-server-standard-enterprise-upgrade-advisor.md)  
  
-   [Contas de domínio necessárias para o farm do SharePoint &#40;supervisor de atualização&#41;](../../../2014/sql-server/install/domain-accounts-required-for-sharepoint-farm-upgrade-advisor.md)  
  
-   [Navegação direta para o servidor de relatório &#40;supervisor de atualização&#41;](../../../2014/sql-server/install/direct-browsing-to-report-server-upgrade-advisor.md)  
  
-   [O Microsoft SharePoint 2007 está instalado &#40;supervisor de atualização&#41;](../../../2014/sql-server/install/microsoft-sharepoint-2007-is-installed-upgrade-advisor.md)  
  
-   [Microsoft SQL Server Reporting Services serviço compartilhado do SharePoint está instalado lado a lado &#40;o supervisor de atualização&#41;](../../../2014/sql-server/install/sql-server-reporting-services-sharepoint-shared-service-side-by-side-upgrade-advisor.md)  
  
-   [&#40;do supervisor de atualização do Mecanismo de Banco de Dados incompatível&#41;](../../../2014/sql-server/install/incompatible-database-engine-server-collation-upgrade-advisor.md)  
  
-   [Outros problemas de atualização do Reporting Services](../../../2014/sql-server/install/other-reporting-services-upgrade-issues.md)  
  
  
