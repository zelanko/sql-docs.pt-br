---
title: Serviços de análise do SQL Server 2014 | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 986356e6ebf7697bf0b425553f6803659a0fc5cb
ms.sourcegitcommit: 8f99d15c5b23d9f3c08a77e2b8bea5772f570493
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "80760307"
---
# <a name="sql-server-2014-analysis-services"></a>SQL Server 2014 Analysis Services

  O SQL Server 2014 Analysis Services é um mecanismo de dados analítico usado em soluções de suporte a decisões e inteligência de negócios (BI), fornecendo dados analíticos para relatórios de negócios e aplicativos de clientes, como Excel, relatórios de serviços de relatórios e outras ferramentas de BI de terceiros. 

## <a name="about-sql-server-analysis-services-documentation"></a>Sobre a documentação dos Serviços de Análise de Servidores SQL

A documentação é separada por versão. Você está atualmente na documentação do SQL Server 2014 Analysis Services.

- Para saber mais sobre o SQL Server 2012 e anteriormente, consulte a [documentação das versões anteriores do SQL Server](https://docs.microsoft.com/previous-versions/sql/).
- Para saber mais sobre o SQL Server 2014, consulte [Livros Online para SQL Server 2014](../2014-toc/index.yml)
- Para saber mais sobre o SQL Server 2016 e posteriormente, consulte [a documentação dos Serviços de Análise](https://docs.microsoft.com/analysis-services/).
- Para saber mais sobre os Serviços de Análise do Azure, consulte [a documentação dos serviços de análise do Azure](https://docs.microsoft.com/azure/analysis-services/).

## <a name="analysis-services-workflow"></a>Fluxo de trabalho dos Serviços de Análise

Um fluxo de trabalho típico inclui a construção de um modelo de dados OLAP ou tabular, implantar o modelo como um banco de dados em uma instância de servidor, processar o banco de dados para carregá-lo com dados e, em seguida, atribuir permissões para permitir o acesso aos dados. Quando ele estiver pronto, esse modelo de dados com vários fins poderá ser acessado por qualquer aplicativo cliente que suporte o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] como uma fonte de dados.  
  
 Para criar um modelo, use as Ferramentas de Dados do Servidor SQL (veja [Ferramentas e aplicativos usados em Serviços de Análise),](tools-and-applications-used-in-analysis-services.md)escolhendo um modelo de projeto tabular ou multidimensional e de mineração de dados. O modelo de projeto contém pastas de todos os objetos necessários em um modelo. É possível utilizar assistentes para criar todos os elementos básicos, como fontes de dados, modos de exibição de fonte de dados, dimensões, cubos e funções.  
  
 Os modelos são preenchidos com dados de sistemas de dados externos, geralmente data warehouses hospedados em um SQL Server ou um mecanismo de banco de dados relacional Oracle (os modelos de tabela oferecem suporte a tipos de fontes de dados). Modelos especificam objetos de consulta, como cubos, mas também especificam as dimensões que podem ser utilizadas em vários cubos, cálculos e KPIs que encapsulam a lógica de negócios e as interações, como comportamentos de detalhamento e navegação.  
  
 Para usar um modelo, ele é implantado em uma instância de servidor que executa bancos de dados em um determinado modo de servidor, disponibilizando os dados para usuários autorizados que se conectam através do Excel ou outros aplicativos.  
  
 Você pode instalar uma instância em um dos três modos de servidor:  
  
-   Como uma instância de Tabela, executando modelos de Tabela.  
  
-   Como uma instância Multidimensional e Mineração de Dados, executando cubos OLAP e modelos de mineração de dados (este é o padrão).  
  
-   Como PowerPivot para SharePoint, executando modelos de dados PowerPivot e Excel no SharePoint (PowerPivot para SharePoint é um mecanismo de dados de camada intermediária que carrega, consulta e atualiza modelos de dados hospedados no SharePoint).  
  
 Mesmo mecanismo de dados; três maneiras diferentes de utilizá-lo. Observe que os modos de servidor são configurados durante a instalação e não podem ser alterados posteriormente. Você deve instalar uma nova instância se precisar de um modo diferente.  
  
 A documentação fundamental do Analysis Services é organizada em seções que correspondem ao tipo de projeto que você está criando. Escolha entre os links a seguir para saber mais sobre cada modo ou área de recurso.  
  
 **Procurar conteúdo por área**  
 ![Ícone de pasta de pequeno porte](../../2014/integration-services/media/filefolder-small.gif "Pequeno ícone de pasta de arquivos") comparando [soluções tabulares e multidimensionais &#40;SSAS&#41;](comparing-tabular-and-multidimensional-solutions-ssas.md)  
  
 Gerenciamento de instâncias de [serviços de análise](instances/analysis-services-instance-management.md) de ![ícones de pequena pasta de arquivos](../../2014/integration-services/media/filefolder-small.gif "Pequeno ícone de pasta de arquivos")  
  
 ![Ícone da pasta de arquivo pequeno](../../2014/integration-services/media/filefolder-small.gif "Pequeno ícone de pasta de arquivos") Modelo [tabular &#40;&#41;Tabular SSAS](tabular-models/tabular-models-ssas.md)  
  
 ![Ícone de pasta de arquivo pequeno modelo](../../2014/integration-services/media/filefolder-small.gif "Pequeno ícone de pasta de arquivos") [multidimensional &#40;ssas&#41;](multidimensional-models/multidimensional-models-ssas.md)  
  
 ![Ícone de pasta de pequenos arquivos](../../2014/integration-services/media/filefolder-small.gif "Pequeno ícone de pasta de arquivos") &#40;&#41;[SSAS](data-mining/data-mining-ssas.md)  
  
 ![Ícone da pasta de arquivo pequeno](../../2014/integration-services/media/filefolder-small.gif "Pequeno ícone de pasta de arquivos") [PowerPivot para sharePoint &#40;ssas&#41;](power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] recursos variam de acordo com a edição. Modelos multidimensional e de mineração de dados estão disponíveis em uma edição padrão, com menos recursos do que edições posteriores. Modelos de tabela e PowerPivot para SharePoint são recursos premium e não estão disponíveis em uma licença de edição padrão. Para obter mais informações, consulte [Recursos suportados pelas edições do SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Tutoriais de serviços de análise &#40;&#41;SSAS](analysis-services-tutorials-ssas.md)   
 [Instalação para SQL Server 2014](../database-engine/install-windows/installation-for-sql-server.md)   
 [Guia do desenvolvedor &#40;Serviços de Análise&#41;](analysis-services-developer-documentation.md)   
 [Centro de recursos do servidor SQL](https://go.microsoft.com/fwlink/?linkID=219676)   
 [SQLCat.com](https://go.microsoft.com/fwlink/?linkID=220963)  
  
  
