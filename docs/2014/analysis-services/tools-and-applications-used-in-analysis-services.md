---
title: Ferramentas e aplicativos usados no Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 0ddb3b7a-7464-4d04-8659-11cb2e4cf3c3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6e8425b3d6fdb461b369c2311ba415dd8f032293
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62794618"
---
# <a name="tools-and-applications-used-in-analysis-services"></a>Ferramentas e aplicativos usados no Analysis Services
  Encontre as ferramentas e aplicativos que você precisa para a criação de modelos do Analysis Services e o gerenciamento de bancos de dados associados em uma instância do Analysis Services.  
  
## <a name="analysis-services-model-designers"></a>Designers de modelos do Analysis Services  
 Crie modelos de tabela e multidimensionais a partir de modelos de projeto em uma solução criada no shell do Visual Studio. O modelo de projeto possibilita aos designers a criação de modelos, cubos, dimensões e funções que compõem uma solução do Analysis Services.  
  
### <a name="download-sql-server-data-tools-for-business-intelligence-ssdt-bi"></a>Baixe o SQL Server Data Tools para Business Intelligence (SSDT-BI)  
 O [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] para Business Intelligence (SSDT-BI), anteriormente conhecido como Business Intelligence Development Studio (BIDS), é usado para criar modelos do Analysis Services, relatórios do Reporting Services e pacotes do Integration Services. Você pode baixar o SSDT-BI nos locais a seguir:  
  
-   [Baixar o SSDT-BI para Visual Studio 2013](https://go.microsoft.com/fwlink/p/?LinkId=396526)  
  
-   [Baixar o SSDT-BI para Visual Studio 2012](https://go.microsoft.com/fwlink/p/?LinkID=273673)  
  
 Se você tiver uma versão anterior do SSDT-BI ou BIDS instalado no computador, a versão mais recente será instalada lado a lado da versão anterior. É comum executar versões mais recentes e anteriores das ferramentas de design em uma única estação de trabalho para que você possa modificar projetos e soluções associados às versões específicas do servidor.  
  
> [!NOTE]  
>  Existem vários sites de download para as versões do Visual Studio 2012 e do Visual Studio 2013 do SSDT. A maioria deles não incluem os modelos de projeto de BI. O uso dos links acima oferecerão a você a versão correta. Você saberá que você tenha a versão correta do SSDT-BI, se você vir a pasta de modelos de projeto de Business Intelligence. Essa pasta contém modelos de projeto para o Analysis Services, o Reporting Services e o Integration Services. Dependendo de como você tiver instalado o SSDT-BI, provavelmente também verá um modelo de projeto adicional para bancos de dados do SQL Server.  
  
 ![Novos modelos de Projeto no SSDT](media/ssdt-biprojects.png "Novos modelos de Projeto no SSDT")  
  
## <a name="administrative-tools"></a>Ferramentas administrativas  
  
### <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 O Management Studio é a principal ferramenta de administração para todos os recursos do SQL Server, incluindo o Analysis Services. O SQL Server Management Studio é um componente opcional. Se você não vê-lo com outros aplicativos do SQL Server na página de aplicativos do Windows Server 2012, execute a instalação do SQL Server para adicioná-lo à sua instalação.  
  
### <a name="sql-server-profiler"></a>SQL Server Profiler  
 O SQL Server Profiler foi oficialmente preterido, mas oferece uma maneira fácil de monitorar as conexões, a execução de consultas MDX e outras operações do servidor. O SQL Server Profiler é instalado por padrão. Você pode encontrá-lo entre os aplicativos do SQL Server nos aplicativos do Windows Server 2012.  
  
### <a name="powershell"></a>PowerShell  
 Você pode usar os comandos do PowerShell para realizar muitas tarefas administrativas. Consulte [Analysis Services PowerShell](analysis-services-powershell.md) para obter mais informações.  
  
### <a name="community-and-third-party-tools"></a>Ferramentas da comunidade e de terceiros  
 Verifique a [página de codeplex do Analysis Services](http://sqlsrvanalysissrvcs.codeplex.com/) para ver exemplos de código da comunidade. [Fóruns](http://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlanalysisservices) podem ser úteis para você buscar recomendações de ferramentas de terceiros com suporte para o Analysis Services.  
  
  
