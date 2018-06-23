---
title: Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Analysis Services, about Analysis Services - Multidimensional Data
- SSAS
- Analysis Services
- SQL Server Analysis Services, about Analysis Services - Multidimensional Data
- SQL Server Analysis Services
- multidimensional data [Analysis Services]
- SSAS, about Analysis Services - Multidimensional Data
ms.assetid: 49d186f4-4b4d-4a5a-bb1a-e2699c64a731
caps.latest.revision: 49
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b2cfc01ba3942ff431ca9bef78ea7bb16a5d56d5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009252"
---
# <a name="analysis-services"></a>Analysis Services
  O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] é um mecanismo de dados analíticos online usado em soluções de apoio à decisão e business intelligence (BI), que fornece os dados analíticos para relatórios de negócios e aplicativos cliente, tais como Excel, relatórios do Reporting Services e outras ferramentas de BI de terceiros. Um fluxo de trabalho típico do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] inclui criar um modelo de dados OLAP ou de tabela, implantar o modelo como um banco de dados em uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], processar o banco de dados para carregá-lo com dados e, em seguida, atribuir permissões para permitir o acesso aos dados. Quando ele estiver pronto, esse modelo de dados com vários fins poderá ser acessado por qualquer aplicativo cliente que suporte o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] como uma fonte de dados.  
  
 Para criar um modelo, use o SQL Server Data Tools (consulte [ferramentas e aplicativos usados no Analysis Services](tools-and-applications-used-in-analysis-services.md)), escolhendo um modelo de projeto Tabular ou Multidimensional e mineração de dados. O modelo de projeto contém pastas de todos os objetos necessários em um modelo. É possível utilizar assistentes para criar todos os elementos básicos, como fontes de dados, modos de exibição de fonte de dados, dimensões, cubos e funções.  
  
 Os modelos são preenchidos com dados de sistemas de dados externos, geralmente data warehouses hospedados em um SQL Server ou um mecanismo de banco de dados relacional Oracle (os modelos de tabela oferecem suporte a tipos de fontes de dados). Modelos especificam objetos de consulta, como cubos, mas também especificam as dimensões que podem ser utilizadas em vários cubos, cálculos e KPIs que encapsulam a lógica de negócios e as interações, como comportamentos de detalhamento e navegação.  
  
 Para usar um modelo, ele é implantado em uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que executa bancos de dados em um modo de servidor específico, tornando os dados disponíveis para usuários autorizados que se conectam pelo Excel ou por outros aplicativos.  
  
 Você pode instalar uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] em um dos três modos de servidor:  
  
-   Como uma instância de Tabela, executando modelos de Tabela.  
  
-   Como uma instância Multidimensional e Mineração de Dados, executando cubos OLAP e modelos de mineração de dados (este é o padrão).  
  
-   Como PowerPivot para SharePoint, executando modelos de dados PowerPivot e Excel no SharePoint (PowerPivot para SharePoint é um mecanismo de dados de camada intermediária que carrega, consulta e atualiza modelos de dados hospedados no SharePoint).  
  
 Mesmo mecanismo de dados; três maneiras diferentes de utilizá-lo. Observe que os modos de servidor são configurados durante a instalação e não podem ser alterados posteriormente. Você deve instalar uma nova instância se precisar de um modo diferente.  
  
 A documentação fundamental do Analysis Services é organizada em seções que correspondem ao tipo de projeto que você está criando. Escolha entre os links a seguir para saber mais sobre cada modo ou área de recurso.  
  
 **Procurar conteúdo por área**  
 ![Ícone de pasta do arquivo pequeno](../../2014/integration-services/media/filefolder-small.gif "arquivo pequeno ícone da pasta") [comparando soluções tabulares e multidimensionais &#40;SSAS&#41;](comparing-tabular-and-multidimensional-solutions-ssas.md)  
  
 ![Ícone de pasta do arquivo pequeno](../../2014/integration-services/media/filefolder-small.gif "arquivo pequeno ícone da pasta") [gerenciamento de instância do Analysis Services](instances/analysis-services-instance-management.md)  
  
 ![Ícone de pasta do arquivo pequeno](../../2014/integration-services/media/filefolder-small.gif "arquivo pequeno ícone da pasta") [modelagem Tabular &#40;Tabular do SSAS&#41;](tabular-models/tabular-models-ssas.md)  
  
 ![Ícone de pasta do arquivo pequeno](../../2014/integration-services/media/filefolder-small.gif "arquivo pequeno ícone da pasta") [modelagem Multidimensional &#40;SSAS&#41;](multidimensional-models/multidimensional-models-ssas.md)  
  
 ![Ícone de pasta do arquivo pequeno](../../2014/integration-services/media/filefolder-small.gif "arquivo pequeno ícone da pasta") [mineração de dados &#40;SSAS&#41;](data-mining/data-mining-ssas.md)  
  
 ![Ícone de pasta do arquivo pequeno](../../2014/integration-services/media/filefolder-small.gif "arquivo pequeno ícone da pasta") [PowerPivot para SharePoint &#40;SSAS&#41;](power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] recursos variam de acordo com a edição. Modelos multidimensional e de mineração de dados estão disponíveis em uma edição padrão, com menos recursos do que edições posteriores. Modelos de tabela e PowerPivot para SharePoint são recursos premium e não estão disponíveis em uma licença de edição padrão. Para obter mais informações, consulte [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tutoriais do Analysis Services &#40;SSAS&#41;](analysis-services-tutorials-ssas.md)   
 [Instalação do SQL Server 2014](../database-engine/install-windows/installation-for-sql-server.md)   
 [Guia do desenvolvedor &#40;do Analysis Services&#41;](analysis-services-developer-documentation.md)   
 [Central de recursos do SQL Server](http://go.microsoft.com/fwlink/?linkID=219676)   
 [SQLCat.com](http://go.microsoft.com/fwlink/?linkID=220963)  
  
  