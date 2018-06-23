---
title: Mineração de dados (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data mining [Analysis Services], about data mining
ms.assetid: b1c912da-72f6-4d96-89c8-55a2c4f19e88
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b118f03580aeb0053203cd2535bafecd1649ccb4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118007"
---
# <a name="data-mining-ssas"></a>Mineração de dados (SSAS)
  O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornece uma plataforma integrada para soluções que incorporam mineração de dados. Você pode usar dados relacionais ou de cubo para criar soluções de business intelligence com análises preditivas.  
  
## <a name="benefits-of-data-mining"></a>Benefícios da mineração de dados  
 A mineração de dados usa princípios estatísticos pesquisados para descobrir padrões em seus dados, ajudando-o a tomar decisões inteligentes sobre problemas complexos. Ao aplicar os algoritmos de mineração de dados a seus dados no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , você pode prever tendências, identificar padrões, criar regras e recomendações, analisar a sequência de eventos em conjuntos de dados complexos e ter novas ideias.  
  
 No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], a mineração de dados é um recurso avançado, acessível e integrado com as ferramentas que muitas pessoas preferem usar para análise e relatório. Veja os links nesta seção para obter as informações essenciais sobre mineração de dados de que você precisa para começar.  
  
## <a name="key-data-mining-features"></a>Principais recursos de mineração de dados  
 O SQL Server fornece os recursos a seguir ao dar suporte a soluções de mineração de dados integradas:  
  
-   Várias fontes de dados: você não tem que criar um data warehouse ou um cubo OLAP para fazer mineração de dados. Você pode usar dados de tabelas de provedores externos, de planilhas e até mesmo de arquivos de texto. Também é possível minerar facilmente cubos OLAP criados no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. No entanto, você não pode usar dados de um banco de dados na memória.  
  
-   Limpeza de dados integrada, gerenciamento de dados e ETL: Data Quality Services fornecem ferramentas avançadas para criação de perfil e limpar dados. O Integration Services pode ser usado para criar processos ETL para limpar dados e também para criar, processar, treinar e atualizar modelos.  
  
-   Vários algoritmos personalizáveis: além de fornecer algoritmos como clustering, redes neurais e árvores de decisões, a plataforma dá suporte a desenvolvimento de seus próprios algoritmos de plug-in personalizados.  
  
-   Infraestrutura de testes de modelo: teste seus modelos e conjuntos de dados usando ferramentas estatísticas importantes como validação cruzada, matrizes de classificação, gráficos de comparação de precisão e dispersões. Crie e gerencie conjuntos de teste e treinamento com facilidade.  
  
-   Consulta e detalhamento: crie consultas de previsão, recupere padrões modelo e estatísticas e detalhe os dados de caso.  
  
-   Ferramentas de cliente: além dos estúdios de desenvolvimento e design fornecidos pelo SQL Server, você pode usar os Suplementos de Mineração de Dados para Excel para criar, consultar e procurar modelos. Ou crie clientes personalizados, inclusive serviços Web.  
  
-   Suporte a linguagem de scripts e API gerenciada: todos os objetos de mineração de dados são completamente programáveis. Gerar scripts é possível por meio do MDX, XMLA ou as extensões de PowerShell para o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Use a linguagem DMX (Data Mining Extensions) para consultar e gerar script rapidamente.  
  
-   Segurança e implantação: fornece segurança baseada em função por meio do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], inclusive permissões separadas para drillthrough para modelar e estruturar dados. Implantação fácil de modelos para outros servidores, de forma que os usuários possam acessar os padrões ou executar previsões  
  
## <a name="in-this-section"></a>Nesta seção  
 Os tópicos nesta seção apresentam os recursos principais de Mineração de Dados do SQL Server e tarefas relacionadas.  
  
-   [Conceitos de mineração de dados](data-mining-concepts.md)  
  
-   [Algoritmos de mineração de dados &#40;Analysis Services – mineração de dados&#41;](data-mining-algorithms-analysis-services-data-mining.md)  
  
-   [Estruturas de mineração &#40;Analysis Services – mineração de dados&#41;](mining-structures-analysis-services-data-mining.md)  
  
-   [Modelos de mineração &#40;Analysis Services – mineração de dados&#41;](mining-models-analysis-services-data-mining.md)  
  
-   [Teste e validação &#40;mineração de dados&#41;](testing-and-validation-data-mining.md)  
  
-   [Consultas de mineração de dados](data-mining-queries.md)  
  
-   [Soluções de mineração de dados](data-mining-solutions.md)  
  
-   [Ferramentas de mineração de dados](data-mining-tools.md)  
  
-   [Arquitetura de mineração de dados](data-mining-architecture.md)  
  
-   [Visão geral de segurança &#40;mineração de dados&#41;](security-overview-data-mining.md)  
  
  