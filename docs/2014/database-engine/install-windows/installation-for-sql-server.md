---
title: Instalação do SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
f1_keywords:
- sql12.portal.Installation.f1
helpviewer_keywords:
- installing SQL Server, initial installation
- installation [SQL Server]
- initial installation [SQL Server]
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6dafb1e971b85adfee2ecb3579ac20b83906b9dd
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84932367"
---
# <a name="installation-for-sql-server-2014"></a>Instalação para SQL Server 2014
 ## <a name="download-sql-server-2014-express"></a>[Baixar o SQL Server 2014 Express](http://www.hanselman.com/blog/DownloadSQLServerExpress.aspx)
  **Obrigado a [Scott Hanselman](http://www.hanselman.com/) para coletar todos os links do pacote do instalador em um só lugar!**
  
  O Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece uma única árvore de recurso para instalar todos os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]  
  
-   [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]  
  
-   Ferramentas de gerenciamento  
  
-   Componentes de conectividade  
  
 Você pode instalar cada componente individualmente ou selecionar uma combinação dos componentes listados acima. Para fazer a melhor escolha entre as edições e os componentes disponíveis no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte [edições e componentes do SQL Server 2014](../../sql-server/editions-and-components-of-sql-server-2016.md) e [recursos com suporte nas edições do SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md). O [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] está disponível em edições de 32 e 64 bits.
 
 **Experimente:**  
  
-   Tem uma conta do Azure?  Em seguida, acesse **[aqui](https://ms.portal.azure.com/?flight=1#create/Microsoft.SQLServer2016RTMEnterpriseWindowsServer2012R2)** para criar uma máquina virtual com o SQL Server 2014 Service Pack 1 (SP1) já instalado. Para obter mais informações sobre o SQL Server 2014 (SP1), consulte [informações de versão do SQL Server 2014 Service Pack 1](https://support.microsoft.com/kb/3058865).  
  
## <a name="in-this-section"></a>Nesta seção  
 Independentemente de você usar o Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o prompt de comando para instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a Instalação envolve as seguintes etapas:  
  
 [Planejando uma instalação do SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)  
 Descreve como preparar seu computador para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Requisitos de hardware e software.  
  
-   Requisitos do Verificador de Configuração do Sistema e questões de bloqueio.  
  
-   Considerações sobre segurança.  
  
 [Instalar o SQL Server 2014](install-sql-server.md)  
 Descreve as opções de instalação para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Atualizar para o SQL Server 2014](upgrade-sql-server.md)  
 Descreve as opções de atualização para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Desinstalar o SQL Server 2014](../../sql-server/install/uninstall-sql-server.md)  
 Descreve procedimentos para desinstalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].  
  
 [Instalação do cluster de failover do SQL Server](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 Esta seção da documentação da Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] explica como instalar e configurar o cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 [Install SQL Server 2014 BI Features](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recursos que são parte da plataforma Microsoft BI e que incluem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]e vários aplicativos cliente usados para criação ou funcionamento com dados analíticos. Esta seção da documentação da Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] explica como instalar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Tópicos de instruções sobre a instalação](../../sql-server/install/installation-how-to-topics.md)  
 Fornece links para tópicos de procedimentos para instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do assistente de instalação, no prompt de comando, usando arquivos de configuração e o SysPrep.  
  
 [Instalar SQL Server recursos do BI com o SharePoint &#40;PowerPivot e Reporting Services&#41;](../../sql-server/install/install-sql-server-bi-features-sharepoint-powerpivot-reporting-services.md)  
 Esta seção explica como instalar recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um ambiente do SharePoint. Ela identifica quais recursos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estão disponíveis para uma versão e uma edição específicas do SharePoint. Ela também inclui procedimentos de instalação de PowerPivot para SharePoint e de Reporting Services no modo do SharePoint.  
  
 [Instalando exemplos e bancos de dados de exemplo do SQL Server](https://sqlserversamples.codeplex.com/)  
 Descreve como instalar e configurar os exemplos e bancos de dados de exemplo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte Também  
 [O que há de novo na instalação do SQL Server](../../sql-server/install/what-s-new-in-sql-server-installation.md)   
 [Requisitos de hardware e software para instalação do SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
