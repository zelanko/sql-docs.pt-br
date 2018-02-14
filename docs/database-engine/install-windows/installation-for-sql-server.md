---
title: "Instalação do SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 09/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.portal.Installation.f1
helpviewer_keywords:
- installing SQL Server, initial installation
- installation [SQL Server]
- initial installation [SQL Server]
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8fe0874d637f1597814bf14c8d12d111ece4cee1
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="sql-server-installation"></a>Instalação do SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

O Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece uma única árvore de recurso para instalar todos os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
-   [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]  
-   [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]  
-   Componentes de conectividade  
  
A partir do [!INCLUDE[ss2016](../../includes/sssql15-md.md)], as Ferramentas de Gerenciamento do SQL Server não são mais instaladas por meio da árvore de recursos principal; para obter detalhes, consulte [Baixar o SSMS (SQL Server Management Studio)](../../ssms/download-sql-server-management-studio-ssms.md)  
  
Você pode instalar cada componente individualmente ou selecionar uma combinação dos componentes listados acima. Para escolher a melhor opção entre as edições e os componentes disponíveis no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte os recursos com suporte em sua versão do SQL Server:

- [Edições e recursos com suporte do [!INCLUDE[ss2017](../../includes/sssqlv14-md.md)]](~/sql-server/editions-and-components-of-sql-server-2017.md).  
- [Edições e recursos com suporte do [!INCLUDE[ss2016](../../includes/sssql15-md.md)]](~/sql-server/editions-and-components-of-sql-server-2016.md).  
- [Recursos com suporte nas edições do [!INCLUDE[ss2014](../../includes/sssql14-md.md)]](http://technet.microsoft.com/library/cc645993(v=sql.120).aspx)
  
## <a name="in-this-section"></a>Nesta seção  
Independentemente de você usar o Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o prompt de comando para instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a Instalação envolve as seguintes etapas:  
  
[Planejando uma instalação do SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)  
Descreve como preparar seu computador para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Requisitos de hardware e software.  
-   Requisitos do Verificador de Configuração do Sistema e questões de bloqueio.  
-   Considerações sobre segurança.  
  
[Instalar o SQL Server](../../database-engine/install-windows/install-sql-server.md)  
 Descreve as opções de instalação para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
[Referência da interface de usuário da instalação do SQL Server](http://msdn.microsoft.com/library/183b5cdd-962e-41ca-8064-ea44f622c77d)  
 Descreve as opções de instalação apresentadas pelo Assistente para Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
[Atualizar o SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)  
 Descreve as opções de atualização para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
[Desinstalar o SQL Server](../../sql-server/install/uninstall-sql-server.md)  
 Descreve procedimentos para desinstalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].  
  
[Instalação do cluster de failover do SQL Server](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 Esta seção da documentação da Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] explica como instalar e configurar o cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
[Instalar os recursos do business intelligence do SQL Server](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recursos que são parte da plataforma Microsoft BI e que incluem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]e vários aplicativos cliente usados para criação ou funcionamento com dados analíticos. Esta seção da documentação da Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] explica como instalar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="more-information"></a>Mais Informações
[Instalar recursos de BI do SQL Server com o SharePoint &#40;Power Pivot e Reporting Services&#41;](http://msdn.microsoft.com/library/3166107c-30c2-468e-bb1b-bb42b79b37c3)  
 Esta seção explica como instalar recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um ambiente do SharePoint. Ela identifica quais recursos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estão disponíveis para uma versão e uma edição específicas do SharePoint. Ela também inclui procedimentos de instalação do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint e Reporting Services no modo do SharePoint.  
  
![ssrs_fyi_note](../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png) Instale o novo banco de dados de exemplo, [Wide World Importers](https://msdn.microsoft.com/library/mt734199(v=sql.1).aspx). 
  
[Exemplos e bancos de dados de exemplo do SQL Server](http://sqlserversamples.codeplex.com/)  
 Descreve como instalar e configurar os exemplos e bancos de dados de exemplo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
Confira o [Centro de Atualização do SQL Server](https://msdn.microsoft.com/library/ff803383.aspx) para obter links e informações para todas as versões com suporte do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
[Novidades na instalação do SQL Server](../../sql-server/install/what-s-new-in-sql-server-installation.md)   
[Requisitos de Hardware e Software para a Instalação do SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
