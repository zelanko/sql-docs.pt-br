---
title: SQL Server 2014 Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 04/06/2020
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services, about Analysis Services - Multidimensional Data
- SSAS
- Analysis Services
- SQL Server Analysis Services, about Analysis Services - Multidimensional Data
- SQL Server Analysis Services
- multidimensional data [Analysis Services]
- SSAS, about Analysis Services - Multidimensional Data
ms.assetid: 49d186f4-4b4d-4a5a-bb1a-e2699c64a731
author: minewiskan
ms.author: owend
ms.openlocfilehash: 49258d89858c8cea3a9620f50062d6371e22ec8e
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527992"
---
# <a name="sql-server-2014-analysis-services"></a>SQL Server 2014 Analysis Services

  SQL Server 2014 Analysis Services é um mecanismo de dados analíticos usado em soluções de suporte a decisões e de business intelligence (BI), fornecendo os dados analíticos para relatórios de negócios e aplicativos cliente, como Excel, relatórios de Reporting Services e outras ferramentas de BI de terceiros. 

## <a name="about-sql-server-analysis-services-documentation"></a>Sobre a documentação do SQL Server Analysis Services

A documentação é separada por versão. No momento, você está em SQL Server 2014 Analysis Services documentação.

- Para saber mais sobre o SQL Server 2012 e versões anteriores, consulte [SQL Server a documentação de versões anteriores](https://docs.microsoft.com/previous-versions/sql/).
- Para saber mais sobre o SQL Server 2014, consulte os [manuais online do SQL Server 2014](../2014-toc/index.yml)
- Para saber mais sobre o SQL Server 2016 e posterior, consulte [Analysis Services documentação](https://docs.microsoft.com/analysis-services/).
- Para saber mais sobre Azure Analysis Services, consulte [Azure Analysis Services documentação](https://docs.microsoft.com/azure/analysis-services/).

## <a name="analysis-services-workflow"></a>Fluxo de trabalho Analysis Services

Um fluxo de trabalho típico inclui a criação de um modelo de dados OLAP ou de tabela, a implantação do modelo como um banco de dado em uma instância de servidor, o processamento do banco de dados para carregá-lo e a atribuição de permissões para permitir o acesso a dados. Quando ele estiver pronto, esse modelo de dados com vários fins poderá ser acessado por qualquer aplicativo cliente que suporte o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] como uma fonte de dados.  
  
 Para criar um modelo, use SQL Server Data Tools (consulte [ferramentas e aplicativos usados no Analysis Services](tools-and-applications-used-in-analysis-services.md)), escolhendo um modelo de projeto tabular ou multidimensional e de mineração de dados. O modelo de projeto contém pastas de todos os objetos necessários em um modelo. É possível utilizar assistentes para criar todos os elementos básicos, como fontes de dados, modos de exibição de fonte de dados, dimensões, cubos e funções.  
  
 Os modelos são preenchidos com dados de sistemas de dados externos, geralmente data warehouses hospedados em um SQL Server ou um mecanismo de banco de dados relacional Oracle (os modelos de tabela oferecem suporte a tipos de fontes de dados). Modelos especificam objetos de consulta, como cubos, mas também especificam as dimensões que podem ser utilizadas em vários cubos, cálculos e KPIs que encapsulam a lógica de negócios e as interações, como comportamentos de detalhamento e navegação.  
  
 Para usar um modelo, ele é implantado em uma instância de servidor que executa os bancos de dados em um modo de servidor específico, disponibilizando-os para usuários autorizados que se conectam por meio do Excel ou de outros aplicativos.  
  
 Você pode instalar uma instância em um dos três modos de servidor:  
  
-   Como uma instância de Tabela, executando modelos de Tabela.  
  
-   Como uma instância Multidimensional e Mineração de Dados, executando cubos OLAP e modelos de mineração de dados (este é o padrão).  
  
-   Como PowerPivot para SharePoint, executando modelos de dados PowerPivot e Excel no SharePoint (PowerPivot para SharePoint é um mecanismo de dados de camada intermediária que carrega, consulta e atualiza modelos de dados hospedados no SharePoint).  
  
 Mesmo mecanismo de dados; três maneiras diferentes de utilizá-lo. Observe que os modos de servidor são configurados durante a instalação e não podem ser alterados posteriormente. Você deve instalar uma nova instância se precisar de um modo diferente.  
  
 A documentação fundamental do Analysis Services é organizada em seções que correspondem ao tipo de projeto que você está criando. Escolha entre os links a seguir para saber mais sobre cada modo ou área de recurso.  
  
 **Procurar conteúdo por área**  
 ![Ícone de pasta de arquivos pequenos](../../2014/integration-services/media/filefolder-small.gif "Pequeno ícone de pasta de arquivos") [comparando soluções tabulares e multidimensionais &#40;SSAS&#41;](comparing-tabular-and-multidimensional-solutions-ssas.md)  
  
 ![Ícone de pasta de arquivos pequena](../../2014/integration-services/media/filefolder-small.gif "Pequeno ícone de pasta de arquivos") [Analysis Services gerenciamento de instância](instances/analysis-services-instance-management.md)  
  
 ![Ícone de pasta de arquivos pequena](../../2014/integration-services/media/filefolder-small.gif "Pequeno ícone de pasta de arquivos") [modelagem tabular &#40;SSAS tabular&#41;](tabular-models/tabular-models-ssas.md)  
  
 ![Ícone de pasta de arquivos pequena](../../2014/integration-services/media/filefolder-small.gif "Pequeno ícone de pasta de arquivos") [modelagem multidimensional &#40;SSAS&#41;](multidimensional-models/multidimensional-models-ssas.md)  
  
 ![Ícone de pasta de arquivos pequena](../../2014/integration-services/media/filefolder-small.gif "Pequeno ícone de pasta de arquivos") [&#40;SSAS&#41;](data-mining/data-mining-ssas.md)  
  
 ![Ícone de pasta de arquivos pequena](../../2014/integration-services/media/filefolder-small.gif "Pequeno ícone de pasta de arquivos") [PowerPivot para SharePoint &#40;SSAS&#41;](power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] recursos variam de acordo com a edição. Modelos multidimensional e de mineração de dados estão disponíveis em uma edição padrão, com menos recursos do que edições posteriores. Modelos de tabela e PowerPivot para SharePoint são recursos premium e não estão disponíveis em uma licença de edição padrão. Para obter mais informações, consulte [recursos com suporte nas edições do SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Tutoriais de Analysis Services &#40;SSAS&#41;](analysis-services-tutorials-ssas.md)   
 [Instalação do SQL Server 2014](../database-engine/install-windows/installation-for-sql-server.md)   
 [Guia do desenvolvedor &#40;Analysis Services&#41;](analysis-services-developer-documentation.md)   
 [Centro de recursos de SQL Server](https://go.microsoft.com/fwlink/?linkID=219676)   
 [SQLCat.com](https://go.microsoft.com/fwlink/?linkID=220963)  
  
  
