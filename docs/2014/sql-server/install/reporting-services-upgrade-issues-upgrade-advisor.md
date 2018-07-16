---
title: Problemas (Supervisor de atualização) de atualização do Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Report Manager [Reporting Services], upgrade issues
- Reporting Services, upgrades
- upgrading Reporting Services
- report servers [Reporting Services], upgrade issues
ms.assetid: d9663f25-98d7-4508-ae3c-55a7277211bd
caps.latest.revision: 42
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: a3adf211200ccc2596fe8766c11bffc653a2b3f2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37306926"
---
# <a name="reporting-services-upgrade-issues-upgrade-advisor"></a>Problemas de atualização do Reporting Services (supervisor de atualização)
  Os tópicos a seguir descrevem os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] problemas que podem afetar sua atualização para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Eles descrevem ações que podem ser tomadas para diminuir o efeito dessas alterações em seu ambiente.  
  
 O Supervisor de Atualização analisa uma instalação do servidor de relatório. Se apenas componentes cliente estiverem instalados (por exemplo, se o Designer de Relatórios for o único componente do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalado no computador), nenhum problema será reportado.  
  
 Dependendo de como sua instalação foi configurada, você poderá encontrar outros problemas que não foram reportados pelo Supervisor de Atualização. Esses problemas não impedem que a atualização do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] tenha êxito, mas podem afetar a maneira como os relatórios e os aplicativos são executados depois que a atualização é concluída. Para obter mais informações sobre esses problemas, consulte "Compatibilidade com versões anteriores do Reporting Services" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Se não for possível usar a Instalação para atualizar uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], você poderá instalar uma nova instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e migrar a instalação existente para essa nova instância. Para obter mais informações, consulte "Atualizar e migrar o Reporting Services" na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Manuais Online [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).  
  
 Os tópicos a seguir descrevem problemas conhecidos reportados pelo Supervisor de Atualização e explicam como modificar a instalação existente para permitir que a atualização ocorra.  
  
> [!IMPORTANT]  
>  O Supervisor de Atualização deve estar instalado no servidor de relatório para analisar a instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não dá suporte à análise remota.  
>   
>  Para obter mais informações, consulte [Installing Upgrade Advisor](../../../2014/sql-server/install/installing-upgrade-advisor.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Certificados de cliente no site do servidor de relatório &#40;Supervisor de atualização&#41;](../../../2014/sql-server/install/client-certificates-on-the-report-server-web-site-upgrade-advisor.md)  
  
-   [Extensões personalizadas foram detectadas no servidor de relatório &#40;Supervisor de atualização&#41;](../../../2014/sql-server/install/custom-extensions-were-detected-on-the-report-server-upgrade-advisor.md)  
  
-   [Itens de relatório personalizado detectados no servidor de relatório &#40;Supervisor de atualização&#41;](../../../2014/sql-server/install/custom-report-items-were-detected-on-the-report-server-upgrade-advisor.md)  
  
-   [Componentes de compatibilidade com versões anteriores do IIS não detectados &#40;Supervisor de atualização&#41;](../../../2014/sql-server/install/iis-backward-compatibility-components-were-not-detected-upgrade-advisor.md)  
  
-   [Restrição de endereço IP detectada &#40;Supervisor de atualização&#41;](../../../2014/sql-server/install/ip-address-restriction-detected-upgrade-advisor.md)  
  
-   [Filtros ISAPI detectados no site do servidor de relatório &#40;Supervisor de atualização&#41;](../../../2014/sql-server/install/isapi-filters-detected-on-the-report-server-site-upgrade-advisor.md)  
  
-   [Extensões obsoletas detectadas no computador do servidor de relatório &#40;Supervisor de atualização&#41;](../../../2014/sql-server/install/obsolete-extensions-were-detected-on-the-report-server-computer-upgrade-advisor.md)  
  
-   [Banco de dados de servidor de relatório não está configurado &#40;Supervisor de atualização&#41;](../../../2014/sql-server/install/report-server-database-is-not-configured-upgrade-advisor.md)  
  
-   [Grupo de serviço Web servidor de relatório do SQL Server 2005 detectado &#40;Supervisor de atualização&#41;](../../../2014/sql-server/install/sql-server-2005-report-server-web-service-group-detected-upgrade-advisor.md)  
  
-   [Diretórios virtuais são especificados &#40;Supervisor de atualização&#41;](../../../2014/sql-server/install/virtual-directories-are-unspecified-upgrade-advisor.md)  
  
-   [Diretório virtual tem o método de autenticação sem suporte &#40;Supervisor de atualização&#41;](../../../2014/sql-server/install/virtual-directory-has-unsupported-authentication-method-upgrade-advisor.md)  
  
-   [Alterações em limites de CPU e memória para o SQL Server Standard e Enterprise &#40;Supervisor de atualização&#41;](../../../2014/sql-server/install/cpu-memory-limits-changes-sql-server-standard-enterprise-upgrade-advisor.md)  
  
-   [Contas de domínio necessárias ao farm do SharePoint do &#40;Supervisor de atualização&#41;](../../../2014/sql-server/install/domain-accounts-required-for-sharepoint-farm-upgrade-advisor.md)  
  
-   [Navegação direta para o servidor de relatório &#40;Supervisor de atualização&#41;](../../../2014/sql-server/install/direct-browsing-to-report-server-upgrade-advisor.md)  
  
-   [O Microsoft SharePoint 2007 está instalado &#40;Supervisor de atualização&#41;](../../../2014/sql-server/install/microsoft-sharepoint-2007-is-installed-upgrade-advisor.md)  
  
-   [Microsoft SQL Server Reporting Services serviço compartilhado do SharePoint é instalado lado a lado &#40;Supervisor de atualização&#41;](../../../2014/sql-server/install/sql-server-reporting-services-sharepoint-shared-service-side-by-side-upgrade-advisor.md)  
  
-   [Agrupamento de servidor do mecanismo de banco de dados incompatíveis &#40;Supervisor de atualização&#41;](../../../2014/sql-server/install/incompatible-database-engine-server-collation-upgrade-advisor.md)  
  
-   [Outros problemas de atualização do Reporting Services](../../../2014/sql-server/install/other-reporting-services-upgrade-issues.md)  
  
  
