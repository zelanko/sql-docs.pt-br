---
title: Fazer upgrade do Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- upgrading databases
- databases [Analysis Services], upgrading
- installing Analysis Services, side-by-side installations
- Analysis Services upgrades
- Analysis Services upgrades, about upgrading Analysis Services
- SSAS, database migration
- upgrading Analysis Services
- installing Analysis Services, upgrading
- SSAS, upgrading
ms.assetid: a131d329-386e-4470-aaa9-ffcde4e5ec0c
author: Minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8bbec3cd552434070d76913f72812b302440bcdb
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53363475"
---
# <a name="upgrade-analysis-services"></a>Atualizar o Analysis Services
  Use a configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para atualizar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter informações detalhadas sobre como atualizar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo do SharePoint, consulte [atualizar PowerPivot para SharePoint](upgrade-power-pivot-for-sharepoint.md). Para obter mais informações sobre como atualizar um servidor existente do SQL da instância, consulte [atualizar para o SQL Server 2014 usando o Assistente de instalação &#40;instalação&#41;](upgrade-sql-server-using-the-installation-wizard-setup.md).  
  
## <a name="known-upgrade-issues"></a>Problemas de atualização conhecidos  
 Antes de atualizar para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], revise o seguinte:  
  
-   [Notas de Versão do SQL Server 2014](https://go.microsoft.com/fwlink/?LinkID=296445).  
  
-   Para saber quais [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] recursos e funcionalidades foram descontinuados, preteridos ou alterados ver [compatibilidade com versões anteriores do Analysis Services](../../analysis-services/analysis-services-backward-compatibility.md).  
  
## <a name="pre-upgrade-checklist"></a>Lista de verificação anterior à atualização  
 Antes de atualizar, revise as informações a seguir:  
  
-   [Atualizações de versão e edição com suporte](supported-version-and-edition-upgrades.md)  
  
-   [Requisitos de hardware e software para a instalação do SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
-   [Verificar parâmetros do Verificador de Configuração do Sistema](check-parameters-for-the-system-configuration-checker.md)  
  
-   [Considerações sobre segurança para uma instalação do SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
-   [Backup e restauração de bancos de dados do Analysis Services](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
-   [Usar o Supervisor de Atualização para preparar para atualizações](../../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)  
  
## <a name="upgrading-analysis-services"></a>Atualizando o Analysis Services  
 Você pode escolher entre várias abordagens para atualizar o servidor e os dados:  
  
-   Uma **atualização in loco** substitui o programa existente de arquivos com [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] arquivos de programa. Os bancos de dados permanecem no mesmo local. As pastas de programa são atualizadas para refletir o novo nome.  
  
-   Um **atualização lado a lado** é uma nova instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no mesmo computador que tenha uma instância existente do Analysis Services. Você pode mover bancos de dados para a nova instância no mesmo computador e, em seguida, desinstalar a versão antiga se você não for mais usá-la.  
  
-   Você também pode instalar o Analysis Services em novo hardware e, em seguida, migrar os bancos de dados existentes para aquele servidor.  
  
## <a name="in-place-upgrade"></a>Atualização in-loco  
 É possível atualizar uma instância existente do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e, como parte do processo de atualização, migrar automaticamente os bancos de dados existentes da instância antiga para a nova instância. Como os metadados e os dados binários são incompatíveis entre as duas versões, você reterá os dados depois de atualizar e não precisará migrar os dados manualmente.  
  
 Para atualizar uma instância existente, execute a Instalação e especifique o nome da instância existente como o nome da nova instância.  
  
## <a name="upgrading-databases"></a>Atualizando bancos de dados  
 Bancos de dados que foram criados em versões anteriores do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] são executados no servidor atualizado sob uma configuração em nível de compatibilidade do banco de dados mais antigo. Os bancos de dados criados nas seguintes versões têm um nível de compatibilidade de banco de dados igual a 105. Você pode alterar o nível de compatibilidade se desejar usar recursos que exijam um nível de compatibilidade de banco de dados mais novo. Caso contrário, você poderá executar os bancos de dados no servidor atualizado com o uso das configurações originais. Para obter mais informações, consulte [definir o nível de compatibilidade de um banco de dados Multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md).  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Recursos com suporte nas edições do SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [Planejando uma instalação do SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Noções básicas sobre a arquitetura Microsoft OLAP](../../analysis-services/multidimensional-models/olap-physical/understanding-microsoft-olap-architecture.md)   
 [Atualizar o PowerPivot para SharePoint](upgrade-power-pivot-for-sharepoint.md)   
 [Instalar o Analysis Services em modo multidimensional e de mineração de dados](../../sql-server/install/install-analysis-services-in-multidimensional-and-data-mining-mode.md)   
 [Instalação do PowerPivot para SharePoint 2010](../../sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
