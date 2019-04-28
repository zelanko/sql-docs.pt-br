---
title: Mineração de dados (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], about data mining
ms.assetid: b1c912da-72f6-4d96-89c8-55a2c4f19e88
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c798ff08653e770ea633597dfc64dfadf4639fbf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62722725"
---
# <a name="data-mining-ssas"></a>Mineração de dados (SSAS)
  O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornece uma plataforma integrada para soluções que incorporam mineração de dados. Você pode usar dados relacionais ou de cubo para criar soluções de business intelligence com análises preditivas.  
  
## <a name="benefits-of-data-mining"></a>Benefícios da mineração de dados  
 A mineração de dados usa princípios estatísticos pesquisados para descobrir padrões em seus dados, ajudando-o a tomar decisões inteligentes sobre problemas complexos. Ao aplicar os algoritmos de mineração de dados a seus dados no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , você pode prever tendências, identificar padrões, criar regras e recomendações, analisar a sequência de eventos em conjuntos de dados complexos e ter novas ideias.  
  
 No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], a mineração de dados é um recurso avançado, acessível e integrado com as ferramentas que muitas pessoas preferem usar para análise e relatório. Veja os links nesta seção para obter as informações essenciais sobre mineração de dados de que você precisa para começar.  
  
## <a name="key-data-mining-features"></a>Principais recursos de mineração de dados  
 O SQL Server fornece os recursos a seguir ao dar suporte a soluções de mineração de dados integradas:  
  
-   Várias fontes de dados: Não é necessário que criar um data warehouse ou um cubo OLAP para fazer mineração de dados. Você pode usar dados de tabelas de provedores externos, de planilhas e até mesmo de arquivos de texto. Também é possível minerar facilmente cubos OLAP criados no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. No entanto, você não pode usar dados de um banco de dados na memória.  
  
-   Limpeza de dados integrados, gerenciamento de dados e ETL: Data Quality Services fornece ferramentas avançadas para criação de perfil e limpeza de dados. O Integration Services pode ser usado para criar processos ETL para limpar dados e também para criar, processar, treinar e atualizar modelos.  
  
-   Vários algoritmos personalizáveis: Além de fornecer algoritmos como clustering, redes neurais e árvores de decisões, a plataforma dá suporte ao desenvolvimento de seus próprios algoritmos de plug-in personalizados.  
  
-   Infraestrutura de teste do modelo: Testar seus modelos e conjuntos de dados usando ferramentas estatísticas importantes como validação cruzada, matrizes de classificação, gráficos de comparação e dispersões. Crie e gerencie conjuntos de teste e treinamento com facilidade.  
  
-   Consulta e detalhamento: Criar consultas de previsão, recupere padrões modelo e estatísticas e detalhar os dados do caso.  
  
-   Ferramentas de cliente: Além dos estúdios de desenvolvimento e design fornecidos pelo SQL Server, você pode usar os suplementos de mineração de dados para Excel para criar, consultar e procurar modelos. Ou crie clientes personalizados, inclusive serviços Web.  
  
-   Suporte a idioma scripts e API gerenciada: Todos os objetos de mineração de dados são completamente programáveis. Gerar scripts é possível por meio do MDX, XMLA ou as extensões de PowerShell para o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Use a linguagem DMX (Data Mining Extensions) para consultar e gerar script rapidamente.  
  
-   Segurança e implantação: Fornece segurança baseada em função por meio de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], inclusive permissões separadas para drillthrough para modelar e estruturar dados. Implantação fácil de modelos para outros servidores, de forma que os usuários possam acessar os padrões ou executar previsões  
  
## <a name="in-this-section"></a>Nesta seção  
 Os tópicos nesta seção apresentam os recursos principais de Mineração de Dados do SQL Server e tarefas relacionadas.  
  
-   [Conceitos de mineração de dados](data-mining-concepts.md)  
  
-   [Algoritmos de mineração de dados &#40;Analysis Services – Data Mining&#41;](data-mining-algorithms-analysis-services-data-mining.md)  
  
-   [Estruturas de Mineração &#40;Analysis Services – Data Mining&#41;](mining-structures-analysis-services-data-mining.md)  
  
-   [Modelos de mineração &#40;Analysis Services – Data Mining&#41;](mining-models-analysis-services-data-mining.md)  
  
-   [Teste e validação &#40;Mineração de dados&#41;](testing-and-validation-data-mining.md)  
  
-   [Consultas de mineração de dados](data-mining-queries.md)  
  
-   [Soluções de mineração de dados](data-mining-solutions.md)  
  
-   [Ferramentas de mineração de dados](data-mining-tools.md)  
  
-   [Arquitetura de mineração de dados](data-mining-architecture.md)  
  
-   [Visão geral de segurança &#40;Mineração de dados&#41;](security-overview-data-mining.md)  
  
  
